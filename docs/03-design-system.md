# 🎨 03. Design System & Style Guide

Dokumen ini mendefinisikan bahasa visual, token desain, palet warna, tipografi, efek elevasi, serta aturan styling untuk antarmuka **Carely** berdasarkan referensi desain yang disukai.

---

## 1. Filosofi Desain: *Human Warmth meets Tech Precision*

Carely memadukan dua kutub desain:
- **Presisi Teknologi**: Grid geometri halus, tata letak kartu bento terstruktur, sudut membulat simetris, dan elemen kapsul (*pill*).
- **Kehangatan Emosional**: Pendaran gradien ambient coral-peach (*warm radiant glow*), menghilangkan kesan kaku rumah sakit dan menghadirkan rasa aman serta optimis bagi pasien.

---

## 2. Palet Warna (Color Palette & Tokens)

### A. Core Palette Table

| Token Name | Hex Code | Role & Penggunaan pada UI |
| :--- | :--- | :--- |
| `--color-primary-coral` | `#FF6F59` | Aksen utama: Tombol aktif, card unggulan, status aktif |
| `--color-primary-deep` | `#FF5238` | Gradien akhir (*bottom-right*), hover tombol aktif |
| `--color-peach-light` | `#FFEFEA` | Latar belakang badge, hover state ringan, border aksen |
| `--color-blush-glow` | `#FFDCD1` | Pendaran gradien ambient di latar belakang hero |
| `--color-text-title` | `#111827` | Judul utama, headline tebal, angka statistik |
| `--color-text-body` | `#525866` | Paragraf deskripsi, subtitle, teks sekunder |
| `--color-text-muted` | `#868C98` | Caption, label waktu, teks footer copyright |
| `--color-surface-pure` | `#FFFFFF` | Permukaan kartu utama, modal, container |
| `--color-surface-muted` | `#F8F9FA` | Latar belakang seksi sekunder, tombol sekunder |
| `--color-border-subtle` | `rgba(0, 0, 0, 0.07)` | Garis batas tipis 1px pada kartu dan divider |
| `--color-border-glass` | `rgba(255, 255, 255, 0.8)` | Garis tepi kartu kaca (*glassmorphism border*) |
| `--color-dark-obsidian` | `#141518` | Tombol CTA gelap ("Get Started", "Sign up") |

### B. Gradient System

```css
/* Gradien Aksen Utama (Tombol & Highlight Card) */
--gradient-primary-coral: linear-gradient(135deg, #FF7B5C 0%, #FF5238 100%);

/* Gradien Ambient Background (Pendaran Cahaya Hero & Bento) */
--gradient-ambient-glow: radial-gradient(
  circle at 75% 20%,
  rgba(255, 140, 115, 0.28) 0%,
  rgba(255, 209, 196, 0.18) 35%,
  rgba(255, 245, 242, 0.05) 70%,
  transparent 100%
);

/* Gradien Angka 'How It Works' (01, 02, 03) */
--gradient-number-accent: linear-gradient(180deg, #111827 0%, #9CA3AF 100%);
--gradient-number-coral: linear-gradient(180deg, #FF6F59 0%, #FED7AA 100%);
```

---

## 3. Tipografi (Typography Hierarchy)

- **Font Keluarga Utama**: `Plus Jakarta Sans`, sans-serif (alternatif: `Outfit` atau `Inter`).
- **Skala Ukuran Teks**:

| Role | Font Size | Line Height | Weight | Letter Spacing |
| :--- | :--- | :--- | :--- | :--- |
| **Hero Display H1** | `56px` (`3.5rem`) | `1.15` | `700` (Bold) | `-0.03em` |
| **Section Title H2** | `40px` (`2.5rem`) | `1.2` | `700` (Bold) | `-0.025em` |
| **Subsection Title H3**| `24px` (`1.5rem`) | `1.3` | `600` (SemiBold) | `-0.015em` |
| **Card Heading H4** | `18px` (`1.125rem`)| `1.4` | `600` (SemiBold) | `-0.01em` |
| **Body Large** | `18px` (`1.125rem`)| `1.6` | `400` / `500` | `normal` |
| **Body Regular** | `15px` (`0.9375rem`)| `1.5` | `400` (Regular) | `normal` |
| **Small / Badge** | `13px` (`0.8125rem`)| `1.4` | `500` / `600` | `0.01em` |

---

## 4. Bentuk, Radius, & Grid Latar Belakang

### A. Border Radius (Pill & Soft Curves)
- **Pill (Full Round)**: `rounded-full` (`9999px`) — Digunakan pada:
  - Navbar container & menu pills.
  - Tombol aksi (*"Get Started"*, *"Get in touch"*, *"Sign up"*).
  - Badge tag (*"In 15 min"*, *"Loved by 100K users"*).
- **Cards (Soft Rounded Corners)**: `rounded-3xl` (`24px` hingga `30px`) — Digunakan pada kartu hero widget, bento box, dan paket harga.
- **Inner Small Badges**: `rounded-xl` (`12px` hingga `16px`).

### B. Subtle Background Grid (Efek Garis Kotak Lembut)
Di belakang hero terdapat grid transparan yang memberi tekstur modern:
```css
.bg-subtle-grid {
  background-size: 48px 48px;
  background-image: 
    linear-gradient(to right, rgba(255, 111, 89, 0.06) 1px, transparent 1px),
    linear-gradient(to bottom, rgba(255, 111, 89, 0.06) 1px, transparent 1px);
}
```

---

## 5. Elevasi & Bayangan (Shadows & Glassmorphism)

Kartu pada Carely tampak mengapung (*floating*) di atas latar belakang dengan bayangan bertingkat yang sangat lembut:

```css
/* Card Standar (Floating Widget) */
--shadow-card-float: 
  0 10px 30px -10px rgba(255, 111, 89, 0.12),
  0 4px 6px -2px rgba(0, 0, 0, 0.03),
  0 0 0 1px rgba(0, 0, 0, 0.04);

/* Glassmorphism Navbar & Pill */
--glass-background: rgba(255, 255, 255, 0.85);
--glass-backdrop-blur: blur(16px);
--glass-border: 1px solid rgba(255, 255, 255, 0.9);

/* Active Highlight Card (Kartu Anna Cooper / Plus Pricing) */
--shadow-glow-coral: 
  0 20px 40px -15px rgba(255, 90, 60, 0.45),
  0 2px 4px rgba(255, 90, 60, 0.2);
```

---

## 6. Token Desain CSS Siap Pakai (`variables.css`)

```css
:root {
  /* Colors */
  --carely-coral-500: #FF6F59;
  --carely-coral-600: #FF5238;
  --carely-coral-100: #FFEFEA;
  --carely-dark: #121316;
  --carely-gray-50: #F8F9FA;
  --carely-gray-100: #F1F3F5;
  --carely-gray-500: #6B7280;
  --carely-gray-900: #111827;

  /* Typography */
  --font-family: 'Plus Jakarta Sans', system-ui, -apple-system, sans-serif;

  /* Radii */
  --radius-pill: 9999px;
  --radius-card: 26px;
  --radius-widget: 20px;

  /* Transitions */
  --transition-smooth: all 0.25s cubic-bezier(0.16, 1, 0.3, 1);
}
```
Dokumen selanjutnya menguraikan arsitektur komponen modular yang mengimplementasikan token-token ini.
