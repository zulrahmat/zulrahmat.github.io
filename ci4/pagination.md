Berikut adalah ringkasan sederhana dari dokumentasi *Pagination* di CodeIgniter 4.6.0:

---

### 📚 Apa Itu Pagination?
Pagination adalah fitur untuk membagi data yang banyak menjadi beberapa halaman, sehingga lebih mudah dibaca dan diakses oleh pengguna

---

### ⚙️ Cara Menggunakan Pagination

#### 1. Menggunakan Model
Jika kamu menggunakan model, CodeIgniter menyediakan metode `paginate()` untuk mempermudah

```php$model = new \App\Models\YourModel();
$data['items'] = $model->paginate(10); // 10 item per halaman
$data['pager'] = $model->pager
```

Kemudian, di view

```php<?= $pager->links() ?
```


#### 2. Manual Pagination
Jika tidak menggunakan model, kamu bisa mengatur pagination secara manual

```php$pager = \Config\Services::pager();
$offset = ($this->request->getVar('page') ?? 1) - 1;
$perPage = 10;

$data['items'] = $yourDataSource->limit($perPage, $offset * $perPage)->findAll();
$data['pager'] = $pager->make(count($data['items']), $perPage)
```


---

### 🎨 Kustomisasi Tampilan
Kamu bisa mengubah tampilan pagination dengan membuat template view khusus atau menggunakan template bawaan seperti `default_full` atau `simple.

---

### 🔄 Fitur Tambahan

- **Multiple Paginators*: Mendukung beberapa pagination dalam satu halamn.
- **URI Segment*: Bisa menentukan segmen URI untuk halamn.
- **Query String*: Mendukung pagination dengan query string, misalnya `?page=`.

---

Untuk informasi lebih lengkap, kunjungi dokumentasi resmi CodeIgniter: [Pagination — CodeIgniter 4.6.0](https://codeigniter.com/user_guide/libraries/pagination.html#pagination). 