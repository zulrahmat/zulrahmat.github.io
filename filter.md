Berikut ini adalah **materi singkat tentang Filter di CodeIgniter 4** — cocok untuk kamu yang ingin memahami cara kerja middleware di CodeIgniter 🚀

---

## 📘 Apa itu Filter?

> **Filter** di CodeIgniter 4 mirip dengan **middleware** pada framework lain.  
Digunakan untuk **menangani request atau response sebelum atau sesudah** controller dijalankan.

Contoh penggunaan umum:
- Autentikasi
- Logging
- Maintenance mode
- CORS
- Throttling API

---

## 🛠️ Struktur Filter

Filter disimpan di folder:

```
/app/Filters/
```

---

## 🔧 1. Membuat Filter Baru

```bash
php spark make:filter AuthFilter
```

Hasilnya: `/app/Filters/AuthFilter.php`

---

## ✍️ 2. Contoh Isi Filter

```php
namespace App\Filters;

use CodeIgniter\HTTP\RequestInterface;
use CodeIgniter\HTTP\ResponseInterface;
use CodeIgniter\Filters\FilterInterface;

class AuthFilter implements FilterInterface
{
    public function before(RequestInterface $request, $arguments = null)
    {
        if (! session()->get('logged_in')) {
            return redirect()->to('/login');
        }
    }

    public function after(RequestInterface $request, ResponseInterface $response, $arguments = null)
    {
        // kosongkan jika tidak perlu
    }
}
```

---

## ⚙️ 3. Registrasi Filter

Edit di: `/app/Config/Filters.php`

```php
public $aliases = [
    'auth' => \App\Filters\AuthFilter::class,
];
```

---

## 📌 4. Menggunakan Filter

### 🔹 Global (Semua route)
```php
public $globals = [
    'before' => [
        'auth' // aktif untuk semua route
    ]
];
```

### 🔹 Khusus Route
Di `app/Config/Routes.php`:

```php
$routes->get('dashboard', 'Dashboard::index', ['filter' => 'auth']);
```