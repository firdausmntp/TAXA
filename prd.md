# Product Requirements Document (PRD)

| Metadata | Details |
| :--- | :--- |
| **Project Name** | TAXA (Platform Adaptive Learning Berbasis Multi-Agent RAG) |
| **Team** | Kita Pergi Hari Ini (Universitas Sultan Ageng Tirtayasa) |
| **Event** | Samsung Solve for Tomorrow 2026 |
| **Document Version** | 1.1 |
| **Status** | Draft / MVP Planning |

---

## 1. Product Vision & Problem Statement

### 1.1. Product Vision
Mendemokratisasi literasi perpajakan bagi Gen Z dan Gen Alpha di Indonesia melalui pengalaman simulasi roleplay berbasis AI yang interaktif, personal, dan presisi, sehingga melahirkan generasi "Smart Taxpayer" yang siap menghadapi dinamika ekonomi digital, baik sejak di bangku sekolah maupun saat merintis karier.

### 1.2. Problem Statement
*   **Missing Link Edukasi Nasional:** Literasi keuangan di sekolah dan kampus hanya fokus pada sektor jasa (perbankan, asuransi, investasi), mengabaikan perpajakan. Pemahaman pajak eksklusif hanya untuk jurusan Akuntansi/Ekonomi.
*   **Booming Gig Economy Gen Z & Alpha:** Remaja dan dewasa muda (16-25 tahun) kini bisa berpenghasilan mandiri secara dinamis (Streamer, Content Creator, Freelance Developer, E-commerce) namun buta hukum perpajakan. Mereka rentan terkena sanksi administratif atau melanggar regulasi di masa depan karena ketidaktahuan.
*   **Metode Edukasi Usang & Kaku:** Sosialisasi perpajakan yang ada saat ini bersifat teoretis-statis, dipenuhi jargon hukum (regulasi panjang), dan tidak relevan dengan model pendapatan pekerja kreatif modern.

---

## 2. Target Audience
Pergeseran dari sekadar "pelajar" menjadi demografi generasi muda yang lebih luas yang terdampak langsung oleh ekonomi digital.

### 2.1. Primary Users (Gen Z & Early Gen Alpha: Usia 16–25 Tahun)
*   **Segmen 1: Pelajar Menengah Atas & Mahasiswa**
    Mereka yang sedang mempersiapkan diri masuk dunia kerja namun tidak mendapat bekal ilmu pajak di kurikulum utama.
*   **Segmen 2: Pekerja Gig & Kreatif Muda (First-time Taxpayers)**
    Freelancer, content creator, pemilik online shop pemula, dan pekerja lepas yang sudah memiliki penghasilan tetapi kebingungan mendaftar NPWP atau menghitung PPh 21 mereka sendiri.
*   **Karakteristik:** Digital savvy, terbiasa dengan gamifikasi/interaksi instan, rentan kebosanan terhadap teks panjang, dan lebih menyukai *learning by doing*.
*   **Pain Points:** Takut salah hitung pajak, pusing membaca aturan di website DJP, dan merasa pajak itu rumit serta tidak transparan.

### 2.2. Secondary Users (Edukator & Komunitas)
*   **Demografi:** Guru (PPKn/IPS), Dosen, atau Mentor di komunitas pekerja kreatif/freelance.
*   **Pain Points:** Kesulitan mencari alat peraga (*edtech tool*) yang praktis, selalu *up-to-date* dengan aturan terbaru, dan mudah dievaluasi untuk mengajarkan kepatuhan pajak.

---

## 3. Value Proposition
*   **Roleplay Gamification:** Belajar pajak bukan lewat membaca modul kaku, melainkan bermain peran mengelola keuangan karier modern yang sangat relevan dengan Gen Z (misal: simulasi pendapatan AdSense YouTube atau komisi freelance).
*   **Zero-Hallucination AI (RAG):** Tutor AI dijamin akurat dan berbasis hukum sah karena pengetahuannya dikunci pada dokumen resmi DJP/UU HPP. Sistem bisa di-update tanpa perlu coding ulang jika ada perubahan tarif pajak negara.
*   **Real-world Output:** Menghasilkan dokumen Mock SPT (PDF) yang otentik sebagai bukti kompetensi dan "gladi bersih" sebelum mengisi SPT asli di dunia nyata.

---

## 4. Core Features (MVP Scope)
Fokus MVP adalah menghadirkan siklus (*loop*) simulasi yang utuh dari pemilihan persona hingga pencetakan mock-up SPT.

