# 🎨 Dokumen Desain Antarmuka (UI/UX) & Tata Letak Dokumen E-Resep PDF
## Proyek: Medicare Consult (Telehealth Platform)
> **Penyusun Utama:** Riski (UI/UX Designer & Product Deliverable Lead)  
> **Konsultan Fungsional:** Maulid & Alpian  
> **Modul:** 07 — UI/UX Wireframe & PDF Prescription Specification

---

## 1. 🗺️ Peta Situs Aplikasi (*Application Sitemap*)

Sistem Medicare Consult membagi ruang navigasi menjadi tiga zona terpisah dengan tingkat otorisasi yang berbeda:

```
[ PETA SITUS MEDICARE CONSULT ]
│
├── 1. ZONA PUBLIK (Informasi & Akuisisi)
│   ├── / (index2.html - Landing Page Utama)
│   │   ├── Fitur & Layanan Telehealth
│   │   ├── Showcase Dokter Spesialis AI
│   │   ├── Mood Tracker & Health Widgets
│   │   └── Testimoni & Kontak
│   ├── /auth/login (Halaman Masuk Akun)
│   └── /auth/register (Halaman Pendaftaran Pasien Baru)
│
├── 2. ZONA PRIVAT PASIEN (Web App Portal / CRM)
│   ├── /app/dashboard (Dasbor Ringkasan Pasien & Status Rekam Medis)
│   ├── /app/profile (Formulir Kelengkapan Rekam Medis Wajib / Gatekeeper)
│   ├── /app/consultation
│   │   ├── /select-symptoms (Pemilih Kategori: Gejala Umum vs Organ Dalam)
│   │   ├── /triage (Interaksi Keluhan Awal dengan Bot Penengah)
│   │   └── /chat/:sessionId (Ruang Chat Real-time dengan Dokter Spesialis AI)
│   ├── /app/prescriptions (Daftar Riwayat E-Resep Pasien)
│   └── /app/prescriptions/:rxNumber/view (Pratinjau & Pengunduhan Berkas PDF)
│
└── 3. ZONA ADMINISTRATOR (Manajemen & Audit)
    ├── /admin/dashboard (Statistik Sesi & Volume Konsultasi)
    ├── /admin/master-symptoms (Kelola Kategori & Daftar Gejala)
    ├── /admin/master-doctors (Kelola Persona Bot & No. SIP Virtual)
    ├── /admin/medicines (Katalog Farmasi & Batasan Dosis Obat)
    └── /admin/audit-logs (Monitoring Percakapan & Kepatuhan Etika Medis)
```

---

## 2. 📐 Wireframe Struktural (ASCII Visual Layout)

### 2.1 Wireframe 1: Dasbor Pasien & Indikator Gatekeeper (`/app/dashboard`)

```
+-----------------------------------------------------------------------------------------+
| [🩺 Medicare Consult]        Dashboard   Riwayat Konsultasi   E-Resep     (Andi P.) [Keluar]|
+-----------------------------------------------------------------------------------------+
|                                                                                         |
|  [!] PERINGATAN KELENGKAPAN DATA MEDIS:                                                  |
|  Profil rekam medis Anda baru terisi 40%. Sesuai standar keselamatan klinis, Anda       |
|  WAJIB melengkapi biodata fisik & riwayat alergi obat sebelum memulai konsultasi.       |
|  [ Lengkapi Data Sekarang -> ]                                                          |
|                                                                                         |
|  +-----------------------------------------------------------------------------------+  |
|  | 👋 Selamat Datang, Andi Pratama                                                   |  |
|  | Dapatkan asesmen medis terpercaya dan resep obat digital dalam hitungan menit.    |  |
|  +-----------------------------------------------------------------------------------+  |
|                                                                                         |
|  AKSI CEPAT LAYANAN:                                                                    |
|  +-------------------------------------+   +-----------------------------------------+  |
|  | 🚀 MULAI KONSULTASI BARU            |   | 💊 RIWAYAT RESEP DIGITAL                |  |
|  | Hubungkan keluhan Anda dengan dokter|   | Unduh kembali resep PDF Anda yang siap  |  |
|  | spesialis virtual terbaik kami.     |   | dicetak dan ditebus di apotek terdekat. |  |
|  |                                     |   |                                         |  |
|  | [🔒 Terkunci - Lengkapi Profil]     |   | [ Buka Arsip Resep -> ]                 |  |
|  +-------------------------------------+   +-----------------------------------------+  |
|                                                                                         |
|  RINGKASAN KESEHATAN ANDA:                                                              |
|  - Usia: Belum Diisi     - Golongan Darah: Belum Diisi     - Riwayat Alergi: [!] Wajib  |
+-----------------------------------------------------------------------------------------+
```

