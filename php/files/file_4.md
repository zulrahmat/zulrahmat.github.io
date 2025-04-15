Berikut contoh penggunaan fungsi-fungsi **manipulasi file & direktori** (Kelompok 4) dalam PHP:

### 4. Manipulasi File & Direktori

#### a. `copy()` - Menyalin file
```php
<?php
$source = 'original.txt';
$destination = 'backup/original_backup.txt';

if (copy($source, $destination)) {
    echo "File berhasil disalin dari $source ke $destination";
} else {
    echo "Gagal menyalin file!";
}

// Contoh dengan pengecekan
if (file_exists($source)) {
    if (!file_exists('backup')) {
        mkdir('backup');
    }
    copy($source, $destination);
}
?>
```

#### b. `rename()` - Mengubah nama/memindahkan file
```php
<?php
// Mengubah nama file
$oldName = 'data_old.txt';
$newName = 'data_new.txt';

if (rename($oldName, $newName)) {
    echo "File berhasil diubah nama dari $oldName ke $newName";
}

// Memindahkan file ke direktori lain
$currentLocation = 'uploads/temp_file.txt';
$newLocation = 'archives/2023/file.txt';

if (rename($currentLocation, $newLocation)) {
    echo "File berhasil dipindahkan";
} else {
    echo "Gagal memindahkan file";
}
?>
```

#### c. `unlink()` - Menghapus file
```php
<?php
$fileToDelete = 'temporary_data.tmp';

if (file_exists($fileToDelete)) {
    if (unlink($fileToDelete)) {
        echo "File $fileToDelete berhasil dihapus";
    } else {
        echo "Gagal menghapus file";
    }
} else {
    echo "File tidak ditemukan";
}

// Contoh penghapusan dengan konfirmasi
function deleteFileSafely($filename) {
    if (is_writable($filename)) {
        if (unlink($filename)) {
            return true;
        }
    }
    return false;
}
?>
```

#### d. `mkdir()` - Membuat direktori
```php
<?php
$dirName = 'new_directory';

// Membuat direktori sederhana
if (!file_exists($dirName)) {
    mkdir($dirName);
    echo "Direktori $dirName berhasil dibuat";
}

// Membuat direktori dengan izin 0755 (default)
mkdir('downloads', 0755);

// Membuat direktori secara rekursif
mkdir('project/assets/images', 0777, true);
?>
```

#### e. `rmdir()` - Menghapus direktori
```php
<?php
$dirToRemove = 'empty_directory';

if (is_dir($dirToRemove)) {
    if (count(scandir($dirToRemove)) == 2) { // hanya . dan ..
        rmdir($dirToRemove);
        echo "Direktori $dirToRemove berhasil dihapus";
    } else {
        echo "Direktori tidak kosong!";
    }
}

// Fungsi rekursif untuk menghapus direktori dan isinya
function deleteDirectory($dir) {
    if (!file_exists($dir)) return true;
    
    if (!is_dir($dir)) return unlink($dir);
    
    foreach (scandir($dir) as $item) {
        if ($item == '.' || $item == '..') continue;
        if (!deleteDirectory($dir . DIRECTORY_SEPARATOR . $item)) return false;
    }
    
    return rmdir($dir);
}

// Contoh penggunaan
deleteDirectory('temp_folder');
?>
```

#### f. Contoh praktis: Manajemen Upload File
```php
<?php
function handleFileUpload($file, $targetDir = 'uploads/') {
    // Buat direktori jika belum ada
    if (!file_exists($targetDir)) {
        mkdir($targetDir, 0755, true);
    }
    
    $targetFile = $targetDir . basename($file['name']);
    
    // Cek jika file sudah ada
    if (file_exists($targetFile)) {
        // Tambahkan timestamp ke nama file
        $targetFile = $targetDir . pathinfo($file['name'], PATHINFO_FILENAME) 
                    . '_' . time() . '.' 
                    . pathinfo($file['name'], PATHINFO_EXTENSION);
    }
    
    // Pindahkan file upload
    if (move_uploaded_file($file['tmp_name'], $targetFile)) {
        return $targetFile;
    } else {
        return false;
    }
}

// Contoh penggunaan
if ($_FILES['userfile']) {
    $uploadedFile = handleFileUpload($_FILES['userfile']);
    if ($uploadedFile) {
        echo "File berhasil diupload ke: $uploadedFile";
    }
}
?>
```

#### g. Contoh praktis: Backup File
```php
<?php
function createBackup($sourceFile) {
    if (!file_exists($sourceFile)) return false;
    
    $backupDir = 'backups/' . date('Y-m');
    if (!file_exists($backupDir)) {
        mkdir($backupDir, 0755, true);
    }
    
    $backupFile = $backupDir . '/' . basename($sourceFile) . '_' . date('d-His');
    
    return copy($sourceFile, $backupFile);
}

// Contoh penggunaan
if (createBackup('important_data.txt')) {
    echo "Backup berhasil dibuat!";
}
?>
```

### Tips Penting:
1. Selalu verifikasi file/direktori ada sebelum operasi (`file_exists()`)
2. Periksa izin direktori (`is_writable()`)
3. Untuk operasi kritis, tambahkan error handling:
   ```php
   if (!unlink($file)) {
       error_log("Gagal menghapus file: " . $file);
       throw new Exception("File operation failed");
   }
   ```
4. Gunakan `DIRECTORY_SEPARATOR` untuk kompatibilitas cross-platform
5. Untuk direktori, pastikan kosong sebelum dihapus dengan `rmdir()`

Fungsi-fungsi ini adalah dasar untuk manajemen file system dalam PHP. Untuk operasi yang lebih kompleks, Anda bisa mempertimbangkan menggunakan library seperti Symfony Filesystem.