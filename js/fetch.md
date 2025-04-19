Siap! Berikut materi lengkap tentang **Fetch API** di JavaScript, salah satu fitur modern yang biasa digunakan untuk melakukan **request HTTP (GET, POST, dll)** ke server.

---

## 🌐 Fetch API - JavaScript

**Fetch API** digunakan untuk **mengambil/mengirim data dari/ke server** secara asynchronous (tanpa reload halaman). Digunakan menggantikan `XMLHttpRequest` yang lama.

---

## ✅ Keunggulan Fetch API

- Menggunakan **Promise** (lebih mudah daripada callback)
- Penulisan kode lebih bersih dan modern
- Bisa digunakan dengan `async/await`

---

## 🔧 Struktur Dasar

```js
fetch(url, options)
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error("Error:", error));
```

---

## 📌 Contoh 1: GET Request (Ambil Data)

```js
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then(res => res.json())
  .then(data => {
    console.log(data); // { id: 1, title: ..., body: ... }
  })
  .catch(err => console.error(err));
```

---

## 📌 Contoh 2: POST Request (Kirim Data)

```js
fetch("https://jsonplaceholder.typicode.com/posts", {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    title: "Belajar Fetch API",
    body: "Ini konten dari body",
    userId: 1
  })
})
  .then(res => res.json())
  .then(data => {
    console.log(data); // response dari server
  })
  .catch(err => console.error(err));
```

---

## 📌 Contoh dengan `async/await`

```js
async function ambilData() {
  try {
    let res = await fetch("https://jsonplaceholder.typicode.com/users");
    let data = await res.json();
    console.log(data);
  } catch (err) {
    console.error("Gagal fetch:", err);
  }
}
ambilData();
```

---

## 🎯 Metode HTTP Lain

```js
fetch(url, {
  method: "PUT",      // update data
  method: "DELETE",   // hapus data
  ...
});
```

---

## 📂 Contoh Kirim Form Data

```js
const formData = new FormData();
formData.append("nama", "Zul");
formData.append("email", "zul@example.com");

fetch("/api/kirim", {
  method: "POST",
  body: formData
})
  .then(res => res.text())
  .then(result => console.log(result));
```

---

## ⚠️ Error Handling

Fetch **tidak otomatis melempar error** untuk HTTP 4xx/5xx, harus dicek manual:

```js
fetch("/api/data")
  .then(res => {
    if (!res.ok) throw new Error("HTTP Error: " + res.status);
    return res.json();
  })
  .then(data => console.log(data))
  .catch(err => console.error("Terjadi kesalahan:", err));
```

---

## 🧠 Tips Tambahan

- Gunakan `try...catch` saat pakai `async/await`
- Fetch API cocok untuk berkomunikasi dengan **REST API**
- Bisa digunakan dengan `headers` untuk mengatur token/jwt
- Gunakan loader/spinner agar user tahu sedang fetch

---

## 🔨 Project Mini dengan Fetch API

Kalau kamu mau praktik, bisa coba bikin:
- Aplikasi cuaca (ambil data dari API openweather)
- Form registrasi yang kirim ke API
- Load data user dan tampilkan dalam tabel

Mau mulai dengan project kecil yang mana? Atau ada API yang ingin kamu coba fetch? 😄