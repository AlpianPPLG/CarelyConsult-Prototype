# 📐 Dokumen Pemodelan UML: Use Case & Activity Diagrams
## Proyek: Medicare Consult (Telehealth Platform)
> **Penyusun Utama:** Natun (System Modeler & UML Specialist)  
> **Konsultan Bisnis:** Maulid (Lead Business Analyst)  
> **Modul:** 04 — Use Case & Activity Diagrams

---

## 1. 👥 Diagram Use Case Sistem (Use Case Diagram)

Diagram Use Case berikut memodelkan fungsionalitas sistem yang berinteraksi dengan tiga aktor utama: **Pasien**, **Dokter Virtual (AI Persona)**, dan **Administrator Sistem**.

```mermaid
graph LR
    Pasien((Pasien))
    DokterBot((Dokter Bot AI))
    Admin((Administrator))

    subgraph Batasan Sistem Medicare Consult
        UC01([UC-01: Registrasi & Login Akun])
        UC02([UC-02: Lengkapi Rekam Medis Wajib])
        UC03([UC-03: Pilih Kategori Gejala Penyakit])
        UC04([UC-04: Triage Keluhan Medis Awal])
        UC05([UC-05: Konsultasi Chat Real-Time])
        UC06([UC-06: Deteksi Red Flag Darurat])
        UC07([UC-07: Tetapkan Diagnosis Awal])
        UC08([UC-08: Terbitkan & Unduh E-Resep PDF])
        UC09([UC-09: Kelola Master Gejala & Spesialis])
        UC10([UC-10: Kelola Katalog Farmasi / Obat])
        UC11([UC-11: Monitoring & Audit Log Sesi])
    end

    Pasien --> UC01
    Pasien --> UC02
    Pasien --> UC03
    Pasien --> UC05
    Pasien --> UC08

    UC03 -.->|<<include>>| UC02
    UC04 -.->|<<include>>| UC03
    UC05 -.->|<<include>>| UC04
    UC06 -.->|<<extend>>| UC05
    UC07 -.->|<<include>>| UC05
    UC08 -.->|<<include>>| UC07

    DokterBot --> UC04
    DokterBot --> UC05
    DokterBot --> UC06
    DokterBot --> UC07
    DokterBot --> UC08

    Admin --> UC09
    Admin --> UC10
    Admin --> UC11
```

---

## 2. 📋 Tabel Spesifikasi Skenario Use Case

### 2.1 Skenario UC-02: Lengkapi Rekam Medis Wajib Pasien (*Profile Gatekeeping*)

| Elemen Skenario | Deskripsi Rinci |
|---|---|
| **Use Case ID** | **UC-02** |
| **Nama Use Case** | Lengkapi Rekam Medis Wajib Pasien (*Patient Profile Gatekeeping*) |
| **Aktor Utama** | Pasien |
| **Deskripsi Singkat** | Pasien mengisi biodata medis esensial (NIK, tanggal lahir, jenis kelamin, golongan darah, tinggi/berat badan, alergi obat, dan penyakit bawaan) sebagai syarat mutlak sebelum dapat mengakses layanan konsultasi. |
| **Prekondisi** | Pasien telah berhasil masuk (*login*) ke dalam portal Web App Medicare Consult. |
| **Postkondisi** | Status pasien diperbarui menjadi `profile_completed = TRUE` dan tombol "Mulai Konsultasi" aktif. |
| **Alur Normal (*Main Flow*)** | 1. Pasien membuka halaman profil medis atau diarahkan otomatis dari dasbor utama.<br>2. Sistem menampilkan formulir data diri dan kuesioner medis wajib.<br>3. Pasien memasukkan NIK, tanggal lahir, jenis kelamin, dan golongan darah.<br>4. Pasien memasukkan berat badan (kg) dan tinggi badan (cm).<br>5. Pasien memilih opsi riwayat alergi obat (atau mencentang *"Tidak Memiliki Riwayat Alergi"*).<br>6. Pasien memilih atau mengosongkan riwayat penyakit kronis bawaan.<br>7. Pasien menekan tombol *"Simpan Profil Medis"*.<br>8. Sistem memvalidasi kelengkapan semua bidang mandatory.<br>9. Sistem menyimpan data ke tabel `patients`.<br>10. Sistem menampilkan notifikasi sukses dan mengaktifkan fitur konsultasi. |
| **Alur Alternatif (*Alternative Flow*)** | **8a. Bidang Wajib Belum Terisi Lengkap:**<br>1. Sistem mendeteksi adanya kolom penting yang kosong (misal: belum memilih opsi alergi obat).<br>2. Sistem menolak penyimpanan dan menandai kolom yang belum diisi dengan warna merah.<br>3. Sistem menampilkan instruksi: *"Seluruh data medis wajib dilengkapi demi keselamatan konsultasi klinis."*<br>4. Pasien melengkapi data dan menekan tombol simpan kembali (kembali ke langkah 7). |

