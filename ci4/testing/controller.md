### 📚 Materi: Controller Testing di CodeIgniter 4

---

### 🔰 Apa itu Controller Testing di CodeIgniter 4?

Controller testing adalah proses untuk menguji **Controller** di aplikasi CodeIgniter 4. Controller bertanggung jawab untuk menangani request dari pengguna dan mengarahkan respons ke tampilan atau data yang sesuai. Dengan melakukan controller testing, kita dapat memastikan bahwa controller berfungsi sebagaimana mestinya, baik dalam hal pemrosesan data, pengelolaan input, atau pengiriman response.

Di CodeIgniter 4, controller testing dilakukan dengan menggunakan **PHPUnit** yang terintegrasi dengan framework untuk melakukan unit testing. Pengujian controller bertujuan untuk memastikan bahwa route, method, dan logika yang ada di controller bekerja dengan baik dan memberikan respons yang benar.

---

### 🛠️ Persiapan untuk Controller Testing

#### 1. **Instalasi PHPUnit**

Jika kamu belum menginstal PHPUnit, kamu dapat menginstalnya dengan Composer:

```bash
composer require --dev phpunit/phpunit
```

PHPUnit adalah framework testing yang digunakan untuk menulis dan menjalankan unit test, termasuk pengujian controller.

#### 2. **Menyiapkan Testing Environment**

Pengujian controller memerlukan pengaturan aplikasi yang mendekati lingkungan produksi. Untuk itu, pastikan kamu sudah mengonfigurasi **`baseURL`** dan pengaturan lainnya di file `.env`:

```ini
CI_ENVIRONMENT = development
app.baseURL = 'http://localhost:8080'
```

---

### 🧑‍💻 Menggunakan Controller Testing di CodeIgniter 4

Untuk menguji controller, kita akan menggunakan **CodeIgniter Test Library** yang disediakan untuk melakukan request HTTP terhadap controller dan memeriksa apakah hasilnya sesuai harapan.

#### 1. **Membuat Test Case Controller**

Test controller di CodeIgniter 4 dapat dilakukan dengan menulis class yang mewarisi `CIUnitTestCase`. Berikut adalah contoh pengujian controller sederhana:

```php
<?php

namespace App\Tests;

use CodeIgniter\Test\CIUnitTestCase;

class UserControllerTest extends CIUnitTestCase
{
    public function testIndex()
    {
        // Mengirimkan request GET ke route '/user'
        $response = $this->get('/user');

        // Memeriksa apakah response status code adalah 200 (OK)
        $response->assertStatus(200);

        // Memeriksa apakah respons mengandung teks tertentu
        $response->assertSee('List of Users');
    }

    public function testCreate()
    {
        // Mengirimkan data POST untuk membuat user baru
        $data = [
            'username' => 'johndoe',
            'email'    => 'john@example.com',
            'password' => 'password123',
        ];

        $response = $this->post('/user/create', $data);

        // Memeriksa apakah response status code adalah 201 (Created)
        $response->assertStatus(201);

        // Memeriksa apakah respons mengandung pesan tertentu
        $response->assertSee('User created successfully');
    }

    public function testUpdate()
    {
        // Mengirimkan data PUT untuk mengupdate user dengan ID 1
        $data = [
            'username' => 'johndoe_updated',
            'email'    => 'john_updated@example.com',
        ];

        $response = $this->put('/user/update/1', $data);

        // Memeriksa apakah response status code adalah 200 (OK)
        $response->assertStatus(200);

        // Memeriksa apakah respons mengandung teks tertentu
        $response->assertSee('User updated successfully');
    }

    public function testDelete()
    {
        // Mengirimkan request DELETE untuk menghapus user dengan ID 1
        $response = $this->delete('/user/delete/1');

        // Memeriksa apakah response status code adalah 200 (OK)
        $response->assertStatus(200);

        // Memeriksa apakah respons mengandung pesan tertentu
        $response->assertSee('User deleted successfully');
    }
}
```

Penjelasan dari contoh di atas:

