Mantap! Sekarang kita masuk ke bagian yang sangat penting untuk **keamanan database**, yaitu:

---

## 🔹 4. Prepared Statements (MySQLi Prosedural)

Prepared statements melindungi dari **SQL Injection**, dan bagus dipakai saat input berasal dari user (form, API, dll).

### ✅ Fungsi yang akan digunakan:
| Fungsi | Deskripsi |
|--------|-----------|
| `mysqli_prepare()` | Mempersiapkan query SQL |
| `mysqli_stmt_bind_param()` | Mengikat parameter ke query |
| `mysqli_stmt_execute()` | Menjalankan query |
| `mysqli_stmt_get_result()` | Mengambil hasil SELECT |
| `mysqli_stmt_fetch()` | Ambil data (kalau tidak pakai `get_result`) |
| `mysqli_stmt_close()` | Menutup statement |

---

### 📄 Contoh Prepared Statement: `INSERT`

```php
<?php
$koneksi = mysqli_connect("localhost", "root", "", "belajar_php");

if (mysqli_connect_errno()) {
    echo "Koneksi gagal: " . mysqli_connect_error();
    exit();
}

// Query dengan placeholder ?
$sql = "INSERT INTO siswa (nama) VALUES (?)";

// Persiapkan statement
$stmt = mysqli_prepare($koneksi, $sql);

// Bind parameter ke statement
// s = string (tipe data untuk parameter)
mysqli_stmt_bind_param($stmt, "s", $nama);

// Isi variabel dan eksekusi
$nama = "Dewi";
mysqli_stmt_execute($stmt);

echo "Data berhasil ditambahkan.";

// Tutup statement
mysqli_stmt_close($stmt);
mysqli_close($koneksi);
?>
```

---

### 📄 Contoh Prepared Statement: `SELECT`

```php
<?php
$koneksi = mysqli_connect("localhost", "root", "", "belajar_php");

$sql = "SELECT id, nama FROM siswa WHERE nama = ?";

// Siapkan statement
$stmt = mysqli_prepare($koneksi, $sql);

// Bind parameter
mysqli_stmt_bind_param($stmt, "s", $nama);

// Nilai yang akan dicari
$nama = "Dewi";

// Eksekusi statement
mysqli_stmt_execute($stmt);

// Ambil hasil
$hasil = mysqli_stmt_get_result($stmt);

// Tampilkan hasil
while ($row = mysqli_fetch_assoc($hasil)) {
    echo "ID: {$row['id']} - Nama: {$row['nama']}<br>";
}

mysqli_stmt_close($stmt);
mysqli_close($koneksi);
?>
```

---

### 📝 Catatan:
- `"s"` dalam `bind_param()` artinya parameter adalah **string**. Format:
  - `"i"` = integer
  - `"d"` = double
  - `"s"` = string
  - `"b"` = blob
- Kamu **tidak perlu escape string** manual, karena prepared statements sudah otomatis aman.

---

Kalau kamu sudah paham prepared statement ini, kita lanjut ke **Nomor 5: Insert, Update, Delete** (cek baris yang terpengaruh & ambil ID terakhir). Mau gas lanjut? 😎