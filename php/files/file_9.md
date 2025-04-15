Berikut contoh penggunaan fungsi-fungsi **pointer file** (Kelompok 9) dalam PHP:

### 9. Pointer File

#### a. `ftell()` - Mendapatkan posisi pointer
```php
<?php
$file = fopen("data.txt", "r");
fseek($file, 10); // Pindah ke posisi ke-10
echo "Posisi pointer: " . ftell($file); // Output: 10
fclose($file);
?>
```

#### b. `fseek()` - Memindahkan pointer file
```php
<?php
$file = fopen("largefile.bin", "rb");

// Pindah ke posisi 100 byte dari awal
fseek($file, 100, SEEK_SET);
echo "Posisi: " . ftell($file); // 100

// Pindah 50 byte dari posisi saat ini
fseek($file, 50, SEEK_CUR);
echo "Posisi: " . ftell($file); // 150

// Pindah ke 20 byte sebelum akhir file
fseek($file, -20, SEEK_END);
echo "Posisi: " . ftell($file); // (ukuran_file - 20)
fclose($file);
?>
```

#### c. `rewind()` - Mengembalikan pointer ke awal
```php
<?php
$file = fopen("data.txt", "r+");

// Tulis data
fwrite($file, "Hello");

// Kembalikan pointer ke awal
rewind($file);

// Baca isi file
echo fread($file, 5); // Output: Hello
fclose($file);
?>
```

#### d. Contoh praktis: Membaca bagian tertentu dari file besar
```php
<?php
function readChunk($filename, $start, $length) {
    $file = fopen($filename, "rb");
    fseek($file, $start, SEEK_SET);
    $data = fread($file, $length);
    fclose($file);
    return $data;
}

// Membaca 100 byte mulai dari posisi 500
$chunk = readChunk("large_video.mp4", 500, 100);
?>
```

#### e. Contoh praktis: Parsing file CSV secara efisien
```php
<?php
function parseLargeCSV($filename) {
    $file = fopen($filename, "r");
    $headers = fgetcsv($file);
    $data = [];
    
    while (!feof($file)) {
        $position = ftell($file); // Simpan posisi sebelum membaca
        $row = fgetcsv($file);
        
        if ($row && count($row) === count($headers)) {
            $data[] = array_combine($headers, $row);
        } else {
            // Jika format salah, kembali ke posisi semula
            fseek($file, $position);
            break;
        }
    }
    
    fclose($file);
    return $data;
}
?>
```

#### f. Contoh praktis: Multi-proses membaca file besar
```php
<?php
function processFileChunk($filename, $chunkSize, $callback) {
    $file = fopen($filename, "rb");
    $size = filesize($filename);
    
    for ($offset = 0; $offset < $size; $offset += $chunkSize) {
        fseek($file, $offset);
        $data = fread($file, $chunkSize);
        $callback($data, $offset);
    }
    
    fclose($file);
}

// Contoh penggunaan
processFileChunk("huge_log.txt", 8192, function($chunk, $offset) {
    echo "Memproses chunk di offset $offset\n";
    // Proses setiap chunk
});
?>
```

#### g. Konstanta Seek Mode:
| Konstanta     | Nilai | Deskripsi                          |
|--------------|-------|-----------------------------------|
| `SEEK_SET`   | 0     | Posisi absolut dalam file         |
| `SEEK_CUR`   | 1     | Relatif terhadap posisi saat ini  |
| `SEEK_END`   | 2     | Relatif terhadap akhir file       |

#### h. Contoh error handling:
```php
<?php
$file = fopen("data.bin", "rb");

try {
    if (fseek($file, 1000, SEEK_SET) === -1) {
        throw new Exception("Gagal memindahkan pointer");
    }
    
    $data = fread($file, 100);
    if ($data === false) {
        throw new Exception("Gagal membaca data");
    }
    
    // Proses data
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
} finally {
    fclose($file);
}
?>
```

### Best Practices:
1. **Gunakan mode binary** ('rb', 'wb', dll) untuk operasi pointer yang presisi
2. **Selalu tutup file** setelah operasi selesai
3. **Verifikasi operasi** fseek dengan memeriksa return value
4. **Hindari SEEK_END** untuk file yang sedang ditulis oleh proses lain
5. **Gunakan ftell()** untuk debugging posisi pointer

### Kasus Penggunaan:
1. **Parsing file besar** tanpa memuat seluruhnya ke memory
2. **Membaca struktur data biner** dengan format tertentu
3. **Memproses file log** secara efisien
4. **Implementasi pagination** untuk file besar
5. **Random access** ke bagian tertentu dari file

Pointer file sangat penting untuk:
- Efisiensi memory saat memproses file besar
- Operasi file yang membutuhkan akses acak
- Manipulasi data biner
- Operasi file yang kompleks dan spesifik