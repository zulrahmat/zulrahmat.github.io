Siap! Berikut ini adalah **materi lengkap tentang Library Form Helper di CodeIgniter 4**, yang digunakan untuk **mempermudah pembuatan form** HTML dengan sintaks PHP yang lebih singkat dan aman (auto-escape, CSRF protection, dll).

---

## 🧰 Materi: Form Helper di CodeIgniter 4

---

### 🔹 1. **Cara Memuat Form Helper**

Form helper tidak otomatis tersedia. Untuk menggunakannya, **muat terlebih dahulu** di controller atau BaseController:

```php
helper('form');
```

Bisa juga banyak sekaligus:
```php
helper(['form', 'url']);
```

---

### 🔹 2. **Fungsi-Fungsi Utama dalam Form Helper**

Berikut adalah daftar fungsi yang sering digunakan:

| Fungsi | Keterangan |
|--------|------------|
| `form_open()` | Membuka tag form `<form>` |
| `form_close()` | Menutup tag form `</form>` |
| `form_input()` | Membuat `<input type="text">` |
| `form_password()` | Membuat `<input type="password">` |
| `form_hidden()` | Membuat input hidden |
| `form_textarea()` | Membuat `<textarea>` |
| `form_dropdown()` | Membuat `<select>` |
| `form_upload()` | Membuat `<input type="file">` |
| `form_submit()` | Membuat `<input type="submit">` |
| `form_button()` | Membuat tombol custom |
| `form_label()` | Membuat `<label>` |

---

### 🔹 3. **Contoh Penggunaan di View**

```php
<?= form_open('user/simpan') ?>

    <?= form_label('Nama', 'nama') ?>
    <?= form_input(['name' => 'nama', 'id' => 'nama', 'value' => old('nama')]) ?>

    <?= form_label('Email', 'email') ?>
    <?= form_input(['name' => 'email', 'type' => 'email', 'id' => 'email']) ?>

    <?= form_label('Keterangan', 'ket') ?>
    <?= form_textarea(['name' => 'ket', 'id' => 'ket']) ?>

    <?= form_submit('submit', 'Simpan') ?>

<?= form_close() ?>
```

---

### 🔹 4. **Contoh Form Dropdown**

```php
$options = [
    'admin' => 'Administrator',
    'editor' => 'Editor',
    'user' => 'User',
];

echo form_dropdown('role', $options, 'editor');
```

---

### 🔹 5. **Form Upload File**

```php
<?= form_open_multipart('upload/do_upload') ?>
    <?= form_upload('berkas') ?>
    <?= form_submit('upload', 'Upload') ?>
<?= form_close() ?>
```

---

### 🔹 6. **Form Hidden dan CSRF**

CI4 otomatis meng-handle CSRF jika kamu mengaktifkannya di `.env`:
```
csrf_protection = true
```

Maka setiap `form_open()` akan otomatis menyisipkan token CSRF.

---

### 🔹 7. **Menampilkan Error Validasi**

Gunakan:
```php
<?= \Config\Services::validation()->getError('nama') ?>
```

Atau untuk semua:
```php
<?= \Config\Services::validation()->listErrors() ?>
```

---

## 🧪 Tips Best Practice

✅ Gunakan `old('field')` untuk tetap menyimpan nilai form setelah validasi gagal.  
✅ Gunakan `esc()` saat mencetak data dari input ke dalam HTML untuk mencegah XSS.  
✅ Untuk Bootstrap, kamu bisa menambahkan class:
```php
form_input(['name' => 'email', 'class' => 'form-control'])
```

---

Kalau kamu mau, aku bisa bantu buatkan **template form full (CRUD)** pakai `form helper` + validasi + Bootstrap. Mau sekalian?