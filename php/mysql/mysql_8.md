Mantap, lanjut ke **Nomor 8: Menangani Tipe Data Khusus di MySQL dan PHP** 🧩  
Bagian ini penting kalau kamu bekerja dengan **tanggal**, **file**, **gambar**, atau bahkan **data JSON** di MySQL.

---

## 🔹 8. Menangani Tipe Data Khusus

### Jenis data yang akan kita bahas:
1. **DATE, DATETIME, TIMESTAMP**
2. **BLOB (Binary Large Object)**
3. **JSON** (sejak MySQL 5.7)

---

### 📆 1. Menyimpan dan Mengambil Tanggal (`DATE`, `DATETIME`)

#### 🔸 Simpan tanggal sekarang:

```php
$tanggal = date('Y-m-d'); // format: 2025-04-15
$sql = "INSERT INTO event (judul, tanggal) VALUES ('Ulang Tahun', '$tanggal')";
mysqli_query($koneksi, $sql);
```

#### 🔸 Ambil tanggal dan format ulang:

```php
$row = mysqli_fetch_assoc($result);
$tanggal = date('d-m-Y', strtotime($row['tanggal']));
echo "Tanggal: $tanggal"; // Contoh: 15-04-2025
```

---

### 🖼 2. Menyimpan Gambar/File (`BLOB`)

#### 🔸 Struktur tabel:

```sql
CREATE TABLE gambar (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nama VARCHAR(100),
  data LONGBLOB
);
```

#### 🔸 Upload gambar ke database:

```php
$gambar = addslashes(file_get_contents($_FILES['file']['tmp_name']));
$nama = $_FILES['file']['name'];
$sql = "INSERT INTO gambar (nama, data) VALUES ('$nama', '$gambar')";
mysqli_query($koneksi, $sql);
```

#### 🔸 Menampilkan gambar:

```php
$sql = "SELECT data FROM gambar WHERE id = 1";
$result = mysqli_query($koneksi, $sql);
$row = mysqli_fetch_assoc($result);
header("Content-type: image/jpeg");
echo $row['data'];
```

> ⚠️ Untuk proyek nyata, biasanya file disimpan di folder, dan database hanya menyimpan path-nya.

---

### 🧩 3. Menyimpan Data JSON (MySQL 5.7+)

#### 🔸 Simpan array atau objek JSON:

```php
$data = ['nama' => 'Agus', 'umur' => 25];
$json = json_encode($data);
$sql = "INSERT INTO pengguna (data_json) VALUES ('$json')";
mysqli_query($koneksi, $sql);
```

#### 🔸 Ambil dan decode:

```php
$sql = "SELECT data_json FROM pengguna WHERE id = 1";
$result = mysqli_query($koneksi, $sql);
$row = mysqli_fetch_assoc($result);
$data = json_decode($row['data_json'], true);

echo $data['nama']; // Agus
```

---

### 📝 Tips:
- Gunakan `date()` dan `strtotime()` untuk menangani tanggal dengan PHP.
- `json_encode()` dan `json_decode()` sangat berguna untuk menyimpan struktur data kompleks.
- Untuk menyimpan file besar, lebih baik simpan path ke file, bukan isi filenya langsung.

---

Kalau kamu udah siap, kita lanjut ke **Nomor 9: Transaksi MySQL** — ini penting buat proses data yang harus terjadi secara *atomic* (semuanya berhasil atau gagal). Gas lanjut? 🔄