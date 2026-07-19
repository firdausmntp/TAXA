<div align="center">

<!-- BANNER -->
<img src="docs/assets/banner.svg" alt="TAXA Banner" width="100%" />

<!-- BADGES -->
<br/><br/>

![Samsung Solve for Tomorrow 2026](https://img.shields.io/badge/Samsung-Solve%20for%20Tomorrow%202026-1428A0?style=for-the-badge&logo=samsung&logoColor=white)
![License MIT](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![SDG 4](https://img.shields.io/badge/UN_SDG-4%20Quality%20Education-E5243B?style=for-the-badge)

<br/>

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)
![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat-square&logo=vite&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?style=flat-square&logo=supabase&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)

<br/>

### 🎯 *Platform Edukasi Pajak Adaptif Berbasis Multi-Agent RAG untuk Pelajar Indonesia*

**Misi kami:** Demokratisasi literasi perpajakan melalui gamifikasi yang berbasis ilmu motivasi — bukan sekadar poin dan level, tapi pengalaman belajar yang benar-benar *memuaskan*.

<br/>

![SDT](https://img.shields.io/badge/Powered%20by-Self--Determination%20Theory-purple?style=for-the-badge)

</div>

---

## 🧠 Mengapa TAXA?

> *"30% siswa tidur di jam kosong, 23% main game, hanya 9% belajar."*

LMS konvensional hanya menghitung nilai. **TAXA** menghitung *motivasi*.

| Masalah | Solusi TAXA |
|---|---|
| 🔒 "Aku ga bisa milih apa yang mau dipelajari" | **Misi Mandiri** — tentukan topik, durasi, dan ritmemu sendiri |
| 😩 "Belajar ga pernah terasa rewarding" | **Umpan Balik Instan** — badge + poin AI langsung setelah kuis |
| 🧍 "Belajar itu sepi" | **Clan** — kelompok belajar dengan peta keahlian AI |

<br/>

## 🔄 Alur Pembelajaran

```mermaid
flowchart LR
    A["🎯 Setel Misi\n(Otonomi)"] --> B["📚 Modul + Kuis\n(Pembelajaran)"]
    B --> C["🏆 Dapat Badge\n(Kompetensi)"]
    C --> D["👥 Clan & Peer Support\n(Relasi)"]
    D --> A
```

1. **🎯 Setel Misi** → Pilih topik, durasi, dan tingkat kesulitan
2. **📚 Belajar** → Modul interaktif yang disesuaikan dengan levelmu
3. **🏆 Kompetisi** → Kuis berbasis AI dengan reward badge instan
4. **👥 Kolaborasi** → Masuk Clan, lihat siapa yang butuh bantu, saling membantu

<br/>

## 🛠 Tech Stack

<table>
<tr>
<td><strong>Frontend</strong></td>
<td>
<img src="https://img.shields.io/badge/Vite-646CFF?style=flat-square&logo=vite&logoColor=white" /> &nbsp;
<img src="https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black" /> &nbsp;
<img src="https://img.shields.io/badge/TanStack_Query-EF4444?style=flat-square&logo=reactquery&logoColor=white" /> &nbsp;
<img src="https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white" />
</td>
</tr>
<tr>
<td><strong>Backend AI</strong></td>
<td>
<img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white" /> &nbsp;
<img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" /> &nbsp;
<img src="https://img.shields.io/badge/LangChain-1C3C3C?style=flat-square&logo=langchain&logoColor=white" /> &nbsp;
<img src="https://img.shields.io/badge/RAG-Pipelines-blueviolet?style=flat-square" />
</td>
</tr>
<tr>
<td><strong>Database</strong></td>
<td>
<img src="https://img.shields.io/badge/Supabase-3FCF8E?style=flat-square&logo=supabase&logoColor=white" /> &nbsp;
<img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white" /> &nbsp;
<img src="https://img.shields.io/badge/Auth-3FCF8E?style=flat-square" /> &nbsp;
<img src="https://img.shields.io/badge/Realtime-3FCF8E?style=flat-square" />
</td>
</tr>
<tr>
<td><strong>Deploy</strong></td>
<td>
<img src="https://img.shields.io/badge/Vercel-000000?style=flat-square&logo=vercel&logoColor=white" /> &nbsp;
<img src="https://img.shields.io/badge/Railway-0B0D0E?style=flat-square&logo=railway&logoColor=white" />
</td>
</tr>
</table>

<br/>

## 📁 Struktur Proyek

```
taxa/
├── apps/
│   └── web/              # Vite + React-TS frontend
│                         # (Tailwind, TanStack Query, react-router-dom, Supabase client)
├── services/
│   └── ai/               # Python FastAPI — multi-agent RAG, adaptive engine
│                         # (LangChain, Supabase server, OpenAI)
├── packages/
│   └── shared/           # Shared TypeScript types & constants
├── supabase/
│   └── migrations/       # SQL migrations + RLS policies
├── docs/                 # Research notes, wireframes, meeting records
├── .env.example          # Root env template
├── .gitignore
└── AGENTS.md             # Guidelines untuk AI coding agents
```

<br/>

## ❓ Kenapa Stack Ini?

| Tool | Alasan |
|---|---|
| **Vite + React** | Bundler tercepat saat ini, bundle kecil — penting untuk low-end phone siswa Indonesia. Next.js overkill tanpa SSR. |
| **TypeScript** | Catch bug saat development bukan runtime — critical untuk app dengan banyak state (misi, badge, clan). |
| **TanStack Query** | Server state + caching tanpa Redux boilerplate. Realtime badge/progress langsung ter-sync. |
| **Tailwind CSS** | Utility-first → UI cepat tanpa context-switch ke CSS file terpisah. Zero runtime overhead. |
| **Supabase** | PostgreSQL + Auth + Realtime dalam satu paket. RLS built-in untuk isolasi data antar siswa. |
| **FastAPI** | Async Python terbaik untuk AI/ML workload. Native async, auto OpenAPI docs, integrasi LangChain mulus. |
| **LangChain** | Ekosistem multi-agent RAG paling matang di Python. Adaptive engine & peer-support mapper jadi lebih mudah dibangun. |

<br/>

## 🔑 Environment Variables

```bash
# Frontend
cp apps/web/.env.example apps/web/.env

# AI Backend
cp services/ai/.env.example services/ai/.env
```

> ⚠️ `VITE_` prefix = aman di browser (anon key, URL publik).
> `SUPABASE_SERVICE_KEY` dan `OPENAI_API_KEY` = server-only, jangan pernah ke frontend.

<br/>

## 🚀 Getting Started

```bash
# 1. Clone repo
git clone https://github.com/firdausmntp/TAXA.git
cd TAXA

# 2. Frontend
cd apps/web
cp .env.example .env        # isi VITE_SUPABASE_URL, VITE_SUPABASE_ANON_KEY
npm install
npm run dev                 # http://localhost:5173

# 3. AI Backend
cd ../../services/ai
cp .env.example .env        # isi SUPABASE_SERVICE_KEY, OPENAI_API_KEY
pip install -r requirements.txt
uvicorn main:app --reload   # http://localhost:8000
```

<br/>

## 🌍 Dampak — SDG Alignment

<div align="center">

<img src="https://img.shields.io/badge/UN_SDG_4-Quality%20Education-E5243B?style=for-the-badge&logo=united-nations&logoColor=white" />

<br/><br/>

<img src="docs/assets/dampak.svg" alt="Dampak TAXA" width="100%" />

</div>

<br/>

## 🤖 Kontribusi AI

| Komponen | Peran |
|---|---|
| **Adaptive Mission Engine** | Rekomendasikan tingkat kesulitan berdasarkan riwayat performa |
| **Personalized Feedback** | Ringkasan umpan balik otomatis & terpersonalisasi |
| **Skill Gap Detection** | Identifikasi kekuatan & kelemahan untuk collaborative matching |
| **Peer Support Mapper** | Peta keahlian real-time untuk setiap anggota Clan |

<br/>

## 👥 Tim

<div align="center">

| | Nama | Peran |
|---|---|---|
| 👑 | **Azhriler Lintang** | Ketua Tim |
| 💻 | **Mujadid Akbar Paryono** | Anggota |
| 🎨 | **Abdulhadi Muntashir** | Anggota |
| 📊 | **Firdaus Satrio Utomo** | Anggota |

<br/>

**🏛 Universitas Sultan Ageng Tirtayasa**

</div>

---

<div align="center">

<img src="https://img.shields.io/badge/Made_with_❤️_for_Indonesian_Students-blue?style=for-the-badge" />

<br/><br/>

**Samsung Solve for Tomorrow 2026** — *Solving for tomorrow. Today.*

</div>
