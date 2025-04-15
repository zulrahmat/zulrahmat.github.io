Oke, lanjut ke **Nomor 5: Insert, Update, Delete (DML – Data Manipulation Language)** ⚙️

Di bagian ini kita akan fokus ke:
- Menjalankan perintah `INSERT`, `UPDATE`, `DELETE`
- Mengecek apakah ada baris yang terpengaruh
- Mengambil ID data terakhir yang dimasukkan (auto increment)

---

## 🔹 5. Fungsi Terkait DML

| Fungsi | Deskripsi |
|--------|-----------|
| `mysqli_query()` | Jalankan perintah DML biasa |
| `mysqli_affected_rows()` | Cek jumlah baris yang terpengaruh |
| `mysqli_insert_id()` | Ambil ID terakhir setelah `INSERT` |

---

### 📄 Contoh `INSERT` + ambil ID terakhir

```php
<?php
$koneksi = mysqli_connect("localhost", "root", "", "belajar_php");

$sql = "INSERT INTO siswa (nama) VALUES ('Agus')";
mysqli_query($koneksi, $sql);

// Ambil ID terakhir (jika auto_increment)
$id_baru = mysqli_insert_id($koneksi);

echo "Data berhasil ditambahkan. ID baru: " . $id_baru;

mysqli_close($koneksi);
?>
```

---

### 📄 Contoh `UPDATE` + cek baris yang diubah

```php
<?php
$koneksi = mysqli_connect("localhost", "root", "", "belajar_php");

$sql = "UPDATE siswa SET nama = 'Agus Update' WHERE id = 1";
mysqli_query($koneksi, $sql);

// Cek berapa baris yang diubah
$terpengaruh = mysqli_affected_rows($koneksi);

echo "Baris yang diubah: $terpengaruh";

mysqli_close($koneksi);
?>
```

---

### 📄 Contoh `DELETE` + cek baris yang dihapus

```php
<?php
$koneksi = mysqli_connect("localhost", "root", "", "belajar_php");

$sql = "DELETE FROM siswa WHERE id = 2";
mysqli_query($koneksi, $sql);

// Cek baris yang terhapus
$hapus = mysqli_affected_rows($koneksi);

echo "Baris yang dihapus: $hapus";

mysqli_close($koneksi);
?>
```

---

### 📝 Catatan Penting:
- **`mysqli_insert_id()`** → hanya bekerja untuk table dengan kolom auto_increment.
- **`mysqli_affected_rows()`** → bisa dipakai setelah `INSERT`, `UPDATE`, atau `DELETE` untuk tahu apakah query berhasil mempengaruhi data.

---

Kalau bagian ini sudah clear, kita lanjut ke **Nomor 6: Error Handling** — buat tahu bagaimana caranya mendeteksi dan menangani error di MySQL. Siap lanjut?