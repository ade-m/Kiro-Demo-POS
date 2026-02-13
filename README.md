# Kiro Demo POS - AI Powered Point of Sale

![Kiro Demo POS Banner](https://via.placeholder.com/1200x400?text=Kiro+Demo+POS+Laravel+Filament)

Selamat datang di repositori **Kiro Demo POS**. Proyek ini adalah aplikasi Point of Sale (POS) modern yang dibangun menggunakan **Laravel Filament**, **Docker**, dan **PostgreSQL**.

Tujuan utama dari repositori ini adalah sebagai **bahan pembelajaran (tutorial)** untuk mendemonstrasikan bagaimana **Kiro** (AWS AI Assistant) dapat digunakan untuk mempercepat pengembangan aplikasi dan membangun fitur asisten AI cerdas di dalam ekosistem Laravel.

## 🚀 Fitur Utama

- **Manajemen Produk & Stok**: CRUD produk dengan kategori, harga, dan manajemen inventaris.
- **Transaksi Kasir (POS)**: Antarmuka kasir yang cepat dan responsif.
- **Laporan Penjualan**: Visualisasi data penjualan harian/bulanan menggunakan Widget Filament.
- **AI Assistant Integration**: Contoh integrasi code-assist menggunakan Kiro untuk analisis data.
- **Full Docker Support**: Aplikasi, Database (PostgreSQL), dan Web Server berjalan sepenuhnya di dalam Docker.

## 🛠 Teknologi yang Digunakan

- **Framework**: [Laravel 11](https://laravel.com/)
- **Admin Panel**: [FilamentPHP v3](https://filamentphp.com/)
- **Database**: PostgreSQL 16 (Running in Docker)
- **Containerization**: Docker & Docker Compose
- **AI Tool**: [Kiro](https://kiro.dev/) (AWS AI Assistant / Agentic IDE)

---

## 📋 Langkah-Langkah Persiapan (Prerequisites)

Sebelum memulai, pastikan perangkat Anda telah memenuhi persyaratan berikut.

**PENTING**: Anda **TIDAK PERLU** menginstall PHP, Composer, atau PostgreSQL secara manual di komputer Anda. Semua akan dijalankan melalui Docker untuk menjamin konsistensi lingkungan pengembangan.

1.  **Docker Desktop**: Wajib diinstal dan dalam keadaan berjalan (Running). [Download di sini](https://www.docker.com/products/docker-desktop/).
2.  **Git**: Untuk melakukan kloning repositori.
3.  **Kiro IDE**: Disarankan menggunakan editor Kiro untuk mengikuti tutorial AI Assistant secara maksimal. [Download Kiro](https://kiro.dev/).
4.  **AWS Builder ID**: Diperlukan untuk login ke Kiro (Gratis).

---

## ⚙️ Instalasi & Konfigurasi

Ikuti langkah-langkah berikut secara berurutan di terminal (Terminal Kiro atau CMD/Terminal biasa):

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

###3. Instalasi Dependensi (Composer) via Docker

Karena kita tidak menggunakan Composer di komputer lokal, kita akan memerintahkan Docker untuk menjalankannya.

Bash
# Perintah ini akan mendownload image, install vendor, lalu menghapus container sementara
# Pastikan nama service sesuai dengan docker-compose.yml (biasanya 'laravel.test' atau 'app')
```bash
docker compose run --rm laravel.test composer install
```
Catatan: Langkah ini mungkin memakan waktu beberapa menit tergantung koneksi internet.

###4. Menjalankan Aplikasi

Setelah folder vendor terbentuk, jalankan seluruh service (App & Database):

```bash
docker compose up -d
```
Pastikan semua container berjalan dengan mengetik docker compose ps.

###5. Setup Database & Aplikasi

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
6. Membuat Akun Admin Filament
```
Buat user untuk login ke dashboard admin:
```bash
docker compose exec laravel.test php artisan filament:user
Ikuti instruksi di layar untuk memasukkan Nama, Email, dan Password.
```

###7. Akses Aplikasi

Buka browser Anda dan akses:

Halaman Utama: http://localhost

Dashboard Admin: http://localhost/admin