---

### 2.2 Wireframe 2: Formulir Rekam Medis Wajib / Gatekeeper (`/app/profile`)

```
+-----------------------------------------------------------------------------------------+
| [🩺 Medicare Consult] > Formulir Rekam Medis Pasien Wajib (Gatekeeper)                  |
+-----------------------------------------------------------------------------------------+
|                                                                                         |
|  LENGKAPI BIODATA REKAM MEDIS                                                           |
|  Data ini digunakan oleh sistem AI untuk menghitung dosis dan mencegah alergi obat.      |
|                                                                                         |
|  1. IDENTITAS UTAMA                                                                     |
|  Nama Lengkap (KTP) : [ Andi Pratama                                              ]     |
|  Nomor KTP (NIK)    : [ 3201234567890001                                          ]     |
|  Tanggal Lahir      : [ 14 / 05 / 1998 ]     Jenis Kelamin : (o) Laki-laki  ( ) Wanita  |
|  Nomor WhatsApp/HP  : [ +62 812-3456-7890                                         ]     |
|                                                                                         |
|  2. DATA FISIK KLINIS                                                                   |
|  Golongan Darah     : [ O  v ]                                                          |
|  Berat Badan (kg)   : [ 68.5 ] kg            Tinggi Badan (cm) : [ 172.0 ] cm           |
|                                                                                         |
|  3. KESELAMATAN OBAT & KONTRAINDIKASI (MUTLAK DIISI!)                                    |
|  Riwayat Alergi Obat:                                                                   |
|  [ ] Saya TIDAK MEMILIKI riwayat alergi obat apapun (Aman)                              |
|  [x] Saya memiliki alergi terhadap obat: [ Penisilin / Amoxicillin                ]     |
|                                                                                         |
|  Riwayat Penyakit Bawaan / Kronis:                                                      |
|  [ Gastritis Ringan (Maag Akut bila telat makan)                                  ]     |
|                                                                                         |
|  [ Batal ]                                           [ SIMPAN PROFIL REKAM MEDIS -> ]   |
+-----------------------------------------------------------------------------------------+
```

---

### 2.3 Wireframe 3: Selektor Gejala — Umum vs Organ Dalam (`/app/consultation/select-symptoms`)

