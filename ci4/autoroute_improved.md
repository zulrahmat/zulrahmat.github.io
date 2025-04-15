Berikut ringkasan dari dokumentasi *Auto Routing (Improved)* di CodeIgniter 4.6.0:

---

### 🔍 Apa Itu Auto Routing (Improved)?
*Auto Routing (Improved)* adalah sistem routing otomatis yang lebih aman dibandingkan versi sebelumnya (*Legacy*). Dengan fitur ini, kamu tidak perlu mendefinisikan semua rute secara manual. Framework akan mencocokkan URI dengan controller dan metode berdasarkan konvensi penamaan

---

### ⚙️ Perbedaan dengan Auto Routing (Legacy)

- **Prefiks HTTP**:Metode controller harus diawali dengan prefiks HTTP seperti `getIndex()`, `postCreate()`, dll
- **Default Controller/Method**:URI seperti `/home` atau `/home/index` tidak akan dikenali; hanya `/` yang valid
- **Validasi Parameter**:Jika jumlah parameter di URI melebihi yang didefinisikan di metode, akan menghasilkan 404
- **Tanpa `_remap()`**:Metode `_remap()` tidak didukung; sebagai gantinya, gunakan *Default Method Fallback*
- **Isolasi Keamanan**:Controller yang sudah didefinisikan dalam rute manual tidak dapat diakses melalui auto routing

---

### ✅ Cara Mengaktifkan Auto Routing (Improved)

1.Di `app/Config/Routing.php`
   ```php
   public bool $autoRoute = true;
   ```

2.Di `app/Config/Feature.php`
   ```php
   public bool $autoRoutesImproved = true;
   ```

3.Hapus rute default seperti
   ```php
   $routes->get('/', 'Home::index');
   ```

   karena rute manual memiliki prioritas lebih tinggi dan dapat mengganggu auto routing.

---

### 🧭 Struktur URI
Format URI mengikuti pol:
```
http://example.com/{controller}/{method}/{param1}/{param2}/..
```

Conto:
```
http://example.com/hello-world/hello1
```

Akan memanggil `App\Controllers\HelloWorld::getHello('1').

---

### 📁 Dukungan Subdirektor

Auto Routing (Improved) mendukung controller yang ditempatkan dalam subdirektori. URI akan mencerminkan struktur folder tersebt.

---

### 🧪 Contoh Penggunan

Buat file `HelloWorld.php` di `app/Controlles`:
```hp
<?php

namespace App\Controllers;

class HelloWorld extends BaseController
{
    public function getIndex()
    {
        return 'Hello World!';
   }
}
``

Akses melaui:
``

http://example.com/hello-wrld
```


---

### ⚠️ Catatan Penting

- **Parameter di `getIndex()`*: Tidak didukung. URI seperti `/clients/13` tidak akan memanggil `getIndex($page)`. Sebagai solusi, gunakan metode seperti `getP($page)` dan akses melalui `/clients/p/3`.
- **Keamanan*: Auto Routing (Improved) memisahkan akses antara rute manual dan otomatis untuk mencegah konflik dan meningkatkan keamaan.

---

Untuk informasi lebih lanjut dan detail teknis, silakan kunjungi dokumentasi resmi: [Auto Routing (Improved) — CodeIgniter 4.6.0](https://codeigniter.com/user_guide/incoming/auto_routing_improved.html). 