### 4.1. Fitur Utama Pengguna (Gen Z/Alpha)
*   **Persona Selection & Onboarding:** Pengguna dapat memilih 1 dari 4 "Persona Karier Modern" (misal: Freelance Dev, Streamer, Online Shop, Content Creator) atau memasukkan estimasi profil pendapatan riil mereka sendiri (opsional).
*   **Dynamic Scenario Generator (Scenario Agent):** Sistem men-generate slip gaji fiktif bulanan, status keluarga fiktif (PTKP), dan daftar aset secara acak namun logis berdasarkan persona yang dipilih.
*   **Interactive Tax Form (Gameplay):** UI/UX interaktif tempat pengguna melakukan klasifikasi pendapatan, menghitung Penghasilan Tidak Kena Pajak (PTKP), dan menghitung PPh 21 progresif (termasuk skema TER/Tarif Efektif Rata-rata terbaru).
*   **RAG Tax Tutor (Tutor Agent):** Tombol bantuan ("Tanya AI") di mana pengguna bisa bertanya istilah/aturan pajak. AI akan menjawab dengan bahasa casual dan relevan bagi Gen Z, berlandaskan dokumen legal yang ditarik via semantic search.
*   **Automated AI Auditor (Auditor Agent):** Tombol "Setor SPT". Sistem mengevaluasi jawaban hitungan matematika pajak pengguna dan memberikan feedback spesifik (contoh: *"Hitungan PTKP kamu kurang tepat, ingat status persona-mu belum menikah (TK/0)!"*).
*   **Mock SPT & Certificate Output:** Generate formulir fisik SPT tersimulasi (PDF) dan sertifikat/badge setelah simulasi berhasil diselesaikan.

### 4.2. Fitur Pendukung (Gamifikasi & Sosial)
*   **Dashboard Profil & Badge:** Menampilkan riwayat misi yang diselesaikan, skor literasi (Tax IQ), dan badge pencapaian.
*   **Sistem Clan / Peer Support (Basic):** Fitur grup kecil di mana pengguna dapat melihat progres rekan se-tim (memicu motivasi berbasis Self-Determination Theory).

### 4.3. Educator/Community Dashboard (Opsional untuk MVP - Fase 2)
*   **Analytical View:** Visualisasi analitik kolektif untuk melihat metrik pemahaman satu kelas atau satu komunitas terhadap topik pajak tertentu.

---

## 5. User Journey & Flow
1.  **Sign Up/Login:** Pengguna masuk dan melihat Dashboard utama.
2.  **Pilih Misi (Otonomi):** Pengguna menekan "Mulai Simulasi" dan memilih Persona Karier (misal: Content Creator) atau menginput skenario pendapatan kustom.
3.  **Terima Kasus:** AI (Scenario Agent) memberikan ringkasan keuangan tahunan, termasuk invoice masuk, potongan platform, dan pengeluaran.
4.  **Mulai Menghitung:** Pengguna mengisi *tax form* interaktif selangkah demi selangkah.
5.  **Tanya Tutor:** Saat bingung membedakan jenis pajak, pengguna klik ikon Tutor AI. Tutor memberikan penjelasan legal dengan bahasa santai (RAG Pipeline).
6.  **Submit & Audit:** Pengguna mengirim jawaban. AI Auditor memeriksa. Jika salah, kembali ke langkah 4 dengan hint adaptif. Jika benar, lanjut ke langkah 7.
7.  **Reward:** Animasi sukses, mendapatkan Badge, poin kompetensi, dan unduhan file Mock SPT PDF.

---

## 6. Success Metrics (KPIs untuk SFT 2026)
*   **Engagement:** Rata-rata waktu penyelesaian 1 siklus simulasi (Target: 10-15 menit per sesi).
*   **Learning Impact (Pre/Post-Test):** Peningkatan metrik pemahaman konsep pajak dasar sebesar minimal 35% sebelum dan sesudah bermain.
*   **System Accuracy:** Tingkat akurasi (*zero-hallucination*) dari Tutor Agent sebesar 99% (diukur dari log QA pengujian internal terhadap UU HPP).
*   **Completion Rate:** Persentase pengguna yang berhasil mendapatkan sertifikat Mock SPT dari total yang memulai simulasi (Target: >80%).

---

## 7. Technical Overview & Constraints
*   **Frontend:** React (Vite) + TypeScript + TailwindCSS. Dirancang seringan mungkin (*mobile-first* dan *low-end friendly*).
*   **Backend & AI:** Python (FastAPI) + LangChain + LLM API (Small Language Model / OpenAI). Arsitektur berbasis Multi-Agent.
*   **Database:** Supabase (PostgreSQL). Wajib menggunakan ekstensi `pgvector` untuk menyimpan embedding dokumen regulasi perpajakan resmi.
*   **Constraints:**
    *   Respons AI Tutor harus cepat (< 3 detik) agar flow gamifikasi tidak terputus.
    *   *Guardrails prompt engineering* harus super ketat: AI harus menolak menjawab pertanyaan di luar konteks perpajakan Indonesia.