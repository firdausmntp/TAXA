# Technical Design Document (TDD)

| Metadata | Details |
| :--- | :--- |
| **Project Name** | TAXA (Platform Adaptive Learning Berbasis Multi-Agent RAG) |
| **Document Version** | 1.0 |
| **Status** | MVP Design |

---

## 1. System Architecture
TAXA employs a decoupled client-server architecture utilizing a Backend-as-a-Service (BaaS) for core CRUD/Auth and a dedicated microservice for AI processing.

### 1.1 High-Level Architecture Diagram

```mermaid
flowchart TD
    Client[Client: React + Vite + TS]
    SupabaseDB[(Supabase: PostgreSQL + pgvector)]
    SupabaseAuth[Supabase Auth]
    FastAPI[AI Backend: FastAPI + Python]
    LLM[LLM API / Local SLM]

    Client <-->|Auth & User State| SupabaseAuth
    Client <-->|Direct CRUD (RLS applied)| SupabaseDB
    Client <-->|REST API (JSON)| FastAPI
    
    FastAPI <-->|Vector Search (pgvector)| SupabaseDB
    FastAPI <-->|Multi-Agent Prompts| LLM
```

### 1.2 Component Responsibilities
*   **Frontend (Client):** Handles UI rendering, user interactions, local state management (React Context/Zustand), and server state caching (TanStack Query). Directly communicates with Supabase for user profiles and mission saving.
*   **AI Backend (FastAPI):** Acts as the orchestrator for all heavy AI and mathematical tasks. Strictly stateless; relies on the client to pass the necessary context or Supabase JWT for verification.
*   **Database (Supabase):** Source of truth for relational data (users, missions) and vector data (tax law embeddings). Secures direct client access via Row Level Security (RLS).

---

## 2. Database Schema (Supabase)

### 2.1 Table: `users`
*Managed by Supabase Auth triggers.*

*   **`id`** (`uuid`, PK, references `auth.users`)
*   **`display_name`** (`text`, not null)
*   **`role`** (`text`, default: `'student'`)
*   **`current_xp`** (`integer`, default: `0`)
*   **`created_at`** (`timestamptz`, default: `now()`)

### 2.2 Table: `missions`
*Stores the state and history of user simulations.*

*   **`id`** (`uuid`, PK, default: `uuid_generate_v4()`)
*   **`user_id`** (`uuid`, FK to `users.id`)
*   **`persona_type`** (`text`, e.g., `'freelancer'`, `'content_creator'`)
*   **`scenario_data`** (`jsonb`) - *Stores the AI-generated scenario (income, expenses, status).*
*   **`user_submission`** (`jsonb`, nullable) - *Stores the user's final tax calculation draft.*
*   **`is_completed`** (`boolean`, default: `false`)
*   **`score`** (`integer`, nullable)
*   **`created_at`** (`timestamptz`, default: `now()`)

### 2.3 Table: `tax_documents_vector`
*Stores the chunks of UU HPP and DJP regulations.*

*   **`id`** (`bigserial`, PK)
*   **`content`** (`text`) - *The actual text chunk of the law.*
*   **`metadata`** (`jsonb`) - *e.g., `{"pasal": "17", "undang_undang": "UU HPP"}`*
*   **`embedding`** (`vector(1536)`) - *Generated via OpenAI `text-embedding-3-small` or similar.*

---

## 3. API Specifications (FastAPI)
All AI interactions will route through the FastAPI backend.
*   **Base URL:** `https://api-taxa.domain.com/v1`

### 3.1 Generate Scenario
*   **Endpoint:** `POST /scenario/generate`
*   **Description:** Triggers the Scenario Agent to build a randomized financial profile.
*   **Request Body:**
    ```json
    {
      "persona": "content_creator",
      "difficulty": "beginner"
    }
    ```
