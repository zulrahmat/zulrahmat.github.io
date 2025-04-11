Berikut adalah **cheatsheet penggunaan Template (View) di CodeIgniter 4** — sangat berguna untuk kamu yang ingin mengatur tampilan website dengan struktur rapi dan efisien.

---

## 📋 CodeIgniter 4 Template/View Cheatsheet

### 🗂️ Struktur Direktori View (Umum)
```plaintext
/app
 └── /Views
      ├── layout/
      │     └── main.php
      ├── pages/
      │     └── home.php
      └── welcome_message.php
```

---

### 📄 1. Load View Sederhana
```php
return view('nama_view');
```

> View berada di `/app/Views/nama_view.php`

---

### 📦 2. Load View + Kirim Data
```php
$data = ['title' => 'Beranda', 'isi' => 'Halo Dunia'];
return view('pages/home', $data);
```

---

### 🧩 3. Template Master (Layouting)

#### 📁 layout/main.php (template utama)
```php
<!doctype html>
<html>
<head>
  <title><?= $title ?? 'Judul Default' ?></title>
</head>
<body>
  <header>Ini Header</header>

  <main>
    <?= $this->renderSection('content') ?>
  </main>

  <footer>Ini Footer</footer>
</body>
</html>
```

#### 📄 pages/home.php (halaman isi)
```php
<?= $this->extend('layout/main') ?>

<?= $this->section('content') ?>
  <h1>Halo <?= $isi ?></h1>
<?= $this->endSection() ?>
```

---

### 🔁 4. Include View Lain (seperti partial/header/footer)
```php
<?= view('partials/navbar') ?>
```

---

### 📥 5. Kirim Data ke Partial
```php
<?= view('partials/navbar', ['menu' => 'Beranda']) ?>
```
