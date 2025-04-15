Siap! Kita mulai dari **Nomor 1: Koneksi & Penutupan** dulu. Ini adalah dasar sebelum kamu bisa pakai fungsi MySQL lainnya.

---

## 🔹 1. Koneksi & Penutupan (MySQLi Prosedural)

### ✅ Fungsi yang akan kita gunakan:
- `mysqli_connect()`
- `mysqli_connect_errno()`
- `mysqli_connect_error()`
- `mysqli_close()`

---

### 📄 Contoh Kode Sederhana

```php
<?php
// Informasi koneksi
$host     = "localhost";
$username = "root";
$password = "";
$database = "belajar_php";

// Membuat koneksi
$koneksi = mysqli_connect($host, $username, $password, $database);

// Cek koneksi
if (mysqli_connect_errno()) {
    echo "Gagal koneksi ke MySQL: " . mysqli_connect_error();
    exit(); // Hentikan skrip kalau gagal koneksi
} else {
    echo "Koneksi berhasil ke database!";
}

// Tutup koneksi
mysqli_close($koneksi);
?>
```

---

### 📝 Penjelasan Singkat:
- `mysqli_connect(...)` → membuat koneksi ke MySQL.
- `mysqli_connect_errno()` → jika ada error, fungsi ini return kode error.
- `mysqli_connect_error()` → ambil pesan error-nya.
- `mysqli_close(...)` → menutup koneksi ke database.

---

Kalau sudah paham bagian ini, selanjutnya kita bisa lanjut ke **Nomor 2: Eksekusi Query** (misalnya SELECT atau INSERT). Lanjut?