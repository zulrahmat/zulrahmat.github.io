Berikut contoh penggunaan fungsi-fungsi **informasi file** (Kelompok 5) dalam PHP:

### 5. Informasi File

#### a. `filesize()` - Mendapatkan ukuran file
```php
<?php
$filename = 'document.pdf';

if (file_exists($filename)) {
    $size = filesize($filename);
    
    // Format ukuran file yang mudah dibaca
    function formatSizeUnits($bytes) {
        if ($bytes >= 1073741824) {
            return number_format($bytes / 1073741824, 2) . ' GB';
        } elseif ($bytes >= 1048576) {
            return number_format($bytes / 1048576, 2) . ' MB';
        } elseif ($bytes >= 1024) {
            return number_format($bytes / 1024, 2) . ' KB';
        } else {
            return $bytes . ' bytes';
        }
    }
    
    echo "Ukuran file: " . formatSizeUnits($size);
} else {
    echo "File tidak ditemukan";
}
?>
```

#### b. `file_exists()`, `is_file()`, `is_dir()` - Pengecekan file/direktori
```php
<?php
$path = 'example.txt';

if (file_exists($path)) {
    if (is_file($path)) {
        echo "$path adalah FILE";
    } elseif (is_dir($path)) {
        echo "$path adalah DIREKTORI";
    }
} else {
    echo "$path tidak ditemukan";
}

// Contoh praktis pengecekan sebelum operasi
function safeFileOperation($path) {
    if (!file_exists($path)) {
        throw new Exception("Path tidak ditemukan");
    }
    
    if (is_dir($path)) {
        return "Ini adalah direktori";
    }
    
    if (is_file($path) && is_readable($path)) {
        return "File bisa dibaca";
    }
    
    return "Tipe path tidak dikenali";
}
?>
```

#### c. `filemtime()`, `fileatime()`, `filectime()` - Waktu file
```php
<?php
$file = 'data.txt';

echo "Informasi waktu untuk file $file:<br>";
echo "Terakhir diubah: " . date('Y-m-d H:i:s', filemtime($file)) . "<br>";
echo "Terakhir diakses: " . date('Y-m-d H:i:s', fileatime($file)) . "<br>";
echo "Waktu perubahan inode: " . date('Y-m-d H:i:s', filectime($file)) . "<br>";

// Contoh penggunaan untuk cache
function isCacheValid($cacheFile, $expiryHours = 24) {
    if (!file_exists($cacheFile)) return false;
    
    $lastModified = filemtime($cacheFile);
    $expiryTime = time() - ($expiryHours * 3600);
    
    return ($lastModified > $expiryTime);
}

if (isCacheValid('cache/data.cache', 2)) {
    echo "Cache masih valid";
} else {
    echo "Cache kedaluwarsa, perlu diperbarui";
}
?>
```

#### d. `filetype()` - Mendapatkan tipe file
```php
<?php
$path = 'example.txt';

$type = filetype($path);
switch ($type) {
    case 'file':
        echo "Ini adalah file biasa";
        break;
    case 'dir':
        echo "Ini adalah direktori";
        break;
    case 'link':
        echo "Ini adalah symbolic link";
        break;
    default:
        echo "Tipe tidak dikenali: $type";
}
?>
```

#### e. `pathinfo()` - Mengurai informasi path
```php
<?php
$filePath = '/var/www/html/project/images/photo.jpg';

$info = pathinfo($filePath);
echo "<pre>";
print_r($info);
echo "</pre>";

// Mengakses komponen individual
echo "Direktori: " . $info['dirname'] . "<br>";
echo "Nama file: " . $info['basename'] . "<br>";
echo "Ekstensi: " . $info['extension'] . "<br>";
echo "Nama tanpa ekstensi: " . $info['filename'] . "<br>";

// Cara alternatif
echo "Ekstensi: " . pathinfo($filePath, PATHINFO_EXTENSION);
?>
```

#### f. `realpath()` - Mendapatkan absolute path
```php
<?php
$relativePath = '../uploads/file.txt';
$absolutePath = realpath($relativePath);

if ($absolutePath !== false) {
    echo "Path absolut: $absolutePath";
} else {
    echo "Path tidak valid";
}

// Contoh keamanan
function secureInclude($relativePath) {
    $baseDir = realpath(__DIR__ . '/includes');
    $requestedPath = realpath($baseDir . '/' . $relativePath);
    
    if ($requestedPath === false || strpos($requestedPath, $baseDir) !== 0) {
        die("Akses file tidak diizinkan");
    }
    
    include $requestedPath;
}
?>
```

#### g. Contoh praktis: File Validator
```php
<?php
function validateFile($filePath) {
    $errors = [];
    
    if (!file_exists($filePath)) {
        $errors[] = "File tidak ditemukan";
        return $errors;
    }
    
    // Batasan ukuran file (5MB)
    if (filesize($filePath) > 5 * 1024 * 1024) {
        $errors[] = "Ukuran file melebihi batas 5MB";
    }
    
    // Hanya izinkan ekstensi tertentu
    $allowedExtensions = ['jpg', 'png', 'pdf'];
    $extension = strtolower(pathinfo($filePath, PATHINFO_EXTENSION));
    if (!in_array($extension, $allowedExtensions)) {
        $errors[] = "Tipe file tidak diizinkan";
    }
    
    // Cek waktu modifikasi terakhir (lebih dari 1 tahun)
    if (filemtime($filePath) < strtotime('-1 year')) {
        $errors[] = "File belum dimodifikasi lebih dari 1 tahun";
    }
    
    return $errors;
}

$fileErrors = validateFile('document.pdf');
if (empty($fileErrors)) {
    echo "File valid";
} else {
    echo "Error validasi file:<br>";
    foreach ($fileErrors as $error) {
        echo "- $error<br>";
    }
}
?>
```

#### h. Contoh praktis: File Metadata Viewer
```php
<?php
function getFileMetadata($filename) {
    if (!file_exists($filename)) return false;
    
    return [
        'name' => basename($filename),
        'size' => filesize($filename),
        'type' => filetype($filename),
        'extension' => pathinfo($filename, PATHINFO_EXTENSION),
        'last_modified' => date('Y-m-d H:i:s', filemtime($filename)),
        'last_accessed' => date('Y-m-d H:i:s', fileatime($filename)),
        'permissions' => substr(sprintf('%o', fileperms($filename)), -4),
        'real_path' => realpath($filename)
    ];
}

$metadata = getFileMetadata('example.txt');
echo "<pre>";
print_r($metadata);
echo "</pre>";
?>
```

### Tips Penting:
1. Selalu clear stat cache jika melakukan operasi berulang:
   ```php
   clearstatcache(); // Membersihkan cache informasi file
   ```
2. Untuk pengecekan keamanan, selalu gunakan `realpath()` sebelum mengakses file
3. Perbedaan waktu file:
   - `filemtime()`: Waktu terakhir konten file diubah
   - `fileatime()`: Waktu terakhir file diakses
   - `filectime()`: Waktu terakhir metadata file diubah (permissions, owner, dll)
4. Gunakan `pathinfo()` untuk memproses nama file daripada manipulasi string manual
5. Untuk aplikasi produksi, tambahkan error handling untuk semua operasi file

Fungsi-fungsi informasi file sangat berguna untuk:
- Validasi file sebelum diproses
- Sistem caching
- Manajemen upload file
- Logging dan monitoring
- Keamanan akses file