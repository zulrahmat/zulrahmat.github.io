Sip, lanjut ke **Nomor 6: Error Handling di MySQL dan PHP** ⚠️  
Bagian ini penting banget buat debugging dan bikin aplikasi kamu lebih stabil.

---

## 🔹 6. Error Handling

### ✅ Fungsi-fungsi utama:
| Fungsi | Deskripsi |
|--------|-----------|
| `mysqli_connect_error()` | Menampilkan pesan error saat koneksi gagal |
| `mysqli_connect_errno()` | Menampilkan kode error koneksi |
| `mysqli_error()` | Menampilkan pesan error dari query |
| `mysqli_errno()` | Menampilkan kode error dari query |

---

### 📄 Contoh Menangani Error Koneksi

```php
<?php
$koneksi = mysqli_connect("localhost", "root", "", "salah_nama_db");

if (mysqli_connect_errno()) {
    echo "Koneksi gagal: " . mysqli_connect_error();
    exit();
}

echo "Koneksi berhasil.";
mysqli_close($koneksi);
?>
```

### Output:
```
Koneksi gagal: Unknown database 'salah_nama_db'
```

---

### 📄 Contoh Menangani Error Query

```php
<?php
$koneksi = mysqli_connect("localhost", "root", "", "belajar_php");

$sql = "SELEC * FROM siswa"; // Salah ketik: "SELECT"
$hasil = mysqli_query($koneksi, $sql);

if (!$hasil) {
    echo "Terjadi kesalahan: " . mysqli_error($koneksi);
} else {
    echo "Query berhasil.";
}

mysqli_close($koneksi);
?>
```

### Output:
```
Terjadi kesalahan: You have an error in your SQL syntax...
```

---

### 📄 Bonus: Tampilkan Kode Error

```php
<?php
$koneksi = mysqli_connect("localhost", "root", "", "belajar_php");

$sql = "SELECT * FROM tidak_ada_table";
$hasil = mysqli_query($koneksi, $sql);

if (!$hasil) {
    echo "Kode error: " . mysqli_errno($koneksi) . "<br>";
    echo "Pesan error: " . mysqli_error($koneksi);
}

mysqli_close($koneksi);
?>
```

---

### 🛠 Tips:
- Selalu periksa koneksi dan hasil query.
- Hindari langsung menampilkan error ke user di produksi (gunakan log).
- Untuk aplikasi besar, gunakan try-catch (di `PDO`) atau log ke file.

---

Kalau error handling ini sudah kamu kuasai, kita bisa lanjut ke **Nomor 7: Escape dan Keamanan** – yaitu bagaimana melindungi data input dari serangan seperti SQL Injection jika belum pakai prepared statement. Mau lanjut bro?