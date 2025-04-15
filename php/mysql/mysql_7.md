Lanjut! Sekarang kita bahas **Nomor 7: Escape dan Keamanan Input** 🔐  
Ini penting banget buat mencegah **SQL Injection**, terutama kalau kamu belum pakai *prepared statement*.

---

## 🔹 7. Escape & Keamanan Input

### ✅ Fungsi utama:
| Fungsi | Deskripsi |
|--------|-----------|
| `mysqli_real_escape_string()` | Meloloskan karakter spesial dalam input string |
| `htmlspecialchars()` | Meloloskan karakter HTML agar aman ditampilkan di browser |
| `strip_tags()` | Menghapus semua tag HTML dari input |

---

### 📄 Contoh: Input dari Form Tanpa Prepared Statement

```php
<?php
$koneksi = mysqli_connect("localhost", "root", "", "belajar_php");

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // 1. Ambil input
    $nama = $_POST['nama'];

    // 2. Escape agar aman dari SQL Injection
    $nama_aman = mysqli_real_escape_string($koneksi, $nama);

    // 3. Buat query
    $sql = "INSERT INTO siswa (nama) VALUES ('$nama_aman')";

    if (mysqli_query($koneksi, $sql)) {
        echo "Data berhasil disimpan!";
    } else {
        echo "Error: " . mysqli_error($koneksi);
    }

    mysqli_close($koneksi);
}
?>

<form method="post">
    Nama: <input type="text" name="nama">
    <button type="submit">Simpan</button>
</form>
```

---

### 📄 Contoh: Menampilkan Data Aman di HTML

```php
<?php
$nama = "<script>alert('xss!')</script>";
echo "Nama: " . htmlspecialchars($nama); // Aman dari XSS
?>
```

---

### 📄 Kombinasi Perlindungan Input

```php
$input = $_POST['komentar'] ?? '';
$input = strip_tags($input);                    // Hapus tag HTML
$input = htmlspecialchars($input);              // Escape karakter HTML
$input = mysqli_real_escape_string($koneksi, $input); // Escape SQL

$sql = "INSERT INTO komentar (isi) VALUES ('$input')";
```

---

### 📝 Tips Keamanan:
- **Gunakan Prepared Statements** untuk keamanan terbaik.
- Gunakan `mysqli_real_escape_string()` hanya jika kamu **tidak** pakai prepared.
- Untuk output ke **HTML**, selalu gunakan `htmlspecialchars()`.
- Gunakan `strip_tags()` kalau input tidak boleh mengandung HTML sama sekali.

---

Kalau sudah beres bagian ini, kita lanjut ke **Nomor 8: Menangani Tipe Data Khusus**, seperti tanggal, waktu, BLOB (gambar/file), dan JSON. Mau lanjut sekarang? 🧭