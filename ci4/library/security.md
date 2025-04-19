Tentu! Berikut ini adalah **materi lengkap tentang Library Security di CodeIgniter 4**, yang dirancang untuk membantu kamu menangani berbagai aspek keamanan seperti **XSS Filtering, CSRF Protection**, dan **pengamanan input**.

---

## 🔐 Materi: Library Security di CodeIgniter 4

---

### 📌 1. **Mengaktifkan Library Security**

`Security` class di CodeIgniter 4 secara default aktif untuk fitur tertentu (seperti CSRF). Untuk mengaksesnya secara manual:

```php
$security = \Config\Services::security();
```

---

## ✳️ 2. **CSRF Protection (Cross Site Request Forgery)**

### 🔹 Cara Mengaktifkan

Buka file `.env` dan atur:
```
csrf_protection = true
```

Atau di file `app/Config/Filters.php`:
```php
public $globals = [
    'before' => [
        'csrf' => ['except' => ['api/*']], // bisa kecualikan API
    ],
];
```

### 🔹 Penambahan Token Otomatis

Jika kamu menggunakan `form_open()` dari **form helper**, maka CSRF token akan otomatis dimasukkan ke form.

Contoh manual:
```html
<input type="hidden" name="<?= csrf_token() ?>" value="<?= csrf_hash() ?>">
```

### 🔹 Cek Validitas Token Secara Manual

```php
if ($this->request->getPost(csrf_token()) !== csrf_hash()) {
    // Token tidak valid
}
```

---

## ✳️ 3. **XSS Filtering (Cross Site Scripting)**

### 🔹 Tujuan
Mencegah input berbahaya seperti JavaScript dari user agar tidak dieksekusi.

### 🔹 Penerapan Manual

```php
$clean_input = $security->clean('<script>alert("xss")</script>');
```

Atau gunakan fungsi `esc()` di view:
```php
<?= esc($nama) ?>
```

---

## ✳️ 4. **Random Bytes / Token**

Untuk membuat token atau kunci acak, kamu bisa gunakan:

```php
$random = bin2hex($security->getRandomBytes(16)); // 32 karakter hex
```

Contoh: untuk reset password, token API, dsb.

---

## ✳️ 5. **Content Security Policy (CSP)**

Untuk meningkatkan keamanan dari serangan seperti XSS/inline script injection, kamu bisa mengatur header CSP:

```php
$response = \Config\Services::response();
$response->setHeader('Content-Security-Policy', "default-src 'self'");
```

---

## 🧪 Tips Keamanan Tambahan

✅ Gunakan `esc()` saat menampilkan data ke browser  
✅ Gunakan **password hashing** seperti `password_hash()` (bukan encryption biasa)  
✅ Jangan gunakan data mentah langsung dari `$this->request->getPost()` tanpa filter  
✅ Selalu sanitasi file upload  
✅ Aktifkan HTTPS di production  

---

## 📘 Dokumentasi Resmi

- [Security Class - CodeIgniter 4 User Guide](https://codeigniter.com/user_guide/libraries/security.html)
- [CSRF Protection - CodeIgniter 4](https://codeigniter.com/user_guide/general/security.html#cross-site-request-forgery-csrf)

---

Kalau kamu mau, aku bisa buatin **contoh implementasi CSRF + validasi input + XSS filtering** secara komplit di form login atau form input data. Mau sekalian?