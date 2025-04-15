Berikut contoh penggunaan fungsi-fungsi **menulis ke file** (Kelompok 3) dalam PHP:

### 3. Menulis ke File

#### a. `file_put_contents()` - Menulis sederhana dalam satu langkah
```php
<?php
// Menulis string ke file (jika file tidak ada akan dibuat)
$data = "Ini adalah contoh teks yang akan ditulis ke file\nBaris kedua";
$bytes = file_put_contents('output.txt', $data);

if ($bytes !== false) {
    echo "Berhasil menulis $bytes bytes ke file";
} else {
    echo "Gagal menulis file!";
}

// Menambahkan konten (dengan flag FILE_APPEND)
$additionalData = "\nData tambahan yang diappend";
file_put_contents('output.txt', $additionalData, FILE_APPEND);
?>
```

#### b. `fwrite()` - Menulis ke file yang sudah dibuka
```php
<?php
// Membuka file untuk ditulis (mode 'w')
$file = fopen('output_fwrite.txt', 'w') or die("Gagal membuat file!");

// Menulis beberapa data
fwrite($file, "Baris pertama\n");
fwrite($file, "Baris kedua\n");

// Menulis array ke file
$dataArray = ["Nama: John Doe\n", "Email: john@example.com\n", "Telepon: 123456789\n"];
foreach ($dataArray as $line) {
    fwrite($file, $line);
}

fclose($file);
echo "File berhasil ditulis!";
?>
```

#### c. Contoh lengkap dengan error handling
```php
<?php
$filename = 'data_log.txt';
$logData = date('Y-m-d H:i:s') . " - User login\n";

try {
    // Membuka file dalam mode append
    if ($file = fopen($filename, 'a')) {
        if (fwrite($file, $logData) === false) {
            throw new Exception("Gagal menulis ke file!");
        }
        fclose($file);
        echo "Log berhasil disimpan";
    } else {
        throw new Exception("Gagal membuka file!");
    }
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
?>
```

#### d. Menulis file CSV
```php
<?php
$csvData = [
    ['Nama', 'Email', 'Telepon'],
    ['John Doe', 'john@example.com', '123456789'],
    ['Jane Smith', 'jane@example.com', '987654321']
];

$file = fopen('data.csv', 'w');
if ($file) {
    foreach ($csvData as $row) {
        fputcsv($file, $row); // Fungsi khusus untuk CSV
    }
    fclose($file);
    echo "File CSV berhasil dibuat!";
} else {
    echo "Gagal membuat file CSV!";
}
?>
```

#### e. Perbandingan `file_put_contents()` vs `fwrite()`

| Fitur                | `file_put_contents()`              | `fwrite()`                      |
|----------------------|------------------------------------|---------------------------------|
| Kemudahan            | Lebih sederhana                    | Membutuhkan fopen/fclose        |
| Performa             | Cepat untuk operasi tunggal        | Lebih efisien untuk operasi berulang |
| Fleksibilitas        | Terbatas                           | Lebih fleksibel                 |
| Append data          | Butuh flag FILE_APPEND             | Tergantung mode fopen           |
| Cocok untuk          | Penulisan sekali/sederhana         | Operasi file kompleks/berulang |

#### f. Contoh praktis: Logger sederhana
```php
<?php
function logMessage($message) {
    $logFile = 'app.log';
    $timestamp = date('[Y-m-d H:i:s]');
    $logMessage = $timestamp . ' ' . $message . PHP_EOL;
    
    // Gunakan FILE_APPEND untuk menambahkan ke file yang ada
    file_put_contents($logFile, $logMessage, FILE_APPEND | LOCK_EX);
}

// Contoh penggunaan
logMessage("Aplikasi dimulai");
logMessage("User login: john_doe");
logMessage("Error: Koneksi database gagal");
?>
```

Tips penting:
1. Selalu verifikasi izin direktori/file
2. Gunakan mode yang tepat:
   - `w` - Timpa file yang ada
   - `a` - Tambahkan ke akhir file
   - `x` - Hanya buat file baru (gagal jika file sudah ada)
3. Untuk file penting, gunakan `LOCK_EX` untuk mencegah konflik penulisan
4. Untuk data besar, gunakan `fwrite()` dengan chunk data

Pilih `file_put_contents()` untuk operasi sederhana, dan `fwrite()` untuk operasi file yang lebih kompleks atau berulang.