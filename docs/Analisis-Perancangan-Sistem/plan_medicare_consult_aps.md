# Rencana Kerja: Analisis & Perancangan Sistem (APS) — Medicare Consult

## Goal Description
Menghasilkan dokumen cetak biru **Analisis & Perancangan Sistem (APS)** yang komprehensif, akademis, dan siap implementasi untuk platform **Medicare Consult** (Web Konsultasi Kesehatan Online berbasis AI / Telemedicine mirip Halodoc) bagi **Kelompok 2** yang beranggotakan:
1. **Alpian**
2. **Maulid**
3. **Sultan**
4. **Natun**
5. **Riski**

Dokumentasi ini merefleksikan pergeseran (*pivot*) dari konsep awal klinik fisik (`Carely`) menjadi platform konsultasi kesehatan daring murni (*telehealth consultation*). Sistem membedakan antarmuka publik (*landing page* `index2.html`) dengan portal aplikasi web (*CRM / Web App Telehealth*), memberlakukan sistem *gatekeeping* kelengkapan data pasien sebelum konsultasi, mengelompokkan gejala (umum vs organ dalam), mengimplementasikan alur mediasi bot ganda (*Triage Bot* $\to$ *Doctor Bot Gemini*), menghasilkan rekomendasi klinis serta e-resep berformat PDF, serta menyusun skema basis data relasional ternormalisasi (1NF–3NF) lengkap dengan diagram UML/Draw.io.

---

## User Review Required

> [!IMPORTANT]
> **1. Alokasi Pembagian Kerja (Jobdesk) Kelompok 2**
> Kami menyusun pembagian tugas terstruktur dan berimbang sesuai metodologi Rekayasa Perangkat Lunak (RPL) & *User-Centered Design (UCD)*:
> - **Alpian (Project Leader & System Architect)**: Bertanggung jawab atas kepemimpinan proyek, orkestrasi arsitektur sistem 3-tier, arsitektur integrasi bot ganda (*Triage Bot* & Google Gemini API), serta spesifikasi API/WebSocket.
> - **Maulid (Business Analyst & PRD Lead)**: Bertanggung jawab atas analisis logika bisnis Halodoc, studi kasus komparatif, matriks kebutuhan fungsional & non-fungsional, serta batasan klinis sistem.
> - **Sultan (Database Administrator & Data Modeler)**: Bertanggung jawab atas desain basis data relasional, pemetaan entitas, tahapan normalisasi tabel (UNF $\to$ 1NF $\to$ 2NF $\to$ 3NF), kamus data (*data dictionary*), dan integritas referensial.
> - **Natun (System Modeler & UML Specialist)**: Bertanggung jawab atas perancangan visual sistem: Flowchart end-to-end, Use Case Diagram & skenario, Activity Diagram multi-role, Sequence Diagram, dan konversi ke file visual Draw.io.
> - **Riski (UI/UX Designer & Product Deliverable Lead)**: Bertanggung jawab atas pemisahan arsitektur Landing Page vs Web App, perancangan sitemap, alur wireframe interaktif (onboarding biodata, triage, chat room), serta layout resmi E-Resep PDF.

> [!NOTE]
> **2. Batasan Etika Medis & AI Doctor Persona**
> Karena dokter pada sistem ini merupakan agen cerdas (*AI Bot* ditenagai Google Gemini), sistem dirancang dengan batasan etika medis ketat:
> - AI hanya berwenang meresepkan obat golongan **Bebas (Hijau)** dan **Bebas Terbatas (Biru)**, serta multivitamin/suplemen.
> - Jika pasien mengalami gejala kritis / kegawatdaruratan (*red flag symptoms* seperti nyeri dada menjalar, batuk darah, sesak napas berat), *Triage Bot* secara otomatis memutus konsultasi bot dan mengeluarkan peringatan darurat menuju IGD rumah sakit terdekat.

---

## Open Questions

> [!NOTE]
> Mohon konfirmasi preferensi teknis kelompok Anda:
> 1. **Target Database**: Apakah perancangan DDL fisik lebih disukai untuk **PostgreSQL** atau **MySQL / MariaDB**? (Standar yang kami siapkan adalah ANSI SQL yang kompatibel untuk keduanya).
> 2. **Format Draw.io**: Apakah Anda membutuhkan file mentah berekstensi `.drawio` yang dapat dibuka langsung di aplikasi Draw.io / VS Code extension, selain kode diagram Mermaid di dalam file markdown?

---

## Proposed Changes

Dokumentasi akan ditempatkan secara modular di dalam folder yang telah disiapkan:
`d:\Development\Carely\docs\Analisis-Perancangan-Sistem/`

