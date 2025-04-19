Tentu! Berikut adalah materi tentang **Clipboard API** di JavaScript yang bisa kamu pelajari secara bertahap.

---

## 📋 **Clipboard API - JavaScript**

Clipboard API digunakan untuk **membaca dan menulis teks ke clipboard** (seperti fungsi copy/paste). API ini sangat berguna untuk membuat fitur seperti:

- Tombol **"Copy to Clipboard"**
- Mendapatkan isi clipboard saat user melakukan paste
- Interaksi langsung dengan clipboard tanpa harus menggunakan elemen input tersembunyi

---

### 🧠 **2 Fungsi Utama Clipboard API**

1. `navigator.clipboard.writeText(text)`  
   ➜ Menyalin teks ke clipboard (copy)

2. `navigator.clipboard.readText()`  
   ➜ Membaca teks dari clipboard (paste)

> ⚠️ Harus dijalankan dalam **context user gesture** (seperti klik), dan hanya bisa digunakan di **HTTPS** (kecuali localhost).

---

### 📌 Contoh 1: Copy Text ke Clipboard

```html
<button onclick="copyText()">Copy</button>
<input type="text" id="myInput" value="Hello Clipboard!">

<script>
function copyText() {
  const input = document.getElementById("myInput");
  navigator.clipboard.writeText(input.value)
    .then(() => alert("Teks berhasil disalin!"))
    .catch(err => alert("Gagal menyalin teks: " + err));
}
</script>
```

---

### 📌 Contoh 2: Paste Text dari Clipboard

```html
<button onclick="pasteText()">Paste</button>
<input type="text" id="pasteTarget">

<script>
function pasteText() {
  navigator.clipboard.readText()
    .then(text => {
      document.getElementById("pasteTarget").value = text;
    })
    .catch(err => alert("Gagal membaca clipboard: " + err));
}
</script>
```

---

### 🔐 Catatan Keamanan

- **HTTPS** dibutuhkan untuk alasan keamanan.
- Penggunaan Clipboard API dibatasi hanya pada event tertentu (misalnya `click`, `keydown`, dsb.).
- Beberapa browser mungkin meminta **izin** dari pengguna.

---

### 📚 Event Clipboard Lain (Non-Clipboard API)

Ada juga event lama yang bisa digunakan pada elemen:

```js
element.addEventListener("copy", handler);
element.addEventListener("cut", handler);
element.addEventListener("paste", handler);
```

Contoh:

```html
<textarea id="myText"></textarea>

<script>
document.getElementById("myText").addEventListener("paste", function(e) {
  e.preventDefault();
  const paste = (e.clipboardData || window.clipboardData).getData("text");
  alert("Teks yang dipaste: " + paste);
});
</script>
```

---

### 🧪 Cek Dukungan Browser

Cek dengan:

```js
if (navigator.clipboard) {
  console.log("Clipboard API didukung!");
} else {
  console.log("Clipboard API tidak didukung.");
}
```

---

Kalau kamu mau, aku bisa bantu buat project mini seperti:
- **Copy-paste untuk form login**
- **Clipboard manager sederhana**
- **Aplikasi catatan dengan auto-copy**

Tertarik coba yang mana dulu? 😄