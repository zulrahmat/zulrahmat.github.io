Tentu! Berikut ini adalah **materi lengkap tentang Library Encryption di CodeIgniter 4**, yang bisa kamu gunakan untuk melakukan **enkripsi** dan **dekripsi** data secara aman menggunakan berbagai metode cipher modern.

---

## 🛡️ Materi: Library Encryption di CodeIgniter 4

### 🔹 1. **Konfigurasi Awal**
Library ini sudah tersedia secara default di CI4, tapi kamu bisa mengatur konfigurasinya di:
```
app/Config/Encryption.php
```

Contoh konfigurasi:
```php
public $key = 'YOUR_RANDOM_SECRET_KEY';
public $driver = 'OpenSSL'; // Bisa juga: Sodium
public $blockSize = 16;
public $cipher = 'AES-256-CTR'; // Cipher modern yang aman
```

> Gunakan `php spark key:generate` untuk membuat key secara otomatis!

---

### 🔹 2. **Cara Menggunakan Encryption**
#### a. **Instansiasi Library**
```php
$encrypter = \Config\Services::encrypter();
```

---

### 🔹 3. **Enkripsi Data**
```php
$data = 'ini rahasia';

$encrypter = \Config\Services::encrypter();
$encrypted = $encrypter->encrypt($data);

echo $encrypted; // Data terenkripsi (bentuk biner atau base64)
```

---

### 🔹 4. **Dekripsi Data**
```php
$decrypted = $encrypter->decrypt($encrypted);

echo $decrypted; // "ini rahasia"
```

---

### 🔹 5. **Menggunakan Base64 (Agar Bisa Disimpan di Database atau URL)**
```php
$encrypted = base64_encode($encrypter->encrypt($data));
$decrypted = $encrypter->decrypt(base64_decode($encrypted));
```

---

### 🔹 6. **Custom Key Sementara**
Kamu bisa menggunakan kunci selain dari config jika ingin key berbeda untuk keperluan tertentu:
```php
$config = new \Config\Encryption();
$config->key = 'kunci-khusus';
$config->driver = 'OpenSSL';

$encrypter = \Config\Services::encrypter($config);

$hasil = $encrypter->encrypt('data sensitif');
```

---

### 🔹 7. **Contoh Implementasi di Controller**
```php
namespace App\Controllers;
use CodeIgniter\Controller;

class SecureData extends Controller
{
    public function index()
    {
        $encrypter = \Config\Services::encrypter();

        $data = 'passwordku';
        $encrypted = base64_encode($encrypter->encrypt($data));
        $decrypted = $encrypter->decrypt(base64_decode($encrypted));

        echo "Encrypted: " . $encrypted . "<br>";
        echo "Decrypted: " . $decrypted;
    }
}
```

---

### 🔹 8. **Catatan Keamanan**
- Jangan simpan hasil `encrypt()` langsung tanpa encoding, gunakan `base64_encode()`.
- Pastikan kamu menggunakan `AES-256-CTR` atau `AES-256-CBC` untuk keamanan tinggi.
- Jangan hard-code key di file `Encryption.php`, lebih baik simpan di `.env`.

---

### 🧪 Tips Tambahan
Gunakan ini untuk debugging key:
```bash
php spark key:generate
```

Untuk `.env`:
```
encryption.key = hex2bin(YourGeneratedHexKey)
```

---

Kalau kamu mau, aku bisa bantu bikin form sederhana untuk **encrypt & decrypt input user** dengan library ini. Mau sekalian?