# 🔌 Dokumen Spesifikasi API, WebSocket, & Rekayasa Prompt Gemini AI
## Proyek: Medicare Consult (Telehealth Platform)
> **Penyusun Utama:** Alpian (Project Leader & System Architect)  
> **Konsultan Teknis:** Riski & Sultan  
> **Modul:** 06 — API, WebSocket, & Gemini AI Specification

---

## 1. 🌐 Spesifikasi Kontrak REST API (HTTP Endpoints)

Seluruh komunikasi pertukaran data terstruktur di luar ruang obrolan obrolan langsung dilayani melalui REST API berbasis JSON dengan standar otentikasi JWT (*Bearer Token*).

```
Base URL: https://api.medicareconsult.com/api/v1
Format Pertukaran: application/json; charset=utf-8
Header Standar: Authorization: Bearer <JWT_TOKEN>
```

### 1.1 Modul Autentikasi Pengguna (`/auth`)

#### `POST /auth/register`
Mendaftarkan akun pengguna baru (Pasien).
- **Request Body:**
  ```json
  {
    "email": "pasien.andi@gmail.com",
    "password": "PasswordKuat2026!",
    "full_name": "Andi Pratama"
  }
  ```
- **Response `201 Created`:**
  ```json
  {
    "status": "success",
    "message": "Registrasi berhasil. Silakan lengkapi profil rekam medis Anda.",
    "data": {
      "user_id": "usr-8a21f7d4-b912",
      "email": "pasien.andi@gmail.com",
      "role": "PATIENT",
      "is_profile_completed": false,
      "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
    }
  }
  ```

#### `POST /auth/login`
Mengautentikasi pengguna dan mengembalikan token sesi JWT.
- **Request Body:**
  ```json
  {
    "email": "pasien.andi@gmail.com",
    "password": "PasswordKuat2026!"
  }
  ```
- **Response `200 OK`:**
  ```json
  {
    "status": "success",
    "data": {
      "user_id": "usr-8a21f7d4-b912",
      "full_name": "Andi Pratama",
      "role": "PATIENT",
      "is_profile_completed": false,
      "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
    }
  }
  ```

---

### 1.2 Modul Rekam Medis & Gatekeeper Pasien (`/patient`)

#### `GET /patient/gatekeeper-status`
Memeriksa apakah pasien telah memenuhi syarat 100% kelengkapan data medis untuk membuka akses konsultasi.
- **Response `200 OK`:**
  ```json
  {
    "status": "success",
    "data": {
      "is_profile_completed": false,
      "completion_percentage": 40,
      "missing_fields": [
        "date_of_birth",
        "weight_kg",
        "drug_allergies"
      ],
      "can_start_consultation": false,
      "message": "Data medis wajib dilengkapi sebelum Anda dapat memilih keluhan dan berkonsultasi."
    }
  }
  ```

#### `PUT /patient/profile`
Memperbarui data diri dan kuesioner medis wajib pasien.
- **Request Body:**
  ```json
  {
    "nik": "3201234567890001",
    "date_of_birth": "1998-05-14",
    "gender": "MALE",
    "blood_type": "O",
    "weight_kg": 68.5,
    "height_cm": 172.0,
    "drug_allergies": "TIDAK ADA RIWAYAT ALERGI",
    "chronic_diseases": "Gastritis Ringan (Maag)",
    "phone_number": "+6281234567890"
  }
  ```
- **Response `200 OK`:**
  ```json
  {
    "status": "success",
    "message": "Profil rekam medis berhasil disimpan dan diverifikasi.",
    "data": {
      "patient_id": "pat-43c2-19e0",
      "is_profile_completed": true,
      "can_start_consultation": true
    }
  }
  ```

---

### 1.3 Modul Gejala & Kategori (`/symptoms`)