```
+-----------------------------------------------------------------------------------------+
| [🩺 Medicare Consult] > Mulai Konsultasi > Pilih Kategori Keluhan                       |
+-----------------------------------------------------------------------------------------+
|                                                                                         |
|  APA YANG SEDANG ANDA RASAKAN SAAT INI?                                                 |
|  Pilihlah kelompok keluhan yang paling menggambarkan kondisi tubuh Anda:                 |
|                                                                                         |
|  +--------------------------------------+   +----------------------------------------+  |
|  | [🌟 KELOMPOK GEJALA UMUM]            |   | [🫁 KELOMPOK GEJALA ORGAN DALAM]       |  |
|  | Cocok untuk keluhan harian sistemik  |   | Keluhan berfokus pada organ tertentu:  |  |
|  | yang sering terjadi:                 |   | pernapasan, pencernaan, atau kulit:    |  |
|  |                                      |   |                                        |  |
|  | [x] Batuk & Pilek Harian             |   | [x] Paru & Napas (Sesak/Mengi/Batuk >2w|  |
|  | [ ] Demam, Menggigil, & Meriang      |   | [ ] Lambung & GERD (Nyeri Ulu Hati)    |  |
|  | [ ] Sakit Kepala, Pusing, Migrain    |   | [ ] Jantung & Berdebar-debar           |  |
|  | [ ] Pegal Linu, Nyeri Otot & Sendi   |   | [ ] Kulit, Ruam Alergi, & Biduran      |  |
|  |                                      |   |                                        |  |
|  | [ Pilih Kategori Umum ]              |   | [ Pilih Kategori Organ Dalam (Dipilih)]|  |
|  +--------------------------------------+   +----------------------------------------+  |
|                                                                                         |
|  URAIKAN KELUHAN ANDA SECARA BEBAS:                                                     |
|  [ Dada terasa agak sesak saat tarik napas panjang, batuk berdahak kental sejak 3 hari. ]|
|                                                                                         |
|  [ <- Kembali ]                                      [ KIRIM KE BOT PENENGAH (TRIAGE) ->]|
+-----------------------------------------------------------------------------------------+
```

---

### 2.4 Wireframe 4: Ruang Chat Telehealth Interaktif (`/app/consultation/chat/:id`)

```
+-----------------------------------------------------------------------------------------+
| [🩺 Medicare Consult]  Dokter: dr. Farah, Sp.P (Spesialis Paru)     Status: [Online 🟢] |
+-----------------------------------------------------------------------------------------+
| [10:02] Bot Penengah Medicare:                                                          |
|         "Halo Andi, keluhan batuk berdahak dan sesak napas Anda telah kami teruskan     |
|          kepada dr. Farah, Sp.P. Dokter sedang membaca rekam medis Anda."               |
|                                                                                         |
| [10:03] dr. Farah, Sp.P (Bot Pulmonologi):                                              |
|         "Halo Andi, salam kenal. Saya dr. Farah. Saya melihat Anda mengalami batuk      |
|          berdahak kental dan dada agak sesak sejak 3 hari lalu.                         |
|          Apakah dahaknya berwarna hijau kekuningan, dan apakah ada riwayat asma?"       |
|                                                                                         |
|                                                   [10:04] Andi Pratama (Anda):          |
|                                                           "Dahaknya kuning dok, saya    |
|                                                            tidak punya riwayat asma."   |
|                                                                                         |
| [10:05] dr. Farah, Sp.P (Bot Pulmonologi):                                              |
|         "Baik Andi. Berdasarkan anamnesis, Anda mengalami gejala Bronkitis Akut Ringan. |
|          Berikut anjuran istirahat dan resep obat pereda gejala yang aman untuk Anda."  |
|                                                                                         |
|         +------------------------------------------------------------------------+      |
|         | 📄 RESEP DIGITAL TERBIT: RX-20261005-0812                              |      |
|         | Diagnosa: Bronkitis Akut Ringan (ICD-10: J20.9)                        |      |
|         | Obat 1: Ambroxol Sirup 30mg/5ml (3x1 sendok takar sesudah makan)       |      |
|         | Obat 2: Vitamin C 500mg Tablet (1x1 tablet per hari)                   |      |
|         | Catatan: Hindari minuman dingin, perbanyak air hangat & istirahat.     |      |
|         |                                                                        |      |
|         | [ 📥 UNDUH E-RESEP RESMI (PDF BER-QR CODE) ]                           |      |
|         +------------------------------------------------------------------------+      |
|                                                                                         |
+-----------------------------------------------------------------------------------------+
| [ Ketik balasan Anda di sini...                                              ] [Kirim ✉️]|
+-----------------------------------------------------------------------------------------+
```

---

## 3. 📄 Spesifikasi Tata Letak Dokumen E-Resep PDF (*Official E-Prescription*)

Dokumen E-Resep dirancang siap cetak (*Print-Ready A5/A4 Layout*) dengan standar format resep dokter Indonesia yang sah untuk ditebus di apotek fisik:

