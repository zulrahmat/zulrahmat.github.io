Berikut adalah **materi lengkap tentang Model di CodeIgniter 4** — cocok untuk kamu yang ingin memahami bagaimana cara kerja Model untuk mengelola data dari database secara efisien dan terstruktur.

---

## 📘 Materi Lengkap Model di CodeIgniter 4

---

### 🔍 Apa itu Model?

> **Model** adalah bagian dari **MVC (Model-View-Controller)** yang bertugas untuk **mengelola data**:
- Berkomunikasi dengan database
- Menyimpan, mengambil, menghapus, dan memproses data
- Menyediakan data ke controller

---

## 🛠️ 1. Struktur Dasar Model

Model di CodeIgniter 4 biasanya dibuat di folder:
```
/app/Models/
```

### Contoh:
```php
namespace App\Models;

use CodeIgniter\Model;

class PegawaiModel extends Model
{
    protected $table = 'pegawai';             // Nama tabel
    protected $primaryKey = 'id';             // Primary key
    protected $allowedFields = [              // Kolom yang bisa diisi
        'nama', 'jabatan', 'email', 'tanggal_lahir'
    ];
}
```

---

## 📥 2. Menggunakan Model di Controller

### Contoh:
```php
use App\Models\PegawaiModel;

class Pegawai extends BaseController
{
    public function index()
    {
        $model = new PegawaiModel();
        $data['pegawai'] = $model->findAll();
        return view('pegawai/index', $data);
    }
}
```

---

## ⚙️ 3. Operasi CRUD di Model

### a. **Create (Insert)**
```php
$model->insert([
    'nama' => 'Budi',
    'jabatan' => 'Staff',
    'email' => 'budi@mail.com',
    'tanggal_lahir' => '1995-05-01'
]);
```

### b. **Read (Select)**
```php
$data = $model->findAll();       // Semua data
$data = $model->find($id);       // Berdasarkan ID
$data = $model->where('jabatan', 'Manager')->findAll(); // Berdasarkan kondisi
```

### c. **Update**
```php
$model->update($id, [
    'jabatan' => 'Supervisor'
]);
```

### d. **Delete**
```php
$model->delete($id);
```

---

## 🔄 4. Menggunakan Query Builder di Model

Model di CodeIgniter 4 mewarisi fitur Query Builder:

```php
$data = $model->select('nama, email')
              ->where('jabatan', 'Manager')
              ->orderBy('nama', 'ASC')
              ->findAll();
```

---

## 🧪 5. Validasi Otomatis

Model dapat memvalidasi data secara otomatis:

```php
protected $validationRules = [
    'nama' => 'required|min_length[3]',
    'email' => 'required|valid_email',
];
```

Untuk memakainya:

```php
if ($model->save($data) === false) {
    $errors = $model->errors();
}
```

---

Berikut adalah **daftar lengkap method yang tersedia pada Model di CodeIgniter 4**, beserta **penjelasan dan contoh penggunaannya**:

---

## 📘 Daftar Method Model di CodeIgniter 4 + Contoh

### 📦 1. `find()`
> Mengambil satu data berdasarkan primary key.

```php
$data = $model->find(1);
```

---

### 📦 2. `findAll()`
> Mengambil semua data dari tabel.

```php
$data = $model->findAll(); // Semua data
$data = $model->findAll(10, 20); // 10 data, mulai dari offset 20
```

---

### 📦 3. `first()`
> Mengambil baris pertama dari query.

```php
$data = $model->where('jabatan', 'Manager')->first();
```

---

### 📦 4. `insert()`
> Menambahkan data ke tabel.

```php
$model->insert([
  'nama' => 'Rina',
  'email' => 'rina@mail.com'
]);
```

---

### 📦 5. `insertBatch()`
> Menambahkan banyak data sekaligus.

```php
$model->insertBatch([
  ['nama' => 'A', 'email' => 'a@mail.com'],
  ['nama' => 'B', 'email' => 'b@mail.com']
]);
```

---

### 📦 6. `update()`
> Mengubah data berdasarkan ID atau kondisi.

```php
$model->update(1, ['nama' => 'Rina Update']);
```

---

### 📦 7. `updateBatch()`
> Update banyak data sekaligus.

```php
$model->updateBatch([
  ['id' => 1, 'nama' => 'A1'],
  ['id' => 2, 'nama' => 'B2']
], 'id');
```

---

### 📦 8. `save()`
> Insert atau update data secara otomatis.

```php
$model->save([
  'id'   => 1,
  'nama' => 'Update Jika Ada, Insert Jika Tidak'
]);
```

---

### 📦 9. `delete()`
> Menghapus data berdasarkan ID atau kondisi.

```php
$model->delete(3); // Hapus berdasarkan ID
$model->where('jabatan', 'Staff')->delete(); // Berdasarkan kondisi
```

---

### 📦 10. `where()`
> Menambahkan kondisi WHERE ke query.

```php
$data = $model->where('jabatan', 'Manager')->findAll();
```

---

### 📦 11. `orWhere()`
> Menambahkan kondisi OR WHERE.

```php
$model->where('jabatan', 'Manager')->orWhere('jabatan', 'Staff');
```

---

### 📦 12. `like()` / `orLike()`
> Untuk pencarian menggunakan LIKE.

```php
$model->like('nama', 'rin'); // nama LIKE '%rin%'
```

---

### 📦 13. `orderBy()`
> Mengurutkan hasil query.

```php
$model->orderBy('nama', 'ASC')->findAll();
```

---

### 📦 14. `groupBy()`
> Mengelompokkan data berdasarkan kolom.

```php
$model->select('jabatan, COUNT(*) as total')
      ->groupBy('jabatan')
      ->findAll();
```

---

### 📦 15. `select()`
> Menentukan kolom yang diambil.

```php
$model->select('nama, email')->findAll();
```

---

### 📦 16. `join()`
> Melakukan JOIN antar tabel.

```php
$model->join('departemen', 'pegawai.dept_id = departemen.id')
      ->findAll();
```

---

### 📦 17. `countAll()`
> Menghitung semua data dalam tabel.

```php
$total = $model->countAll();
```

---

### 📦 18. `countAllResults()`
> Menghitung total baris dengan kondisi.

```php
$total = $model->where('jabatan', 'Staff')->countAllResults();
```

---

### 📦 19. `paginate()`
> Mengambil data dengan pagination.

```php
$data['pegawai'] = $model->paginate(10); // 10 per halaman
$data['pager']   = $model->pager;
```

---

### 📦 20. `setTable()`
> Mengubah nama tabel saat runtime (jarang dipakai).

```php
$model->setTable('pegawai_backup')->findAll();
```

---

### 📦 21. `setAllowedFields()`
> Atur field yang boleh diinput.

```php
$model->setAllowedFields(['nama', 'email']);
```

---

### 📦 22. `errors()`
> Ambil error validasi setelah `save()` atau `insert()` gagal.

```php
if (! $model->save($data)) {
  $errors = $model->errors();
}
```