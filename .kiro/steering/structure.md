# Project Structure

## Directory Organization

```
project-root/
├── .kiro/                         # Kiro configuration dan steering files
│   └── steering/                  # AI assistant guidance documents
│
├── app/                           # Core application logic (Laravel)
│   ├── Filament/                  # Filament resources, pages, widgets
│   │   ├── Resources/
│   │   ├── Pages/
│   │   └── Widgets/
│   ├── Models/                    # Eloquent models
│   ├── Http/
│   │   ├── Controllers/
│   │   └── Middleware/
│   ├── Services/                  # Business logic (POS domain)
│   ├── Policies/                  # Authorization rules
│   └── Providers/
│
├── bootstrap/
├── config/                        # Application & package configuration
│   ├── database.php
│   ├── filament.php
│   └── auth.php
│
├── database/
│   ├── migrations/                # Database schema
│   ├── seeders/                   # Initial & demo data
│   └── factories/
│
├── public/                        # Publicly accessible assets
│   ├── images/
│   └── build/
│
├── resources/
│   ├── views/                     # Blade templates (non-Filament)
│   ├── css/
│   └── js/
│
├── routes/
│   ├── web.php
│   ├── api.php
│   └── filament.php
│
├── storage/
├── tests/                         # Automated tests
│   ├── Feature/
│   └── Unit/
│
├── docs/                          # Project documentation
│   ├── setup.md
│   ├── deployment.md
│   └── user-guide.md
│
├── .env.example
├── composer.json
├── README.md
└── artisan
```

## File Naming Conventions

- **Class & File**: PascalCase
  - Contoh: `ProductVariant.php`, `SaleTransaction.php`
- **Migration**: deskriptif dan berurutan
  - Contoh: `2026_01_31_create_products_table.php`
- **Filament Resource**: 
  - `ProductResource`, `SaleResource`
- **Service Class**: 
  - `SaleService`, `StockService`
- **Config file**: `snake_case.php`

## Code Organization Principles

### Separation of Concerns
- **UI** → Filament Resources & Pages
- **Business logic** → `app/Services`
- **Data access** → Eloquent Models

### Thin Controllers
- Controller hanya sebagai penghubung request → service

### Domain-driven mindset
- POS logic tidak ditaruh di Filament langsung

### Readable over clever
- Mudah dipahami oleh tim kecil / UMKM developer

## Module Structure

Modul disusun berdasarkan domain POS:

```
app/
├── Modules/
│   ├── Product/
│   │   ├── Models/
│   │   ├── Services/
│   │   └── Filament/
│   ├── Sales/
│   │   ├── Models/
│   │   ├── Services/
│   │   └── Filament/
│   └── Inventory/
│       ├── Models/
│       └── Services/
```

## Asset Organization

- **Images**: `public/images/`
- **CSS & JS**:
  - `resources/css/`
  - `resources/js/`
- Asset di-build menggunakan Vite
- Filament menggunakan styling bawaan, custom hanya jika diperlukan

## Configuration Management

- Semua konfigurasi berada di folder `config/`
- Environment-specific settings disimpan di `.env`
- Tidak menyimpan credential di repository
- Database PostgreSQL dikonfigurasi melalui `config/database.php`

## Documentation Structure

- **`README.md`** → Ringkasan proyek & cara menjalankan
- **`docs/setup.md`** → Instalasi lokal & environment
- **`docs/deployment.md`** → Deployment (AWS / VPS)
- **`docs/user-guide.md`** → Panduan owner & kasir UMKM

## Testing Structure

### Unit Tests
- **Location**: `tests/Unit/`
- **Purpose**: Untuk service dan business logic (stok, transaksi)

### Feature Tests
- **Location**: `tests/Feature/`
- **Purpose**: Untuk alur transaksi, login, laporan

Penulisan test mengikuti standar Laravel (`php artisan test`)