#### `GET /symptoms/categories`
Mengambil daftar pengelompokan gejala utama (Gejala Umum vs Gejala Organ Dalam).
- **Response `200 OK`:**
  ```json
  {
    "status": "success",
    "data": [
      {
        "id": 1,
        "code": "CAT-GENERAL",
        "name": "Kelompok Gejala Umum",
        "type": "GENERAL",
        "description": "Keluhan ringan sehari-hari: batuk, pilek, demam, pusing, nyeri otot.",
        "icon": "activity",
        "symptoms_count": 8
      },
      {
        "id": 2,
        "code": "CAT-ORGAN",
        "name": "Kelompok Gejala Organ Dalam & Spesifik",
        "type": "ORGAN_SPECIFIC",
        "description": "Keluhan pada sistem organ tertentu: paru-paru, lambung, jantung, kulit.",
        "icon": "shield-alert",
        "symptoms_count": 14
      }
    ]
  }
  ```

#### `GET /symptoms?categoryId=2`
Mengambil daftar sub-gejala di bawah kategori terpilih.
- **Response `200 OK`:**
  ```json
  {
    "status": "success",
    "data": [
      {
        "id": 101,
        "name": "Sesak Napas & Batuk Kronis (>2 minggu)",
        "target_organ": "Paru-Paru / Pernapasan",
        "default_specialization": "Spesialis Pulmonologi (Sp.P)",
        "is_red_flag": false
      },
      {
        "id": 102,
        "name": "Nyeri Ulu Hati, Sensasi Terbakar di Dada (GERD), Mual",
        "target_organ": "Lambung & Saluran Cerna",
        "default_specialization": "Spesialis Penyakit Dalam (Sp.PD)",
        "is_red_flag": false
      }
    ]
  }
  ```

---

### 1.4 Modul Transaksi Konsultasi & Resep Digital (`/consultations` & `/prescriptions`)

#### `POST /consultations/start-triage`
Inisialisasi sesi baru dan pengiriman keluhan awal ke Bot Penengah.
- **Request Body:**
  ```json
  {
    "initial_category_id": 2,
    "symptom_ids": [101],
    "chief_complaint_text": "Sudah 3 hari dada terasa agak sesak saat bernapas dan batuk berdahak kental kekuningan."
  }
  ```
- **Response `201 Created`:**
  ```json
  {
    "status": "success",
    "data": {
      "session_id": "ses-9921-aa01",
      "session_code": "MC-20261005-0812",
      "status": "IN_TRIAGE",
      "triage_bot_message": "Halo Andi, saya Asisten Triage Medicare. Saya menerima keluhan Anda mengenai sesak napas dan batuk berdahak. Apakah Anda mengalami demam tinggi atau nyeri dada yang menjalar?",
      "websocket_channel": "wss://api.medicareconsult.com/ws/consultation?sessionId=ses-9921-aa01"
    }
  }
  ```

#### `GET /prescriptions/:rxNumber/pdf`
Mengunduh berkas biner E-Resep PDF resmi.
- **Header Respons:** `Content-Type: application/pdf`, `Content-Disposition: attachment; filename="RX-20261005-0812.pdf"`
- **Response Body:** *Binary PDF Stream*.

---

## 2. ⚡ Spesifikasi Protokol WebSocket Real-Time Chat

Koneksi WebSocket digunakan untuk menciptakan ruang percakapan yang responsif dan interaktif antara pasien, Bot Penengah, dan Dokter Bot Spesialis.

### 2.1 Alur Acara (*Event Lifecycle*)
```
Client (Pasien)                                      Server (Chat Engine)
      │                                                       │
      ├───[ client:join_room ] (Kirim token & sessionId) ────>│
      │<──[ server:room_joined ] (Konfirmasi & info dokter) ──┤
      │                                                       │
      ├───[ client:send_message ] (Teks jawaban pasien) ─────>│
      │<──[ server:bot_typing ] (true) ───────────────────────┤
      │<──[ server:bot_message ] (Respons dokter bot) ────────┤
      │<──[ server:bot_typing ] (false) ──────────────────────┤
      │                                                       │
      │   (Jika Bot Penengah selesai melakukan klasifikasi)   │
      │<──[ server:session_handover ] (Alihkan ke Spesialis) ─┤
      │                                                       │
      │   (Jika Terdeteksi Tanda Bahaya Kegawatdaruratan)     │
      │<──[ server:emergency_alert ] (Hentikan chat & ke IGD)─┤
      │                                                       │
      │   (Ketika Konsultasi Selesai & Resep Diterbitkan)     │
      │<──[ server:prescription_ready ] (Tautan unduh PDF) ───┤
```

