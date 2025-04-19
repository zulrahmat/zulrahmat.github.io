### 📚 Materi: Migration di CodeIgniter 4

---

### 🔰 Apa itu Migration di CodeIgniter 4?

Migration di CodeIgniter 4 adalah fitur yang memungkinkan kamu untuk mengelola perubahan struktur database (seperti pembuatan tabel, penambahan kolom, atau pengubahan tipe data) secara sistematis dan terstruktur. Migration memungkinkan tim pengembangan untuk memelihara konsistensi struktur database antara berbagai lingkungan pengembangan dan produksi. Hal ini juga memudahkan dalam mengelola dan melacak perubahan-perubahan pada database.

---

### 🛠️ Keuntungan Menggunakan Migration

- **Menjaga Konsistensi**: Dengan migration, kamu dapat memastikan bahwa struktur database di setiap lingkungan (pengembangan, staging, produksi) selalu konsisten.
- **Mudah Dikelola**: Menambahkan, mengubah, dan menghapus struktur database dilakukan melalui file migration yang mudah dikelola.
- **Mudah Ditindaklanjuti**: Setiap perubahan pada database dapat dilacak dengan file migration yang terstruktur.
- **Mudah Dikembalikan (Rollback)**: Kamu dapat dengan mudah mengembalikan perubahan database menggunakan perintah rollback.

---

### 🔧 Langkah-Langkah Menggunakan Migration di CodeIgniter 4

#### 1. **Mengaktifkan Migration di CodeIgniter 4**

Sebelum mulai menggunakan migration, kamu harus mengaktifkan fitur migration di CodeIgniter 4.

1. **Aktifkan Migration di file konfigurasi**:

   Buka file `app/config/Database.php` dan pastikan bagian `migration` sudah diaktifkan.

   ```php
   public $migrationEnabled = true;
   public $migrationType = 'timestamp'; // Bisa juga menggunakan 'integer'
   public $migrationTable = 'migrations'; // Nama tabel tempat menyimpan informasi migrasi
   public $migrationPath = APPPATH . 'Database/Migrations'; // Path tempat menyimpan file migrasi
   ```

   - **`migrationEnabled`**: Menentukan apakah migrasi diaktifkan atau tidak.
   - **`migrationType`**: Menentukan cara penamaan file migrasi. Pilihan yang tersedia adalah `'timestamp'` atau `'integer'`.
   - **`migrationTable`**: Nama tabel yang digunakan untuk menyimpan informasi migrasi yang sudah dijalankan.
   - **`migrationPath`**: Lokasi file migrasi.

---

#### 2. **Membuat Migration**

Setelah mengaktifkan fitur migration, kamu bisa mulai membuat file migration.

1. **Buat file migration**:

   File migration harus berada di dalam folder `app/Database/Migrations/`. Kamu bisa membuatnya secara manual atau menggunakan perintah artisan di terminal.

   Untuk membuat file migration secara otomatis, jalankan perintah berikut:

   ```bash
   php spark make:migration create_users_table
   ```

   Perintah ini akan menghasilkan file migration dengan nama yang mengandung timestamp dan nama migrasi (`create_users_table`), yang akan disimpan di folder `app/Database/Migrations/`.

2. **Struktur File Migration**:

   File migration memiliki dua fungsi utama:
   - **`up()`**: Digunakan untuk membuat perubahan pada database (misalnya membuat tabel, menambah kolom, dsb).
   - **`down()`**: Digunakan untuk mengembalikan perubahan yang dilakukan pada database (misalnya menghapus tabel atau kolom).

   **Contoh file migration untuk membuat tabel `users`:**

   ```php
   <?php

   namespace App\Database\Migrations;

   use CodeIgniter\Database\Migration;

   class CreateUsersTable extends Migration
   {
       public function up()
       {
           // Membuat tabel users
           $this->forge->addField([
               'id' => [
                   'type' => 'INT',
                   'constraint' => 5,
                   'unsigned' => true,
                   'auto_increment' => true,
               ],
               'username' => [
                   'type' => 'VARCHAR',
                   'constraint' => '100',
               ],
               'email' => [
                   'type' => 'VARCHAR',
                   'constraint' => '100',
               ],
               'password' => [
                   'type' => 'VARCHAR',
                   'constraint' => '255',
               ],
           ]);
           $this->forge->addKey('id', true); // Menambahkan primary key
           $this->forge->createTable('users'); // Membuat tabel users
       }

       public function down()
       {
           // Menghapus tabel users
           $this->forge->dropTable('users');
       }
   }
   ```

   - **`addField()`**: Digunakan untuk mendefinisikan kolom-kolom dalam tabel.
   - **`addKey()`**: Menambahkan key atau index, dalam hal ini primary key.
   - **`createTable()`**: Membuat tabel baru di database.
   - **`dropTable()`**: Menghapus tabel dari database.

