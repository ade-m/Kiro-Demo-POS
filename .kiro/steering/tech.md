# Technology Stack

## Programming Language

- **PHP 8.2+** - Bahasa utama backend aplikasi
- **JavaScript (ES6+)** - Asset frontend dengan Vite
- **SQL (PostgreSQL dialect)** - Pengelolaan data transaksi dan stok

## Framework & Libraries

### Backend
- **Laravel 11** - Web application framework utama
- **Filament** - Admin panel dan UI utama POS
- **Laravel Eloquent ORM** - Database abstraction layer
- **Laravel Sanctum** - Autentikasi (jika API diperlukan)

### Frontend & UI
- **Blade** - Template engine Laravel
- **Livewire** - Interaksi dinamis di Filament
- **Tailwind CSS** - Styling UI
- **Vite** - Asset bundler

### Database
- **PostgreSQL** - Relational database utama

### Supporting Libraries
- **Carbon** - Date & time handling
- **Spatie Laravel Permission** - Role & permission management
- **Laravel Debugbar** (dev only) - Debugging

## Build System

- **Composer** - Dependency manager untuk PHP
- **NPM** - Dependency manager frontend
- **Vite** - Build & hot reload assets

## Development Environment

### Requirements
- PHP ≥ 8.2
- Composer
- Node.js ≥ 18
- PostgreSQL ≥ 14
- Web server (Laravel built-in / Nginx / Apache)

### Recommended Local Setup
- Laravel Herd / Valet / Sail
- Database lokal PostgreSQL
- `.env` untuk environment configuration

## Common Commands

### Setup
```bash
composer install
npm install
cp .env.example .env
php artisan key:generate
php artisan migrate --seed

```

### Development
```bash
php artisan serve
npm run dev

```

### Testing
```bash
php artisan test

```

### Building
```bash
npm run build

```

### Deployment
```bash
php artisan migrate --force
php artisan optimize

```

## Configuration Files

- **`.env`** - Environment variables (database, app key, credentials)
- **`config/app.php`** - Aplikasi utama
- **`config/database.php`** - Konfigurasi PostgreSQL
- **`config/filament.php`** - Pengaturan UI Filament
- **`config/auth.php`** - Autentikasi & guard

## Dependencies Management

- **Backend dependencies** dikelola menggunakan Composer
  - Update: `composer update`
- **Frontend dependencies** dikelola menggunakan NPM
  - Update: `npm update`
- **Dependency versi** dikunci melalui:
  - `composer.lock`
  - `package-lock.json`
- Update dilakukan secara bertahap dan diuji di environment development sebelum production