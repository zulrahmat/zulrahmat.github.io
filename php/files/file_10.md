Berikut contoh penggunaan fungsi-fungsi **upload file** (Kelompok 10) dalam PHP:

### 10. Upload File

#### a. Dasar Upload File dengan `move_uploaded_file()`
```php
<?php
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $uploadDir = 'uploads/';
    $uploadedFile = $uploadDir . basename($_FILES['userfile']['name']);
    
    if (move_uploaded_file($_FILES['userfile']['tmp_name'], $uploadedFile)) {
        echo "File berhasil diupload!";
    } else {
        echo "Upload gagal!";
    }
}
?>

<form method="post" enctype="multipart/form-data">
    <input type="file" name="userfile">
    <button type="submit">Upload</button>
</form>
```

#### b. Validasi Upload File
```php
<?php
function validateUpload($file) {
    // Cek error code
    if ($file['error'] !== UPLOAD_ERR_OK) {
        throw new Exception("Error upload: " . $file['error']);
    }
    
    // Batasan ukuran (5MB)
    $maxSize = 5 * 1024 * 1024;
    if ($file['size'] > $maxSize) {
        throw new Exception("Ukuran file melebihi batas 5MB");
    }
    
    // Validasi tipe file
    $allowedTypes = ['image/jpeg', 'image/png', 'application/pdf'];
    $finfo = new finfo(FILEINFO_MIME_TYPE);
    $mime = $finfo->file($file['tmp_name']);
    
    if (!in_array($mime, $allowedTypes)) {
        throw new Exception("Tipe file tidak diizinkan");
    }
    
    return true;
}

try {
    if (isset($_FILES['userfile'])) {
        validateUpload($_FILES['userfile']);
        // Lanjutkan proses upload...
    }
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
?>
```

#### c. Upload Multiple Files
```php
<?php
if (!empty($_FILES['files']['name'][0])) {
    $uploadDir = 'uploads/';
    
    foreach ($_FILES['files']['tmp_name'] as $key => $tmpName) {
        $fileName = basename($_FILES['files']['name'][$key]);
        $targetPath = $uploadDir . uniqid() . '_' . $fileName;
        
        if (move_uploaded_file($tmpName, $targetPath)) {
            echo "File $fileName berhasil diupload<br>";
        }
    }
}
?>

<form method="post" enctype="multipart/form-data">
    <input type="file" name="files[]" multiple>
    <button type="submit">Upload Multiple</button>
</form>
```

#### d. Secure Filename Handling
```php
<?php
function sanitizeFilename($filename) {
    // Hapus karakter berbahaya
    $dangerousChars = ['../', '<!--', '..\\', '/', '\\', "'", '"', '&', '?', '#'];
    $filename = str_replace($dangerousChars, '', $filename);
    
    // Hapus karakter non-ASCII
    $filename = preg_replace('/[^\x00-\x7F]/', '', $filename);
    
    return $filename;
}

$originalName = $_FILES['userfile']['name'];
$safeName = sanitizeFilename($originalName);
$extension = pathinfo($safeName, PATHINFO_EXTENSION);
$uniqueName = uniqid() . '.' . $extension;
$targetPath = 'uploads/' . $uniqueName;
?>
```

#### e. Upload dengan Progress Bar (PHP 5.4+)
```php
<?php
// session_start(); // Diperlukan untuk tracking progress

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $uploadDir = 'uploads/';
    $tempFile = $_FILES['userfile']['tmp_name'];
    $targetFile = $uploadDir . $_FILES['userfile']['name'];
    
    // Track progress upload
    $progressKey = uniqid();
    $_SESSION['upload_progress_' . $progressKey] = [
        'start_time' => time(),
        'content_length' => $_FILES['userfile']['size'],
        'bytes_processed' => 0
    ];
    
    // Pindahkan file
    $success = move_uploaded_file($tempFile, $targetFile);
    
    // Hapus data progress setelah selesai
    unset($_SESSION['upload_progress_' . $progressKey]);
    
    echo $success ? "Upload berhasil" : "Upload gagal";
}
?>

<!-- JavaScript untuk mengecek progress -->
<script>
function checkProgress(progressKey) {
    fetch('progress.php?key=' + progressKey)
        .then(response => response.json())
        .then(data => {
            console.log(data);
            // Update progress bar
        });
}
</script>
```

File `progress.php`:
```php
<?php
session_start();
$key = $_GET['key'] ?? '';
$progress = $_SESSION['upload_progress_' . $key] ?? null;

if ($progress) {
    header('Content-Type: application/json');
    echo json_encode([
        'progress' => ($progress['bytes_processed'] / $progress['content_length']) * 100
    ]);
}
?>
```

