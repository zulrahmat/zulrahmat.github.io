Berikut ini adalah **materi singkat tentang Controller di CodeIgniter 4** — cocok untuk kamu yang ingin memahami dasar-dasar pengendali alur aplikasi 🚀

---

## 🎮 Apa itu Controller?

> Controller adalah **komponen utama di MVC** (Model-View-Controller) yang bertugas **mengatur alur data antara model dan view**.

---

## 🗂️ Lokasi Controller
Semua controller disimpan di folder:

```
/app/Controllers/
```

---

## 🛠️ Membuat Controller

### 1. Secara manual:
```php
namespace App\Controllers;

class Home extends BaseController
{
    public function index()
    {
        return view('welcome_message');
    }
}
```

### 2. Dengan CLI:
```bash
php spark make:controller User
```

---

## ⚙️ Controller Default

Diatur di file: `/app/Config/Routes.php`
```php
$routes->get('/', 'Home::index'); // Route ke Home controller
```

---

## 📦 Fungsi dalam Controller

```php
class User extends BaseController
{
    public function index()
    {
        return 'Daftar User';
    }

    public function detail($id)
    {
        return "Detail user dengan ID: $id";
    }
}
```

---

## 📌 Mengakses Model dari Controller

```php
use App\Models\UserModel;

public function index()
{
    $userModel = new UserModel();
    $data['users'] = $userModel->findAll();
    return view('user/index', $data);
}
```

---

## 🧰 BaseController

`BaseController.php` adalah tempat untuk menyimpan fungsi yang umum digunakan di semua controller, seperti:
```php
protected $session;

public function initController(...)
{
    parent::initController(...);
    $this->session = \Config\Services::session();
}
```