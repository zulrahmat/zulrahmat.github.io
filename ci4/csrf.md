Berikut ringkasan materi **CSRF (Cross-Site Request Forgery) Protection** dalam **CodeIgniter 4** dari dokumentasi resmi:

---

### **1. Konsep CSRF**  
- **CSRF** adalah serangan di mana pengguna terautentikasi dipaksa menjalankan aksi tanpa sadar di situs web (contoh: mengubah password, transfer dana).  
- CodeIgniter 4 menyediakan proteksi bawaan dengan **CSRF Token**.

---

### **2. Konfigurasi CSRF**  
File konfigurasi: **`app/Config/Security.php`**.  
Beberapa parameter penting:  
```php
public $csrfProtection = 'cookie'; // 'session' atau 'cookie'  
public $tokenName     = 'csrf_token_name';  
public $headerName   = 'X-CSRF-TOKEN';  
public $expires      = 7200; // Durasi token (detik)  
public $regenerate   = true; // Regenerasi token setelah submit  
```

---

### **3. Cara Kerja**  
- Sistem secara otomatis generate **token unik** saat form di-load.  
- Token harus disertakan dalam setiap **request POST/PUT/DELETE**.  
- Token divalidasi oleh sistem sebelum eksekusi aksi.  

---

### **4. Implementasi di Form**  
Gunakan helper **`form_open()`** atau sisipkan token secara manual:  
```php
// Otomatis menyertakan CSRF token  
<?= form_open('route/action') ?>  

// Manual (jika menggunakan AJAX)  
<input type="hidden" name="<?= csrf_token() ?>" value="<?= csrf_hash() ?>">  
```

---

### **5. AJAX & API**  
- **Header HTTP**: Tambahkan token di header:  
  ```javascript
  headers: {  
    'X-CSRF-TOKEN': '<?= csrf_hash() ?>'  
  }
  ```
- **Exempt URI**: Jika perlu menonaktifkan CSRF untuk route tertentu, tambahkan di `$except` pada `Security.php`:  
  ```php
  public $except = ['api/webhook'];  
  ```

---

### **6. Error Handling**  
- Jika token tidak valid/invalid, CodeIgniter akan menolak request dengan respons **HTTP 403 (Forbidden)**.  
- Pesan error dapat dikustomisasi di **`app/Language/en/Security.php`**.

---

### **7. Best Practices**  
1. Aktifkan **`$regenerate`** untuk mencegah reuse token.  
2. Gunakan **HTTPS** untuk keamanan tambahan.  
3. Jangan nonaktifkan CSRF kecuali untuk endpoint khusus (e.g., webhook).  

---

### **Catatan Penting**  
- CSRF **tidak diperlukan** untuk request GET/HEAD/OPTIONS.  
- Token disimpan di **cookie** (default) atau **session** tergantung konfigurasi.  

Dengan mengaktifkan CSRF, aplikasi Anda lebih aman dari eksploitasi berbasis serangan silang.  

Untuk detail lengkap, lihat [dokumentasi resmi](https://codeigniter.com/user_guide/libraries/security.html).