*   **Response Body (200 OK):**
    ```json
    {
      "gross_income_monthly": 12000000,
      "platform_deductions": 500000,
      "marital_status": "TK/0",
      "assets": ["Kamera Lumix", "MacBook Pro"],
      "narrative": "Kamu adalah seorang Content Creator YouTube..."
    }
    ```

### 3.2 Tutor Chat (RAG Pipeline)
*   **Endpoint:** `POST /tutor/chat`
*   **Description:** Streams an answer from the Tutor Agent using RAG.
*   **Request Body:**
    ```json
    {
      "query": "Apa bedanya TK/0 dan K/1?",
      "chat_history": [ ... ]
    }
    ```
*   **Response:** Server-Sent Events (SSE) stream of text chunks.

### 3.3 Auditor Evaluation
*   **Endpoint:** `POST /auditor/evaluate`
*   **Description:** Evaluates the user's submitted tax calculation.
*   **Request Body:**
    ```json
    {
      "scenario_data": { ... }, 
      "user_calculation": {
         "ptkp": 54000000,
         "pkp": 85000000,
         "pph21_annual": 4250000
      }
    }
    ```
*   **Response Body (200 OK):**
    ```json
    {
      "is_correct": false,
      "error_type": "PTKP_CALCULATION",
      "hint_message": "Coba cek lagi perhitungan PTKP-mu. Ingat, statusmu adalah TK/0, yang berarti kamu tidak memiliki tanggungan.",
      "awarded_xp": 0
    }
    ```

---

## 4. AI Multi-Agent Pipeline Design (LangChain)

### 4.1 RAG Implementation (Tutor Agent)
*   **Ingestion (Pre-computation):**
    1.  PDFs of UU HPP and DJP Regulations are parsed using PyPDF.
    2.  Text is chunked using `RecursiveCharacterTextSplitter` (chunk_size=1000, overlap=200).
    3.  Chunks are embedded and stored in Supabase `pgvector`.
*   **Retrieval:**
    1.  User query is converted to an embedding.
    2.  FastAPI queries Supabase for the top $K$ (e.g., $K=3$) most similar document chunks using Cosine Similarity.
*   **Generation:**
    *   **System Prompt:** *"Anda adalah TAXA, tutor pajak ramah untuk Gen Z. Jawab HANYA berdasarkan konteks berikut: {context}. Jika jawaban tidak ada di konteks, tolak dengan sopan."*
    *   LLM receives the prompt + context chunks + user query and streams the answer.

### 4.2 Mathematical Validation (Auditor Agent)
To prevent LLM hallucination in math, the Auditor Agent will use **Hybrid Validation**:
*   **Deterministic Math Engine (Python):** Python backend computes the exact mathematical truth (PTKP, PKP, PPh 21 tiers) based on the JSON `scenario_data`.
*   **Comparison Logic:** Python strictly compares `user_calculation` vs deterministic truth.
*   **LLM Formatting:** If an error is detected (e.g., Python flags PTKP mismatch), the backend passes the error type to the LLM (Auditor Agent) to generate a friendly, Gen Z-appropriate hint without giving the exact number away.

---

## 5. Security & Deployment Strategy

### 5.1 Security
*   **Row Level Security (RLS):** Supabase `missions` table will have a policy: `auth.uid() = user_id`. Users cannot read or write others' missions.
*   **API Authentication:** FastAPI routes will require a Bearer token (Supabase JWT). FastAPI will verify this JWT using the Supabase project secret before executing AI tasks.
*   **Prompt Injection Protection:** Tutor Agent prompts will be strictly bounded. Input sanitization will be performed on FastAPI before passing to LangChain.

### 5.2 Deployment
*   **Frontend:** Vercel (connected to `main` branch for CI/CD).
*   **Backend:** Railway or Render (Containerized via Dockerfile). Configured with auto-scaling to prevent downtime during LLM traffic spikes.
*   **Database:** Supabase Managed Cloud (Free Tier for MVP).