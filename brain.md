# TAXA Agent Brain

This file acts as a persistent memory for AI agents working on the TAXA project. It tracks current project status, architectural decisions, recent changes, and upcoming tasks. **Always update this file when you complete a task or change the project state.**

---

## 1. Project Context & Stack
- **Project Name:** TAXA (Platform Edukasi Pajak Adaptif Berbasis Multi-Agent RAG)
- **Goal:** Empower Gen Z and Gen Alpha in Indonesia with adaptive tax roleplay simulation (PPh 21 and PTKP rules).
- **Core Frameworks:**
  - **Frontend:** Vite + React + TypeScript + Tailwind CSS + TanStack Query
  - **Backend:** Python FastAPI + LangChain
  - **Database:** Supabase (PostgreSQL with `pgvector` and Auth)
- **Source of Truth Documents:** [PRD](prd.md) | [SRS](srs.md) | [TDD](tdd.md)

---

## 2. Key Architecture & Logical Decisions
- **Gamification (Self-Determination Theory):**
  - **Autonomy:** User selects a Career Persona (Freelancer, Streamer, etc.) or inputs a custom profile.
  - **Competence:** Deterministic evaluation feedback by the Auditor Agent, earning XP, badges, and Mock SPT (PDF).
  - **Relatedness:** "Clan" feature showing team progress and peer support recommendations.
- **Hybrid Validation for Math Tasks:**
  - Prevents LLM hallucinations in tax mathematics.
  - Calculations of PPh 21, PTKP, and TER tiers are executed deterministically on the Python backend.
  - Results (errors/success) are passed to the Auditor LLM Agent solely for formatting user-friendly, adaptive feedback.
- **RAG Pipeline (Tutor Agent):**
  - Text parsed from official tax laws (UU HPP & DJP Regulations).
  - Stored as vector embeddings in Supabase (`pgvector`).
  - Chatbot responds strictly using context chunks retrieved via semantic similarity search.

---

## 3. Persistent Change Log

| Date | Agent / User Action | Description | Affected Files |
| :--- | :--- | :--- | :--- |
| 2026-07-20 | Antigravity (Agent) | Aligned documentation with PRD/SRS/TDD source of truth. Streamlined `AGENTS.md` to YAGNI style. Deleted obsolete `CONCEPT.md`. Initialized `brain.md`. | `README.md`, `AGENTS.md`, `brain.md`, `CONCEPT.md` |
| 2026-07-20 | Antigravity (Agent) | Added Core Rule 6 to `AGENTS.md` to ensure future agents read and update `brain.md`. | `AGENTS.md`, `brain.md` |

---

## 4. Next Steps & Active Roadmap
1. [ ] **Supabase Setup:**
   - Initialize PostgreSQL schemas for `users`, `missions`, and `tax_documents_vector`.
   - Setup RLS policies where `auth.uid() = user_id`.
2. [ ] **FastAPI Backend Implementations:**
   - `/scenario/generate` endpoint for generating randomized persona financial scenarios.
   - `/tutor/chat` RAG pipeline endpoint with SSE stream.
   - `/auditor/evaluate` endpoint implementing hybrid mathematical auditing.
3. [ ] **Frontend React Implementations:**
   - App Shell with mobile-first layout.
   - Step-by-step interactive Tax Calculation form.
   - Chat component for Tutor AI.
   - Certificate & Mock SPT PDF download module.
