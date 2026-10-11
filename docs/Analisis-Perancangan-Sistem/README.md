# 🩺 Medicare Consult — Dokumentasi Analisis & Perancangan Sistem (APS)
> **Platform Telemedicine & Konsultasi Medis Online Berbasis Dual-Bot AI (Terinspirasi dari Halodoc)**  
> Disusun oleh **Kelompok 2** — Tema Kesehatan (*Health Tech*)

---

## 📌 Ringkasan Eksekutif Proyek

**Medicare Consult** adalah platform konsultasi kesehatan daring (*telemedicine*) cerdas yang dirancang untuk menjembatani kebutuhan pasien dalam memperoleh asesmen medis awal, rujukan dokter spesialis yang tepat, dan resep obat digital (*e-prescription*) secara instan, aman, dan terpercaya.

Proyek ini menandai evolusi (*pivot*) strategis:
- **Sebelumnya**: Proyek berfokus pada manajemen klinik fisik konvensional (*Carely Landing Page*).
- **Kini**: Proyek bertransformasi menjadi **platform konsultasi daring murni (*Medicare Consult*)**, di mana seluruh proses anamnesis, asesmen gejala, percakapan interaktif, hingga penerbitan resep obat digital berlangsung di dalam sistem aplikasi web terpadu.

Sistem ini mengadopsi model bisnis platform terkemuka seperti **Halodoc**, namun diperkuat dengan inovasi **Dual-Bot AI Architecture** yang memanfaatkan *Large Language Model (LLM)* Google Gemini:
1. **Bot Penengah (*Triage Agent*)**: Menganalisis keluhan awal pasien, mengklasifikasikan gejala (umum vs organ dalam), dan menentukan spesialisasi medis yang paling relevan.
2. **Bot Dokter Spesialis (*Doctor Persona Agent*)**: Bertindak sebagai dokter spesialis virtual yang melakukan anamnesis terstruktur, memberikan edukasi medis, menetapkan diagnosis kerja, dan menerbitkan resep digital siap cetak berformat PDF.

---

## 👥 Tim Pengembang (Kelompok 2)

| Nama Anggota | Peran / Spesialisasi | Kontribusi Dokumen Utama |
|---|---|---|
| **Alpian** | Project Leader & System Architect | [jobdesk.md](./jobdesk.md), [02-system-architecture-and-triage.md](./02-system-architecture-and-triage.md), [06-api-websocket-and-gemini-spec.md](./06-api-websocket-and-gemini-spec.md) |
| **Maulid** | Lead Business Analyst & PRD Specialist | [01-business-logic-and-prd.md](./01-business-logic-and-prd.md) |
| **Sultan** | Database Administrator & Data Modeler | [05-database-design-erd-normalization.md](./05-database-design-erd-normalization.md) |
| **Natun** | System Modeler & UML Specialist | [03-user-journey-and-flowcharts.md](./03-user-journey-and-flowcharts.md), [04-usecase-and-activity-diagrams.md](./04-usecase-and-activity-diagrams.md), [medicare_consult_diagrams.drawio](./medicare_consult_diagrams.drawio) |
| **Riski** | UI/UX Designer & Product Deliverable Lead | [07-uiux-wireframe-and-pdf-recipe.md](./07-uiux-wireframe-and-pdf-recipe.md) |

Rincian pembagian kerja, matriks RACI, dan jadwal kerja tim dapat dilihat pada [**Dokumen Pembagian Kerja (jobdesk.md)**](./jobdesk.md).

---

## 💡 Nilai Inovasi & Logika Kunci Sistem

Sistem dirancang dengan 6 pilar arsitektur dan bisnis yang kokoh:

```
[ Landing Page Publik (index2.html) ]
                │
                ▼ (Daftar / Masuk Akun)
[ Autentikasi Pengguna (Pasien / Admin) ]
                │
                ▼ (Pengalihan ke Web App Mandiri)
[ Portal Web App Medicare Consult (CRM Telehealth) ]
                │
                ▼ (Gatekeeping: Validasi Rekam Medis Pasien)
[ Profil Lengkap 100%? ] ──(TIDAK)──► [ Form Kelengkapan Biodata Medis Wajib ]
                │
              (YA)
                ▼
[ Seleksi Gejala: Gejala Umum vs Gejala Organ Dalam ]
                │
                ▼
[ Bot Penengah (Triage Agent): Analisis Keluhan & Rujukan Spesialis ]
                │
                ▼
[ Sesi Chat Real-Time (WebSocket): Bot Dokter Spesialis (Gemini AI) ]
                │
                ▼
[ Hasil Diagnosis Klinis & Generasi E-Resep PDF Siap Tebus di Apotek ]
```

1. **Pemisahan Antarmuka Publik & Aplikasi Terproteksi**:  
   Halaman *landing page* (`index2.html`) murni berfungsi untuk *branding*, pengenalan fitur, dan gerbang registrasi/login. Setelah terautentikasi, pengguna dialihkan ke sistem aplikasi web terpisah (*Single Page Application / CRM Telehealth*) yang memiliki tata letak khusus (sidebar navigasi, dasbor rekam medis, dan ruang chat interaktif).
2. **Aturan Validasi Wajib (*Patient Profile Gatekeeper*)**:  
   Pasien tidak dapat langsung melompat ke ruang konsultasi. Pasien wajib melengkapi profil biodata dasar (NIK, tanggal lahir, jenis kelamin, tinggi/berat badan, riwayat alergi obat, dan penyakit bawaan). Hal ini memastikan AI memiliki data anamnesis yang aman sebelum memberikan anjuran obat.
