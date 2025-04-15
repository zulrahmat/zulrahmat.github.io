Oke, lanjut ke **Nomor 3: Mengambil Data (Result Handling)** 📦

Bagian ini penting banget buat menampilkan data hasil query `SELECT`.

---

## 🔹 3. Mengambil Data dari Result

### ✅ Fungsi yang akan digunakan:
| Fungsi | Deskripsi |
|--------|-----------|
| `mysqli_fetch_assoc()` | Hasil sebagai array asosiatif (`$row['kolom']`) |
| `mysqli_fetch_row()` | Hasil sebagai array numerik (`$row[0]`) |
| `mysqli_fetch_array()` | Gabungan assoc + numerik |
| `mysqli_fetch_object()` | Hasil sebagai objek (`$row->kolom`) |
| `mysqli_num_rows()` | Hitung jumlah baris hasil |
| `mysqli_free_result()` | Bebaskan memori dari result |

---

### 📄 Contoh Lengkap

```php
<?php
$koneksi = mysqli_connect("localhost", "root", "", "belajar_php");

if (mysqli_connect_errno()) {
    echo "Koneksi gagal: " . mysqli_connect_error();
    exit();
}

// Query SELECT
$sql = "SELECT id, nama FROM siswa";
$hasil = mysqli_query($koneksi, $sql);

// Cek jumlah baris
$jumlah = mysqli_num_rows($hasil);
echo "Jumlah data: $jumlah<br><br>";

// Tampilkan data pakai mysqli_fetch_assoc()
echo "📌 Pakai fetch_assoc():<br>";
while ($row = mysqli_fetch_assoc($hasil)) {
    echo "ID: " . $row["id"] . " - Nama: " . $row["nama"] . "<br>";
}

// Kembalikan pointer ke awal hasil untuk dicoba ulang
mysqli_data_seek($hasil, 0);

// Tampilkan data pakai mysqli_fetch_row()
echo "<br>📌 Pakai fetch_row():<br>";
while ($row = mysqli_fetch_row($hasil)) {
    echo "ID: $row[0] - Nama: $row[1]<br>";
}

// Kembalikan pointer ke awal lagi
mysqli_data_seek($hasil, 0);

// Tampilkan data pakai mysqli_fetch_object()
echo "<br>📌 Pakai fetch_object():<br>";
while ($row = mysqli_fetch_object($hasil)) {
    echo "ID: {$row->id} - Nama: {$row->nama}<br>";
}

// Bebaskan hasil
mysqli_free_result($hasil);

// Tutup koneksi
mysqli_close($koneksi);
?>
```

---

### 📝 Penjelasan Singkat:
- **`mysqli_fetch_assoc()`** – Array asosiatif (`$row['nama']`)
- **`mysqli_fetch_row()`** – Array numerik (`$row[0]`)
- **`mysqli_fetch_object()`** – Objek (`$row->nama`)
- **`mysqli_num_rows()`** – Hitung berapa baris hasilnya
- **`mysqli_free_result()`** – Bebaskan resource dari hasil query
- **`mysqli_data_seek()`** – Geser pointer result ke posisi tertentu (misal ulangi dari awal)

---

Kalau kamu sudah paham bagian ini, kita bisa lanjut ke **Nomor 4: Prepared Statements**, biar kamu bisa bikin query yang lebih aman (anti SQL injection). Mau lanjut sekarang?