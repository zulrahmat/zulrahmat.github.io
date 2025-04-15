Berikut contoh penggunaan fungsi-fungsi **manipulasi path** (Kelompok 7) dalam PHP:

### 7. Manipulasi Path

#### a. `basename()` - Mengambil nama file dari path
```php
<?php
$path = "/var/www/html/project/images/photo.jpg";

echo "Nama file: " . basename($path); // photo.jpg
echo "Nama file tanpa ekstensi: " . basename($path, ".jpg"); // photo

// Contoh dengan path Windows
$windowsPath = "C:\\xampp\\htdocs\\index.php";
echo "Nama file: " . basename($windowsPath); // index.php
?>
```

#### b. `dirname()` - Mengambil direktori dari path
```php
<?php
$fullPath = "/home/user/documents/report.pdf";

echo "Direktori: " . dirname($fullPath); // /home/user/documents
echo "Parent direktori: " . dirname($fullPath, 2); // /home/user

// Contoh praktis
$configFile = dirname(__DIR__) . '/config/settings.ini';
echo "Path konfigurasi: " . $configFile;
?>
```

#### c. `pathinfo()` - Mengurai informasi path (lengkap)
```php
<?php
$filePath = "/var/www/html/assets/js/app.min.js";

$info = pathinfo($filePath);
echo "<pre>";
print_r($info);
/*
Array (
    [dirname] => /var/www/html/assets/js
    [basename] => app.min.js
    [extension] => js
    [filename] => app.min
)
*/
echo "</pre>";

// Mengakses nilai individual
echo "Ekstensi: " . pathinfo($filePath, PATHINFO_EXTENSION) . "<br>";
echo "Nama file: " . pathinfo($filePath, PATHINFO_FILENAME) . "<br>";
?>
```

#### d. `realpath()` - Mengkonversi ke absolute path
```php
<?php
$relativePath = "../images/logo.png";
$absolutePath = realpath($relativePath);

if ($absolutePath !== false) {
    echo "Path absolut: " . $absolutePath;
} else {
    echo "Path tidak valid";
}

// Contoh keamanan
function includeSafe($relativePath) {
    $baseDir = realpath(__DIR__ . '/includes');
    $requestedPath = realpath($baseDir . '/' . $relativePath);
    
    if ($requestedPath && strpos($requestedPath, $baseDir) === 0) {
        include $requestedPath;
    } else {
        die("Akses file tidak diizinkan");
    }
}
?>
```

#### e. Contoh praktis: Normalisasi path
```php
<?php
function normalizePath($path) {
    // Mengganti backslash dengan forward slash
    $path = str_replace('\\', '/', $path);
    
    // Menghilangkan ./
    $path = preg_replace('/\/\.\//', '/', $path);
    
    // Menyederhanakan ../ 
    while (preg_match('/\/[^\/]+\/\.\.\//', $path)) {
        $path = preg_replace('/\/[^\/]+\/\.\.\//', '/', $path);
    }
    
    return $path;
}

$messyPath = "C:\\www\\htdocs\\project/../assets/./css/style.css";
echo normalizePath($messyPath);
// Output: C:/www/htdocs/assets/css/style.css
?>
```

#### f. Contoh praktis: Membuat path cross-platform
```php
<?php
function buildPath(...$segments) {
    return implode(DIRECTORY_SEPARATOR, $segments);
}

$configPath = buildPath(__DIR__, 'config', 'db.ini');
echo "Path konfigurasi: " . $configPath;
?>
```

#### g. Contoh praktis: Ekstrak ekstensi file
```php
<?php
function getFileExtension($filename) {
    // Beberapa pendekatan:
    
    // 1. Menggunakan pathinfo()
    // return pathinfo($filename, PATHINFO_EXTENSION);
    
    // 2. Menggunakan explode()
    $parts = explode('.', $filename);
    if (count($parts) > 1) {
        return strtolower(end($parts));
    }
    return '';
}

$filename = "Document.Archive.ZIP";
echo "Ekstensi file: " . getFileExtension($filename); // zip
?>
```

#### h. Contoh praktis: Validasi path upload
```php
<?php
function validateUploadPath($uploadDir, $filename) {
    // Dapatkan path absolut
    $uploadDir = realpath($uploadDir) ?: $uploadDir;
    $targetPath = realpath($uploadDir . DIRECTORY_SEPARATOR . $filename);
    
    // Pastikan path upload berada dalam direktori yang diizinkan
    if ($targetPath === false || strpos($targetPath, $uploadDir) !== 0) {
        return false;
    }
    
    // Validasi karakter berbahaya
    if (preg_match('/[\/\\\\:"*?<>|]/', $filename)) {
        return false;
    }
    
    return true;
}

$isValid = validateUploadPath('uploads', '../../etc/passwd');
echo $isValid ? "Path valid" : "Path tidak valid";
?>
```

### Perbandingan Fungsi Manipulasi Path:
| Fungsi          | Kegunaan Utama                          | Catatan Penting                     |
|----------------|----------------------------------------|------------------------------------|
| `basename()`   | Mengambil nama file dari path          | Bisa menghilangkan ekstensi        |
| `dirname()`    | Mengambil direktori parent             | Support level parent dengan parameter kedua |
| `pathinfo()`   | Mengurai semua komponen path           | Mengembalikan array atau komponen spesifik |
| `realpath()`   | Mengkonversi ke absolute path          | Mengembalikan false jika path tidak valid |
| `DIRECTORY_SEPARATOR` | Konstanta untuk separator path | Lebih baik daripada hardcode '/' atau '\' |

### Tips Penting:
1. **Keamanan Path**:
   - Selalu validasi input path pengguna
   - Gunakan `realpath()` untuk mencegah directory traversal
   - Hindari penggunaan path relatif untuk operasi kritis

2. **Kompatibilitas Cross-Platform**:
   - Gunakan `DIRECTORY_SEPARATOR` daripada hardcode slash
   - Fungsi path PHP umumnya bekerja di Windows dan Unix

3. **Best Practice**:
   ```php
   // Lebih baik
   $path = __DIR__ . DIRECTORY_SEPARATOR . 'config.ini';
   
   // Daripada
   $path = dirname(__FILE__) . '/config.ini';
   ```

4. **Untuk operasi modern**, pertimbangkan menggunakan kelas `SplFileInfo`:
   ```php
   $file = new SplFileInfo('documents/report.pdf');
   echo $file->getExtension(); // pdf
   echo $file->getBasename('.pdf'); // report
   ```

Fungsi-fungsi manipulasi path sangat penting untuk:
- Keamanan sistem file
- Kompatibilitas cross-platform
- Manajemen file yang terorganisir
- Pembuatan aplikasi yang portabel