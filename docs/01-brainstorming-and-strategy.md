# 💡 01. Brainstorming & Strategi Pengembangan

Dokumen ini mendiskusikan keputusan strategis perancangan landing page **Carely**, membandingkan skenario pembuatan (Cloning vs New Design), serta merumuskan persona dan proposisi nilai.

---

## 1. Analisis & Dilema: Clone 1:1 vs Template Adaptif Baru

User menyampaikan kebutuhan: *apakah sebaiknya membuat baru (fresh concept) atau meng-clone sama persis seperti referensi yang disukai?*

Berikut adalah komparasi mendalam dari 3 opsi pendekatan:

| Parameter | Opsi A: Pure Exact Clone (1:1 Hardcoded) | Opsi B: **Cloning + Production-Grade Modular Template (Rekomendasi)** | Opsi C: Totally New Concept (Eksplorasi Baru) |
| :--- | :--- | :--- | :--- |
| **Estetika Visual** | 100% identik dengan gambar screenshot | 100% visual fidelity (identik) dengan polish interaktif modern | Berbeda dari referensi |
| **Modularitas & Skalabilitas** | Rendah (biasanya elemen statis/kaku) | **Tinggi** (komponen terisolasi, data terpisah dalam config) | Tinggi |
| **Kegunaan Sebagai Template** | Kaku, sulit diedit untuk klien/proyek lain | **Sangat Fleksibel**, teks/angka/grafik dapat diganti dengan mudah | Fleksibel |
| **Responsivitas (Mobile/Tablet)** | Tidak ada di referensi (harus ditebak) | **Diadaptasi secara sistematis** menjadi mobile-first | Dibuat dari nol |
| **Interaktivitas** | Statis menyerupai mockup Dribbble | **Dihidupkan dengan micro-interactions** (hover, toggle role, slider mood) | Bergantung implementasi |

### 🏆 Rekomendasi Keputusan: **Opsi B (Faithful Visual Clone with Modular Architecture)**
Mengapa opsi ini adalah yang paling ideal?
1. **Mempertahankan Nilai yang Disukai User**: Karakter visual referensi (*warm coral ambient glow, clean glassmorphism, pill navbar, floating dashboard widgets*) adalah poin utama yang membuat user tertarik. Kita tidak boleh membuang keindahan visual ini.
2. **Transformasi Mockup Menjadi Produk Nyata**: Gambar referensi adalah mockup desain grafis (UI art). Jika hanya di-clone secara dangkal, widget seperti grafik atau mood tracker hanya akan menjadi gambar mati. Dengan pendekatan Opsi B, setiap widget (grafik kunjungan pasien, slider mood, bento box) direalisasikan menjadi komponen web interaktif sungguhan.
3. **Template Ready**: Setiap teks, statistik (`1,250 Appointments`, `4.9/5`, `50K+ Satisfied Patients`), dan harga dibuat berbasis data/props terpisah, sehingga bila user ingin menjual template ini atau menggunakannya untuk berbagai klien klinik, kustomisasinya sangat cepat.

---

## 2. Definisi Produk & Value Proposition

- **Nama Produk**: Carely
- **Tagline**: *"Care that starts with simplicity and trust."*
- **Kategori**: Healthcare SaaS / Clinic Management & Patient Experience Platform.
- **Masalah yang Dipecahkan**:
  - Pasien sering merasa sistem reservasi dan follow-up kesehatan rumit, kaku, dan membingungkan.
  - Klinik kewalahan mengelola jadwal dokter, rekam medis ringkas, dan jalur komunikasi pasien dalam aplikasi terpisah.
- **Solusi Carely**:
  - Satu platform terpadu yang menjembatani klinik (*workflow & booking management*) dan pasien (*easy appointment & direct follow-up*).

---

## 3. Analisis Persona & Dual-Audience Experience

Salah satu keunikan yang tampak pada referensi Carely adalah adanya **Toggle Segmentasi Pengguna**:
```
[ For clinics ]   [ For patients ]
```

Strategi konten landing page ini harus melayani dua persona secara harmonis:

### A. Persona 1: Klinik, Praktik Mandiri, & Tenaga Medis (*For Clinics*)
- **Fokus Utama**: Efisiensi kerja, otomatisasi jadwal, retensi pasien, integrasi alat (Google Meet, Zoom, Slack), dan pelacakan metrik klinik.
- **Fitur yang Disorot**:
  - *Set up your workflow*: Konfigurasi profil klinik, jam praktik, dan aturan follow-up.
  - *Manage bookings*: Dashboard antrean dan jadwal konsultasi real-time.
  - *Analytics*: Grafik tren kunjungan pasien (pria vs wanita, tingkat kehadiran).

### B. Persona 2: Pasien & Pengguna Layanan Kesehatan (*For Patients*)
- **Fokus Utama**: Kenyamanan, kepastian jadwal, transparansi biaya, dan komunikasi tanpa rasa cemas (*anxiety-free healthcare*).
- **Fitur yang Disorot**:
  - *1-Click Booking*: Memilih slot dokter dalam 15 detik.
  - *Mood & Health Tracking*: Pemantauan kondisi harian pasca perawatan.
  - *Secure Direct Messaging*: Chat langsung dengan perawat/dokter tanpa harus telepon berulang kali.

---

## 4. Tone of Voice & Karakter Emosional Desain

Desain web medis tradisional sering kali terasa:
- Terlalu dingin (*cold medical blue* atau putih rumah sakit steril).
- Menakutkan atau berkesan birokratis.

**Carely mengusung paradigma baru:**
1. **Warm & Welcoming**: Penggunaan gradien *soft coral, peach, dan blush pink* memberikan rasa empati, tenang, dan bersahabat.
2. **Modern & High-Trust**: Tipografi sans-serif geometris tebal dan layout bento grid memberikan kesan teknologi tinggi dan reliabilitas enterprise (setara Apple Health / Linear).
3. **Clutter-Free & Focused**: Jarak spasial (white space) yang lapang memastikan pengguna yang sedang cemas atau sibuk tidak merasa terbebani saat melihat antarmuka.

---

## 5. Roadmap Tahapan Pengerjaan

1. **Fase 1 (Selesai pada sesi ini)**: Dokumentasi komprehensif, arsitektur sistem desain, spesifikasi komponen, dan rekomendasi tech stack 2026.
2. **Fase 2 (Validasi User)**: Review dokumen oleh user dan persetujuan pemilihan framework.
3. **Fase 3 (Fondasi & Setup Proyek)**: Setup repository, token CSS design system, dan aset grafis.
4. **Fase 4 (Pembangunan Komponen)**: Pembuatan komponen atomik (Capsule Buttons, Floating Cards, Bento Grid).
5. **Fase 5 (Assembling & Interactive Polish)**: Pemasangan section lengkap, animasi scroll/hover, dan pengujian responsif di berbagai resolusi layar.
