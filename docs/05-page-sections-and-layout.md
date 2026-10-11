# 📐 05. Spesifikasi Layout & Detail Section

Dokumen ini membedah rancangan struktural setiap section pada landing page **Carely**, mencakup tata letak, konten teks (*copywriting*), elemen visual, dan interaksi yang harus ada sesuai dengan referensi visual.

---

## 1. Floating Capsule Navigation Bar (Header)

Navigasi melayang dengan efek kapsul transparan (*floating pill navbar*) yang modern dan bersih.

- **Struktur Layout**:
  ```
  [ Carely Logo ] --------- [ Home | Features | For clinics | For patients | Contact ] --------- [ Log in ] [ Sign up ]
  ```
- **Elemen & Interaksi**:
  - **Kiri**: Logo teks *"Carely"* menggunakan font `Plus Jakarta Sans` dengan bobot `Bold 700`.
  - **Tengah (Nav Links)**: Terbungkus dalam kapsul putih berbayangan lembut (`backdrop-blur-md`). Link aktif memiliki warna teks gelap pekat, sedangkan link non-aktif berwarna abu-abu netral.
  - **Kanan (Auth Buttons)**:
    - *"Log in"*: Tombol ghost/minimalis tanpa latar belakang tebal.
    - *"Sign up"*: Tombol kapsul hitam obsidian (`#141518`) dengan teks putih cerah.
  - **Behavior Scroll**: Navbar tetap melayang (*sticky with blur*) saat halaman digulir.

---

## 2. Hero Section (Simplicity & Trust)

Bagian paling krusial yang langsung memikat perhatian pengunjung (*above the fold*).

- **Latar Belakang**:
  - Pendaran gradien ambient coral-peach lembut di sisi kanan atas (`radial-glow`).
  - Grid geometris transparan tipis (`bg-subtle-grid`).
- **Kolom Kiri (Value & CTA)**:
  - **Social Proof Pill**:
    - Klaster 4 avatar pengguna yang bertumpuk.
    - Rating: `4.9/5` dengan 5 ikon bintang emas.
    - Teks: *"Loved by 100K users"*.
  - **Headline Utama (H1)**:
    - Teks: *"Care that starts with simplicity and trust."*
    - Tipografi: Ukuran besar (`56px - 64px`), bobot tebal (*bold*), baris renggang proporsional.
  - **Deskripsi Ringkas**:
    - Teks: *"Carely connects patients and clinics in one intuitive space - for appointments, messages, and follow-up care."*
  - **Dual CTA Buttons**:
    - Tombol 1: *"Get Started"* (Kapsul hitam, hover efek sedikit terangkat).
    - Tombol 2: *"Get in touch"* (Kapsul abu-abu/putih dengan border halus).
- **Kolom Kanan (Floating Dashboard Widgets Mockup)**:
  - Komposisi dinamis beberapa kartu UI yang saling bertingkat (*staggered floating layer*):
    1. **Widget Mood Tracking**: Bar interaktif dengan 5 status emosi (*Terrible, Bad, Okay, Good, Great*).
    2. **Widget Appointment Alert (Pusat Perhatian)**: Kartu oranye bersinar dengan teks *"Anna Cooper • In 15 min"*, *"Follow-up Consultation"*, waktu `10:00 - 11:00`, tanggal `January 18`, serta tombol panggil video.
    3. **Widget Metrik 1**: *"1,250 Appointments"* (+5.8% dari minggu lalu).
    4. **Widget Metrik 2**: *"1,002 Call Consultancy"* (+40% dari minggu lalu) dengan ikon telepon oranye.
    5. **Widget Grafik Pasien**: Grafik garis halus dwi-warna (pink untuk wanita, ungu untuk pria) yang menampilkan tren kunjungan.
    6. **Floating Icon**: Ikon kalender oranye kecil melayang untuk memperkuat tema penjadwalan.

---

## 3. Section: "How It Works?" (Alur Penggunaan Bertahap)

Bagian edukatif yang menjelaskan alur kerja platform secara intuitif dengan kontrol peran pengguna.

- **Header Section**:
  - Judul: *"How It Works?"* di sebelah kiri.
  - **Role Segmented Switcher** di sebelah kanan:
    ```
    [ (Active Coral Pill) For clinics ]   [ For patients ]
    ```
    Memungkinkan pengunjung berganti perspektif: melihat alur bagi klinik atau alur bagi pasien.
- **Tiga Kartu Langkah Berurutan (Sequential Step Cards)**:
  - **Langkah 01**:
    - Nomor: *"01"* berukuran besar dengan gradien elegan.
    - Judul: *"Set up your workflow"*.
    - Deskripsi: *"Create your clinic profile, configure schedules, and define how appointments and follow-ups are handled - all in one setup flow."*
    - Preview Visual: Mockup mini kartu formulir registrasi/konfigurasi (*"Create an account"*).
  - **Langkah 02**:
    - Nomor: *"02"* dengan aksen oranye gradien.
    - Judul: *"Manage bookings"*.
    - Deskripsi: *"Patient appointments come in automatically and appear in a shared dashboard, keeping your team aligned and schedules up."*
    - Preview Visual: Mockup kartu antrean reservasi pasien.
  - **Langkah 03**:
    - Nomor: *"03"*.
    - Judul: *"Stay connected"*.
    - Deskripsi: *"Send messages and follow-up instructions directly through Carely, ensuring patients stay informed and supported between visits."*
    - Preview Visual: Mockup kartu notifikasi & pesan instruksi medis.