---

### 2.2 Skenario UC-04: Triage Keluhan Medis Awal oleh Bot Penengah

| Elemen Skenario | Deskripsi Rinci |
|---|---|
| **Use Case ID** | **UC-04** |
| **Nama Use Case** | Triage Keluhan Medis Awal (*Symptom Triage & Specialist Routing*) |
| **Aktor Utama** | Pasien, Bot Penengah (*Triage Agent*) |
| **Deskripsi Singkat** | Bot Penengah menganalisis keluhan yang dipilih dan diketik oleh pasien untuk menentukan apakah kasus bersifat darurat atau dapat diteruskan ke dokter spesialis tertentu. |
| **Prekondisi** | Pasien berstatus `profile_completed = TRUE` dan telah memilih kategori gejala (Umum atau Organ Dalam). |
| **Postkondisi** | Spesialisasi dokter terpilih dan sesi obrolan dialihkan ke persona dokter spesialis yang relevan. |
| **Alur Normal (*Main Flow*)** | 1. Pasien memilih sub-gejala yang tersedia dan mengetikkan uraian keluhan tambahan.<br>2. Pasien menekan tombol *"Kirim Keluhan ke Bot Penengah"*.<br>3. Bot Penengah membaca keluhan dan mengajukan 1-2 pertanyaan klarifikasi terkait durasi gejala dan tingkat keparahan.<br>4. Pasien merespons pertanyaan klarifikasi.<br>5. Bot Penengah mengevaluasi aturan pemetaan spesialisasi.<br>6. Bot Penengah menyimpulkan bahwa pasien memerlukan penanganan Dokter Spesialis (misal: Spesialis Pulmonologi untuk keluhan batuk sesak).<br>7. Bot Penengah menginformasikan kepada pasien bahwa sesi akan dialihkan ke dokter spesialis terkait.<br>8. Sistem melakukan serah terima (*session handover*) ke ruang chat dokter spesialis. |
| **Alur Alternatif (*Alternative Flow*)** | **5a. Deteksi Gejala Kegawatdaruratan (*Red Flags*):**<br>1. Bot Penengah mendeteksi kata kunci bahaya (misal: sesak napas berat, nyeri dada tembus ke punggung, batuk darah).<br>2. Bot Penengah menghentikan proses perujukan biasa.<br>3. Sistem memunculkan jendela darurat: *"Peringatan Medis: Gejala Anda memerlukan penanganan darurat segera!"*<br>4. Sistem menyertakan panduan pertolongan pertama dan kontak IGD terdekat / ambulans 119.<br>5. Konsultasi bot dibatalkan secara aman demi keselamatan pasien. |

---

### 2.3 Skenario UC-05: Konsultasi Chat Real-Time dengan Dokter Bot Gemini

