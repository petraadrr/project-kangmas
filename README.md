# KANGMAS — Platform Penghubung Masyarakat dengan Tenaga Pertukangan Terpercaya

<p align="center">
  <img src="https://img.shields.io/badge/Laravel-11.x-FF2D20?style=for-the-badge&logo=laravel&logoColor=white" alt="Laravel">
  <img src="https://img.shields.io/badge/React-19.x-61DAFB?style=for-the-badge&logo=react&logoColor=black" alt="React">
  <img src="https://img.shields.io/badge/Flutter-3.x-02569B?style=for-the-badge&logo=flutter&logoColor=white" alt="Flutter">
  <img src="https://img.shields.io/badge/Tailwind_CSS-3.x-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white" alt="Tailwind CSS">
  <img src="https://img.shields.io/badge/MySQL-8.x-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL">
</p>

**KANGMAS** adalah aplikasi berbasis platform (Full-Stack Web & Mobile App) yang mempertemukan masyarakat yang membutuhkan layanan perbaikan atau pembangunan rumah dengan tenaga pertukangan (mitra tukang) profesional, terverifikasi, dan terdekat di wilayahnya.

---

## Fitur Utama

### Untuk Masyarakat / Pengguna (Web & Mobile)
- **Pencarian & Rekomendasi Pintar**: Temukan tukang terdekat menggunakan kalkulasi jarak (*Haversine formula*) berdasarkan koordinat lokasi GPS.
- **Kategori Layanan Lengkap**: Solusi untuk perbaikan Kelistrikan & Kabel, Saluran & Pompa Air, serta Konstruksi & Bangunan.
- **Pemesanan Mudah**: Buat pesanan layanan perbaikan dengan melampirkan foto bukti kerusakan, deskripsi, dan titik lokasi.
- **Riwayat & Ulasan**: Pantau status pesanan (*Pending, Diterima, Menunggu Persetujuan, Selesai, Dibatalkan*) serta berikan rating & ulasan kepada tukang.

### Untuk Mitra Tukang
- **Registrasi Mitra**: Pendaftaran online dengan verifikasi identitas (KTP, Foto Selfie) dan dokumen Portofolio.
- **Manajemen Status Kerja**: Atur status ketersediaan kerja (*Available / Busy*) secara real-time.
- **Manajemen Pesanan**: Terima, tolak, dan selesaikan pesanan masuk langsung dari genggaman.

### Untuk Admin Portal (Web)
- **Dashboard Analitik Interaktif**: Visualisasi statistik pesanan, distribusi kategori tukang, dan performa mitra menggunakan grafik dinamis.
- **Verifikasi Ketat**: Tinjau dokumen pendaftaran mitra tukang sebelum menyetujui (*Approve*), menolak (*Reject*), atau memblokir (*Blacklist*) mitra.
- **Pemantauan Total**: Kelola seluruh data pengguna, mitra tukang, dan transaksi pesanan dalam satu dasbor terpusat.

---

## Arsitektur & Teknologi

| Komponen | Teknologi | Keterangan |
| :--- | :--- | :--- |
| **Backend API** | **Laravel 11** (PHP 8.2+) | RESTful API, Eloquent ORM, Sanctum Token Auth, Database Transactions |
| **Web Frontend** | **React 19** + **Vite** | Single Page Application (SPA), Tailwind CSS, Lucide Icons, Recharts |
| **Mobile App** | **Flutter** (Dart) | Cross-platform Android & iOS App, HTTP Client, Shared Preferences |
| **Database** | **MySQL** | Relational Database Management System |

---

## Panduan Instalasi & Pengaturan (Local Setup)

### 1. Prasyarat Sistem
Pastikan komputer Anda telah terinstal:
- **PHP** >= 8.2 & **Composer**
- **Node.js** >= 18 & **npm**
- **MySQL** / MariaDB Server (misal lewat XAMPP, Laragon, atau Docker)
- **Flutter SDK** (opsional, jika ingin menjalankan aplikasi mobile)

---

### 2. Pengaturan Backend & Web (Laravel + React)

1. **Clone Repositori**
   ```bash
   git clone https://github.com/username-anda/project-kangmas.git
   cd project-kangmas
   ```

2. **Instal Dependensi PHP & JavaScript**
   ```bash
   composer install
   npm install
   ```

