Berikut contoh penggunaan fungsi-fungsi **navigasi direktori** (Kelompok 6) dalam PHP:

### 6. Navigasi Direktori

#### a. `scandir()` - Mendaftar isi direktori
```php
<?php
$directory = 'project';

// Mendapatkan semua file dan folder
$items = scandir($directory);

echo "<h3>Isi direktori '$directory':</h3>";
echo "<ul>";
foreach ($items as $item) {
    if ($item != '.' && $item != '..') {
        $path = $directory . '/' . $item;
        $type = is_dir($path) ? '📁 Directory' : '📄 File';
        echo "<li>$type: $item</li>";
    }
}
echo "</ul>";

// Dengan sorting descending
$itemsSorted = scandir($directory, SCANDIR_SORT_DESCENDING);
?>
```

#### b. `glob()` - Mencari file dengan pola
```php
<?php
// Mencari semua file PHP
$phpFiles = glob('*.php');
echo "<h3>File PHP:</h3>";
print_r($phpFiles);

// Mencari semua file gambar
$images = glob('images/*.{jpg,png,gif}', GLOB_BRACE);
echo "<h3>File Gambar:</h3>";
foreach ($images as $image) {
    echo "<img src='$image' height='100' style='margin:5px'>";
}

// Mencari file secara rekursif (PHP 7+)
$allPhpFiles = glob('**/*.php', GLOB_BRACE | GLOB_NOSORT | GLOB_RECUR);
?>
```

#### c. `opendir()`, `readdir()`, `closedir()` - Browsing direktori manual
```php
<?php
$dir = opendir('uploads');

echo "<h3>File di folder uploads:</h3>";
echo "<ul>";
while (($file = readdir($dir)) !== false) {
    if ($file != '.' && $file != '..') {
        $filePath = 'uploads/' . $file;
        $size = is_dir($filePath) ? '' : ' (' . filesize($filePath) . ' bytes)';
        echo "<li>" . htmlspecialchars($file) . $size . "</li>";
    }
}
closedir($dir);
echo "</ul>";
?>
```

#### d. `chdir()` dan `getcwd()` - Mengubah dan mendapatkan direktori kerja
```php
<?php
// Menyimpan direktori kerja saat ini
$originalDir = getcwd();

echo "Direktori awal: " . $originalDir . "<br>";

// Pindah ke direktori lain
chdir('subfolder');
echo "Direktori sekarang: " . getcwd() . "<br>";

// Kembali ke direktori awal
chdir($originalDir);
echo "Direktori setelah kembali: " . getcwd() . "<br>";

// Contoh praktis
function processFilesInDirectory($dir) {
    $oldDir = getcwd();
    chdir($dir);
    
    $results = [];
    foreach (glob('*.txt') as $file) {
        $results[$file] = filesize($file);
    }
    
    chdir($oldDir);
    return $results;
}
?>
```

#### e. Contoh praktis: Recursive Directory Iterator
```php
<?php
function listFilesRecursively($dir) {
    $iterator = new RecursiveIteratorIterator(
        new RecursiveDirectoryIterator($dir, RecursiveDirectoryIterator::SKIP_DOTS),
        RecursiveIteratorIterator::SELF_FIRST
    );
    
    echo "<h3>Struktur folder $dir:</h3>";
    echo "<ul>";
    foreach ($iterator as $item) {
        $indent = str_repeat('&nbsp;&nbsp;', $iterator->getDepth());
        if ($item->isDir()) {
            echo "<li>📁 {$indent}{$item->getFilename()}</li>";
        } else {
            $size = $item->getSize();
            echo "<li>📄 {$indent}{$item->getFilename()} ($size bytes)</li>";
        }
    }
    echo "</ul>";
}

listFilesRecursively('project');
?>
```

#### f. Contoh praktis: Menghitung ukuran direktori
```php
<?php
function directorySize($path) {
    $totalSize = 0;
    $files = scandir($path);
    
    foreach ($files as $file) {
        if ($file != '.' && $file != '..') {
            $filePath = $path . '/' . $file;
            if (is_dir($filePath)) {
                $totalSize += directorySize($filePath);
            } else {
                $totalSize += filesize($filePath);
            }
        }
    }
    
    return $totalSize;
}

$dir = 'downloads';
$size = directorySize($dir);
echo "Total ukuran folder $dir: " . formatSizeUnits($size);

// Helper function dari contoh sebelumnya
function formatSizeUnits($bytes) {
    // ... sama seperti sebelumnya ...
}
?>
```

#### g. Contoh praktis: Membersihkan folder cache
```php
<?php
function clearCache($cacheDir, $maxAgeHours = 24) {
    if (!is_dir($cacheDir)) return false;
    
    $files = glob($cacheDir . '/*');
    $now = time();
    $deleted = 0;
    
    foreach ($files as $file) {
        if (is_file($file)) {
            $fileTime = filemtime($file);
            if ($now - $fileTime > $maxAgeHours * 3600) {
                unlink($file);
                $deleted++;
            }
        }
    }
    
    return $deleted;
}

$cleaned = clearCache('tmp/cache', 2);
echo "Berhasil menghapus $cleaned file cache yang kedaluwarsa";
?>
```

#### h. Contoh praktis: Mencari file duplikat
```php
<?php
function findDuplicateFiles($dir) {
    $fileHashes = [];
    $duplicates = [];
    
    $iterator = new RecursiveIteratorIterator(
        new RecursiveDirectoryIterator($dir, RecursiveDirectoryIterator::SKIP_DOTS)
    );
    
    foreach ($iterator as $file) {
        if ($file->isFile()) {
            $hash = md5_file($file->getPathname());
            if (isset($fileHashes[$hash])) {
                $duplicates[$hash][] = $file->getPathname();
            } else {
                $fileHashes[$hash] = [$file->getPathname()];
            }
        }
    }
    
    // Hanya kembalikan yang benar-benar duplikat
    return array_filter($duplicates, function($files) {
        return count($files) > 1;
    });
}

$duplicates = findDuplicateFiles('documents');
echo "<h3>File duplikat ditemukan:</h3>";
foreach ($duplicates as $hash => $files) {
    echo "<p>Hash: $hash<br>";
    echo implode("<br>", $files) . "</p>";
}
?>
```

### Perbandingan Fungsi Navigasi Direktori:
| Fungsi/Method               | Kelebihan                              | Kekurangan                     |
|----------------------------|---------------------------------------|--------------------------------|
| `scandir()`                | Sederhana, cepat                      | Tidak rekursif                |
| `glob()`                   | Support pattern matching              | Tidak rekursif (kecuali flag) |
| `opendir()/readdir()`      | Kontrol lebih granular                | Lebih verbose                 |
| `RecursiveIteratorIterator`| Rekursif, OOP approach                | Lebih kompleks               |
| `chdir()/getcwd()`         | Memungkinkan perubahan konteks        | Perlu mengembalikan state     |

### Tips Penting:
1. Gunakan `SKIP_DOTS` (`scandir()` atau `DirectoryIterator`) untuk menghindari '.' dan '..'
2. Untuk operasi rekursif, pertimbangkan menggunakan `RecursiveDirectoryIterator`
3. Selalu verifikasi direktori ada dan dapat diakses sebelum operasi
4. Gunakan `realpath()` untuk memastikan path yang valid
5. Untuk aplikasi produksi, tambahkan error handling untuk permission issues

Fungsi-fungsi navigasi direktori sangat berguna untuk:
- Membangun file browser
- Membuat sistem backup
- Manajemen file upload
- Pembersihan file otomatis
- Analisis penyimpanan