| Elemen Skenario | Deskripsi Rinci |
|---|---|
| **Use Case ID** | **UC-05** |
| **Nama Use Case** | Konsultasi Chat Real-Time (*Interactive Teleconsultation*) |
| **Aktor Utama** | Pasien, Dokter Bot Spesialis (*Gemini AI Engine*) |
| **Deskripsi Singkat** | Pasien dan Dokter Bot berdialog secara interaktif melalui koneksi WebSocket untuk melakukan tanya-jawab klinis (anamnesis) hingga dokter menyimpulkan masalah kesehatan pasien. |
| **Prekondisi** | Handover dari Bot Penengah berhasil dan ruang obrolan WebSocket telah terhubung. |
| **Postkondisi** | Percakapan selesai, diagnosis kerja ditetapkan, dan sesi siap menerbitkan resep obat. |
| **Alur Normal (*Main Flow*)** | 1. Dokter Bot menyapa pasien dengan ramah dan menyebutkan rangkuman keluhan awal yang diterima dari Bot Penengah.<br>2. Dokter Bot mengajukan pertanyaan terstruktur (faktor pencetus, riwayat konsumsi makanan/obat sebelumnya).<br>3. Pasien membalas pertanyaan dokter melalui kotak input pesan.<br>4. Sistem menampilkan indikator *"Dokter sedang mengetik..."* saat AI memproses jawaban.<br>5. Dokter Bot memberikan penjelasan mengenai mekanisme tubuh dan anjuran non-farmakologis (istirahat, asupan cairan, kompres hangat, dsb.).<br>6. Dokter Bot mengonfirmasi apakah pasien memiliki pertanyaan tambahan.<br>7. Pasien menyatakan telah memahami penjelasan dokter.<br>8. Dokter Bot menutup sesi konsultasi dan mengaktifkan pembuatan resep. |
| **Alur Alternatif (*Alternative Flow*)** | **3a. Koneksi Internet Pasien Terputus:**<br>1. Sesi WebSocket mendeteksi putusnya sambungan jaringan (*socket disconnect*).<br>2. Sistem menampilkan banner: *"Koneksi terputus. Mencoba menghubungkan kembali..."*<br>3. Riwayat pesan tersimpan aman di database lokal.<br>4. Saat koneksi pulih, sistem menyinkronkan pesan terakhir tanpa kehilangan progres anamnesis. |

---

### 2.4 Skenario UC-08: Terbitkan & Unduh E-Resep PDF Resmi

| Elemen Skenario | Deskripsi Rinci |
|---|---|
| **Use Case ID** | **UC-08** |
| **Nama Use Case** | Terbitkan & Unduh E-Resep PDF Resmi (*E-Prescription Issuance & Download*) |
| **Aktor Utama** | Pasien, Dokter Bot AI |
| **Deskripsi Singkat** | Sistem menyusun formulir resep digital resmi berdasarkan saran obat bebas/terbatas dari dokter bot, menghasilkan berkas PDF ber-QR Code, dan menyediakannya untuk diunduh pasien. |
| **Prekondisi** | Konsultasi telah selesai (UC-05) dan diagnosis kerja telah terbentuk (UC-07). |
| **Postkondisi** | Berkas PDF E-Resep tersimpan di server dan terunduh ke perangkat lokal pasien. |
| **Alur Normal (*Main Flow*)** | 1. Dokter Bot mengirimkan payload resep obat (nama obat, dosis, sediaan, waktu minum, aturan sebelum/sesudah makan).<br>2. Sistem memverifikasi kembali bahwa tidak ada obat yang memicu alergi pasien.<br>3. Mesin PDF Generator menyusun layout dokumen resmi dengan kop surat Medicare Consult, nomor SIP dokter virtual, dan QR Code verifikasi.<br>4. Berkas PDF disimpan di penyimpanan server dengan penamaan unik (contoh: `RX-202610-001.pdf`).<br>5. Ruang chat menampilkan kartu resep dengan tombol *"Unduh E-Resep PDF"*.<br>6. Pasien mengklik tombol unduh.<br>7. Beramban pasien mengunduh berkas PDF siap cetak.<br>8. Pasien dapat membawa resep cetak ke apotek terdekat untuk ditebus. |

---

## 3. 🏃 Diagram Aktivitas (Activity Diagrams)

### 3.1 Activity Diagram 1: Onboarding Pasien & Gatekeeper Rekam Medis

```mermaid
stateDiagram-v2
    [*] --> BukaAplikasi
    BukaAplikasi --> PeriksaStatusProfil
    
    state PeriksaStatusProfil <<choice>>
    PeriksaStatusProfil --> DasborAktif : Jika profile_completed == TRUE
    PeriksaStatusProfil --> TampilkanFormWajib : Jika profile_completed == FALSE
    
    TampilkanFormWajib --> InputBiodata : Pasien mengisi NIK, Usia, Gender, BB, TB
    InputBiodata --> InputAlergi : Pasien memilih opsi alergi obat
    InputAlergi --> SimpanData : Pasien klik Simpan
    
    state ValidasiInput <<choice>>
    SimpanData --> ValidasiInput
    ValidasiInput --> TampilkanPesanGalat : Kolom mandatory kosong
    TampilkanPesanGalat --> TampilkanFormWajib
    
    ValidasiInput --> UpdateDatabase : Data lengkap & sah
    UpdateDatabase --> SetProfilLengkap : Ubah profile_completed = TRUE
    SetProfilLengkap --> DasborAktif
    DasborAktif --> [*]
```

