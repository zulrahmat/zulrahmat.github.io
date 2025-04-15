Oke! Yuk kita belajar **password hashing di PHP** — ini penting banget buat bikin aplikasi login yang aman.

---

## 🔐 Apa itu Password Hashing?
Hashing adalah proses mengubah password menjadi **kode acak tetap** (hash) yang **tidak bisa dibalik**. Jadi kalau databasenya bocor, password aslinya tetap aman.

---

## ✅ Fungsi Utama di PHP

| Fungsi | Kegunaan |
|--------|----------|
| `password_hash()` | Untuk **membuat hash password** |
| `password_verify()` | Untuk **memeriksa password yang dimasukkan** cocok dengan hash-nya |

---

## 🧪 Contoh Kode

### 1. Hash Password
```php
$password = "rahasia123";
$hash = password_hash($password, PASSWORD_DEFAULT);

echo "Password: $password\n";
echo "Hash: $hash\n";
```

### 🔽 Contoh Output:
```
Password: rahasia123
Hash: $2y$10$u2m3V3L5uUq8HABbOZSzA.jRk0GzqN0d0nFZcVg1wVwpu7BYA4U5y
```

> Hash-nya akan selalu **berbeda** setiap kali dijalankan karena ada **salt** otomatis.

---

### 2. Verifikasi Password
```php
$password = "rahasia123";
$hash = '$2y$10$u2m3V3L5uUq8HABbOZSzA.jRk0GzqN0d0nFZcVg1wVwpu7BYA4U5y'; // contoh hash

if (password_verify($password, $hash)) {
    echo "Password benar!";
} else {
    echo "Password salah!";
}
```

---

## 🛡️ Kelebihan `password_hash()`

- Otomatis menambahkan **salt** (pengacak).
- Pakai algoritma **BCRYPT** atau **ARGON2** (PHP >= 7.2).
- Aman dan **direkomendasikan** oleh PHP.

---

Kalau kamu mau, kita bisa buat contoh form login pakai ini. Mau lanjut?