### 2.2 Format Payload Acara (*WebSocket Payloads*)

#### Event: `client:send_message`
```json
{
  "event": "client:send_message",
  "sessionId": "ses-9921-aa01",
  "text": "Dahaknya berwarna agak kental dok, tidak ada demam tinggi tapi tenggorokan terasa sakit."
}
```

#### Event: `server:bot_typing`
```json
{
  "event": "server:bot_typing",
  "isTyping": true,
  "botName": "dr. Farah, Sp.P"
}
```

#### Event: `server:session_handover`
```json
{
  "event": "server:session_handover",
  "previousBot": "Triage Agent Medicare",
  "newDoctor": {
    "name": "dr. Farah, Sp.P",
    "title": "Spesialis Pulmonologi & Kedokteran Respirasi",
    "sipNumber": "SIP.440/129/SP-P/2026",
    "avatarUrl": "/assets/doctors/dr-farah.png"
  },
  "message": "Terima kasih informasinya. Keluhan Anda telah saya teruskan ke dr. Farah, Sp.P. Dokter sedang meninjau rekam medis Anda."
}
```

#### Event: `server:prescription_ready`
```json
{
  "event": "server:prescription_ready",
  "rxNumber": "RX-20261005-0812",
  "doctorName": "dr. Farah, Sp.P",
  "diagnosis": "Bronkitis Akut Ringan (ICD-10: J20.9)",
  "downloadUrl": "/api/v1/prescriptions/RX-20261005-0812/pdf",
  "medications": [
    {
      "name": "Ambroxol Sirup 30mg/5ml",
      "dosage": "3x1 sendok takar (5ml) sehari",
      "timing": "Sesudah makan",
      "notes": "Pengencer dahak"
    },
    {
      "name": "Vitamin C 500mg Tablet",
      "dosage": "1x1 tablet sehari",
      "timing": "Pagi hari sesudah makan",
      "notes": "Menjaga daya tahan tubuh"
    }
  ]
}
```

---

## 3. 🧠 Rekayasa Prompt Sistem AI (Google Gemini AI Engine)

Integrasi kecerdasan buatan memanfaatkan API Google Gemini dengan dua rancangan *System Prompt* spesifik untuk menjamin akurasi klinis dan kepatuhan etika medis:

### 3.1 Prompt 1: Bot Penengah (*Triage Classifier Agent*)

```markdown
Anda adalah "Medicare Triage Assistant", sebuah sistem triage cerdas untuk platform telehealth Medicare Consult.
Tugas Anda:
1. Menerima kategori gejala awal yang dipilih pengguna dan teks keluhan bebasnya.
2. Mengevaluasi apakah keluhan mengandung tanda bahaya kegawatdaruratan (RED FLAGS):
   - Nyeri dada menjalar ke punggung/lengan kiri, keringat dingin, pingsan.
   - Batuk darah segar dalam jumlah banyak.
   - Sesak napas sangat berat hingga tidak mampu mengucapkan kalimat.
   - Muntah darah atau BAB hitam pekat.
3. Jika terdapat RED FLAG: Set "is_red_flag": true, dan berikan arahan segera ke IGD rumah sakit terdekat.
4. Jika aman: Klasifikasikan keluhan ke salah satu kode spesialisasi medis berikut:
   - SP-PULMO: Paru-paru, saluran pernapasan, batuk kronis, asma ringan, bronkitis.
   - SP-INTERNIST-GI: Lambung, usus, GERD, maag, diare, mual, pencernaan.
   - SP-DERMA: Kulit, ruam, gatal alergi, biduran.
   - SP-GEN-MED: Flu, demam biasa, pusing, pegal linu, kelelahan umum.

OUTPUT WAJIB BERUPA FORMAT JSON TUNGGAL:
{
  "is_red_flag": boolean,
  "red_flag_alert_message": string | null,
  "recommended_specialization_code": "SP-PULMO" | "SP-INTERNIST-GI" | "SP-DERMA" | "SP-GEN-MED",
  "chief_complaint_summary": string,
  "confidence_score": number (0.0 - 1.0)
}
```

