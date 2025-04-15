Berikut contoh penggunaan fungsi **file locking** (Kelompok 8) dalam PHP:

### 8. File Locking dengan `flock()`

#### a. Dasar Penggunaan `flock()`
```php
<?php
$file = fopen("data.txt", "a+") or die("Gagal membuka file!");

// Mengunci file untuk penulisan (LOCK_EX = exclusive lock)
if (flock($file, LOCK_EX)) {
    fwrite($file, "Data baru: " . date('Y-m-d H:i:s') . "\n");
    
    // Buka kunci setelah selesai
    flock($file, LOCK_UN);
} else {
    echo "Gagal mendapatkan lock!";
}

fclose($file);
?>
```

#### b. Locking dengan Timeout
```php
<?php
function writeWithTimeout($filename, $data, $timeout = 5) {
    $file = fopen($filename, "c+");
    if (!$file) return false;
    
    $start = time();
    $locked = false;
    
    // Coba dapatkan lock dengan timeout
    while ((time() - $start) < $timeout) {
        if (flock($file, LOCK_EX | LOCK_NB)) {
            $locked = true;
            break;
        }
        sleep(1); // Tunggu 1 detik sebelum coba lagi
    }
    
    if ($locked) {
        ftruncate($file, 0); // Kosongkan file
        fwrite($file, $data);
        fflush($file);        // Pastikan data ditulis
        flock($file, LOCK_UN);
        fclose($file);
        return true;
    }
    
    fclose($file);
    return false;
}

// Contoh penggunaan
if (writeWithTimeout("log.txt", "Log entry\n")) {
    echo "Berhasil menulis dengan locking";
} else {
    echo "Timeout: Gagal mendapatkan lock";
}
?>
```

#### c. Shared Lock vs Exclusive Lock
```php
<?php
// File 1: Proses membaca (shared lock)
$file = fopen("shared.txt", "r");
if (flock($file, LOCK_SH)) { // Shared lock
    echo "Membaca file:\n";
    echo fread($file, filesize("shared.txt"));
    sleep(3); // Simulasi proses panjang
    flock($file, LOCK_UN);
}
fclose($file);

// File 2: Proses menulis (exclusive lock)
$file = fopen("shared.txt", "a");
if (flock($file, LOCK_EX)) { // Exclusive lock
    echo "Menulis ke file...\n";
    fwrite($file, "Data baru\n");
    sleep(3); // Simulasi proses panjang
    flock($file, LOCK_UN);
}
fclose($file);
?>
```

#### d. Contoh Praktis: Counter yang Thread-Safe
```php
<?php
function incrementCounter() {
    $file = fopen("counter.txt", "c+");
    if (flock($file, LOCK_EX)) {
        $count = (int)fread($file, 20);
        $count++;
        
        ftruncate($file, 0);
        fseek($file, 0);
        fwrite($file, $count);
        
        flock($file, LOCK_UN);
    }
    fclose($file);
    return $count;
}

// Simulasi concurrent access
for ($i = 0; $i < 10; $i++) {
    $pid = pcntl_fork();
    if ($pid == -1) {
        die("Gagal fork");
    } elseif ($pid == 0) {
        // Proses child
        $val = incrementCounter();
        exit();
    }
}

// Tunggu semua proses selesai
while (pcntl_waitpid(0, $status) != -1);

echo "Nilai counter akhir: " . file_get_contents("counter.txt");
?>
```

#### e. Locking untuk File Konfigurasi
```php
<?php
function updateConfig($key, $value) {
    $filename = "config.json";
    $file = fopen($filename, "c+");
    
    if (flock($file, LOCK_EX)) {
        $config = json_decode(fread($file, filesize($filename)), true) ?: [];
        $config[$key] = $value;
        
        ftruncate($file, 0);
        fseek($file, 0);
        fwrite($file, json_encode($config, JSON_PRETTY_PRINT));
        
        flock($file, LOCK_UN);
        fclose($file);
        return true;
    }
    
    fclose($file);
    return false;
}

// Contoh penggunaan
updateConfig("last_updated", date('Y-m-d H:i:s'));
?>
```

#### f. Menghindari Deadlock
```php
<?php
function safeFileUpdate($file1, $file2) {
    // Buka kedua file
    $fp1 = fopen($file1, "a");
    $fp2 = fopen($file2, "a");
    
    // Urutkan lock untuk menghindari deadlock
    if (strcmp($file1, $file2) < 0) {
        $first = $fp1;
        $second = $fp2;
    } else {
        $first = $fp2;
        $second = $fp1;
    }
    
    // Dapatkan lock secara berurutan
    if (flock($first, LOCK_EX)) {
        if (flock($second, LOCK_EX)) {
            // Lakukan operasi file
            fwrite($fp1, "Update file 1\n");
            fwrite($fp2, "Update file 2\n");
            
            flock($second, LOCK_UN);
        }
        flock($first, LOCK_UN);
    }
    
    fclose($fp1);
    fclose($fp2);
}
?>
```

### Jenis Lock pada `flock()`:
| Konstanta     | Deskripsi                                                                 |
|--------------|--------------------------------------------------------------------------|
| `LOCK_SH`    | Shared lock (bisa dibagi dengan proses lain untuk membaca)               |
| `LOCK_EX`    | Exclusive lock (hanya satu proses yang bisa menulis)                     |
| `LOCK_UN`    | Melepaskan lock                                                          |
| `LOCK_NB`    | Non-blocking (digunakan dengan LOCK_SH atau LOCK_EX untuk menghindari blocking) |

### Best Practices:
1. **Selalu lepaskan lock** setelah selesai (`LOCK_UN`)
2. **Gunakan timeout** untuk menghindari blocking tak terbatas
3. **Urutkan lock** ketika bekerja dengan multiple file untuk mencegah deadlock
4. **Jangan bergantung pada lock** untuk sistem terdistribusi (flock() hanya bekerja pada sistem file lokal)
5. **Gunakan `fflush()`** sebelum melepas lock untuk memastikan data sudah ditulis

### Catatan Penting:
- File locking di PHP bersifat **advisory** (hanya bekerja jika semua proses menggunakannya)
- Tidak bekerja pada sistem file NFS atau beberapa filesystem jaringan
- Untuk sistem kritis, pertimbangkan menggunakan database sebagai alternatif

File locking sangat penting untuk:
- Mencegah race condition
- Memastikan konsistensi data
- Aplikasi yang diakses bersamaan (concurrent access)
- Proses batch yang berjalan paralel