### 1. Modul Manajemen Proyek & Pembagian Tugas
#### [NEW] `jobdesk.md`
- Identitas Kelompok 2 & Deskripsi Proyek Medicare Consult.
- Matriks Tanggung Jawab RACI (*Responsible, Accountable, Consulted, Informed*).
- Rincian *Deliverables* per anggota tim (Alpian, Maulid, Sultan, Natun, Riski).
- Timeline pengerjaan (Sprint 1: Analisis Kebutuhan, Sprint 2: Pemodelan Sistem & Data, Sprint 3: Desain UI/UX & Spesifikasi API, Sprint 4: Finalisasi & Validasi).

#### [NEW] `README.md`
- Ringkasan Eksekutif (*Executive Summary*) Medicare Consult.
- Latar Belakang Masalah, Masalah Industri Telehealth, dan Solusi yang Diusulkan.
- Metodologi *User-Centered Design (UCD)*: *Research, Define, Design, Prototype, Test*.
- Panduan navigasi seluruh modul dokumentasi APS.

---

### 2. Analisis Bisnis & Persyaratan Sistem
#### [NEW] `01-business-logic-and-prd.md`
- *Product Requirement Document (PRD)* & Studi Kasus Medicare Consult.
- Analisis komparatif alur bisnis sistem Halodoc vs Medicare Consult.
- Definisi 3 Hak Akses (RBAC): Pasien (*Patient*), Dokter (*AI Bot Persona/Specialist*), Administrator.
- Matriks Kebutuhan Fungsional (FR) dan Kebutuhan Non-Fungsional (NFR).
- Taksonomi Pengelompokan Gejala:
  - **Gejala Umum**: Batuk, pilek, demam, sakit kepala, migrain, flu, nyeri otot, lemas.
  - **Gejala Organ Dalam & Spesifik**: Paru-paru (respirasi), Lambung/Saluran Cerna (GERD, gastritis, diare), Jantung (kardiovaskular), Ginjal/Saluran Kemih, Kulit & Kelamin (dermatologi).
- Kebijakan *Onboarding Gatekeeper*: Aturan wajib melengkapi rekam medis biodata sebelum membuka sesi konsultasi.

---

### 3. Arsitektur Sistem & Alur Dual-Bot
#### [NEW] `02-system-architecture-and-triage.md`
- Arsitektur Sistem 3-Tier: Frontend (Landing Page `index2.html` vs Web App Portal), Backend API/WebSocket, AI Knowledge Engine (Gemini API) & Database.
- Mekanisme Transisi: Dari Public Landing Page $\to$ Autentikasi $\to$ Private CRM Web App.
- Logika Mediasi Bot Ganda:
  1. *Pasien $\to$ Bot Penengah (Triage Bot)*: Ekstraksi keluhan utama (*Chief Complaint*), klasifikasi gejala, pemetaan spesialisasi.
  2. *Bot Penengah $\to$ Bot Dokter Spesialis*: Pengalihan sesi dan context passing ke persona dokter spesialis.
  3. *Bot Dokter Spesialis $\to$ Diagnosa & E-Resep*: Anamnesis bertahap, kesimpulan medis, penulisan resep.

---

### 4. Pemodelan Alur Kerja & Diagram Proses
#### [NEW] `03-user-journey-and-flowcharts.md`
- *User Journey Map* Pasien dari pendaftaran hingga cetak e-resep.
- Flowchart Bisnis End-to-End:
  - Alur Registrasi & Pengisian Profil Wajib Pasien.
  - Alur Pemilihan Gejala & Triage Otomatis.
  - Alur Sesi Konsultasi Live Chat.
  - Alur Generasi & Unduh Resep PDF.
- Kode diagram Mermaid yang dapat langsung dirender dan diekspor ke Draw.io.

#### [NEW] `04-usecase-and-activity-diagrams.md`
- Diagram Use Case Keseluruhan (Aktor: Pasien, Dokter Bot, Admin).
- Tabel Spesifikasi Use Case mendalam (Prekondisi, Aktor, Alur Utama, Alur Alternatif, Postkondisi).
- Activity Diagram untuk 4 proses utama:
  1. *Activity Diagram: Onboarding & Verifikasi Biodata Pasien*.
  2. *Activity Diagram: Triage Gejala & Penugasan Bot Spesialis*.
  3. *Activity Diagram: Konsultasi Interaktif & Analisis Gemini AI*.
  4. *Activity Diagram: Pembuatan Resep Obat & Pengunduhan PDF*.

---

