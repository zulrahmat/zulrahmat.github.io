Tentu! Berikut ini adalah **materi lengkap tentang Library File Uploads di CodeIgniter 4**, yang sangat berguna ketika kamu ingin membuat fitur seperti **upload gambar, dokumen, atau file lainnya** di aplikasi kamu.

---

## 📂 Materi: File Uploads di CodeIgniter 4

---

### 🔹 1. **Struktur Form Upload**

Agar bisa mengupload file, form kamu **harus menggunakan `enctype="multipart/form-data"`**. Gunakan `form_open_multipart()` dari form helper:

```php
<?= form_open_multipart('upload/simpan') ?>
    <input type="file" name="berkas">
    <button type="submit">Upload</button>
<?= form_close() ?>
```

---

### 🔹 2. **Mengambil File di Controller**

Gunakan method `getFile()` dari `$this->request`:

```php
$file = $this->request->getFile('berkas');
```

---

### 🔹 3. **Validasi dan Penyimpanan File**

Contoh upload dan simpan file:

```php
public function simpan()
{
    $file = $this->request->getFile('berkas');

    if ($file->isValid() && !$file->hasMoved()) {
        // Simpan dengan nama asli
        $file->move(WRITEPATH . 'uploads');

        echo "File berhasil diupload!";
    } else {
        echo "Upload gagal.";
    }
}
```

> 📝 `WRITEPATH` biasanya menunjuk ke folder `writable/`. Kamu bisa ganti dengan `FCPATH . 'uploads'` jika ingin simpan ke public folder.

---

### 🔹 4. **Custom Nama File Upload**

```php
$newName = $file->getRandomName(); // random, aman untuk nama file
$file->move(WRITEPATH . 'uploads', $newName);
```

---

### 🔹 5. **Mengecek Informasi File**

```php
echo $file->getName();      // nama asli
echo $file->getSize();      // ukuran dalam bytes
echo $file->getClientMimeType(); // tipe MIME
```

---

### 🔹 6. **Validasi Upload via Rules**

Di `Controller`, kamu bisa pakai validasi bawaan:

```php
$validationRule = [
    'berkas' => [
        'label' => 'File',
        'rules' => 'uploaded[berkas]|mime_in[berkas,image/png,image/jpg,image/jpeg]|max_size[berkas,2048]',
    ],
];

if (!$this->validate($validationRule)) {
    return redirect()->back()->withInput()->with('errors', $this->validator->getErrors());
}
```

---

## 📁 Struktur Folder Upload

Sebaiknya simpan file ke dalam folder `writable/uploads/` atau `public/uploads/` tergantung keperluan kamu:

- `writable/uploads/`: tidak bisa diakses langsung oleh user (lebih aman)
- `public/uploads/`: bisa diakses langsung (untuk gambar, dsb)

Buat folder secara manual jika belum ada.

---

## 🧪 Tips Best Practice

✅ Gunakan `getRandomName()` untuk menghindari nama file bentrok  
✅ Validasi mime type agar tidak upload file berbahaya  
✅ Batasi ukuran file  
✅ Gunakan folder `writable/` untuk menyimpan file sensitif  
✅ Tambahkan logika hapus file jika diperlukan

---

## 📘 Dokumentasi Resmi

- [File Uploading - CodeIgniter 4 User Guide](https://codeigniter.com/user_guide/libraries/uploaded_files.html)

---

Kalau kamu mau, aku bisa bantu buatin **template form upload + controller lengkap + validasi**. Mau sekalian?