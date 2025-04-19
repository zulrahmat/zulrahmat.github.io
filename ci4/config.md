### 📚 Materi: Config di CodeIgniter 4

---

### 🔰 Apa itu Config di CodeIgniter 4?

Konfigurasi (Config) di CodeIgniter 4 adalah sekumpulan pengaturan yang digunakan untuk mengelola berbagai parameter aplikasi, seperti database, email, session, URL, dan pengaturan lainnya yang mempengaruhi cara aplikasi berfungsi. File konfigurasi digunakan untuk mengatur berbagai pengaturan dan memastikan aplikasi berfungsi dengan baik dalam berbagai lingkungan (development, staging, produksi).

---

### 🛠️ File Konfigurasi di CodeIgniter 4

CodeIgniter 4 memiliki berbagai file konfigurasi yang berada di dalam folder `app/config`. Setiap file konfigurasi digunakan untuk tujuan yang spesifik. Berikut adalah beberapa file konfigurasi penting di CodeIgniter 4:

1. **`App.php`**
2. **`Database.php`**
3. **`Email.php`**
4. **`Logger.php`**
5. **`Session.php`**
6. **`Cache.php`**
7. **`Paths.php`**

---

### 🧑‍💻 Mengelola Konfigurasi Aplikasi di CodeIgniter 4

#### 1. **`app/config/App.php`**

File `App.php` adalah tempat untuk menyimpan pengaturan global aplikasi, seperti base URL, lingkungan (environment), dan pengaturan timezone.

- **Contoh pengaturan di `App.php`:**

  ```php
  <?php

  namespace Config;

  use CodeIgniter\Config\BaseConfig;

  class App extends BaseConfig
  {
      public $baseURL = 'http://localhost:8080';  // URL dasar aplikasi
      public $indexPage = ''; // Nama file index (jika tidak ada, biarkan kosong)
      public $uriProtocol = 'REQUEST_URI'; // Metode URI
      public $timezone = 'Asia/Jakarta'; // Waktu default
      public $locale = 'en_US'; // Lokal aplikasi
      public $appID = ''; // ID aplikasi
  }
  ```

- **Parameter Penting:**
  - **`baseURL`**: URL dasar aplikasi, bisa berbeda di lingkungan pengembangan dan produksi.
  - **`indexPage`**: Jika menggunakan index.php di URL, kamu bisa menambahkan di sini.
  - **`timezone`**: Menetapkan zona waktu aplikasi, biasanya disesuaikan dengan zona waktu lokal.
  - **`locale`**: Menentukan lokalisasi, misalnya `en_US` untuk bahasa Inggris.

---

#### 2. **`app/config/Database.php`**

File `Database.php` digunakan untuk mengatur pengaturan database, seperti driver yang digunakan (MySQL, PostgreSQL, SQLite), hostname, username, password, dan nama database.

- **Contoh pengaturan di `Database.php`:**

  ```php
  <?php

  namespace Config;

  use CodeIgniter\Database\Config;

  class Database extends Config
  {
      public $default = [
          'DSN'      => '',
          'hostname' => 'localhost',
          'username' => 'root',
          'password' => '',
          'database' => 'ci4_database',
          'DBDriver' => 'MySQLi',
          'DBPrefix' => '',
          'pConnect' => false,
          'DBDebug'  => (ENVIRONMENT !== 'production'),
          'cacheOn'  => false,
          'encrypt'  => false,
          'compress' => false,
          'strictOn' => false,
          'failover' => [],
          'port'     => 3306,
      ];
  }
  ```

- **Parameter Penting:**
  - **`hostname`**: Alamat server database (biasanya `localhost`).
  - **`username`** dan **`password`**: Pengguna dan kata sandi untuk mengakses database.
  - **`database`**: Nama database yang digunakan oleh aplikasi.
  - **`DBDriver`**: Driver database yang digunakan, seperti `MySQLi`, `Postgre`, dll.
  - **`DBDebug`**: Menentukan apakah debug database diaktifkan atau tidak, berguna untuk debugging.

---

#### 3. **`app/config/Email.php`**

File `Email.php` mengatur pengaturan email untuk aplikasi, seperti driver email (SMTP, sendmail), server email, port, dan kredensial.

- **Contoh pengaturan di `Email.php`:**

  ```php
  <?php

  namespace Config;

  use CodeIgniter\Config\BaseConfig;

  class Email extends BaseConfig
  {
      public $protocol = 'smtp';
      public $SMTPHost = 'smtp.example.com';
      public $SMTPUser = 'user@example.com';
      public $SMTPPass = 'password';
      public $SMTPPort = 587;
      public $mailType = 'html';
      public $charset = 'utf-8';
  }
  ```

