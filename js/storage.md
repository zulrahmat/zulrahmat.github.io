Siap! Berikut materi lengkap tentang **Web Storage API** di JavaScript yang sering digunakan untuk menyimpan data di browser seperti **localStorage** dan **sessionStorage**.

---

## 🗂️ Web Storage API - JavaScript

Web Storage API digunakan untuk **menyimpan data di sisi client (browser)**, yang bisa digunakan antar halaman tanpa perlu backend.

---

## 📦 Tipe Storage:

### 1. **localStorage**
- Data **permanen** sampai dihapus manual.
- Masih ada meskipun tab atau browser ditutup.
- Ukuran sekitar 5MB per origin.

### 2. **sessionStorage**
- Data hanya ada selama **tab/browser aktif**.
- Akan hilang jika tab/browser ditutup.
- Ukuran sama (5MB), tapi scope lebih kecil.

---

## 🔑 Format Data
- **Key-value pair**
- Semua data disimpan sebagai **string**.
  (Kalau objek/array → perlu di-`JSON.stringify()` dulu.)

---

## 🛠️ Metode Utama

| Metode                        | Keterangan                         |
|------------------------------|------------------------------------|
| `setItem(key, value)`        | Menyimpan data                     |
| `getItem(key)`               | Mengambil data                     |
| `removeItem(key)`            | Menghapus data                     |
| `clear()`                    | Menghapus semua data               |
| `key(index)`                 | Mengambil nama key berdasarkan index |

---

## 🧪 Contoh: localStorage

```js
// Simpan data
localStorage.setItem("nama", "Zul");

// Ambil data
let nama = localStorage.getItem("nama");
console.log(nama); // Output: Zul

// Hapus data
localStorage.removeItem("nama");

// Hapus semua data
localStorage.clear();
```

---

## 💾 Menyimpan Objek/Array

```js
let user = { nama: "Zul", umur: 20 };

// Simpan ke localStorage
localStorage.setItem("user", JSON.stringify(user));

// Ambil dan ubah ke objek lagi
let userData = JSON.parse(localStorage.getItem("user"));
console.log(userData.nama); // Zul
```

---

## 🧪 Contoh: sessionStorage

```js
sessionStorage.setItem("token", "abc123");

let token = sessionStorage.getItem("token");
console.log(token); // abc123

sessionStorage.removeItem("token");
```

---

## 📌 Perbandingan `localStorage` vs `sessionStorage`

| Fitur             | localStorage     | sessionStorage     |
|-------------------|------------------|---------------------|
| Waktu hidup       | Selamanya        | Sampai tab ditutup  |
| Scope             | Per origin       | Per tab             |
| Ukuran            | ~5MB             | ~5MB                |
| Persistent?       | Ya               | Tidak               |

---

## 🧠 Tips & Best Practice

- Jangan simpan data sensitif (misalnya password atau token login).
- Gunakan `try...catch` untuk menangani error quota atau parsing JSON.
- Cocok untuk menyimpan:
  - Tema (dark/light)
  - Preferensi user
  - Draft teks
  - Keranjang belanja sederhana

---

Kalau kamu mau, aku bisa bantu bikin project kecil seperti:
- Aplikasi To-Do List dengan localStorage
- Dark mode toggle yang disimpan di localStorage
- Form isian yang tetap tersimpan walau refresh

Mau coba yang mana dulu? 😄