3. **Konfigurasi Environment (`.env`)**
   Salin file `.env.example` menjadi `.env`:
   ```bash
   cp .env.example .env
   ```
   Buka file `.env` dan sesuaikan konfigurasi koneksi database MySQL Anda:
   ```ini
   APP_NAME="KANGMAS"
   APP_URL=http://localhost:8000

   DB_CONNECTION=mysql
   DB_HOST=127.0.0.1
   DB_PORT=3306
   DB_DATABASE=project_kangmas
   DB_USERNAME=root
   DB_PASSWORD=

   # (Opsional) API Key Google Maps jika ingin fitur peta interaktif berfungsi penuh
   VITE_GOOGLE_MAPS_API_KEY=your_api_key_here
   ```

4. **Generate Application Key & Link Storage**
   ```bash
   php artisan key:generate
   php artisan storage:link
   ```

5. **Migrasi Database & Seeding Data Awal**
   Pastikan service MySQL Anda sudah berjalan dan database `project_kangmas` sudah dibuat, lalu jalankan:
   ```bash
   php artisan migrate --seed
   ```
   *Perintah ini akan membuat seluruh tabel struktur database beserta akun testing (Admin, User, dan Mitra Tukang beserta sampel portofolio).*

---

### 3. Menjalankan Aplikasi Web Secara Lokal

Anda membutuhkan **2 terminal** yang berjalan bersamaan:

- **Terminal 1 (Laravel API Server):**
  ```bash
  php artisan serve
  ```
  *Server API akan aktif di: `http://127.0.0.1:8000`*

- **Terminal 2 (Vite Frontend Dev Server):**
  ```bash
  npm run dev
  ```
  *Aplikasi Web React akan aktif di: `http://localhost:5173` (atau sesuai url di terminal)*

---

### 4. Pengaturan & Menjalankan Aplikasi Mobile (Flutter)

1. Masuk ke direktori mobile:
   ```bash
   cd mobile
   ```
2. Instal package dependensi Flutter:
   ```bash
   flutter pub get
   ```
3. Sesuaikan URL API Backend di file `lib/services/api_service.dart`:
   - Jika menggunakan **Android Emulator**: ubah `baseUrl` ke `http://10.0.2.2:8000/api`
   - Jika menggunakan **Perangkat Asli / iOS Simulator**: ubah `baseUrl` ke `http://localhost:8000/api` atau `http://<IP_LAN_KOMPUTER_ANDA>:8000/api`
4. Jalankan aplikasi:
   ```bash
   flutter run
   ```

---

## Akun Uji Coba (Test Accounts)

Setelah menjalankan `php artisan migrate --seed`, Anda dapat menggunakan akun berikut untuk pengujian:

| Role | Email | Password | Akses URL / Fitur |
| :--- | :--- | :--- | :--- |
| **Admin Portal** | `admin@kangmas.com` | `password` | Login di Web `http://localhost:8000/admin/login` |
| **Pengguna / Masyarakat** | `user1@kangmas.com` | `password` | Login di Aplikasi Mobile / Web |
| **Mitra Tukang** | `tukang1@kangmas.com` | `password` | Login di Aplikasi Mobile (Mitra) |

---

## Struktur Direktori Penting

```text
project-kangmas/
├── app/Http/Controllers/Api/   # Controller logika bisnis API (Auth, Tukang, Order, Admin, Recommender)
├── database/
│   ├── migrations/             # Skema struktur tabel database
│   └── seeders/                # Data sampel awal sistem
├── mobile/                     # Proyek aplikasi mobile Flutter (Dart)
│   └── lib/                    # Screen UI, provider state, dan service API mobile
├── public/                     # Aset statis dan symlink storage file upload
├── resources/
│   ├── css/                    # Tailwind stylesheet
│   └── js/                     # Proyek Frontend React (Pages, Components, Services)
├── routes/
│   ├── api.php                 # Daftar endpoint REST API
│   └── web.php                 # Routing halaman web SPA
├── .env.example                # Templat variabel environment
└── README.md                   # Dokumentasi proyek
```

---

## Kontribusi & Pengembang

Proyek ini dikembangkan sebagai bagian dari Tugas Besar Mata Kuliah **Aplikasi Berbasis Platform** (Semester 6).

---