---

## 4. Section: Product Overview (Bento Grid Showcase)

Bagian fitur utama yang dikemas dalam bentuk **Bento Grid** (tata letak modern bergaya Apple).

- **Header Section**:
  - Judul: *"Product Overview"*
  - Deskripsi: *"Carely connects patients and clinics in one simple, intuitive space. Book appointments, chat with your clinic, and manage follow-up care — all in one place."*
- **Komposisi 5 Kartu Bento**:
  1. **Kartu 1 (Kiri - Tinggi Vertikal)**:
     - Foto beresolusi tinggi seorang profesional medis/pasien yang tersenyum ramah.
     - Badge overlay: *"50K+ Satisfied Patients"*.
  2. **Kartu 2 (Integrations)**:
     - Judul: *"Integrations"*.
     - Deskripsi: *"Seamless integration across everyday tools."*
     - Aset: Ikon melayang 3D Slack, Google Meet, dan Zoom.
  3. **Kartu 3 (Follow-Up Care - Solid Coral)**:
     - Latar belakang gradien coral cerah berenergi tinggi.
     - Judul: *"Follow-Up Care Made Easy"*.
     - Tombol: Kapsul putih *"Learn more"*.
  4. **Kartu 4 (Appointments, Simplified)**:
     - Judul: *"Appointments, Simplified"*.
     - Deskripsi: *"Easy scheduling for patients and clinics alike."*
     - Preview: Miniatur date picker dan slot janji temu dokter.
  5. **Kartu 5 (Secure Patient Messaging)**:
     - Judul: *"Secure Patient Messaging"*.
     - Deskripsi: *"Stay connected with clinics through safe, real-time communication."*
     - Preview: Thread chat terenkripsi dengan balon percakapan konsultasi dan input pengiriman.

---

## 5. Section: Streamline Healthcare in One Place (Banner CTA)

Bagian penegasan (*conversion booster*) di tengah halaman sebelum bagian harga.

- **Desain**:
  - Background dengan ambient glow coral melingkar di tengah.
  - Judul H2: *"Streamline Healthcare in One Place"*
  - Paragraf: *"Join patients and clinics on a single intuitive platform for appointments, messaging, and follow-ups, ensuring seamless communication."*
  - Tombol CTA: *"Get Started"* (Hitam) & *"Get in touch"* (Putih/border).

---

## 6. Section: Pricing (Paket & Transparansi Biaya)

Bagian harga dengan sistem kartu perbandingan yang jelas.

- **Header Section**:
  - Judul: *"Pricing"*
  - Teks penjelas di sisi kanan: *"No credit card required — get full access and try all features today. Explore at your own pace."*
- **Kartu Paket**:
  - **Paket 1: Basic (Free)**
    - Badge: `Basic`
    - Harga: **Free**
    - Subtitle: *"Essential tools to start"*
    - Fitur:
      - ✔ Book appointments
      - ✔ Personal reminders
      - ✔ Basic message history
    - CTA: Tombol kapsul *"Get started"*
  - **Paket 2: Plus ($249/mon) — KARTU UNGGULAN**
    - Visual: Warna kartu **Full Coral Orange Gradient**, teks putih dengan kontras tinggi.
    - Badge: `Plus`
    - Harga: **$249** `/mon`
    - Subtitle: *"For regular users / clinics"*
    - Fitur:
      - ✔ All Basic features
      - ✔ Unlimited bookings
      - ✔ Instant follow-up care alerts
      - ✔ Priority customer support
    - CTA: Tombol kapsul putih kontras *"Get started"*
  - **Paket 3: Professional ($... / mon)**
    - Badge: `Professional`
    - Subtitle: *"Advanced insights and tools for multi-doctor clinics"*
    - Fitur: Tim manajemen dokter, analitik lanjutan, integrasi API rekam medis kustom, 24/7 support.

---

## 7. Section: Footer (Penutup Halaman)

Penutup halaman yang rapi dan fungsional.

- **Newsletter Subscription**:
  - Teks: *"Sign up to receive health tips"*
  - Input kapsul: Field input email terintegrasi langsung dengan tombol kapsul submit di dalamnya.
- **Navigasi Kolom Tautan**:
  - **Product**: Features, Pricing, Integrations, FAQ
  - **Support**: Help Center, Terms of Service, Privacy Policy
  - **Connect**: Newsletter, Social Media, Request a Demo
  - **Company**: About Us, Careers, Blog / News, Contact
- **Copyright Bar**:
  - `© 2026 Carely Inc. All rights reserved.`
