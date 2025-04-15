Berikut contoh penggunaan fungsi-fungsi **membaca file** (Kelompok 2) dalam PHP:

### 2. Membaca File

#### a. `file_get_contents()` - Membaca seluruh file sekaligus
```php
<?php
// Membaca seluruh isi file ke string
$content = file_get_contents('contoh.txt');

if ($content !== false) {
    echo "<pre>" . htmlspecialchars($content) . "</pre>";
} else {
    echo "Gagal membaca file!";
}
?>
```

#### b. `fread()` - Membaca file yang sudah dibuka (binary-safe)
```php
<?php
$file = fopen('gambar.png', 'rb'); // Mode binary read
if ($file) {
    $data = fread($file, filesize('gambar.png'));
    fclose($file);
    
    // Proses data binary (misal: menampilkan gambar)
    header('Content-Type: image/png');
    echo $data;
} else {
    echo "Gagal membuka file!";
}
?>
```

#### c. `fgets()` - Membaca per baris
```php
<?php
$file = fopen('contoh.txt', 'r');
if ($file) {
    echo "<h3>Isi file baris per baris:</h3>";
    $line_number = 1;
    while (!feof($file)) {
        $line = fgets($file);
        echo "Baris $line_number: " . htmlspecialchars($line) . "<br>";
        $line_number++;
    }
    fclose($file);
} else {
    echo "File tidak ditemukan!";
}
?>
```

#### d. `fgetc()` - Membaca per karakter
```php
<?php
$file = fopen('contoh.txt', 'r');
if ($file) {
    echo "<h3>Isi file karakter per karakter:</h3>";
    while (!feof($file)) {
        $char = fgetc($file);
        echo htmlspecialchars($char);
    }
    fclose($file);
} else {
    echo "File tidak ditemukan!";
}
?>
```

#### e. `file()` - Membaca file ke array
```php
<?php
$lines = file('contoh.txt', FILE_IGNORE_NEW_LINES | FILE_SKIP_EMPTY_LINES);
if ($lines !== false) {
    echo "<h3>Isi file sebagai array:</h3>";
    echo "<pre>";
    print_r($lines);
    echo "</pre>";
    
    // Menampilkan dengan nomor baris
    echo "<h3>Daftar Baris:</h3>";
    foreach ($lines as $i => $line) {
        echo ($i+1) . ". " . htmlspecialchars($line) . "<br>";
    }
} else {
    echo "Gagal membaca file!";
}
?>
```

#### f. `readfile()` - Membaca dan output langsung
```php
<?php
// Langsung mengirim isi file ke output
$bytes = readfile('contoh.txt');
echo "<br><br>Total $bytes bytes dibaca.";
?>

<!-- Contoh untuk file download -->
<a href="download.php">Download File</a>
```
File `download.php`:
```php
<?php
header('Content-Type: application/octet-stream');
header('Content-Disposition: attachment; filename="contoh.txt"');
readfile('contoh.txt');
exit;
?>
```

### Perbandingan Fungsi Membaca:
| Fungsi               | Cocok Untuk              | Kelebihan                     | Kekurangan                |
|----------------------|--------------------------|-------------------------------|---------------------------|
| `file_get_contents()`| File kecil, satu operasi | Sederhana, cepat             | Tidak cocok untuk file besar |
| `fread()`            | File binary besar        | Bisa membaca sebagian        | Perlu fopen/fclose        |
| `fgets()`            | File teks per baris      | Hemat memory untuk file besar| Lebih lambat              |
| `file()`             | Butuh array per baris    | Praktis untuk pemrosesan baris| Memakan memory untuk file besar |

Anda bisa memilih fungsi yang sesuai dengan kebutuhan:
- Gunakan `file_get_contents()` untuk file kecil
- Gunakan `fgets()` atau `file()` untuk file teks besar
- Gunakan `fread()` untuk file binary seperti gambar