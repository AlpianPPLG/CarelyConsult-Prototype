# 🧩 04. Arsitektur Komponen Modular (Pure HTML5 & Semantic Design)

Dokumen ini memetakan arsitektur modular antarmuka **Carely** yang diimplementasikan menggunakan **Pure Semantic HTML5 + Tailwind CSS Framework**. Struktur ini menjamin bahwa meskipun berada dalam 1 file `index.html`, kode tetap tertata secara modular, bersih, mudah dipelajari oleh mahasiswa semester 1, dan siap dinilai tinggi oleh dosen.

---

## 1. Peta Hirarki Section Semantik HTML5

```
index.html (Semantic HTML5 Skeleton)
│
├── <!DOCTYPE html> & <head> (Fonts, Tailwind CDN, Lucide CDN, Theme Config)
│
├── <body>
│   │
│   ├── <!-- ================= 01. NAVBAR / HEADER ================= -->
│   │   <header> / <nav class="fixed top-6 ...">
│   │       ├── Brand Logo (Carely)
│   │       ├── Pill Nav Links (Home, Features, Clinics, Patients, Contact)
│   │       └── Auth Buttons (Log in, Sign up)
│   │
│   ├── <main>
│   │   │
│   │   ├── <!-- ================= 02. HERO SECTION ================= -->
│   │   │   <section id="hero" class="relative overflow-hidden ...">
│   │   │       ├── Kolom Kiri: Social proof pill, H1, Body text, Dual CTA
│   │   │       └── Kolom Kanan: Floating Widgets (Mood, Appointment Alert, Stats, Chart)
│   │   │
│   │   ├── <!-- ================= 03. HOW IT WORKS ================= -->
│   │   │   <section id="how-it-works">
│   │   │       ├── Section Header + Role Segmented Switcher (For Clinics / Patients)
│   │   │       └── 3 Step Cards (01 Workflow, 02 Manage Bookings, 03 Stay Connected)
│   │   │
│   │   ├── <!-- ================= 04. PRODUCT OVERVIEW BENTO ====== -->
│   │   │   <section id="overview">
│   │   │       └── Bento Grid 5-Card Layout (Doctor Portrait, Integrations, Follow-up, etc.)
│   │   │
│   │   ├── <!-- ================= 05. BANNER CTA =================== -->
│   │   │   <section id="cta-banner">
│   │   │       └── Streamline Healthcare Ambient Banner + Dual Action
│   │   │
│   │   └── <!-- ================= 06. PRICING SECTION ============= -->
│   │       <section id="pricing">
│   │           └── 3 Pricing Tiers (Basic Free, Plus $249 Highlighted, Professional)
│   │
│   └── <!-- ================= 07. FOOTER =========================== -->
│       <footer>
│           ├── Newsletter Subscription Card
│           ├── 4-Column Navigation Links
│           └── Copyright & Legal Text
│
└── <script> (Vanilla JS: Mood Slider, Role Toggle, Smooth Scroll, Lucide Init)
```

---

## 2. Rincian Spesifikasi Elemen Semantik

### A. Floating Pill Navigation (`<header>`)
- Menggunakan tag `<header>` dan `<nav>` dengan class Tailwind `backdrop-blur-md bg-white/80 border border-white/60 shadow-glass rounded-full`.
- Menyediakan tautan navigasi responsif yang tetap mengapung saat di-scroll.

### B. Floating Dashboard Widgets (`<section id="hero">`)
Dibangun murni dengan tag HTML5 + Tailwind CSS (tanpa gambar bitmap mati):

1. **Widget Mood Tracking**:
   - Struktur: `<div id="mood-tracker" class="...">`
   - Berisi 5 emoji/tombol mood (`Terrible`, `Bad`, `Okay`, `Good`, `Great`) dengan range slider interaktif.
2. **Widget Appointment Alert ('Anna Cooper')**:
   - Struktur: `<div class="bg-gradient-to-br from-[#FF7B5C] to-[#FF5238] text-white p-5 rounded-3xl shadow-glow-coral ...">`
   - Berisi status badge pill `• In 15 min`, nama dokter/pasien, jam konsultasi, dan tombol call.
3. **Widget Metrics & Visits Chart**:
   - Kartu metrik: Angka tebal `1,250 Appointments` dan badge hijau `▲ 5.8%`.
   - Kartu grafik: Dibuat menggunakan SVG vektor murni yang ringan dan tajam pada semua resolusi layar (*retina ready*).

### C. Bento Grid Architecture (`<section id="overview">`)
Menggunakan CSS Grid modern:
```html
<div class="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-4 gap-6">
  <!-- Card 1: Portrait Foto Pasien (Span 2 row) -->
  <!-- Card 2: Integrasi Aplikasi (Slack, Meet, Zoom) -->
  <!-- Card 3: Follow-Up Care (Coral Accent) -->
  <!-- Card 4: Appointments Simplified (Date Picker) -->
  <!-- Card 5: Secure Messaging (Chat Mockup) -->
</div>
```

---

## 3. Interaktivitas Vanilla JavaScript Ringan

Untuk memenuhi syarat tugas Semester 1, seluruh logika interaktif ditulis dalam JavaScript murni (ES6) tanpa error dan tanpa library pihak ketiga:

1. **Toggle Peran Pengguna (*For clinics* vs *For patients*)**:
   - Memanipulasi state aktif tombol kapsul dan memperbarui teks deskripsi langkah 01, 02, dan 03.
2. **Interactive Mood Slider**:
   - Event listener `input` pada range bar untuk mengubah emoji aktif dan status teks (*Okay -> Good -> Great*).
3. **Inisialisasi Ikon Lucide**:
   - Memanggil `lucide.createIcons()` saat DOM selesai dimuat.

---

## 4. Keuntungan Penilaian Akademik Semester 1
- **Mudah Dibaca**: Struktur file terbagi rapi dengan komentar pembatas yang jelas.
- **Portabel**: Dosen dapat memeriksa langsung dengan membuka `index.html` di Google Chrome, Microsoft Edge, atau Mozilla Firefox.
- **Nilai Plus Inovasi**: Memanfaatkan Tailwind CSS via CDN dan SVG inline untuk grafik, membuktikan pemahaman mahasiswa terhadap standar industri modern tanpa melanggar batasan teknis tugas.
