# Kiro Demo POS - Spec-Driven Development Showcase

Selamat datang di repositori **Kiro Demo POS**.

Proyek ini adalah demonstrasi nyata penggunaan **Kiro** (AWS AI Assistant) untuk membangun perangkat lunak Point of Sale (POS) yang kompleks menggunakan pendekatan **Spec-Driven Development (SDD)**.

Aplikasi ini dibangun dari nol dengan menuliskan spesifikasi (Specs) terlebih dahulu, kemudian membiarkan Kiro meng-generate kode, tes, dan struktur database menggunakan stack modern: **Laravel Filament**, **Docker**, dan **PostgreSQL**.

## 🎯 Tujuan Repositori

Repositori ini bukan sekadar source code aplikasi POS, melainkan bahan pembelajaran untuk:
1.  **Mempraktikkan Spec-Driven Development**: Cara menulis prompt dan spesifikasi yang efektif untuk AI.
2.  **Workflow AI-First**: Bagaimana Kiro mempercepat pembuatan fitur CRUD, logika transaksi, dan laporan.
3.  **Modern Stack Deployment**: Menjalankan Laravel & PostgreSQL sepenuhnya di dalam Docker.

## 🚀 Fitur Aplikasi (Hasil Build)

Aplikasi POS yang dihasilkan memiliki fitur:
- **Manajemen Inventaris**: Produk, Kategori, dan Stok (Laravel Filament Resource).
- **Kasir / POS**: Halaman transaksi kasir.
- **Laporan**: Dashboard analitik penjualan harian/bulanan.
- **Manajemen User**: Role dan permission untuk Kasir dan Admin.

## 🛠 Teknologi yang Digunakan

- **AI Assistant**: [Kiro](https://kiro.dev/) (Digunakan untuk generate code berdasarkan Specs)
- **Framework**: [Laravel 11](https://laravel.com/)
- **Admin Panel**: [FilamentPHP v3](https://filamentphp.com/)
- **Database**: PostgreSQL 16 (Running in Docker)
- **Containerization**: Docker & Docker Compose

---

## 📋 Langkah-Langkah Persiapan (Prerequisites)

**PENTING**: Karena proyek ini berbasis Docker, Anda **TIDAK PERLU** menginstall PHP, Composer, atau PostgreSQL di komputer lokal (Host) Anda.

1.  **Docker Desktop**: Wajib diinstal dan dalam keadaan berjalan (Running).
2.  **Git**: Untuk melakukan kloning repositori.
3.  **Kiro IDE**: Sangat disarankan menggunakan editor Kiro untuk mempelajari *prompt history* dan *specs* yang digunakan.
4.  **AWS Builder ID**: Untuk login ke Kiro.

---

## ⚙️ Instalasi & Menjalankan Proyek

Ikuti langkah-langkah berikut di terminal Anda:

### 1. Clone Repositori
```bash
git clone [https://github.com/ade-m/Kiro-Demo-POS.git](https://github.com/ade-m/Kiro-Demo-POS.git)
cd Kiro-Demo-POS
```

### 2. Konfigurasi Environment
Salin file contoh konfigurasi `.env`.

cp .env.example .env
PENTING: Buka file .env dan pastikan konfigurasi database mengarah ke container Docker (DB_HOST=pgsql), bukan localhost.

```bash
DB_CONNECTION=pgsql
DB_HOST=pgsql
DB_PORT=5432
DB_DATABASE=kiro_pos
DB_USERNAME=sail
DB_PASSWORD=password
```

### 3. Instalasi Dependensi (Composer) via Docker

Karena kita tidak menggunakan Composer di komputer lokal, kita akan memerintahkan Docker untuk menjalankannya.

#### Perintah ini akan mendownload image, install vendor, lalu menghapus container sementara
#### Pastikan nama service sesuai dengan docker-compose.yml (biasanya 'laravel.test' atau 'app')
```bash
docker compose run --rm laravel.test composer install
```
Catatan: Langkah ini mungkin memakan waktu beberapa menit tergantung koneksi internet.

### 4. Menjalankan Aplikasi

Setelah folder vendor terbentuk, jalankan seluruh service (App & Database):

```bash
docker compose up -d
```
Pastikan semua container berjalan dengan mengetik docker compose ps.

### 5. Setup Database & Aplikasi

Jalankan perintah-perintah Laravel berikut di dalam container agar terhubung ke PostgreSQL:

```bash
# 1. Generate Application Key
docker compose exec laravel.test php artisan key:generate

# 2. Migrasi Database (Membuat tabel di PostgreSQL)
docker compose exec laravel.test php artisan migrate

# 3. Seed Data (Mengisi data dummy produk & transaksi awal)
docker compose exec laravel.test php artisan db:seed

# 4. Link Storage (Agar gambar produk dapat diakses publik)
docker compose exec laravel.test php artisan storage:link
### 6. Membuat Akun Admin Filament
```
Buat user untuk login ke dashboard admin:
```bash
docker compose exec laravel.test php artisan filament:user
Ikuti instruksi di layar untuk memasukkan Nama, Email, dan Password.
```

### 7. Akses Aplikasi

Buka browser Anda dan akses:

Halaman Utama: http://localhost

Dashboard Admin: http://localhost/admin

📚 Mempelajari Spec-Driven Development
Untuk memahami bagaimana kode ini dibuat oleh Kiro:
1. Cek folder specs/ (jika disertakan) untuk melihat file markdown spesifikasi.
2. Perhatikan struktur kode yang dihasilkan oleh Kiro di app/Filament/Resources.
