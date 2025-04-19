### 📚 Materi: **Mocking** dalam Unit Testing di CodeIgniter 4

---

### 🔰 Apa itu Mocking dalam Testing?

**Mocking** adalah teknik dalam unit testing di mana kita membuat objek tiruan (mock objects) untuk menggantikan objek nyata, seperti model, service, atau dependensi lain yang digunakan dalam aplikasi. Tujuan dari mocking adalah untuk mengisolasi bagian tertentu dari aplikasi yang sedang diuji, sehingga kita bisa memverifikasi bahwa komponen tersebut berfungsi sebagaimana mestinya tanpa mengakses dependensi eksternal, seperti database atau API.

Di CodeIgniter 4, kamu dapat menggunakan mocking untuk menggantikan interaksi dengan model atau objek lain dalam controller atau service.

---

### 🧑‍💻 Menggunakan Mocking di CodeIgniter 4

CodeIgniter 4 tidak memiliki pustaka mocking built-in seperti PHPUnit, tetapi kamu tetap bisa membuat mock menggunakan **PHPUnit mocking capabilities**. Sebagai contoh, jika controller atau service kamu bergantung pada model, kamu bisa membuat mock model untuk menghindari akses database nyata saat melakukan pengujian.

Berikut adalah cara untuk menggunakan mocking di CodeIgniter 4 dalam pengujian controller.

---

### 🛠️ Langkah-Langkah untuk Menggunakan Mocking di CodeIgniter 4

#### 1. **Instalasi PHPUnit**

Pastikan PHPUnit sudah terpasang di proyek kamu. Jika belum, kamu bisa menginstalnya menggunakan Composer:

```bash
composer require --dev phpunit/phpunit
```

#### 2. **Membuat Test Case dengan Mocking**

Misalkan kamu memiliki controller `UserController` yang bergantung pada model `UserModel`. Kita akan membuat mock untuk `UserModel` dalam test controller.

**Contoh Controller**: `UserController`

```php
<?php

namespace App\Controllers;

use App\Models\UserModel;

class UserController extends BaseController
{
    public function create()
    {
        $model = new UserModel();
        
        $userData = $this->request->getPost();
        
        if ($model->save($userData)) {
            return $this->response->setStatusCode(201)->setBody('User created successfully');
        } else {
            return $this->response->setStatusCode(400)->setBody('Failed to create user');
        }
    }
}
```

**Test Case dengan Mocking untuk `UserController`**:

```php
<?php

namespace App\Tests;

use CodeIgniter\Test\CIUnitTestCase;
use CodeIgniter\Test\Mock\MockModel;
use App\Models\UserModel;

class UserControllerTest extends CIUnitTestCase
{
    public function testCreateUser()
    {
        // Membuat mock untuk UserModel
        $mockUserModel = $this->createMock(UserModel::class);
        
        // Mengatur agar method save() mengembalikan true
        $mockUserModel->method('save')->willReturn(true);
        
        // Mengganti instance UserModel di controller dengan mock model
        $this->instance(UserModel::class, $mockUserModel);
        
        // Data untuk request
        $data = [
            'username' => 'johndoe',
            'email'    => 'john@example.com',
            'password' => 'password123',
        ];
        
        // Mengirimkan request POST ke controller
        $response = $this->post('/user/create', $data);
        
        // Memeriksa status code respons
        $response->assertStatus(201);
        
        // Memeriksa apakah respons mengandung pesan yang sesuai
        $response->assertSee('User created successfully');
    }
}
```

**Penjelasan**:
1. **Mocking Model**: Kita menggunakan **`createMock()`** dari PHPUnit untuk membuat objek tiruan dari `UserModel`.
2. **Mengatur Return Value**: Dengan **`method('save')->willReturn(true)`**, kita mengatur bahwa ketika method `save()` dipanggil, ia akan mengembalikan `true` sebagai respons, seolah-olah data berhasil disimpan tanpa mengakses database.
3. **Mengganti Model di Controller**: **`$this->instance()`** digunakan untuk menggantikan model `UserModel` dengan mock model di controller.
4. **Mengirimkan Request**: Kita menggunakan `$this->post()` untuk mengirim request POST ke controller dan memeriksa hasilnya.

---

### 🎯 Keuntungan Mocking dalam Unit Testing

