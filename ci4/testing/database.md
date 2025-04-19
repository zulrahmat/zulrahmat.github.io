### 📚 Materi: Database Testing di CodeIgniter 4

---

### 🔰 Apa itu Database Testing di CodeIgniter 4?

Database testing di CodeIgniter 4 adalah bagian penting dari pengujian aplikasi untuk memastikan bahwa operasi database berjalan dengan benar. Dengan menggunakan framework ini, kamu dapat menguji interaksi aplikasi dengan database seperti query `SELECT`, `INSERT`, `UPDATE`, dan `DELETE`. Database testing ini dapat dilakukan dengan memanfaatkan unit testing yang ada di CodeIgniter 4, dan beberapa tools tambahan seperti **CodeIgniter Testing Library** dan **PHPUnit**.

---

### 🛠️ Persiapan untuk Database Testing di CodeIgniter 4

#### 1. **Instalasi PHPUnit**

CodeIgniter 4 menggunakan **PHPUnit** untuk melakukan unit testing. Jika PHPUnit belum diinstal, kamu bisa menginstalnya melalui **Composer**:

```bash
composer require --dev phpunit/phpunit
```

Setelah itu, kamu dapat menjalankan PHPUnit di aplikasi CodeIgniter 4.

#### 2. **Konfigurasi Database untuk Testing**

Saat melakukan pengujian, kamu tidak ingin berinteraksi langsung dengan database produksi. Oleh karena itu, kamu perlu mengonfigurasi database khusus untuk pengujian.

Buka file `.env` di root folder proyek dan atur pengaturan database untuk testing. Misalnya:

```ini
# Database Testing Configuration
database.default.hostname = localhost
database.default.database = ci4_test_db
database.default.username = root
database.default.password = 
database.default.DBDriver = MySQLi
```

Pastikan untuk membuat database `ci4_test_db` terlebih dahulu agar pengujian tidak mencampuri data di database produksi.

#### 3. **Autoloading Testing Library**

CodeIgniter 4 sudah menyediakan library untuk testing. Untuk mengaktifkan autoloading, buka file `app/config/Autoload.php` dan pastikan untuk memuat `Test` di bagian `libraries`:

```php
public $libraries = ['database'];
```

---

### 🧑‍💻 Menggunakan Database untuk Unit Testing di CodeIgniter 4

Setelah mengonfigurasi database untuk pengujian, kamu bisa mulai menulis test case yang berinteraksi dengan database.

#### 1. **Membuat Test Case untuk Database**

Untuk membuat test case di CodeIgniter 4, kamu perlu membuat file di folder `tests/_support/Database`. Berikut adalah langkah-langkah untuk membuat dan menjalankan pengujian database.

- **Contoh Test Case:**

  Buat file pengujian di `tests/Database/UserTest.php`.

```php
<?php

namespace App\Tests\Database;

use CodeIgniter\Test\DatabaseTestTrait;
use CodeIgniter\Test\CIUnitTestCase;

class UserTest extends CIUnitTestCase
{
    use DatabaseTestTrait;

    public function testInsertUser()
    {
        // Data yang akan dimasukkan
        $data = [
            'username' => 'john_doe',
            'email'    => 'john@example.com',
            'password' => password_hash('123456', PASSWORD_BCRYPT),
        ];

        // Melakukan insert
        $this->db->table('users')->insert($data);

        // Mengecek apakah data berhasil dimasukkan
        $user = $this->db->table('users')->where('username', 'john_doe')->first();
        $this->assertNotEmpty($user);
        $this->assertEquals('john_doe', $user['username']);
    }

    public function testDeleteUser()
    {
        // Data untuk insert
        $data = [
            'username' => 'jane_doe',
            'email'    => 'jane@example.com',
            'password' => password_hash('abcdef', PASSWORD_BCRYPT),
        ];

        // Melakukan insert
        $this->db->table('users')->insert($data);

        // Melakukan delete
        $this->db->table('users')->where('username', 'jane_doe')->delete();

        // Mengecek apakah data berhasil dihapus
        $user = $this->db->table('users')->where('username', 'jane_doe')->first();
        $this->assertEmpty($user);
    }
}
```

