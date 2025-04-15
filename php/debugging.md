Berikut adalah materi **debugging di PHP** secara **singkat dan sederhana**:

---

## 🛠️ Cara Debugging di PHP

### 1. **Menggunakan `var_dump()` atau `print_r()`**
Ini cara paling sederhana untuk melihat nilai dari variabel.

- **`var_dump()`**: Menampilkan tipe data dan nilai variabel.
- **`print_r()`**: Menampilkan nilai variabel (lebih rapi untuk array dan objek).

Contoh:
```php
$nama = "Budi";
$umur = 25;

var_dump($nama);  // Output: string(4) "Budi"
print_r($umur);   // Output: 25
```

---

### 2. **Menggunakan `error_reporting()` dan `ini_set()`**

Untuk menampilkan semua error di PHP.

```php
ini_set('display_errors', 1);  // Menampilkan error
error_reporting(E_ALL);        // Menampilkan semua tipe error
```

---

### 3. **Menggunakan `debug_backtrace()`**

Untuk melihat urutan fungsi yang dipanggil, sangat berguna untuk pelacakan stack trace.

```php
function contohDebug() {
    var_dump(debug_backtrace());
}

contohDebug();
```

---

### 4. **Menggunakan Xdebug**
**Xdebug** adalah ekstensi PHP untuk debugging yang lebih canggih. Beberapa fitur utama:
- Stack trace
- Profiling
- Breakpoints

Cara install Xdebug:
```bash
pecl install xdebug
```

Untuk setup di PHP, tambahkan baris ini di `php.ini`:
```ini
zend_extension="xdebug.so"
```

---

### 5. **Menggunakan IDE (Integrated Development Environment)**

IDE seperti **PHPStorm**, **Visual Studio Code**, atau **NetBeans** mendukung debugging dengan:
- Breakpoints
- Step-by-step execution
- Inspeksi variabel

Biasanya, kamu perlu mengonfigurasi **Xdebug** agar IDE bisa berfungsi.

---

## 📌 Tips Debugging

- Gunakan **log** dengan `error_log()` untuk menyimpan pesan error ke file log.
- Jangan lupa **matikan error display** di lingkungan produksi untuk keamanan:
  ```php
  ini_set('display_errors', 0);
  ```

---

Itu dia! Jika butuh bantuan lebih lanjut atau contoh menggunakan Xdebug, beri tahu aku ya!