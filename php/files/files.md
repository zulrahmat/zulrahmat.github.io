Berikut adalah daftar fungsi-fungsi PHP yang berkaitan dengan pengelolaan file, dikelompokkan berdasarkan fungsionalitasnya:

### [1. **Membuka/Menutup File**](file_1.md)
- `fopen()` - Membuka file atau URL
- `fclose()` - Menutup file yang terbuka

### [2. **Membaca File**](file_2.md)
- `file_get_contents()` - Membaca seluruh file ke dalam string
- `fread()` - Membaca file yang sudah dibuka (binary-safe)
- `fgets()` - Membaca satu baris dari file
- `fgetc()` - Membaca satu karakter dari file
- `file()` - Membaca seluruh file ke dalam array (per baris)
- `readfile()` - Membaca file dan menulis ke output buffer

### [3. **Menulis ke File**](file_3.md)
- `file_put_contents()` - Menulis string ke file (versi sederhana)
- `fwrite()` - Menulis ke file yang sudah dibuka (binary-safe)
- `fputs()` - Alias dari `fwrite()`

### [4. **Manipulasi File & Direktori**](file_4.md)
- `copy()` - Menyalin file
- `rename()` - Mengubah nama/memindahkan file
- `unlink()` - Menghapus file
- `mkdir()` - Membuat direktori
- `rmdir()` - Menghapus direktori kosong

### [5. **Informasi File**](file_5.md)
- `filesize()` - Mendapatkan ukuran file
- `file_exists()` - Memeriksa apakah file/direktori ada
- `is_file()` - Memeriksa apakah path adalah file biasa
- `is_dir()` - Memeriksa apakah path adalah direktori
- `filemtime()` - Mendapatkan waktu modifikasi terakhir file
- `fileatime()` - Mendapatkan waktu akses terakhir file
- `filectime()` - Mendapatkan waktu perubahan inode file
- `filetype()` - Mendapatkan tipe file
- `pathinfo()` - Mengembalikan informasi tentang path file
- `realpath()` - Mengembalikan absolute/real path

### [6. **Navigasi Direktori**](file_6.md)
- `scandir()` - Mendaftar file dan direktori dalam path
- `glob()` - Mencari path yang cocok dengan pola
- `opendir()` - Membuka handle direktori
- `readdir()` - Membaca entri dari handle direktori
- `closedir()` - Menutup handle direktori
- `chdir()` - Mengubah direktori kerja
- `getcwd()` - Mendapatkan direktori kerja saat ini

### [7. **Manipulasi Path**](file_7.md)
- `basename()` - Mengembalikan komponen nama file dari path
- `dirname()` - Mengembalikan komponen direktori dari path
- `pathinfo()` - Mengembalikan informasi tentang path

### [8. **Locking File**](file_8.md)
- `flock()` - Memberikan advisory file locking

### [9. **Pointer File**](file_9.md)
- `ftell()` - Mengembalikan posisi pointer file
- `fseek()` - Memindahkan pointer file
- `rewind()` - Mengembalikan pointer file ke awal

### [10. **Upload File**](file_10.md)
- `move_uploaded_file()` - Memindahkan file yang diupload ke lokasi baru
- `is_uploaded_file()` - Memeriksa apakah file diupload via HTTP POST

### [11. **Stream & Konteks**](file_11.md)
- `stream_context_create()` - Membuat konteks stream
- `stream_get_contents()` - Membaca seluruh stream ke string

### [12. **Fungsi Tambahan**](file_12.md)
- `tempnam()` - Membuat file dengan nama unik
- `tmpfile()` - Membuat file sementara
- `clearstatcache()` - Membersihkan cache stat file

Untuk memulai, Anda bisa mencoba fungsi dasar seperti:
```php
// Membaca file
$content = file_get_contents('file.txt');

// Menulis file
file_put_contents('newfile.txt', 'Hello World!');

// Mengecek apakah file ada
if (file_exists('file.txt')) {
    echo "File exists!";
}
```

Ingat untuk selalu memeriksa izin file/direktori dan menangani error dengan baik saat bekerja dengan file.