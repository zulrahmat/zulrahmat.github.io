Tentu! Berikut adalah **materi lengkap tentang Library Email di CodeIgniter 4**, yang sangat berguna untuk mengirim email seperti notifikasi, verifikasi akun, dan laporan otomatis dari aplikasi kamu.

---

## 📧 Materi: Library Email di CodeIgniter 4

---

### 🔰 1. Konfigurasi Email

Sebelum mengirim email, kamu perlu mengatur konfigurasi SMTP. Kamu bisa mengatur konfigurasi langsung di controller, atau menyimpannya di file `app/Config/Email.php`.

#### 📁 Contoh konfigurasi SMTP Gmail:

```php
public $protocol = 'smtp';
public $SMTPHost = 'smtp.gmail.com';
public $SMTPUser = 'youremail@gmail.com';
public $SMTPPass = 'yourpassword'; // atau App Password Gmail
public $SMTPPort = 465;
public $SMTPCrypto = 'ssl';
public $mailType = 'html';
```

Atau kamu bisa juga langsung set di controller:

```php
$email = \Config\Services::email();

$config = [
    'protocol' => 'smtp',
    'SMTPHost' => 'smtp.gmail.com',
    'SMTPUser' => 'youremail@gmail.com',
    'SMTPPass' => 'yourpassword',
    'SMTPPort' => 465,
    'SMTPCrypto' => 'ssl',
    'mailType'  => 'html',
    'charset'   => 'utf-8',
];

$email->initialize($config);
```

> ⚠️ Jika kamu menggunakan Gmail, aktifkan 2FA dan buat **App Password** untuk SMTP.

---

## ✉️ 2. Mengirim Email

Setelah konfigurasi siap, kamu bisa mengirim email seperti ini:

```php
$email->setFrom('youremail@gmail.com', 'Nama Pengirim');
$email->setTo('target@example.com');
$email->setSubject('Judul Email');
$email->setMessage('<h1>Halo Dunia!</h1><p>Ini adalah email pertama saya dari CodeIgniter 4.</p>');

if ($email->send()) {
    echo 'Email berhasil dikirim!';
} else {
    echo $email->printDebugger(['headers']);
}
```

---

## 📎 3. Mengirim ke Banyak Penerima

```php
$email->setTo(['email1@example.com', 'email2@example.com']);
$email->setCC('cc@example.com');
$email->setBCC('bcc@example.com');
```

---

## 📎 4. Melampirkan File

```php
$email->attach(WRITEPATH . 'uploads/laporan.pdf');
```

---

## 📤 5. Menampilkan Debugger

Jika gagal kirim, gunakan:

```php
echo $email->printDebugger(['headers']);
```

Untuk melihat detail error.

---

## ✅ 6. Tips Best Practice

| Tips | Penjelasan |
|------|------------|
| ✅ Gunakan App Password Gmail | Lebih aman daripada password utama |
| ✅ Gunakan mailtrap.io untuk testing | Cocok untuk environment development |
| ✅ Validasi input sebelum kirim | Hindari spam dan penyalahgunaan |
| ✅ Kirim dalam format HTML dan Text | Gunakan `setAltMessage()` |

---

## 🧪 Contoh Fungsi Lengkap

```php
public function kirimEmail()
{
    $email = \Config\Services::email();

    $config = [
        'protocol' => 'smtp',
        'SMTPHost' => 'smtp.gmail.com',
        'SMTPUser' => 'youremail@gmail.com',
        'SMTPPass' => 'yourpassword',
        'SMTPPort' => 465,
        'SMTPCrypto' => 'ssl',
        'mailType'  => 'html',
        'charset'   => 'utf-8',
    ];

    $email->initialize($config);

    $email->setFrom('youremail@gmail.com', 'Admin');
    $email->setTo('target@example.com');
    $email->setSubject('Uji Kirim Email');
    $email->setMessage('<strong>Halo, ini pesan HTML!</strong>');

    if ($email->send()) {
        echo 'Email berhasil dikirim.';
    } else {
        echo $email->printDebugger(['headers']);
    }
}
```

---

## 📘 Dokumentasi Resmi

- [Email Class - CodeIgniter 4](https://codeigniter.com/user_guide/libraries/email.html)

---

Kalau kamu mau, aku bisa bantu buatkan:
- Fungsi **verifikasi email pengguna baru**
- Fungsi **notifikasi otomatis saat ada data baru**

Mau lanjut ke salah satu contoh tersebut?