---

### 3.2 Activity Diagram 2: Triage Gejala & Penugasan Dokter Spesialis

```mermaid
stateDiagram-v2
    [*] --> KlikMulaiKonsultasi
    KlikMulaiKonsultasi --> PilihKategoriGejala : Pasien memilih Umum atau Organ Dalam
    PilihKategoriGejala --> InputKeluhanDetail : Pasien mencentang gejala & ketik keluhan
    InputKeluhanDetail --> KirimKeTriage : Kirim ke Bot Penengah
    
    KirimKeTriage --> AnalisisKataKunci : Triage Bot evaluasi teks keluhan
    
    state EvaluasiRedFlag <<choice>>
    AnalisisKataKunci --> EvaluasiRedFlag
    EvaluasiRedFlag --> TriggerDarurat : Ditemukan indikasi Red Flag (Gawat Darurat)
    TriggerDarurat --> TampilkanRujukanIGD : Instruksi ke Rumah Sakit + Telp 119
    TampilkanRujukanIGD --> [*]
    
    EvaluasiRedFlag --> KlasifikasiSpesialis : Gejala aman (Kategori Ringan - Sedang)
    KlasifikasiSpesialis --> TentukanDokter : Petakan kode spesialisasi (Paru/Lambung/Kulit/Umum)
    TentukanDokter --> HandoverKonteks : Kemas biodata + keluhan ke sesi dokter
    HandoverKonteks --> SambungkanKeRuangChat : Buka koneksi WebSocket ke Dokter Bot
    SambungkanKeRuangChat --> [*]
```

---

### 3.3 Activity Diagram 3: Konsultasi Interaktif & Analisis Klinis (Metode SOAP)

```mermaid
stateDiagram-v2
    [*] --> DokterKirimSalamPembuka
    DokterKirimSalamPembuka --> KonfirmasiKeluhanUtama
    
    KonfirmasiKeluhanUtama --> PasienBalasPesan : Pasien kirim tanggapan
    PasienBalasPesan --> GeminiMemproses : Server oper pesan ke Google Gemini
    GeminiMemproses --> TampilkanIndikatorKetik : UI tampilkan "Dokter sedang mengetik..."
    
    GeminiMemproses --> DokterKirimBalasan : Dokter bot berikan respons edukatif
    
    state CekKelengkapanAnamnesis <<choice>>
    DokterKirimBalasan --> CekKelengkapanAnamnesis
    CekKelengkapanAnamnesis --> PasienBalasPesan : Masih butuh data tambahan
    CekKelengkapanAnamnesis --> TetapkanDiagnosis : Data klinis sudah cukup
    
    TetapkanDiagnosis --> TampilkanRangkumanKlinis : Dokter paparkan diagnosa & edukasi
    TampilkanRangkumanKlinis --> BeralihKeResep
    BeralihKeResep --> [*]
```

---

### 3.4 Activity Diagram 4: Penerbitan Resep Obat Digital & Cetak PDF

```mermaid
stateDiagram-v2
    [*] --> DokterRumuskanResep : Dokter tentukan obat golongan bebas/terbatas
    DokterRumuskanResep --> CekAlergiPasien : Sistem bandingkan nama obat vs riwayat alergi
    
    state EvaluasiAlergi <<choice>>
    CekAlergiPasien --> EvaluasiAlergi
    EvaluasiAlergi --> GantiObatAman : Ditemukan potensi alergi
    GantiObatAman --> CekAlergiPasien
    
    EvaluasiAlergi --> KunciDaftarObat : Aman dari alergen
    KunciDaftarObat --> PanggilPDFGenerator : Kirim payload resep ke engine PDF
    
    PanggilPDFGenerator --> SusunLayoutPDF : Tambahkan Kop Medicare, SIP, & QR Code
    SusunLayoutPDF --> SimpanBerkasKeServer : Tulis file biner RX-XXXX.pdf
    SimpanBerkasKeServer --> KirimTautanUnduh : Munculkan tombol unduh di chat
    
    KirimTautanUnduh --> PasienKlikUnduh : Pasien download berkas
    PasienKlikUnduh --> PasienCetakResep : Cetak fisik / bawa ke Apotek
    PasienCetakResep --> [*]
```
