# Software Requirements Specification (SRS)

| Metadata | Details |
| :--- | :--- |
| **Project Name** | TAXA (Platform Adaptive Learning Berbasis Multi-Agent RAG) |
| **Team** | Kita Pergi Hari Ini (Universitas Sultan Ageng Tirtayasa) |
| **Event** | Samsung Solve for Tomorrow 2026 |
| **Document Version** | 1.0 |
| **Status** | MVP Planning |

---

## 1. Introduction

### 1.1 Purpose
The purpose of this document is to define the software requirements for the TAXA MVP. It specifies what the system should do (Functional Requirements), how it should perform (Non-Functional Requirements), and the technical constraints under which it must operate.

### 1.2 Scope
TAXA is a web-based educational platform targeting Gen Z and Early Gen Alpha (16-25 years old) in Indonesia. The MVP focuses on a single end-to-end gamified loop: user onboarding, persona selection, dynamic financial scenario generation, interactive tax calculation (PPh 21), AI-assisted tutoring (RAG), AI auditing, and Mock SPT generation.

---

## 2. System Architecture & Environment

### 2.1 Tech Stack
*   **Frontend:** React (Vite) + TypeScript, Tailwind CSS, TanStack Query.
*   **Backend (AI & Logic):** Python 3.10+, FastAPI, LangChain.
*   **Database & Auth:** Supabase (PostgreSQL with `pgvector`, Supabase Auth).
*   **LLM Provider:** OpenAI API (GPT-4o-mini or similar cost-effective Small Language Model) or local SLM.

### 2.2 System Flow
1.  Client (Browser) sends user actions to the FastAPI Backend.
2.  FastAPI acts as an orchestrator for the Multi-Agent System (Scenario, Tutor, Auditor).
3.  For RAG queries, FastAPI retrieves vector embeddings from Supabase (`pgvector`).
4.  The Agent interacts with the LLM and returns the processed payload to the Client.
5.  Persistent data (user profiles, mission history, badges) is synced directly between the Client and Supabase.

---

## 3. Functional Requirements (FR)

### FR1: Authentication & User Profile
*   **FR1.1:** The system shall allow users to register and log in using Email/Password and Google OAuth via Supabase Auth.
*   **FR1.2:** The system shall maintain a user profile containing: Username, XP/Points, Acquired Badges, and Mission History.

### FR2: Dynamic Scenario Generation (Scenario Agent)
*   **FR2.1:** The system shall provide a minimum of 4 Career Personas (e.g., Freelance Developer, Content Creator, E-commerce Owner, Streamer).
*   **FR2.2:** Upon persona selection, the Scenario Agent shall generate a randomized but mathematically logical financial JSON payload containing:
    *   Monthly Gross Income (*Penghasilan Bruto*)
    *   Platform Deductions/Expenses (*Biaya Jabatan* / Potongan)
    *   Marital Status for PTKP (e.g., TK/0, K/1)
    *   List of dummy assets.

### FR3: Interactive Gameplay (Tax Form)
*   **FR3.1:** The system shall provide a step-by-step interactive UI for users to classify income, deduct expenses, calculate PTKP, and calculate progressive PPh 21.
*   **FR3.2:** The UI shall save draft calculations locally to prevent data loss upon accidental refresh.

### FR4: RAG Tax Tutor (Tutor Agent)
*   **FR4.1:** The system shall feature a chat interface accessible during the gameplay phase.
*   **FR4.2:** The Tutor Agent shall accept user queries and perform a semantic search against the `pgvector` database containing Indonesian Tax Laws (UU HPP).
*   **FR4.3:** The Tutor Agent's system prompt shall strictly restrict answers to the retrieved context to prevent hallucination. If the query is unrelated to taxes, the AI must politely decline to answer.

### FR5: AI Auditor & Output Generation (Auditor Agent)
*   **FR5.1:** When the user clicks "Setor SPT", the Auditor Agent shall validate the user's calculations against the absolute mathematical truth.
*   **FR5.2:** If incorrect, the Auditor Agent shall identify the specific error (e.g., *"Your PTKP calculation is wrong for status K/0"*) and return a hint without giving the exact answer.
*   **FR5.3:** If correct, the system shall award points/badges and generate a downloadable PDF (Mock SPT) using a predefined HTML-to-PDF template.

---

## 4. Mathematical Logic & Business Rules
The backend Auditor Agent must strictly implement the rules of Undang-Undang Harmonisasi Peraturan Perpajakan (UU HPP) and the Tarif Efektif Rata-Rata (TER) scheme.

### 4.1 Penghasilan Tidak Kena Pajak (PTKP)
The base formula for determining PTKP is:

$$PTKP = Base + (Tanggungan \times 4,500,000) + Status_{Kawin}$$

Where:
*   $Base = 54,000,000$ IDR per year.
*   $Status_{Kawin}$ adds an additional $4,500,000$ IDR if married.
*   Maximum number of dependents (*Tanggungan*) is 3.

### 4.2 Penghasilan Kena Pajak (PKP)
Calculated annually based on net income:

$$PKP = \left( \sum_{i=1}^{12} Penghasilan\_Bersih_i \right) - PTKP$$

### 4.3 PPh 21 Progressive Calculation (Pasal 17 UU HPP)
For annual tax calculation, the tax is applied progressively across tiers (*lapis*):

$$Total\_Pajak = \sum (Tarif_n \times Bagian\_PKP_n)$$

Where the tiers ($n$) are:
*   $0 \le PKP \le 60,000,000 \rightarrow Tarif = 5\%$
*   $60,000,000 < PKP \le 250,000,000 \rightarrow Tarif = 15\%$
*   $250,000,000 < PKP \le 500,000,000 \rightarrow Tarif = 25\%$
*   $500,000,000 < PKP \le 5,000,000,000 \rightarrow Tarif = 30\%$
*   $PKP > 5,000,000,000 \rightarrow Tarif = 35\%$

---

## 5. Non-Functional Requirements (NFR)

### 5.1 Performance & Responsiveness
*   **NFR1:** The AI Tutor Agent must return the first byte of a streamed response within $< 1.5$ seconds. Complete response generation must take $< 4$ seconds.
*   **NFR2:** The web interface must render seamlessly on low-end Android devices via mobile browsers (Mobile-First Design). Minimum supported resolution: $320 \times 568$px.

### 5.2 Reliability & Accuracy (AI Guardrails)
*   **NFR3 (Zero-Hallucination Target):** The RAG implementation must achieve a 99% accuracy rate on factual tax questions, validated against standard test datasets before deployment.
*   **NFR4:** The system must implement rate limiting on the Tutor AI (e.g., max 10 messages per simulation session) to prevent API abuse and control costs.

### 5.3 Security
*   **NFR5:** Database access from the frontend must strictly use Row Level Security (RLS) in Supabase. Users can only read/write their own mission progress.
*   **NFR6:** OpenAI / LLM API keys must be securely stored in the backend environment variables and never exposed to the frontend.

---

## 6. Data Requirements

### 6.1 Core Entities (Supabase Schema Plan)
*   **`users`:** `id` (uuid), `role`, `display_name`, `current_xp`, `created_at`.
*   **`missions`:** `id` (uuid), `user_id`, `persona_type`, `scenario_data` (jsonb), `is_completed`, `score`, `created_at`.
*   **`tax_documents_vector`:** `id`, `chunk_content` (text), `metadata` (jsonb), `embedding` (vector(1536)).

---

### Document Sign-off
*Prepared for the TAXA SFT 2026 technical development phase.*