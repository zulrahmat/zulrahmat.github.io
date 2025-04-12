## ⚙️ Cara Menjalankan Spark

```bash
php spark
```

Ini akan menampilkan semua daftar perintah yang tersedia.

---

## 📜 DAFTAR PERINTAH `spark` PENTING

| Perintah                        | Fungsi                                                                 |
|--------------------------------|------------------------------------------------------------------------|
| `php spark serve`              | Menjalankan server lokal di `localhost:8080`                          |
| `php spark make:controller Nama`| Membuat file controller baru                                          |
| `php spark make:model Nama`    | Membuat file model baru                                               |
| `php spark make:migration Nama`| Membuat file migration                                                |
| `php spark migrate`            | Menjalankan semua file migration ke database                         |
| `php spark migrate:refresh`    | Menghapus semua tabel & jalankan ulang semua migration               |
| `php spark migrate:rollback`   | Mengembalikan (rollback) satu langkah migration                      |
| `php spark db:seed NamaSeeder` | Menjalankan file seeder untuk isi data awal                         |
| `php spark make:seeder Nama`   | Membuat file seeder baru                                             |
| `php spark routes`             | Menampilkan daftar routing aktif                                     |
| `php spark make:command Nama`  | Membuat custom CLI command                                           |
| `php spark cache:clear`        | Menghapus cache framework                                            |
| `php spark clear-logs`         | Menghapus file log                                                   |
| `php spark help`               | Menampilkan bantuan/perintah CLI                                     |

---

## 🛠️ CONTOH PENGGUNAAN

### 🔹 Membuat Controller
```bash
php spark make:controller Blog
```

### 🔹 Membuat Model
```bash
php spark make:model ArtikelModel
```

### 🔹 Membuat Migration
```bash
php spark make:migration CreateUsersTable
```

### 🔹 Menjalankan Seeder
```bash
php spark db:seed UserSeeder
```

---

## 🔥 TIPS

- Gunakan `--suffix` untuk menambahkan suffix ke nama file, misal:
  ```bash
  php spark make:model User --suffix
  ```
  Ini akan membuat `UserModel.php`.

- Perintah `spark` hanya bisa digunakan di terminal yang berada di direktori proyek CodeIgniter 4.

---