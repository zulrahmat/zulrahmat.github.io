Siap! Berikut adalah **materi lengkap tentang penggunaan `Pager` (Pagination)** di **CodeIgniter 4**, yang biasa digunakan untuk membagi data ke dalam beberapa halaman, misalnya pada daftar produk, artikel, atau data pegawai.

---

## 📚 Materi: Pagination (Pager) di CodeIgniter 4

---

### 🔹 1. **Setup Awal**
`Pager` sudah termasuk dalam core CodeIgniter 4, kamu hanya perlu:

```php
$pager = \Config\Services::pager();
```

Dan pastikan kamu memuat **library** dan **helper** di controller atau `BaseController`:
```php
helper('url'); // agar fungsi site_url() bisa dipakai
```

---

### 🔹 2. **Pagination dengan Model (paling umum)**
CI4 menyediakan metode `paginate()` di model bawaan.

#### Contoh:
```php
namespace App\Controllers;
use App\Models\MahasiswaModel;

class Mahasiswa extends BaseController
{
    public function index()
    {
        $model = new MahasiswaModel();

        $data['mahasiswa'] = $model->paginate(10); // tampil 10 per halaman
        $data['pager']     = $model->pager;

        return view('mahasiswa/index', $data);
    }
}
```

---

### 🔹 3. **View: Menampilkan Data dan Navigasi Pager**
```php
<!-- app/Views/mahasiswa/index.php -->

<h2>Daftar Mahasiswa</h2>
<ul>
<?php foreach ($mahasiswa as $mhs): ?>
    <li><?= esc($mhs['nama']) ?></li>
<?php endforeach ?>
</ul>

<!-- Pagination -->
<div>
    <?= $pager->links() ?>
</div>
```

---

### 🔹 4. **Custom Template untuk Pagination**
CodeIgniter punya beberapa template pager bawaan:

- `default_full` (dengan nomor dan tombol prev/next)
- `simple`
- `semantic`
- `bootstrap` (untuk Bootstrap 4/5)
  
#### Contoh:
```php
<?= $pager->links('default', 'bootstrap') ?>
```

Kamu juga bisa membuat template sendiri di:
```
app/Views/Pagers/
```

Contoh file: `app/Views/Pagers/custom_pager.php`

Lalu panggil dengan:
```php
<?= $pager->links('default', 'custom_pager') ?>
```

---

### 🔹 5. **Menentukan Nama Grup Pager**
Kalau kamu ingin melakukan pagination untuk lebih dari satu dataset dalam satu halaman:

```php
$data['produk'] = $produkModel->paginate(10, 'produk');
$data['kategori'] = $kategoriModel->paginate(5, 'kategori');

$data['pagerProduk'] = $produkModel->pager;
$data['pagerKategori'] = $kategoriModel->pager;
```

Di view:
```php
<?= $pagerProduk->links('produk', 'bootstrap') ?>
<?= $pagerKategori->links('kategori', 'bootstrap') ?>
```

---

### 🔹 6. **Custom URL Segment**
Secara default pagination menggunakan segment ke-3:
```
http://localhost/mahasiswa/index/2
```

Kamu bisa mengatur offset segment di konfigurasi:
```
app/Config/Pager.php

public $segment = 3;
```

---

### 🔹 7. **Manual Pagination (Jika Tidak Pakai Model)**
```php
$perPage = 10;
$page = $this->request->getVar('page') ?? 1;

$total = count($data);
$offset = ($page - 1) * $perPage;

$pager = \Config\Services::pager();
$pagination = $pager->makeLinks($page, $perPage, $total, 'bootstrap');

$data = array_slice($data, $offset, $perPage);
```

---

## 🧪 Tips Tambahan
- Jangan lupa gunakan `esc()` di view untuk mencegah XSS.
- Jika pakai Bootstrap, langsung panggil:  
  ```php
  <?= $pager->links('default', 'bootstrap') ?>
  ```

---

Kalau kamu mau, aku bisa buatin contoh project CRUD + pagination (misal daftar pegawai). Mau sekalian?