### 5. Perancangan Basis Data & Normalisasi
#### [NEW] `05-database-design-erd-normalization.md`
- Kamus Data (*Data Dictionary*) lengkap dengan tipe data, batasan (*constraints*), dan indeks.
- Entitas Inti: `users`, `roles`, `patients` (data rekam medis dasar, riwayat alergi, golongan darah), `specializations`, `symptom_categories`, `symptoms`, `bot_doctors`, `consultation_sessions`, `chat_messages`, `diagnoses`, `medicines`, `prescriptions`, `prescription_items`, `audit_logs`.
- Proses Normalisasi Lengkap:
  - Bentuk Tidak Ternormalisasi (UNF).
  - Bentuk Normal Pertama (1NF) — Eliminasi *repeating groups* dan pemisahan nilai atomik.
  - Bentuk Normal Kedua (2NF) — Eliminasi ketergantungan parsial (*partial functional dependency*).
  - Bentuk Normal Ketiga (3NF) — Eliminasi ketergantungan transitif (*transitive functional dependency*).
- Diagram ERD Fisik & Logikal (Mermaid ERD).
- Skrip DDL SQL Schema untuk inisialisasi tabel, relasi foreign key, dan indeks.

---

### 6. Spesifikasi Teknis API & Engine AI
#### [NEW] `06-api-websocket-and-gemini-spec.md`
- Desain REST API Endpoints (Auth, Profil Pasien, Master Gejala, Sesi Konsultasi, Unduh PDF Resep).
- Protokol WebSocket untuk Live Chat (Format payload JSON kirim pesan, status bot mengetik, indikator pengalihan bot).
- *System Prompt Engineering* untuk Google Gemini:
  - Prompt untuk Bot Penengah (Triage Agent).
  - Prompt untuk Bot Dokter Umum & Spesialis (Persona dokter ramah, empati, format anamnesis SOAP).
  - Pedoman keamanan klinis & penolakan pemberian obat keras.

---

### 7. Desain UI/UX & Layout Resep Digital
#### [NEW] `07-uiux-wireframe-and-pdf-recipe.md`
- Sitemap Navigasi Aplikasi Web Pasien vs Admin.
- Wireframe struktural (ASCII / Layout Grid):
  - Halaman Dashboard Pasien (*Health Overview*).
  - Halaman Onboarding Profil Pasien (Formulir Rekam Medis Wajib).
  - Halaman Pemilih Gejala (Grid Kategori Gejala Umum vs Organ Dalam).
  - Halaman Ruang Chat Konsultasi (Dual Persona Chat UI).
- Spesifikasi Tata Letak Dokumen E-Resep PDF:
  - Kop Surat Medicare Consult & Nomor Izin Praktik Digital.
  - Identitas Pasien & Tanggal Konsultasi.
  - Rincian Resep Obat (Nama Obat, Dosis, Waktu Konsumsi, Aturan Pakai, Catatan Khusus).
  - QR Code Otentikasi & Tanda Tangan Digital.

---

### 8. File Integrasi Visual Draw.io
#### [NEW] `medicare_consult_diagrams.drawio`
- File visual berbasis XML standar Draw.io yang memuat tab diagram:
  - Tab 1: *System Architecture Diagram*.
  - Tab 2: *Business Process Flowchart*.
  - Tab 3: *Use Case Diagram*.
  - Tab 4: *Entity Relationship Diagram (ERD Physical)*.

---

## Verification Plan

### Automated / Syntax Verification
- Validasi rendering seluruh sintaks Markdown dan diagram Mermaid di lingkungan preview.
- Validasi struktur XML pada file `medicare_consult_diagrams.drawio` agar dapat diimpor sempurna di draw.io / diagrams.net tanpa galat parsing.
- Verifikasi keutuhan relasi Foreign Key pada DDL SQL yang disertakan pada modul basis data.

### Manual Verification
- Memastikan seluruh kebutuhan yang diminta pengguna terpenuhi secara mendalam:
  - [x] Hak akses multi-role (Pasien, Dokter/Bot, Admin).
  - [x] Alur bot penengah $\to$ bot dokter spesialis.
  - [x] Pembagian gejala umum vs organ dalam.
  - [x] Syarat wajib pengisian data profil pasien sebelum konsultasi.
  - [x] Pemisahan landing page (`index2.html`) vs aplikasi web konsultasi.
  - [x] Resep PDF yang dapat dicetak dan ditebus ke apotek.
  - [x] Dokumen `jobdesk.md` untuk 5 anggota Kelompok 2 (Alpian, Maulid, Sultan, Natun, Riski).
  - [x] Normalisasi database 1NF–3NF dan relasi lengkap.
