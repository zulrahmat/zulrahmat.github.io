Berikut contoh penggunaan fungsi **membuka dan menutup file** (Kelompok 1) dalam PHP:

### 1. Membuka dan Menutup File dengan `fopen()` & `fclose()`

```php
<?php
// Membuka file (mode 'r' untuk membaca saja)
$file = fopen("contoh.txt", "r") or die("Gagal membuka file!");

// Lakukan operasi pada file di sini...
echo "File berhasil dibuka.<br>";

// Menutup file
fclose($file);
echo "File telah ditutup.";
?>
```

#### Penjelasan Mode `fopen()`:
- `"r"` - Read (hanya membaca, pointer di awal)
- `"w"` - Write (menulis, membuat file baru/hapus isi jika ada)
- `"a"` - Append (menulis, pointer di akhir file)
- `"x"` - Create (hanya membuat file baru, gagal jika sudah ada)
- `"r+"` - Baca/tulis, pointer di awal
- `"w+"` - Baca/tulis, membuat file baru/hapus isi jika ada
- `"a+"` - Baca/tulis, pointer di akhir file

#### Contoh dengan Error Handling:
```php
<?php
$filename = "data.txt";

// Membuka file dengan pengecekan error
if ($file = fopen($filename, "r")) {
    echo "File berhasil dibuka!<br>";
    
    // Proses file...
    
    fclose($file);
} else {
    echo "Error: Gagal membuka file!";
}
?>
```

#### Contoh Praktis (Membaca isi file):
```php
<?php
$file = fopen("contoh.txt", "r");
if ($file) {
    echo "Isi file:<br>";
    while (!feof($file)) {
        $line = fgets($file);
        echo $line . "<br>";
    }
    fclose($file);
} else {
    echo "File tidak ditemukan!";
}
?>
```

Penting selalu menutup file dengan `fclose()` setelah selesai untuk menghindari memory leak atau lock file yang tidak perlu.