3. **Taksonomi Gejala Dua Tingkat**:  
   Memudahkan pasien awam memilih keluhan tanpa kebingungan istilah medis:
   - **Gejala Umum**: Batuk, pilek, flu, demam, sakit kepala, nyeri otot, pusing, kelelahan.
   - **Gejala Organ Dalam & Spesifik**: Paru-paru (sesak napas, batuk kronis), Lambung/Pencernaan (GERD, perih ulu hati, mual, diare), Jantung (debar berlebih, rasa tertekan), Saraf, serta Kulit & Kelamin.
4. **Mekanisme Mediasi Bot Ganda (*Dual-Bot Pipeline*)**:  
   Pasien berinteraksi pertama kali dengan **Bot Penengah**. Bot ini mengevaluasi urgensi dan mencocokkan keluhan dengan dokter spesialis yang paling tepat, lalu mengalihkan sesi ke **Bot Dokter Spesialis** (ditenagai Gemini API dengan *system prompt* persona dokter dan kaidah anamnesis SOAP).
5. **Output Hasil Nyata: Resep Digital PDF (*E-Prescription*)**:  
   Tujuan akhir konsultasi bukan sekadar obrolan, melainkan solusi terapeutik: Pasien mendapatkan berkas PDF resmi berisikan diagnosis ringkas, anjuran gaya hidup, daftar obat golongan bebas/bebas terbatas dengan dosis presisi, dan QR Code verifikasi untuk dicetak dan ditebus ke apotek terdekat.
6. **Desain Basis Data Relasional Ternormalisasi (1NF–3NF)**:  
   Menjamin konsistensi data riwayat konsultasi, katalog obat, spesialisasi dokter, dan pesan chat tanpa anomali redudansi.

---

## 📂 Struktur Dokumentasi Analisis & Perancangan Sistem (APS)

Setiap bagian dari perancangan sistem ini telah diuraikan ke dalam berkas-berkas modular berikut:

| Berkas | Judul Dokumen | Ringkasan Konten |
|---|---|---|
| 📄 [**jobdesk.md**](./jobdesk.md) | Pembagian Kerja Kelompok 2 | Matriks RACI, rincian peran, target pengerjaan, dan standar *Definition of Done*. |
| 📄 [**01-business-logic-and-prd.md**](./01-business-logic-and-prd.md) | Logika Bisnis & PRD | Studi kasus, analisis Halodoc, kebutuhan fungsional (FR) & non-fungsional (NFR), taksonomi gejala, dan batasan klinis. |
| 📄 [**02-system-architecture-and-triage.md**](./02-system-architecture-and-triage.md) | Arsitektur Sistem & Alur Dual-Bot | Arsitektur 3-tier, transisi landing page ke web app, alur orkestrasi Triage Bot $\to$ Doctor Bot Gemini. |
| 📄 [**03-user-journey-and-flowcharts.md**](./03-user-journey-and-flowcharts.md) | User Journey & Flowchart Sistem | Peta perjalanan pengguna (*User Journey Map*) dan diagram alir proses bisnis end-to-end (Mermaid). |
| 📄 [**04-usecase-and-activity-diagrams.md**](./04-usecase-and-activity-diagrams.md) | Use Case & Activity Diagrams | Diagram Use Case, tabel spesifikasi skenario lengkap, dan Activity Diagrams untuk tiap aktivitas bisnis krusial. |
| 📄 [**05-database-design-erd-normalization.md**](./05-database-design-erd-normalization.md) | Basis Data, ERD, & Normalisasi | Kamus data terperinci, tahapan normalisasi 1NF, 2NF, 3NF, skema relasional, dan skrip DDL SQL lengkap. |
| 📄 [**06-api-websocket-and-gemini-spec.md**](./06-api-websocket-and-gemini-spec.md) | Spesifikasi API & AI Gemini Engine | Kontrak REST API, skema WebSocket real-time chat, dan rekayasa *system prompt* AI Gemini untuk persona medis. |
| 📄 [**07-uiux-wireframe-and-pdf-recipe.md**](./07-uiux-wireframe-and-pdf-recipe.md) | Wireframe Antarmuka & Layout Resep PDF | Peta situs (*sitemap*), *wireframe* tata letak aplikasi web (onboarding, chat, triage), dan template PDF e-resep resmi. |
| 📦 [**medicare_consult_diagrams.drawio**](./medicare_consult_diagrams.drawio) | Berkas Visual Draw.io Multi-Tab | Berkas XML Draw.io siap buka yang memuat seluruh diagram arsitektur, flowchart, use case, dan ERD fisik. |

---

## 🛠️ Metodologi Analisis: *User-Centered Design (UCD)*

Penyusunan analisis sistem ini mempedomani siklus UCD yang berfokus pada kebutuhan pasien saat sakit:
1. **Empathize & Research**: Memahami kecemasan pasien yang ingin segera tahu obat yang harus diminum tanpa antre lama di fasilitas kesehatan.
2. **Define**: Menetapkan batasan masalah: sistem berfokus pada keluhan umum dan organ dalam kategori ringan-sedang, dengan rujukan otomatis untuk kondisi darurat.
3. **Design**: Memodelkan interaksi sederhana: pemilihan gejala visual $\to$ bot penengah yang ramah $\to$ dokter spesialis AI yang berempati $\to$ resep instan.
4. **Prototype**: Merancang skema arsitektur, basis data ternormalisasi, dan antarmuka aplikasi web.
5. **Evaluate**: Meninjau rancangan bersama dosen/asisten lab dengan dasar dokumen APS yang terstruktur dan lengkap.
