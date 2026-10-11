# 🏥 Carely — Modern Healthcare Landing Page Template
> Dokumentasi Komprehensif Arsitektur UI/UX, Design System, & Implementasi HTML5 (Semester 1 Academic Edition)

Selamat datang di repositori dokumentasi **Carely**. Repositori ini berisi cetak biru (blueprint) perancangan antarmuka landing page kesehatan modern berbasis referensi visual *Carely*.

Dokumentasi ini disesuaikan khusus untuk **tugas kuliah Semester 1**, di mana proyek dibangun menggunakan **HTML5 murni tanpa build step yang rumit (Zero-Build Setup)**, tetapi tetap mempertahankan pemanfaatan **UI Framework (Tailwind CSS via CDN)**, sistem desain mutakhir, dan estetika premium tahun 2026.

---

## 📌 Daftar Isi Dokumentasi

Dokumentasi ini disusun secara bertahap dan modular agar mudah dipelajari, dinilai oleh dosen, dan dikembangkan:

1. [**01. Brainstorming & Strategi Pengembangan**](./01-brainstorming-and-strategy.md)
   - Evaluasi: *Clone 1:1* vs *Enhancement / Adaptable Template*.
   - Adaptasi untuk standar penilaian tugas kuliah Semester 1.
   - Target pengguna (*Clinics* & *Patients*) dan *Tone of Voice*.

2. [**02. Rekomendasi Tech Stack & UI Framework (HTML5 & Tailwind CDN)**](./02-tech-stack-and-frameworks-2026.md)
   - Analisis solusi *Zero-Build*: Menjalankan UI Framework Tailwind CSS & Lucide Icons di dalam file HTML murni.
   - Alasan keunggulan format ini untuk pengujian dosen (cukup double-click atau gunakan Live Server).
   - Konfigurasi tema kustom Carely di header HTML.

3. [**03. Design System & Style Guide**](./03-design-system.md)
   - Palet warna (*Warm Coral/Peach Glow*, Clean Slate, Pure White, Velvet Dark).
   - Tipografi modern (*Plus Jakarta Sans* via Google Fonts).
   - Radius, shadows, efek kaca (*Glassmorphism*), dan grid latar belakang halus.
   - Token desain siap pakai (CSS Custom Properties).

4. [**04. Arsitektur Komponen Modular (Atomic HTML Structure)**](./04-component-architecture.md)
   - Pembagian modul per seksi semantik HTML5 (`<header>`, `<main>`, `<section>`, `<article>`, `<footer>`).
   - Floating Widgets (Mood Tracker, Appointment Alert, Quick Stats, Mini Analytics).
   - Script interaktivitas Vanilla JavaScript ringan untuk toggle role dan mood slider.

5. [**05. Spesifikasi Layout & Detail Section**](./05-page-sections-and-layout.md)
   - Section 1: Floating Capsule Navigation Bar.
   - Section 2: Hero Section dengan Dual CTA & Floating Mockup Widgets.
   - Section 3: "How It Works?" dengan Segmented Role Control.
   - Section 4: Product Overview Bento Showcase (Feature Grid).
   - Section 5: Streamline Healthcare Banner CTA.
   - Section 6: Tiered Pricing Matrix.
   - Section 7: Modern Clean Footer.

---

## 🎯 Ringkasan Eksekutif Proyek
- **Nama Konsep:** Carely (Healthcare & Clinic Management Platform)
- **Kategori:** Modern Healthcare Web Landing Page
- **Teknologi Utama:** Pure Semantic HTML5, Tailwind CSS CDN Engine, Vanilla JavaScript ES6, Lucide Icons, Google Fonts.
- **Portabilitas:** 100% mandiri, tanpa perlu instalasi `npm`, `node`, atau build terminal.
