# AGENTS.md

<!-- Simplified to the absolute minimum to keep instructions dry and focused -->

TAXA: Platform Edukasi Pajak Adaptif Berbasis Multi-Agent RAG.
Source of Truth: [PRD](prd.md), [SRS](srs.md), [TDD](tdd.md).

## Stack & Conventions
- **Frontend (`apps/web`):** React + TS + Tailwind + TanStack Query (Format: Prettier).
- **Backend AI (`services/ai`):** FastAPI + LangChain + Python (Format: Black).
- **Database & Auth:** Supabase (PostgreSQL + pgvector with strict RLS).
- **Git:** Conventional Commits (`feat:`, `fix:`, `docs:`, `chore:`). Branch: `main` or `feat/*`.

## Core Rules
1. **YAGNI First:** Build only the minimum working solution. No unrequested abstractions or third-party packages.
2. **SDT Alignment:** Every feature/UI must serve Autonomy (career choice), Competence (instant feedback, Mock SPT), or Relatedness (Clan peer-support).
3. **No Hallucinations:** RAG chatbot must strictly reference retrieved context from UU HPP.
4. **Hybrid Validation:** Backend evaluates tax calculations using deterministic Python logic. LLM is only used for formatting hints.
5. **Security:** Use environment variables for API keys. Database access must enforce RLS.
6. **Persistent Memory:** Always read [brain.md](file:///Users/nomina/Projects/TAXA/brain.md) at the start of a task to get context, and update its change log and roadmap when you make any changes.
