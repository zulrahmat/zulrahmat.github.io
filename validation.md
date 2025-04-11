## ✅ Cara Menggunakan Validation

### 1. **Melalui Controller**

```php
$validation = \Config\Services::validation();

$input = $this->request->getPost();

$rules = [
    'username' => 'required|min_length[5]|max_length[20]',
    'email'    => 'required|valid_email',
    'password' => 'required|min_length[8]'
];

if (! $this->validate($rules)) {
    return redirect()->back()->withInput()->with('errors', $this->validator->getErrors());
}

// Lolos validasi → lanjut simpan data
```

---

### 2. **Tampilan Error di View**

```php
<?= session('errors.username') ?>
<?= session('errors.email') ?>
```

Untuk menampilkan kembali value yang sudah diinput:
```php
<input type="text" name="username" value="<?= old('username') ?>">
```

---

## 🧪 Daftar Rule Validasi Umum

| Rule               | Fungsi                                  |
|--------------------|------------------------------------------|
| `required`         | Harus diisi                              |
| `min_length[6]`    | Minimal 6 karakter                       |
| `max_length[12]`   | Maksimal 12 karakter                     |
| `alpha`            | Hanya huruf                              |
| `alpha_numeric`    | Huruf dan angka                          |
| `numeric`          | Hanya angka                              |
| `valid_email`      | Format email yang valid                  |
| `matches[password]`| Harus sama dengan input lain             |
| `is_unique[users.email]` | Harus unik di tabel database       |

---

## 🧱 Custom Pesan Error

```php
$rules = [
    'email' => [
        'rules' => 'required|valid_email',
        'errors' => [
            'required'    => 'Email wajib diisi.',
            'valid_email' => 'Format email tidak valid.'
        ]
    ]
];
```

---

## 📦 Validasi dengan `Validation` Secara Manual

```php
$validation = \Config\Services::validation();

$data = [
    'username' => 'andi',
    'email'    => 'salah_format'
];

$validation->setRules([
    'username' => 'required|min_length[3]',
    'email'    => 'required|valid_email'
]);

if (! $validation->run($data)) {
    $errors = $validation->getErrors();
}
```

---

## 🔁 Validasi di Model (Auto Validate)

```php
protected $validationRules = [
    'email'    => 'required|valid_email|is_unique[users.email]',
    'password' => 'required|min_length[8]'
];

protected $validationMessages = [
    'email' => [
        'is_unique' => 'Email sudah digunakan.',
        'required'  => 'Email wajib diisi.'
    ]
];
```