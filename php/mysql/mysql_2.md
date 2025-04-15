Sip, kita lanjut ke **Nomor 2: Eksekusi Query** 🎯

---

## 🔹 2. Eksekusi Query (MySQLi Prosedural)

### ✅ Fungsi yang akan digunakan:
- `mysqli_query()`
- `mysqli_multi_query()` (opsional)
- `mysqli_prepare()` (disinggung, lebih fokus nanti di prepared statements)

---

### 📄 Contoh Query Sederhana: `SELECT`

```php
<?php
// Koneksi ke database
$koneksi = mysqli_connect("localhost", "root", "", "belajar_php");

// Cek koneksi
if (mysqli_connect_errno()) {
    echo "Koneksi gagal: " . mysqli_connect_error();
    exit();
}

// Eksekusi query SELECT
$sql = "SELECT id, nama FROM siswa";
$hasil = mysqli_query($koneksi, $sql);

// Cek apakah query berhasil
if ($hasil) {
    echo "Data siswa:<br>";
    while ($row = mysqli_fetch_assoc($hasil)) {
        echo "ID: " . $row["id"] . " - Nama: " . $row["nama"] . "<br>";
    }
} else {
    echo "Query error: " . mysqli_error($koneksi);
}

// Tutup koneksi
mysqli_close($koneksi);
?>
```

---

### 📄 Contoh Query Sederhana: `INSERT`

```php
<?php
$koneksi = mysqli_connect("localhost", "root", "", "belajar_php");

if (mysqli_connect_errno()) {
    echo "Koneksi gagal: " . mysqli_connect_error();
    exit();
}

$sql = "INSERT INTO siswa (nama) VALUES ('Budi')";
$hasil = mysqli_query($koneksi, $sql);

if ($hasil) {
    echo "Data berhasil ditambahkan!";
} else {
    echo "Gagal tambah data: " . mysqli_error($koneksi);
}

mysqli_close($koneksi);
?>
```

---

### 📄 Contoh: `mysqli_multi_query()` (Beberapa query sekaligus)

```php
<?php
$koneksi = mysqli_connect("localhost", "root", "", "belajar_php");

$sql = "
INSERT INTO siswa (nama) VALUES ('Ani');
INSERT INTO siswa (nama) VALUES ('Tono');
";

if (mysqli_multi_query($koneksi, $sql)) {
    echo "Beberapa data berhasil ditambahkan.";
} else {
    echo "Gagal: " . mysqli_error($koneksi);
}

mysqli_close($koneksi);
?>
```

---

### 📝 Kesimpulan Singkat:
- `mysqli_query()` untuk query biasa (SELECT, INSERT, UPDATE, DELETE).
- `mysqli_multi_query()` bisa eksekusi beberapa query sekaligus, tapi hati-hati untuk keamanan.
- `mysqli_error()` bantu debug kalau query gagal.

---

Kalau sudah paham, kita lanjut ke **Nomor 3: Mengambil Data (Result Handling)**? Di situ kita bahas fungsi seperti `mysqli_fetch_assoc()`, `mysqli_fetch_array()`, dll. Mau lanjut?