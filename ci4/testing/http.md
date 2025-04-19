### 📚 Materi: HTTP Testing di CodeIgniter 4

---

### 🔰 Apa itu HTTP Testing di CodeIgniter 4?

HTTP testing di CodeIgniter 4 adalah proses untuk menguji interaksi aplikasi web kamu dengan HTTP request dan response. Dengan menguji HTTP, kamu dapat memastikan bahwa aplikasi menghandle berbagai jenis request (GET, POST, PUT, DELETE) dengan benar, serta memeriksa response yang diberikan oleh aplikasi sesuai dengan harapan.

Di CodeIgniter 4, HTTP testing dilakukan dengan memanfaatkan **CodeIgniter Test Library** dan **PHPUnit** yang memungkinkan kita untuk melakukan simulasi HTTP request dan memeriksa output atau response dari aplikasi.

---

### 🛠️ Persiapan untuk HTTP Testing di CodeIgniter 4

#### 1. **Instalasi PHPUnit**

Jika kamu belum menginstal PHPUnit, kamu bisa menginstalnya melalui Composer dengan perintah berikut:

```bash
composer require --dev phpunit/phpunit
```

PHPUnit adalah framework testing yang digunakan di CodeIgniter 4 untuk pengujian unit maupun HTTP.

#### 2. **Menyiapkan Testing Environment**

Pengujian HTTP memerlukan **base URL** yang benar. Untuk itu, pastikan kamu telah mengonfigurasi `baseURL` di file `.env`:

```ini
CI_ENVIRONMENT = development
app.baseURL = 'http://localhost:8080'
```

Selain itu, kamu juga bisa membuat pengaturan database atau session untuk mendukung pengujian.

---

### 🧑‍💻 Menggunakan HTTP Testing di CodeIgniter 4

CodeIgniter 4 menyediakan beberapa fitur untuk melakukan testing terhadap HTTP request, termasuk fitur untuk mengirim request HTTP dan memeriksa response.

#### 1. **Membuat Test Case HTTP**

Untuk menguji HTTP request di CodeIgniter 4, kita akan menggunakan PHPUnit yang terintegrasi dengan **CodeIgniter HTTP Test Helper**.

Contoh pengujian HTTP menggunakan **CodeIgniter's TestCase**:

```php
<?php

namespace App\Tests;

use CodeIgniter\Test\CIUnitTestCase;

class UserTest extends CIUnitTestCase
{
    public function testIndexPage()
    {
        // Mengirimkan request GET ke URL
        $response = $this->get('/');

        // Memeriksa apakah response status code adalah 200 (OK)
        $response->assertStatus(200);

        // Memeriksa apakah ada teks dalam response body
        $response->assertSee('Welcome to CodeIgniter 4!');
    }

    public function testCreateUser()
    {
        // Data yang akan dikirim via POST
        $data = [
            'username' => 'john_doe',
            'email'    => 'john@example.com',
            'password' => '123456',
        ];

        // Mengirimkan request POST ke URL
        $response = $this->post('/user/create', $data);

        // Memeriksa apakah response status code adalah 201 (Created)
        $response->assertStatus(201);

        // Memeriksa apakah ada pesan di response body
        $response->assertSee('User created successfully');
    }
}
```

- **`$this->get()`**: Digunakan untuk mengirimkan HTTP request dengan metode GET ke endpoint yang ditentukan.
- **`$this->post()`**: Digunakan untuk mengirimkan HTTP request dengan metode POST.
- **`assertStatus()`**: Digunakan untuk memeriksa apakah status code dari response sesuai dengan yang diharapkan.
- **`assertSee()`**: Digunakan untuk memeriksa apakah string tertentu ada dalam body response.

#### 2. **Menjalankan HTTP Test**

Untuk menjalankan HTTP test, kamu bisa menggunakan perintah berikut di terminal:

```bash
php spark test
```

Perintah ini akan menjalankan semua unit tests, termasuk HTTP testing, dan menunjukkan hasilnya di terminal.

