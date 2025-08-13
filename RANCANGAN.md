# RANCANGAN SISTEM INFORMASI ADUAN HOAKS MAFINDO YOGYAKARTA

**Versi Dokumen:** 0.1
**Tanggal:** 13 Agustus 2025

---

## 1. Deskripsi Singkat & Latar Belakang Masalah

### 1.1. Deskripsi Proyek
Sistem ini adalah aplikasi berbasis web yang bertujuan untuk menjadi kanal utama pelaporan berita hoaks dari masyarakat kepada tim verifikator Mafindo Korda Yogyakarta. Sistem ini akan mengelola aduan yang masuk secara terpusat agar lebih mudah dilacak, didistribusikan, dan diarsip.

### 1.2. Identifikasi Masalah (Problem Statement)
* **Masalah 1: Kanal Aduan Tersebar.** Saat ini, aduan hoaks masuk melalui kanal yang tidak terpusat (contoh: Direct Message Instagram, WhatsApp pribadi relawan, mention di Twitter).
* **Masalah 2: Sulit Melacak Progres.** Sulit untuk mengetahui sebuah aduan sudah ditangani atau belum, dan siapa yang sedang menanganinya. Tidak ada sistem pelacakan status yang jelas.
* **Masalah 3: Data Tidak Terstruktur.** Aduan yang masuk tidak seragam dan tersimpan dalam format yang berbeda-beda (screenshot, teks, link), menyulitkan untuk rekapitulasi dan analisis tren hoaks di wilayah Yogyakarta.

---

## 2. Tujuan & Ruang Lingkup Proyek

### 2.1. Tujuan Proyek
* Menyediakan satu platform tunggal (single platform) untuk masyarakat Yogyakarta dalam melaporkan dugaan hoaks.
* Meningkatkan efisiensi kerja relawan Mafindo dalam mengelola dan memverifikasi aduan yang masuk.
* Menciptakan database aduan yang terstruktur untuk keperluan arsip dan analisis internal.

### 2.2. Pengguna Sistem (Aktor)
1.  **Pelapor (Publik/Guest):** Masyarakat umum yang melaporkan hoaks. Tidak perlu login.
2.  **Admin (Relawan Mafindo):** Anggota Mafindo yang bertugas mengelola dan memverifikasi aduan. Perlu login untuk mengakses sistem.

### 2.3. Ruang Lingkup (Batasan Masalah)
* Sistem ini FOKUS pada manajemen pelaporan, bukan deteksi hoaks otomatis (AI).
* Sistem tidak melakukan verifikasi, hanya sebagai alat bantu alur kerja verifikasi.
* Output akhir dari sistem adalah perubahan status aduan (misal: "Selesai - Hoaks"), bukan publikasi artikel klarifikasi.

---

## 3. Analisis Alur & Fitur Sistem

### 3.1. Alur Pengguna (User Flow)

**A. Alur Pelapor (Publik):**
1.  Membuka halaman utama web.
2.  Mengklik tombol "Lapor Hoaks".
3.  Mengisi formulir aduan yang berisi:
    - Narasi hoaks (wajib diisi).
    - Link sumber (opsional).
    - Upload gambar/screenshot (opsional).
4.  Menekan tombol "Kirim".
5.  Menerima notifikasi berhasil dan sebuah kode pelacakan unik.
6.  (Opsional) Mengecek status aduan di halaman "Cek Status" dengan memasukkan kode unik.

**B. Alur Admin (Relawan Mafindo):**
1.  Membuka halaman login admin.
2.  Memasukkan email dan password.
3.  Masuk ke Dashboard yang menampilkan daftar semua aduan.
4.  Melihat aduan terbaru di bagian paling atas dengan status "Baru".
5.  Mengklik salah satu aduan untuk melihat detailnya.
6.  Mengubah status aduan (misal: dari "Baru" ke "Diproses").
7.  Menambahkan catatan internal (misal: "Sudah dikonfirmasi ke sumber X").
8.  Menyimpan perubahan.

### 3.2. Rancangan Fitur (Features)

* **Fitur Publik:**
    - Halaman Utama (Landing Page).
    - Formulir Aduan.
    - Halaman Cek Status Aduan.
* **Fitur Admin (Wajib Login):**
    - Autentikasi (Login & Logout).
    - Dashboard Aduan (Menampilkan semua aduan dalam bentuk tabel).
    - Halaman Detail Aduan.
    - Fitur Ubah Status Aduan.
    - Fitur Tambah Catatan Internal.

---

## 4. Rancangan Database (Versi Teks)

**Tabel 1: `users`** (Untuk menyimpan data Admin)
- `id` (Primary Key, Auto Increment)
- `name` (VARCHAR)
- `email` (VARCHAR, Unique)
- `password` (VARCHAR)
- `created_at` (TIMESTAMP)
- `updated_at` (TIMESTAMP)

**Tabel 2: `reports`** (Untuk menyimpan data aduan hoaks)
- `id` (Primary Key, Auto Increment)
- `tracking_code` (VARCHAR, Unique) - Kode unik untuk pelapor.
- `content` (TEXT) - Narasi hoaksnya.
- `image_path` (VARCHAR, Nullable) - Path ke file gambar yang diupload.
- `source_link` (VARCHAR, Nullable) - Link ke sumber hoaks.
- `status` (ENUM: 'Baru', 'Diproses', 'Selesai - Hoaks', 'Selesai - Fakta', 'Tidak Relevan') - Status aduan.
- `notes` (TEXT, Nullable) - Catatan internal dari admin.
- `created_at` (TIMESTAMP)
- `updated_at` (TIMESTAMP)

---

## 5. Teknologi yang Direncanakan
* **Bahasa Pemrograman:** PHP 8.x
* **Framework Backend:** Laravel 10.x
* **Framework Frontend:** Bootstrap 5
* **Database:** MySQL / MariaDB
* **Web Server Lokal:** XAMPP