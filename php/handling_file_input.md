Berikut ini adalah **materi singkat** tentang **handling file upload di PHP native**, cukup untuk jadi bekal awal:

---

## 📂 1. Form HTML untuk Upload File

```html
<form action="upload.php" method="post" enctype="multipart/form-data">
  <label>Pilih file:</label>
  <input type="file" name="fileUpload">
  <input type="submit" value="Upload">
</form>
```

### ⚠️ Penting:
- `enctype="multipart/form-data"` wajib agar file bisa dikirimkan ke server.

---

## 🧠 2. Logika PHP untuk Menangani Upload (`upload.php`)

```php
<?php
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $file = $_FILES['fileUpload'];

    // Cek jika tidak ada error
    if ($file['error'] === 0) {
        $namaFile = basename($file['name']);
        $tujuan = 'uploads/' . $namaFile;

        // Pindahkan file dari temporary ke folder tujuan
        if (move_uploaded_file($file['tmp_name'], $tujuan)) {
            echo "File berhasil diupload ke $tujuan";
        } else {
            echo "Gagal memindahkan file.";
        }
    } else {
        echo "Terjadi error: " . $file['error'];
    }
}
?>
```

---

## 🔐 3. Tips Keamanan Dasar
- Buat folder `uploads` dan beri permission yang sesuai.
- Validasi tipe file dengan `mime_content_type()` atau ekstensi.
- Batasi ukuran file dengan `$_FILES['file']['size']`.
- Hindari menerima file `.php`, `.exe`, dsb. dari user.

Contoh validasi MIME:

```php
$allowedTypes = ['image/jpeg', 'image/png', 'application/pdf'];
$mime = mime_content_type($file['tmp_name']);

if (!in_array($mime, $allowedTypes)) {
    die("Tipe file tidak diizinkan.");
}
```

---

Kalau kamu butuh versi dengan validasi lengkap dan rename otomatis, tinggal bilang aja! Mau upload banyak file juga bisa.