```
+-----------------------------------------------------------------------------------------+
|                                    MEDICARE CONSULT                                     |
|                           Layanan Telemedisin & Konsultasi Digital                      |
|                  Surat Tanda Registrasi Kemenkes RI No: 042/TD-TLM/2026                 |
|             Jl. Kesehatan Digital No. 88, Jakarta | Hotline Bantuan: 1500-888           |
+-----------------------------------------------------------------------------------------+
|                                    RESEP ELEKTRONIK                                     |
|                                 No. Resep: RX-20261005-0812                             |
+-----------------------------------------------------------------------------------------+
| TANGGAL KONSULTASI : 05 Oktober 2026                  MASA BERLAKU : s.d. 12 Okt 2026   |
| DOKTER PEMERIKSA   : dr. Farah, Sp.P                  NO. SIP VIRT : SIP.440/129/SP-P   |
| SPESIALISASI       : Pulmonologi & Respirasi          KODE SESI    : MC-20261005-0812   |
+-----------------------------------------------------------------------------------------+
| IDENTITAS PASIEN:                                                                       |
| Nama Lengkap : Andi Pratama                           Usia / Gender : 28 Th / Laki-laki |
| NIK          : 3201234567890001                       Berat / Tinggi: 68.5 kg / 172 cm  |
| Alergi Obat  : Penisilin / Amoxicillin                Penyakit Lain : Gastritis Ringan  |
+-----------------------------------------------------------------------------------------+
| KESIMPULAN KLINIS:                                                                      |
| Diagnosis Primer : Bronkitis Akut Ringan (ICD-10: J20.9)                                |
| Terapi Non-Obat  : Istirahat tirah baring minimal 2 hari, hidrasi air hangat 2.5L/hari, |
|                    hindari paparan asap rokok dan pendingin ruangan berlebih.           |
+-----------------------------------------------------------------------------------------+
| RINCIAN RESEP OBAT (FORMULA R/):                                                        |
|                                                                                         |
|   R/  Ambroxol Sirup 30 mg / 5 ml                                     Fl. No. I         |
|       S 3 d d cth I  p.c. (3x sehari 1 sendok takar 5 ml, sesudah makan)                |
|       -------------------------------------------------------------                     |
|                                                                                         |
|   R/  Vitamin C 500 mg Tablet                                         Tab. No. X        |
|       S 1 d d tab I  p.c. mane (1x sehari 1 tablet, pagi hari sesudah makan)            |
|       -------------------------------------------------------------                     |
|                                                                                         |
+-----------------------------------------------------------------------------------------+
| CATATAN KEAMANAN & TEBUS APOTEK:                                                        |
| 1. Seluruh obat yang diresepkan masuk dalam kategori Obat Bebas & Bebas Terbatas.       |
| 2. Pasien memiliki pantangan obat golongan Penisilin (Telah diverifikasi sistem aman).  |
| 3. Resep ini sah untuk dicetak dan ditebus di Apotek Kimia Farma, K-24, atau Apotek     |
|    Berizin Resmi mana pun di wilayah Republik Indonesia.                                |
+-----------------------------------------------------------------------------------------+
|                                           |                                             |
|   [ QR CODE OTENTIKASI RESEP ]            |              DOKTER PEMERIKSA               |
|                                           |            Tanda Tangan Digital             |
|   (Pindai untuk verifikasi integritas     |                                             |
|    data di server Medicare Consult)       |               [ CAP DIGITAL ]               |
|                                           |                                             |
|   Hash: 8a7f9c2e4b1a03...                 |             (dr. Farah, Sp.P)               |
|                                           |         SIP: SIP.440/129/SP-P/2026          |
+-----------------------------------------------------------------------------------------+
| DISCLAIMER: Berkas ini diterbitkan melalui sistem asistensi AI Medicare Consult dengan   |
| pengawasan protokol klinis terstandar. Bila gejala berlanjut >3 hari atau memburuk,     |
| segera hubungi fasilitas pelayanan kesehatan terdekat.                                  |
+-----------------------------------------------------------------------------------------+
```
