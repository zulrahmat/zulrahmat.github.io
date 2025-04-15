Siap! Berikut materi **Composer di PHP** secara **singkat dan sederhana**:

---

## 🧰 Apa itu Composer?

> Composer adalah **manajer dependensi** untuk PHP.  
Kamu bisa **menginstal library** (package) dari luar, seperti `guzzle`, `dompdf`, dll, dengan mudah.

---

## 🔧 Cara Pakai Composer

### 1. **Install Composer**
Unduh dari: https://getcomposer.org/download/

Cek versi:
```bash
composer --version
```

---

### 2. **Inisialisasi Project**
```bash
composer init
```

Ini akan membuat file `composer.json`.

---

### 3. **Install Package**
Misal kita mau install `guzzlehttp/guzzle`:
```bash
composer require guzzlehttp/guzzle
```

Composer akan otomatis:
- Unduh library-nya
- Buat file `vendor/`
- Update `composer.json` dan `composer.lock`

---

### 4. **Autoloading**
Composer menyediakan autoload otomatis lewat file `vendor/autoload.php`.

Contoh penggunaan:
```php
require 'vendor/autoload.php';

use GuzzleHttp\Client;

$client = new Client();
```

---

## 📁 Struktur Project Composer

```
project/
├── composer.json
├── composer.lock
├── vendor/
│   └── autoload.php
└── index.php
```

---

## 📌 Perintah Composer Umum

| Perintah | Keterangan |
|----------|------------|
| `composer init` | Buat file `composer.json` |
| `composer require vendor/package` | Install package |
| `composer install` | Install semua dari `composer.json` |
| `composer update` | Update semua package |
| `composer dump-autoload` | Regenerasi file autoload |

---

Kalau kamu mau, aku bisa bantu bikin project contoh sederhana pakai composer. Mau?