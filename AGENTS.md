# AGENTS.md

Panduan untuk AI coding agent yang bekerja di proyek TAXA.

---

## Proyek

**TAXA** — Platform Edukasi Pajak Adaptif Berbasis Multi-Agent RAG untuk Pelajar Indonesia. Platform pembelajaran adaptif berbasis gamifikasi menggunakan Self-Determination Theory (SDT) untuk meningkatkan motivasi belajar siswa.

**Stack:** Vite + React + TanStack Query + Tailwind CSS + Supabase (PostgreSQL + Auth) + Python FastAPI (AI/RAG backend)

## Konvensi Kode

- **Bahasa:** TypeScript (frontend), Python (backend AI)
- **Formatting:** Prettier (frontend), Black (Python)
- **Commit:** Conventional Commits (`feat:`, `fix:`, `docs:`, `chore:`)
- **Branch:** `main` (stabil), `feat/*`, `fix/*`
- **PR:** Kecil dan fokus. Satu fitur/perbaikan per PR.

## Arsitektur

```
taxa/
├── apps/
│   └── web/          # Vite + React + TS frontend
│                     # → src/App.tsx      komponen entry
│                     # → src/main.tsx     root render + providers (QueryClient, BrowserRouter)
│                     # → src/index.css    Tailwind directives + global resets
│                     # → tailwind.config.js, postcss.config.js
├── services/
│   └── ai/           # Python FastAPI — multi-agent RAG, adaptive engine
│                     # → main.py          FastAPI app entry + CORS + /health
│                     # → requirements.txt pinned deps (fastapi, langchain, supabase, openai)
├── packages/
│   └── shared/       # Shared TypeScript types & constants (diimpor oleh apps/web)
├── supabase/
│   └── migrations/   # File migrasi SQL + RLS policies
├── docs/             # Catatan riset, notulen, wireframe
├── .env.example      # Template env vars (salin ke .env, jangan pernah commit .env)
├── .gitignore        # Mengabaikan node_modules, dist, .venv, .env, __pycache__
├── AGENTS.md         # File ini — panduan untuk AI coding agent
├── CONCEPT.md        # Concept paper — masalah, solusi, pemetaan SDT
├── LICENSE           # MIT
└── README.md         # Gambaran proyek, badges, cara memulai
```

## Prinsip

1. **SDT di setiap fitur.** Setiap elemen UI harus melayani Otonomi, Kompetensi, atau Relasi. Kalau tidak melayani salah satunya, hapus.
2. **Dependensi minimal.** Kirim versi paling sederhana dulu. Tambah library hanya ketika solusi native tidak cukup.
3. **AI melayani siswa.** AI adalah coach pembelajaran, bukan generator konten. Umpan balik harus personal, bukan generik.
4. **Aksesibilitas pertama.** Siswa Indonesia pakai berbagai perangkat dan koneksi. Optimalkan untuk HP low-end.
5. **Privasi data.** Data siswa sensitif. Supabase RLS wajib. Tidak ada PII di logs.

## Larangan

- Jangan over-engineering. Jangan buat abstraksi yang hanya dipakai satu kali.
- Jangan fitur "jaga-jaga". Kirim MVP dulu, lalu iterasi.
- Jangan dark patterns. Gamifikasi untuk memotivasi, bukan memanipulasi.
- Jangan hardcode secrets. Gunakan `.env` dan Supabase Vault.