- **Parameter Penting:**
  - **`protocol`**: Protokol pengiriman email (biasanya `smtp`).
  - **`SMTPHost`**: Alamat server SMTP.
  - **`SMTPUser`** dan **`SMTPPass`**: Kredensial untuk login ke server SMTP.
  - **`SMTPPort`**: Port server SMTP, biasanya `587` untuk SMTP dengan enkripsi TLS.

---

#### 4. **`app/config/Session.php`**

File `Session.php` digunakan untuk mengonfigurasi sesi aplikasi, seperti driver sesi yang digunakan (files, database), pengaturan cookie, dan waktu kadaluwarsa sesi.

- **Contoh pengaturan di `Session.php`:**

  ```php
  <?php

  namespace Config;

  use CodeIgniter\Config\BaseConfig;

  class Session extends BaseConfig
  {
      public $driver         = 'CodeIgniter\Session\Handlers\FileHandler';
      public $savePath       = WRITEPATH . 'session';  // Lokasi file sesi
      public $cookieName     = 'ci_session';
      public $expireOnClose  = false;
      public $sessionLifetime = 7200; // 2 jam
      public $matchIP        = false;
      public $useSecureCookie = false;
  }
  ```

- **Parameter Penting:**
  - **`driver`**: Menentukan driver sesi yang digunakan, seperti `FileHandler`, `DatabaseHandler`, dll.
  - **`cookieName`**: Nama cookie sesi.
  - **`expireOnClose`**: Menentukan apakah sesi akan berakhir saat browser ditutup.
  - **`sessionLifetime`**: Durasi sesi dalam detik (misalnya 7200 detik = 2 jam).

---

#### 5. **`app/config/Cache.php`**

File `Cache.php` digunakan untuk mengonfigurasi pengaturan cache, seperti driver yang digunakan untuk caching (file, Redis, Memcached).

- **Contoh pengaturan di `Cache.php`:**

  ```php
  <?php

  namespace Config;

  use CodeIgniter\Config\BaseConfig;

  class Cache extends BaseConfig
  {
      public $handler = 'file';  // Menentukan handler cache, bisa 'file', 'redis', 'memcached'
      public $backupHandler = 'file';
      public $cachePath = WRITEPATH . 'cache';  // Lokasi penyimpanan cache
      public $cacheQueryString = false;
  }
  ```

- **Parameter Penting:**
  - **`handler`**: Menentukan jenis cache yang digunakan, seperti `file`, `redis`, atau `memcached`.
  - **`cachePath`**: Lokasi penyimpanan file cache.
  - **`backupHandler`**: Menentukan backup handler cache jika handler utama gagal.

---

### 🔧 Menambahkan Pengaturan Konfigurasi Baru

Selain file konfigurasi yang sudah ada di CodeIgniter 4, kamu bisa menambahkan file konfigurasi baru di folder `app/config` untuk kebutuhan aplikasi kamu.

- **Langkah-langkah:**
  1. Buat file baru di folder `app/config` dengan nama yang sesuai (misalnya, `CustomConfig.php`).
  2. Definisikan pengaturan yang diperlukan di dalam file tersebut.
  3. Akses file konfigurasi di kode aplikasi menggunakan:

   ```php
   $config = config('CustomConfig');
   ```

---

### 🔑 Best Practices dalam Penggunaan Config di CodeIgniter 4

| Praktik Terbaik                   | Penjelasan |
|------------------------------------|------------|
| **Simpan Konfigurasi di File**     | Semua konfigurasi aplikasi sebaiknya disimpan di dalam file konfigurasi untuk memudahkan pemeliharaan dan pengelolaan. |
| **Gunakan `.env` untuk Pengaturan Lingkungan** | Untuk pengaturan yang berbeda antara lingkungan (development, staging, produksi), gunakan file `.env` agar tidak perlu mengubah kode. |
| **Pemisahan Konfigurasi Sensitif** | Jangan simpan informasi sensitif seperti password atau kunci API di file konfigurasi secara langsung. Gunakan `.env` atau penyimpanan aman lainnya. |

---

### 📘 Dokumentasi Resmi

Untuk informasi lebih lanjut tentang pengaturan konfigurasi di CodeIgniter 4, kamu dapat merujuk ke dokumentasi resmi:

- [CodeIgniter 4 Configuration Guide](https://codeigniter4.github.io/userguide/)

---

### 💡 Kesimpulan

Pengaturan konfigurasi di CodeIgniter 4 adalah salah satu aspek penting dalam membangun aplikasi. Dengan menggunakan file konfigurasi, kamu dapat mengelola pengaturan aplikasi dengan lebih mudah dan terstruktur. Konfigurasi ini mempengaruhi berbagai aspek, seperti pengaturan database, email, session, dan cache, serta membantu menjaga konsistensi aplikasi di berbagai lingkungan.

Jika ada hal lain yang ingin didalami atau ada pertanyaan lebih lanjut, beri tahu aku!