1. **Isolasi Pengujian**: Dengan mocking, kamu dapat mengisolasi bagian controller yang sedang diuji dan menghindari pengaruh dari dependensi seperti database atau API eksternal.
2. **Meningkatkan Kecepatan Test**: Tanpa perlu berinteraksi dengan database atau server eksternal, pengujian bisa lebih cepat.
3. **Kontrol Terhadap Output**: Mocking memungkinkan kamu untuk mengontrol nilai yang dikembalikan oleh objek dependensi, seperti model, sehingga kamu dapat menguji berbagai skenario tanpa tergantung pada data yang sebenarnya.
4. **Fleksibilitas**: Kamu dapat menguji controller dengan berbagai hasil yang berbeda dari dependensi menggunakan mocking. Misalnya, kamu bisa menguji respons yang berbeda jika model mengembalikan `true` atau `false`.

---

### 🛠️ Mocking Lain yang Bisa Digunakan

Selain mocking model, kamu juga bisa melakukan mocking terhadap:

- **Service**: Jika controller bergantung pada service, kamu bisa membuat mock untuk service tersebut.
- **Database**: Jika controller melakukan query database, kamu bisa mock model untuk mencegah query asli dijalankan.
- **HTTP Requests**: Jika controller melakukan panggilan HTTP eksternal, kamu bisa mock library HTTP seperti `CodeIgniter\HTTP\CURLRequest`.

---

### 🧑‍💻 Contoh Mocking untuk Service

Jika controller kamu bergantung pada service eksternal, kamu juga bisa menggunakan mocking untuk service tersebut.

**Contoh Service**: `UserService`

```php
<?php

namespace App\Services;

use App\Models\UserModel;

class UserService
{
    protected $userModel;

    public function __construct(UserModel $userModel)
    {
        $this->userModel = $userModel;
    }

    public function createUser(array $data)
    {
        return $this->userModel->save($data);
    }
}
```

**Controller yang Menggunakan `UserService`**:

```php
<?php

namespace App\Controllers;

use App\Services\UserService;

class UserController extends BaseController
{
    protected $userService;

    public function __construct(UserService $userService)
    {
        $this->userService = $userService;
    }

    public function create()
    {
        $data = $this->request->getPost();
        
        if ($this->userService->createUser($data)) {
            return $this->response->setStatusCode(201)->setBody('User created successfully');
        } else {
            return $this->response->setStatusCode(400)->setBody('Failed to create user');
        }
    }
}
```

**Test Case untuk Controller dengan Mocking Service**:

```php
<?php

namespace App\Tests;

use CodeIgniter\Test\CIUnitTestCase;
use App\Services\UserService;
use App\Models\UserModel;

class UserControllerTest extends CIUnitTestCase
{
    public function testCreateUserWithServiceMocking()
    {
        // Mock UserModel
        $mockUserModel = $this->createMock(UserModel::class);
        $mockUserModel->method('save')->willReturn(true);

        // Mock UserService dengan mock UserModel
        $mockUserService = $this->createMock(UserService::class);
        $mockUserService->method('createUser')->willReturn(true);

        // Mengganti instance service di controller dengan mock service
        $this->instance(UserService::class, $mockUserService);

        // Data untuk request
        $data = [
            'username' => 'johndoe',
            'email'    => 'john@example.com',
            'password' => 'password123',
        ];

        // Mengirimkan request POST ke controller
        $response = $this->post('/user/create', $data);

        // Memeriksa status code respons
        $response->assertStatus(201);
        
        // Memeriksa apakah respons mengandung pesan yang sesuai
        $response->assertSee('User created successfully');
    }
}
```

---

### ⚡ Kesimpulan

Mocking adalah teknik yang sangat berguna dalam unit testing untuk memastikan bahwa setiap komponen diuji secara terpisah tanpa bergantung pada bagian lain seperti database atau service eksternal. Dengan menggunakan mocking, kita dapat mengontrol output dari dependensi dan mengisolasi komponen yang sedang diuji. Di CodeIgniter 4, kita bisa menggunakan PHPUnit untuk melakukan mocking pada objek, model, atau service yang digunakan dalam controller, sehingga pengujian menjadi lebih terfokus dan cepat.

Jika ada yang ingin kamu tanyakan lebih lanjut atau contoh lainnya, beri tahu saja! 😄