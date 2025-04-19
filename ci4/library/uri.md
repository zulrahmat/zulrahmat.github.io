Tentu! Di CodeIgniter 4, library **URI** digunakan untuk menangani bagian URL dari permintaan HTTP. Library ini sangat berguna untuk mendapatkan segmen URL, manipulasi path, dan lainnya. Di CI4, URI dikelola melalui **`CodeIgniter\HTTP\URI`** yang diakses melalui `request()` atau `service()`.

---

## 🧾 Materi: Library URI di CodeIgniter 4

### 1. **Mendapatkan Objek URI**
```php
$uri = service('uri');
// atau
$uri = current_url(true);
```

---

### 2. **Mengakses Segmen URI**
Misalnya URL:
```
http://localhost/myapp/user/edit/5
```

#### Mendapatkan segmen
```php
$uri = service('uri');

echo $uri->getSegment(1); // user
echo $uri->getSegment(2); // edit
echo $uri->getSegment(3); // 5
```

#### Jumlah total segmen
```php
echo $uri->getTotalSegments(); // 3
```

#### Semua segmen
```php
print_r($uri->getSegments());
```

---

### 3. **Mengakses Bagian URL Lainnya**
```php
$uri = service('uri');

echo $uri->getScheme();      // http atau https
echo $uri->getHost();        // localhost
echo $uri->getPort();        // 80 atau 443
echo $uri->getPath();        // user/edit/5
echo $uri->getQuery();       // name=andi
echo $uri->getFragment();    // bagian setelah #
```

---

### 4. **Menggunakan current_url() dan previous_url()**
```php
echo current_url();  // URL saat ini
echo previous_url(); // URL sebelumnya
```

---

### 5. **Mengubah Objek URI**
```php
$uri = new \CodeIgniter\HTTP\URI('http://localhost/user/edit/5');

$newUri = $uri->setSegment(3, '10');
echo $newUri->getPath(); // user/edit/10
```

---

### 6. **Contoh Penggunaan di Controller**
```php
namespace App\Controllers;

use CodeIgniter\Controller;

class User extends Controller
{
    public function edit()
    {
        $uri = service('uri');
        $id = $uri->getSegment(3);

        echo "Edit user dengan ID: " . $id;
    }
}
```

---

### 7. **Debugging URI**
```php
helper('url');

echo uri_string();      // user/edit/5
echo current_url();     // http://localhost/user/edit/5
echo site_url();        // http://localhost/
echo base_url();        // http://localhost/
```

---

Kalau kamu mau, aku bisa bantu bikin *project demo* kecil yang menunjukkan penggunaan URI untuk routing dinamis dan pengambilan data berdasarkan segmen. Mau?