- **`$this->get()`**: Mengirimkan request HTTP GET ke route yang ditentukan.
- **`$this->post()`**: Mengirimkan request HTTP POST dengan data tertentu.
- **`$this->put()`**: Mengirimkan request HTTP PUT dengan data tertentu.
- **`$this->delete()`**: Mengirimkan request HTTP DELETE.
- **`assertStatus()`**: Memastikan bahwa status code dari response sesuai dengan yang diharapkan (misalnya 200, 201).
- **`assertSee()`**: Memeriksa apakah respons mengandung string tertentu, yang dapat digunakan untuk memeriksa apakah tampilan atau pesan yang tepat ditampilkan.

#### 2. **Menjalankan Test Case**

Untuk menjalankan semua test, termasuk controller testing, kamu dapat menggunakan perintah `spark test`:

```bash
php spark test
```

Ini akan menjalankan semua test yang ada dalam aplikasi, termasuk pengujian controller.

---

### ⚡ Tips untuk Controller Testing di CodeIgniter 4

- **Penggunaan Mocking**: Jika controller kamu bergantung pada model atau service lain, pertimbangkan untuk menggunakan mocking untuk menghindari interaksi langsung dengan database. Ini dapat membantu mempercepat pengujian dan memastikan pengujian unit.
- **Memeriksa Respons JSON**: Jika controller kamu menghasilkan output dalam format JSON, kamu bisa menggunakan metode `assertJsonFragment()` untuk memverifikasi bahwa respons JSON berisi data yang diinginkan.
- **Autentikasi**: Jika controller mengharuskan pengguna untuk terautentikasi, pastikan untuk menambahkan token atau session dalam header request menggunakan `withHeader()` atau `withCookie()`.
- **Menggunakan Database dalam Test**: Untuk pengujian yang melibatkan data, pastikan kamu mengonfigurasi database testing dengan benar di environment test.
- **Test Response Body**: Selain memeriksa status code, kamu bisa memeriksa seluruh body respons untuk memastikan bahwa data yang diberikan controller sesuai dengan yang diharapkan.

---

### 🧑‍💻 Contoh Mocking di Controller Testing

Jika controller kamu bergantung pada model, kamu bisa menggunakan mocking untuk menghindari interaksi langsung dengan database. Berikut adalah contoh penggunaan mocking di controller test:

```php
<?php

namespace App\Tests;

use CodeIgniter\Test\CIUnitTestCase;
use CodeIgniter\Test\Mock\MockModel;
use App\Models\UserModel;

class UserControllerTest extends CIUnitTestCase
{
    public function testCreateWithMockModel()
    {
        // Mock model UserModel
        $mockUserModel = new MockModel(UserModel::class);
        $mockUserModel->setReturnValue('create', true);

        // Menggunakan mock model di controller
        $this->instance(UserModel::class, $mockUserModel);

        // Data untuk request
        $data = [
            'username' => 'johndoe',
            'email'    => 'john@example.com',
            'password' => 'password123',
        ];

        // Mengirimkan request POST
        $response = $this->post('/user/create', $data);

        // Memeriksa response
        $response->assertStatus(201);
        $response->assertSee('User created successfully');
    }
}
```

Penjelasan:
- **Mocking** memungkinkan kita untuk menggantikan implementasi model dengan versi palsu yang mengembalikan data yang diinginkan tanpa mengakses database.

---

### 📘 Dokumentasi Resmi

Untuk mempelajari lebih lanjut tentang pengujian di CodeIgniter 4, kamu bisa merujuk ke dokumentasi resmi:

- [CodeIgniter 4 Testing Documentation](https://codeigniter4.github.io/userguide/testing/index.html)

---

### 💡 Kesimpulan

Controller testing di CodeIgniter 4 memungkinkan kamu untuk memverifikasi bahwa controller dapat menangani request HTTP dengan benar, memproses data dengan benar, dan memberikan respons yang sesuai. Dengan menggunakan PHPUnit dan CodeIgniter Test Library, kamu dapat menulis pengujian yang mencakup berbagai metode HTTP (GET, POST, PUT, DELETE), serta memeriksa status code, konten response, dan interaksi dengan model atau service.

Jika ada pertanyaan atau butuh penjelasan lebih lanjut, beri tahu saya!