#### 3. **Test Case HTTP dengan Headers dan Cookies**

Terkadang kamu perlu mengirimkan HTTP request dengan headers atau cookies khusus. Berikut adalah contoh mengirim request dengan header dan cookies:

```php
<?php

namespace App\Tests;

use CodeIgniter\Test\CIUnitTestCase;

class UserTest extends CIUnitTestCase
{
    public function testUserLogin()
    {
        // Data login
        $data = [
            'username' => 'john_doe',
            'password' => '123456',
        ];

        // Mengirimkan request POST dengan header
        $response = $this->withHeader('Content-Type', 'application/json')
                         ->post('/user/login', $data);

        // Memeriksa apakah response status code adalah 200 (OK)
        $response->assertStatus(200);

        // Memeriksa apakah ada token di response body
        $response->assertJsonFragment(['token' => 'some_token_value']);
    }

    public function testSetCookie()
    {
        // Mengirimkan request GET dan menerima cookie
        $response = $this->get('/set-cookie');

        // Memeriksa apakah cookie 'user_session' ada
        $response->assertCookie('user_session');
    }
}
```

- **`withHeader()`**: Menambahkan header khusus untuk HTTP request.
- **`assertJsonFragment()`**: Memeriksa apakah respons JSON mengandung fragmen tertentu (misalnya token).
- **`assertCookie()`**: Memeriksa apakah cookie tertentu ada di response.

#### 4. **Testing Route dengan HTTP**

CodeIgniter 4 memungkinkan kita untuk menguji route HTTP secara langsung. Ini memudahkan untuk memeriksa apakah route yang sudah didefinisikan berfungsi dengan baik.

```php
<?php

namespace App\Tests;

use CodeIgniter\Test\CIUnitTestCase;

class RouteTest extends CIUnitTestCase
{
    public function testRoute()
    {
        // Memeriksa apakah route '/user/create' mengarah ke controller yang benar
        $this->assertTrue(route_is('user/create', 'UserController::create'));
    }
}
```

- **`route_is()`**: Digunakan untuk memeriksa apakah route yang didefinisikan sesuai dengan controller yang dituju.

---

### ⚡ Tips untuk HTTP Testing di CodeIgniter 4

- **Gunakan Mocking**: Untuk menghindari interaksi langsung dengan database atau API eksternal, kamu bisa menggunakan mocking untuk mensimulasikan respon dari HTTP request.
- **Autentikasi dan Pengguna**: Jika aplikasi memerlukan autentikasi, pastikan untuk menambahkan token atau cookie session saat melakukan testing, menggunakan **`withHeader()`** atau **`withCookie()`**.
- **Jalankan secara Otomatis**: Kamu bisa mengonfigurasi CI4 untuk menjalankan pengujian HTTP secara otomatis melalui CI/CD pipeline, seperti GitHub Actions atau GitLab CI.
- **Testing JSON Response**: Jika aplikasi menggunakan JSON untuk berinteraksi, gunakan `assertJson()` dan `assertJsonFragment()` untuk memeriksa apakah data yang dikirimkan sesuai.

---

### 📘 Dokumentasi Resmi

Untuk informasi lebih lanjut tentang HTTP Testing di CodeIgniter 4, kamu bisa merujuk ke dokumentasi resmi:

- [CodeIgniter 4 HTTP Testing](https://codeigniter4.github.io/userguide/testing/http.html)

---

### 💡 Kesimpulan

HTTP testing di CodeIgniter 4 memungkinkan kamu untuk memverifikasi apakah aplikasi dapat menangani berbagai jenis request dan menghasilkan response yang sesuai. Dengan menggunakan PHPUnit dan helper **CodeIgniter Test**, kamu dapat menulis pengujian yang mencakup request GET, POST, serta memeriksa response, header, cookies, dan JSON data. Pengujian ini sangat penting untuk memastikan aplikasi web kamu bekerja sesuai harapan.

Jika ada pertanyaan atau butuh penjelasan lebih lanjut, beri tahu saya!