---

### 3.2 Prompt 2: Bot Dokter Spesialis (*Doctor Persona Agent*)

```markdown
Anda adalah dokter spesialis virtual berlisensi di platform Medicare Consult.
Identitas Anda saat ini:
- Nama: {DOCTOR_NAME}
- Spesialisasi: {SPECIALIZATION_NAME}
- No. SIP: {DOCTOR_SIP}

Data Rekam Medis Pasien yang Anda Layani:
- Nama: {PATIENT_NAME}
- Usia: {PATIENT_AGE} tahun ({PATIENT_GENDER})
- Berat Badan: {PATIENT_WEIGHT} kg | Tinggi Badan: {PATIENT_HEIGHT} cm
- RIWAYAT ALERGI OBAT: {PATIENT_DRUG_ALLERGIES} (MUTLAK DIPATUHI!)
- Penyakit Penyerta: {PATIENT_CHRONIC_DISEASES}
- Ringkasan Keluhan Awal: {TRIAGE_SUMMARY}

PEDOMAN KONSULTASI KLINIS:
1. Bersikaplah hangat, sopan, berempati, dan menenangkan. Gunakan Bahasa Indonesia yang ramah dan mudah dipahami orang awam.
2. Lakukan anamnesis metode SOAP (tanyakan durasi, keparahan, riwayat obat yang sudah diminum).
3. JANGAN PERNAH meresepkan obat golongan Keras (lingkaran merah berhuruf K), Antibiotik keras, Narkotika, atau Psikotropika. HANYA rekomendasikan obat golongan BEBAS (Hijau) dan BEBAS TERBATAS (Biru) serta Suplemen/Vitamin.
4. PERIKSA RIWAYAT ALERGI PASIEN! Jika pasien alergi terhadap zat tertentu, hindari obat tersebut atau turunannya.
5. Pada akhir sesi, berikan:
   - Diagnosis awal secara ringkas.
   - Penjelasan penyebab masalah kesehatan.
   - Anjuran non-obat (pola istirahat, makanan yang dihindari, asupan cairan).
   - Rencana obat digital untuk diteruskan ke mesin E-Resep PDF.

Jika konsultasi telah cukup dan siap membuat resep, akhiri respons Anda dengan blok JSON khusus:
```json
{
  "action": "FINALIZE_CONSULTATION",
  "primary_diagnosis": "Diagnosis Kerja",
  "icd10_code": "Kode ICD-10",
  "clinical_summary": "Rangkuman hasil anamnesis",
  "lifestyle_advice": "Anjuran non-farmakologis",
  "prescriptions": [
    {
      "medicine_name": "Nama Obat Sediaan",
      "quantity": 1,
      "dosage": "Aturan Dosis",
      "timing": "Sesudah / Sebelum Makan",
      "notes": "Catatan Penggunaan"
    }
  ]
}
```
```

---

## 4. 🛡️ Keamanan Sistem & Penanganan Galat (*Error Handling*)

1. **Rate Limiting**: Setiap akun pasien dibatasi maksimal 30 pesan chat per menit untuk mencegah penyalahgunaan kuota Gemini API (*API exhaustion*).
2. **Sanitasi Input**: Mencegah serangan *Prompt Injection* (pasien mencoba memerintahkan AI untuk mengabaikan instruksi medis atau meresepkan zat berbahaya) dengan menyaring pesan melalui filter keamanan berbasis *regex* dan penegakan *system prompt guardrails*.
3. **Pemberian Fallback**: Jika server Gemini API mengalami kendala konektivitas (*timeout* > 5 detik), sistem secara otomatis mengembalikan pesan penenang: *"Dokter sedang menganalisis catatan medis Anda lebih lanjut, mohon tunggu beberapa saat..."* serta melakukan *retry* eksponensial.