---

#### 3. **Menjalankan Migration**

Setelah membuat file migration, kamu bisa menjalankan migration untuk membuat perubahan pada database.

1. **Jalankan Migration**:

   Untuk menjalankan semua migration yang belum diterapkan, jalankan perintah berikut di terminal:

   ```bash
   php spark migrate
   ```

   Ini akan menjalankan semua migration yang ada dan belum diterapkan di database.

2. **Rollback Migration**:

   Jika kamu perlu mengembalikan (rollback) perubahan yang telah diterapkan oleh migration, kamu bisa menggunakan perintah berikut:

   ```bash
   php spark migrate:rollback
   ```

   Ini akan menjalankan method `down()` pada migration terakhir yang diterapkan.

3. **Rollback Semua Migration**:

   Jika kamu ingin mengembalikan semua perubahan migration (reset database), jalankan perintah berikut:

   ```bash
   php spark migrate:reset
   ```

---

#### 4. **Melihat Status Migration**

Untuk memeriksa status migration, apakah sudah diterapkan atau belum, kamu bisa menggunakan perintah berikut:

```bash
php spark migrate:status
```

Ini akan menampilkan daftar migration yang telah diterapkan dan yang belum diterapkan.

---

### 📝 Contoh Lengkap Penggunaan Migration

1. **Membuat Migration untuk Menambah Kolom**

Misalnya, kamu ingin menambah kolom `created_at` dan `updated_at` ke dalam tabel `users`. Kamu bisa membuat file migration baru dengan nama `add_timestamp_to_users_table.php`.

```php
<?php

namespace App\Database\Migrations;

use CodeIgniter\Database\Migration;

class AddTimestampToUsersTable extends Migration
{
    public function up()
    {
        // Menambah kolom created_at dan updated_at ke tabel users
        $this->forge->addColumn('users', [
            'created_at' => [
                'type' => 'DATETIME',
                'null' => true,
            ],
            'updated_at' => [
                'type' => 'DATETIME',
                'null' => true,
            ],
        ]);
    }

    public function down()
    {
        // Menghapus kolom created_at dan updated_at
        $this->forge->dropColumn('users', 'created_at');
        $this->forge->dropColumn('users', 'updated_at');
    }
}
```

Jalankan migration ini untuk menambah kolom dengan perintah:

```bash
php spark migrate
```

Jika kamu perlu menghapus perubahan tersebut, jalankan rollback:

```bash
php spark migrate:rollback
```

---

### 🔑 Best Practices untuk Menggunakan Migration

| Praktik Terbaik | Penjelasan |
|-----------------|------------|
| **Gunakan Timestamp pada Nama File** | Gunakan timestamp untuk penamaan file migration agar urutannya terjaga dengan baik. |
| **Buat Migration Terkait dengan Fitur** | Pisahkan migration berdasarkan fitur atau modul untuk memudahkan pemeliharaan dan pemahaman. |
| **Selalu Gunakan `down()` untuk Rollback** | Pastikan selalu mendefinisikan method `down()` untuk mengembalikan perubahan ketika dibutuhkan. |
| **Jangan Mengubah File Migration yang Sudah Dijalankan** | Jangan mengubah file migration yang sudah dijalankan di lingkungan produksi karena bisa menyebabkan masalah konsistensi. Buat migration baru jika diperlukan perubahan.

---

### 📘 Dokumentasi Resmi

Untuk informasi lebih lanjut mengenai migration di CodeIgniter 4, kamu dapat merujuk ke dokumentasi resmi:

- [CodeIgniter 4 Migration](https://codeigniter4.github.io/userguide/cli/migrations.html)

---

### 💡 Kesimpulan

Migration di CodeIgniter 4 adalah fitur yang memungkinkan kamu untuk mengelola perubahan struktur database secara sistematis dan terstruktur. Dengan menggunakan migration, kamu dapat dengan mudah membuat dan mengelola tabel, kolom, dan perubahan lainnya, serta memastikan konsistensi database di berbagai lingkungan.

Jika ada yang ingin didalami lebih lanjut atau ada yang kurang jelas, beri tahu aku!