- **Penjelasan:**
  - **`DatabaseTestTrait`**: Ini adalah trait yang memungkinkan kamu untuk menggunakan operasi database dalam pengujian.
  - **`insert()`**: Digunakan untuk memasukkan data ke dalam tabel.
  - **`where()`**: Digunakan untuk mencari data berdasarkan kondisi tertentu.
  - **`assertNotEmpty()`**: Memastikan bahwa data yang dimasukkan ada di database.
  - **`assertEquals()`**: Memastikan bahwa nilai yang diharapkan sesuai dengan nilai yang ditemukan di database.

#### 2. **Menjalankan Test Case**

Untuk menjalankan test case, kamu bisa menggunakan perintah berikut:

```bash
php spark test
```

Perintah ini akan menjalankan semua test yang ada di folder `tests` dan melaporkan hasilnya.

#### 3. **Menjalankan Test dengan Database Seeder**

Jika kamu membutuhkan data tertentu untuk pengujian, kamu bisa menggunakan Seeder untuk mengisi database sebelum pengujian dimulai. Contoh menggunakan Seeder dalam test:

```php
<?php

namespace App\Tests\Database;

use CodeIgniter\Test\DatabaseTestTrait;
use CodeIgniter\Test\CIUnitTestCase;

class UserTest extends CIUnitTestCase
{
    use DatabaseTestTrait;

    public function setUp(): void
    {
        parent::setUp();
        // Menjalankan seeder sebelum pengujian dimulai
        $this->runSeeder('UserSeeder');
    }

    public function testUserData()
    {
        $user = $this->db->table('users')->where('username', 'john_doe')->first();
        $this->assertEquals('john_doe', $user['username']);
    }
}
```

- **`setUp()`**: Fungsi ini digunakan untuk melakukan persiapan sebelum setiap pengujian dijalankan. Di sini, kita memanggil seeder untuk mengisi database dengan data awal.

#### 4. **Menggunakan Database untuk Pengujian Model**

Selain menguji query langsung, kamu juga bisa menguji **Model** CodeIgniter 4. Misalnya:

```php
<?php

namespace App\Tests\Database;

use App\Models\UserModel;
use CodeIgniter\Test\DatabaseTestTrait;
use CodeIgniter\Test\CIUnitTestCase;

class UserModelTest extends CIUnitTestCase
{
    use DatabaseTestTrait;

    protected $userModel;

    protected function setUp(): void
    {
        parent::setUp();
        $this->userModel = new UserModel();
    }

    public function testInsertUser()
    {
        $user = [
            'username' => 'test_user',
            'email'    => 'test@example.com',
            'password' => password_hash('123456', PASSWORD_BCRYPT),
        ];

        $this->userModel->insert($user);

        $insertedUser = $this->userModel->where('username', 'test_user')->first();

        $this->assertNotEmpty($insertedUser);
        $this->assertEquals('test_user', $insertedUser['username']);
    }
}
```

Di sini kita menguji Model `UserModel` untuk melakukan operasi `insert` dan memastikan data berhasil dimasukkan ke dalam database.

---

### ⚡ Tips untuk Database Testing di CodeIgniter 4

- **Isolasi Pengujian**: Gunakan database khusus untuk pengujian sehingga tidak mengganggu data produksi.
- **Gunakan Transaction**: Untuk menghindari perubahan data yang tidak diinginkan, kamu bisa menggunakan transaksi untuk rollback perubahan setelah pengujian selesai.
- **Seeder untuk Data Dummy**: Gunakan Seeder untuk mengisi database dengan data yang diperlukan sebelum pengujian dilakukan.
- **Test SetUp dan TearDown**: Gunakan `setUp()` dan `tearDown()` untuk memastikan bahwa setiap pengujian dimulai dengan kondisi yang bersih.

---

### 📘 Dokumentasi Resmi

Untuk informasi lebih lanjut tentang pengujian database di CodeIgniter 4, kamu bisa merujuk ke dokumentasi resmi:

- [CodeIgniter 4 Database Testing](https://codeigniter4.github.io/userguide/testing/database.html)

---

### 💡 Kesimpulan

Database testing di CodeIgniter 4 memungkinkan kamu untuk memverifikasi bahwa operasi database berjalan dengan benar, apakah itu melalui query langsung atau melalui model. Dengan PHPUnit dan fitur **DatabaseTestTrait**, kamu dapat dengan mudah melakukan pengujian dan memastikan bahwa interaksi dengan database sesuai harapan, baik dalam lingkungan pengujian lokal maupun pengembangan.

Jika ada pertanyaan atau butuh klarifikasi lebih lanjut, beri tahu saya!