#### f. Error Code Upload
Berikut tabel error code yang mungkin muncul di `$_FILES['file']['error']`:

| Konstanta               | Nilai | Deskripsi                                                                 |
|-------------------------|-------|--------------------------------------------------------------------------|
| `UPLOAD_ERR_OK`         | 0     | Tidak ada error                                                          |
| `UPLOAD_ERR_INI_SIZE`   | 1     | Ukuran file melebihi `upload_max_filesize` di php.ini                    |
| `UPLOAD_ERR_FORM_SIZE`  | 2     | Ukuran file melebihi MAX_FILE_SIZE di form HTML                          |
| `UPLOAD_ERR_PARTIAL`    | 3     | File hanya terupload sebagian                                            |
| `UPLOAD_ERR_NO_FILE`    | 4     | Tidak ada file yang diupload                                            |
| `UPLOAD_ERR_NO_TMP_DIR` | 6     | Folder temporary tidak ditemukan                                        |
| `UPLOAD_ERR_CANT_WRITE` | 7     | Gagal menulis file ke disk                                              |
| `UPLOAD_ERR_EXTENSION`  | 8     | Upload dihentikan oleh ekstensi PHP                                     |

#### g. Konfigurasi PHP untuk Upload
Tambahkan di `php.ini`:
```ini
; Batas ukuran upload
upload_max_filesize = 10M
post_max_size = 12M

; Lokasi temporary file
upload_tmp_dir = "/tmp"

; Batas waktu eksekusi
max_execution_time = 300
```

#### h. Contoh Praktis: Upload Gambar dengan Thumbnail
```php
<?php
if (isset($_FILES['image'])) {
    $uploadDir = 'uploads/images/';
    $originalName = $_FILES['image']['name'];
    $tempFile = $_FILES['image']['tmp_name'];
    
    // Validasi gambar
    $imageInfo = getimagesize($tempFile);
    if (!$imageInfo) {
        die("File bukan gambar valid");
    }
    
    // Generate nama unik
    $extension = strtolower(pathinfo($originalName, PATHINFO_EXTENSION));
    $uniqueName = uniqid('img_') . '.' . $extension;
    $targetFile = $uploadDir . $uniqueName;
    
    // Pindahkan file
    if (move_uploaded_file($tempFile, $targetFile)) {
        // Buat thumbnail
        createThumbnail($targetFile, $uploadDir . 'thumbs/' . $uniqueName, 200);
        echo "Gambar berhasil diupload dan thumbnail dibuat";
    }
}

function createThumbnail($sourcePath, $destPath, $thumbWidth) {
    $imageInfo = getimagesize($sourcePath);
    $sourceType = $imageInfo[2];
    
    switch ($sourceType) {
        case IMAGETYPE_JPEG:
            $sourceImage = imagecreatefromjpeg($sourcePath);
            break;
        case IMAGETYPE_PNG:
            $sourceImage = imagecreatefrompng($sourcePath);
            break;
        default:
            return false;
    }
    
    $width = imagesx($sourceImage);
    $height = imagesy($sourceImage);
    
    // Hitung ukuran thumbnail
    $thumbHeight = floor($height * ($thumbWidth / $width));
    
    // Buat gambar thumbnail
    $thumbImage = imagecreatetruecolor($thumbWidth, $thumbHeight);
    
    // Resize
    imagecopyresampled($thumbImage, $sourceImage, 0, 0, 0, 0, 
        $thumbWidth, $thumbHeight, $width, $height);
    
    // Simpan thumbnail
    switch ($sourceType) {
        case IMAGETYPE_JPEG:
            imagejpeg($thumbImage, $destPath);
            break;
        case IMAGETYPE_PNG:
            imagepng($thumbImage, $destPath);
            break;
    }
    
    imagedestroy($sourceImage);
    imagedestroy($thumbImage);
    
    return true;
}
?>
```

### Best Practices untuk Upload File:
1. **Selalu validasi** tipe dan ukuran file
2. **Gunakan nama file unik** untuk menghindari overwrite
3. **Batasi akses** ke direktori upload
4. **Simpan file di luar root** web jika memungkinkan
5. **Gunakan HTTPS** untuk transfer yang aman
6. **Periksa virus/malware** untuk file yang diupload
7. **Batasi ekstensi file** yang diizinkan
8. **Nonaktifkan eksekusi** PHP di direktori upload

Fitur upload file sangat penting untuk:
- Sistem CMS
- Aplikasi berbagi file
- Upload dokumen
- Galeri gambar
- Sistem backup melalui web