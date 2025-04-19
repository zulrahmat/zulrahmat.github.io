Tentu! Berikut ini adalah **materi lengkap tentang Library Cache di CodeIgniter 4**, yang bisa kamu gunakan untuk meningkatkan performa aplikasi dengan menyimpan data sementara dan mengurangi beban proses berulang.

---

## ⚡ Materi: Library Cache di CodeIgniter 4

---

### 🔰 1. Apa itu Cache?

Cache digunakan untuk menyimpan data sementara, seperti hasil query database atau halaman view, agar bisa digunakan kembali **tanpa harus memproses ulang**.

---

## 🔧 2. Mengaktifkan dan Mengatur Cache Driver

### 📁 Konfigurasi Cache

File konfigurasi: `app/Config/Cache.php`

```php
public string $handler = 'file'; // Bisa diganti dengan redis, memcached, dll
```

> Secara default, CodeIgniter 4 menggunakan **File-based cache** (disimpan di folder `writable/cache`).

---

## 🧰 3. Menggunakan Cache di Controller

### 🔹 Inisialisasi

```php
$cache = \Config\Services::cache();
```

### 🔹 Menyimpan Data ke Cache

```php
$cache->save('nama_cache', $data, 300); // 300 = detik (5 menit)
```

Contoh:

```php
$cache->save('user_aktif', ['id' => 1, 'nama' => 'Budi'], 600);
```

---

### 🔹 Mengambil Data dari Cache

```php
$data = $cache->get('nama_cache');
```

Jika tidak ditemukan, akan bernilai `null`.

---

### 🔹 Menghapus Cache

```php
$cache->delete('nama_cache');
```

Atau menghapus semua:

```php
$cache->clean(); // hati-hati di production!
```

---

## 🧪 4. Contoh Implementasi

```php
public function daftar()
{
    $cache = \Config\Services::cache();

    $data = $cache->get('daftar_barang');

    if (!$data) {
        // Ambil dari database jika belum ada di cache
        $data = $this->barangModel->findAll();

        // Simpan ke cache selama 10 menit
        $cache->save('daftar_barang', $data, 600);
    }

    return view('barang/index', ['barang' => $data]);
}
```

---

## 🚀 5. Menentukan Handler Cache Lain

### 🔹 Redis

- Ubah `handler` menjadi `'redis'`
- Pastikan ekstensi Redis aktif dan Redis server berjalan

### 🔹 Memcached

- Ubah `handler` menjadi `'memcached'`
- Pastikan ekstensi Memcached aktif

> Atur pengaturan tambahan di `app/Config/Cache.php`

---

## 🧱 6. Menyimpan View ke Cache

Jika kamu ingin **men-cache seluruh view**, bisa gunakan `Page Caching`:

### Aktifkan Page Cache

Di controller:
```php
$this->cachePage(60); // cache 60 detik
```

> Hanya berlaku untuk controller bawaan dari `CodeIgniter\Controller`.

---

## 🧠 Tips Best Practice

✅ Gunakan cache untuk data yang jarang berubah  
✅ Tetapkan durasi cache sesuai kebutuhan  
✅ Jangan cache data sensitif  
✅ Untuk REST API, cache response JSON  
✅ Monitor dan bersihkan cache lama secara berkala

---

## 📘 Dokumentasi Resmi

- [Cache Library - CodeIgniter 4](https://codeigniter.com/user_guide/libraries/caching.html)

---

Kalau kamu mau, aku bisa bantu buatin contoh lengkap caching data produk dari database menggunakan `File Cache` dan disisipkan ke tampilan. Mau sekalian?