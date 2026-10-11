# ⚡ 02. Rekomendasi Tech Stack & UI Framework (Semester 1 Academic & 2026 Modern HTML Edition)

Dokumen ini telah **dirombak khusus** untuk memenuhi batasan tugas kuliah **Semester 1 (Web Dasar/Front-End Fundamental)** yang mewajibkan penggunaan **file HTML murni (Zero Build Setup)**, namun tetap mempertahankan estetika desain mutakhir tahun 2026 setara referensi desain *Carely*.

---

## 1. Tantangan & Kebutuhan Tugas Semester 1

Pada jenjang perkuliahan semester 1:
- Dosen/asisten laboratorium menilai file yang dapat **langsung dibuka di browser** (cukup double-click `index.html` atau menggunakan ekstensi VS Code *Live Server*).
- **Dilarang** menggunakan build tools yang rumit (Node.js, npm, bundler webpack/vite, atau framework SSR seperti Next.js) karena kode harus dapat dievaluasi secara independen tanpa instalasi dependensi di mesin penguji.
- Mahasiswa dinilai dari:
  1. **Struktur Semantik HTML5** (`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<figure>`, `<footer>`).
  2. **Kerapian Kode & Indentasi**.
  3. **Visual & Estetika Antarmuka** (Kesesuaian dengan tren UI modern 2026).
  4. **Interaktivitas Dasar** (JavaScript murni tanpa error di console).

---

## 2. Pilihan UI Framework untuk Ekosistem Pure HTML

Bagaimana cara tetap menggunakan kecanggihan UI Framework tanpa build step? Berikut adalah komparasi pilihannya:

| Opsi Framework | Dukungan Pure HTML (Zero-Build) | Fleksibilitas Desain Modern | Kesesuaian Desain Carely |
| :--- | :--- | :--- | :--- |
| **Tailwind CSS (via CDN Engine)** ⭐ | **Ya** (Cukup 1 tag `<script>`) | **Sangat Tinggi** (Bisa custom gradient glow, bento grid, pill button) | **100% Sempurna** untuk meniru referensi |
| **Bootstrap 5.3 (via CDN)** | Ya (1 tag `<link>`) | Rendah-Sedang (Bentuk kartu & tombol terkesan kaku/klasik) | Sulit meniru efek *ambient peach glow* & bento grid |
| **Pure Vanilla CSS Murni** | Ya (File `.css` terpisah) | Tinggi (namun memakan ratusan baris kode manual) | Bagus, tapi lambat dalam prototyping |

---

## 3. The Winning Tech Stack: "Modern Zero-Build HTML5 Stack"

Untuk tugas ini, arsitektur terbaik yang menggabungkan kemudahan HTML biasa dengan kekuatan framework adalah:

```
┌────────────────────────────────────────────────────────────────────────┐
│                   CARELY SEMESTER 1 ARCHITECTURE                       │
├────────────────────────────────────────────────────────────────────────┤
│  Document Structure : Pure Semantic HTML5 (index.html)                 │
│  UI Framework       : Tailwind CSS Play CDN (Modern Utility Engine)    │
│  Custom Tokens      : Embedded CSS Variables (Glow, Grid, Animations)  │
│  Iconography        : Lucide Icons CDN (SVG rendering otomatis)        │
│  Typography         : Google Fonts ('Plus Jakarta Sans')               │
│  Interactivity      : Vanilla JavaScript (Zero-dependency ES6)         │
│  Portability        : 100% Plug-and-Play (Buka langsung di browser)    │
└────────────────────────────────────────────────────────────────────────┘
```

### Mengapa Kombinasi Ini Sangat Unggul untuk Tugas Kuliah?
1. **Dosen Melihat File HTML Murni**: File utamanya tetap berupa `index.html` yang bersih, rapi, dan modular.
2. **Kekuatan UI Framework Tetap Aktif**: Dengan menyertakan script Tailwind CSS CDN, kita bisa menggunakan seluruh class modern (`backdrop-blur-md`, `rounded-3xl`, `grid-cols-12`, `shadow-2xl`).
3. **Dukungan Kustomisasi Theme Carely**: Melalui tag `<script>` konfigurasi Tailwind, kita mendaftarkan warna kustom (*coral*, *peach*, *obsidian*) sehingga class seperti `bg-carely-coral` atau `text-carely-dark` langsung tersedia.
4. **Interaktivitas Nyata**: Slider *Mood Tracker*, tombol ganti peran *For clinics / For patients*, dan efek klik pada paket harga dijalankan dengan script Vanilla JS ringkas (< 50 baris) tanpa dependensi eksternal.

---

## 4. Konfigurasi Head Dokumen HTML

Berikut adalah blueprint header dokumen HTML yang siap disematkan pada `index.html`:

```html
<!DOCTYPE html>
<html lang="id" class="scroll-smooth">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Carely — Healthcare Platform for Clinics & Patients</title>

  <!-- Google Fonts: Plus Jakarta Sans -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">

  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>

  <!-- Lucide Icons CDN -->
  <script src="https://unpkg.com/lucide@latest"></script>

  <!-- Konfigurasi Tailwind Custom Theme Carely -->
  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: {
            sans: ['"Plus Jakarta Sans"', 'sans-serif'],
          },
          colors: {
            carely: {
              coral: '#FF6F59',
              'coral-dark': '#FF5238',
              'coral-light': '#FFEFEA',
              blush: '#FFDCD1',
              dark: '#141518',
              muted: '#64748B',
              surface: '#FFFFFF',
              bg: '#FAF9F8',
            }
          },
          boxShadow: {
            'glow-coral': '0 20px 40px -15px rgba(255, 111, 89, 0.35)',
            'float-card': '0 12px 32px -8px rgba(0, 0, 0, 0.06), 0 4px 8px -2px rgba(0,0,0,0.03)',
            'glass': '0 8px 32px 0 rgba(31, 38, 135, 0.05)',
          }
        }
      }
    }
  </script>
</head>
```

---

## 5. Keunggulan Nilai Akademik
1. **Lolos Kriteria Validasi W3C**: Menggunakan tag semantik HTML5 standar.
2. **Standar Responsif**: Tampilan tetap proporsional dari layar smartphone (375px), tablet (768px), hingga laptop/desktop (1440px).
3. **Kerapian Dokumentasi Kode**: Setiap seksi diberi komentar penanda yang jelas (`<!-- SECTION: HERO -->`, dsb.) sehingga sangat mudah dijelaskan saat presentasi tugas kepada dosen pengampu.
