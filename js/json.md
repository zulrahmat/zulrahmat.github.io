Tentu, mari kita lihat beberapa cara menangani JSON di JavaScript! JSON itu seperti format pertukaran data yang ringan dan mudah dibaca, sering banget dipake di web.

Katakanlah kamu punya string JSON seperti ini:

```javascript
const jsonString = '{"nama": "Budi", "umur": 30, "kota": "Jakarta"}';
```

**1. Mengubah JSON String menjadi Objek JavaScript (Parsing):**

Untuk bisa bekerja dengan data JSON ini di JavaScript, kamu perlu mengubahnya jadi objek JavaScript. Caranya pakai `JSON.parse()`:

```javascript
const dataObjek = JSON.parse(jsonString);
console.log(dataObjek); // Output: { nama: 'Budi', umur: 30, kota: 'Jakarta' }
console.log(dataObjek.nama); // Output: Budi
console.log(dataObjek.umur); // Output: 30
```

**2. Mengubah Objek JavaScript menjadi JSON String (Stringify):**

Nah, kalau kamu punya objek JavaScript dan pengen ngubahnya jadi string JSON (misalnya buat dikirim ke server), kamu bisa pakai `JSON.stringify()`:

```javascript
const dataJavaScript = { nama: "Siti", pekerjaan: "Guru", hobi: ["membaca", "menulis"] };
const jsonBaru = JSON.stringify(dataJavaScript);
console.log(jsonBaru); // Output: {"nama":"Siti","pekerjaan":"Guru","hobi":["membaca","menulis"]}
```

**3. Beberapa Opsi Tambahan dengan `JSON.stringify()`:**

* **Memformat output agar lebih mudah dibaca:** Kamu bisa menambahkan argumen ketiga ke `JSON.stringify()` untuk memberikan spasi atau karakter lain sebagai indentasi.

    ```javascript
    const jsonTerformat = JSON.stringify(dataJavaScript, null, 2);
    console.log(jsonTerformat);
    /* Output:
    {
      "nama": "Siti",
      "pekerjaan": "Guru",
      "hobi": [
        "membaca",
        "menulis"
      ]
    }
    */
    ```

* **Memilih properti mana saja yang ingin diubah jadi JSON:** Kamu bisa menggunakan argumen kedua (replacer) berupa array yang berisi nama properti yang ingin kamu sertakan.

    ```javascript
    const jsonNamaPekerjaan = JSON.stringify(dataJavaScript, ["nama", "pekerjaan"]);
    console.log(jsonNamaPekerjaan); // Output: {"nama":"Siti","pekerjaan":"Guru"}
    ```

Itulah beberapa contoh dasar untuk menangani JSON di JavaScript. Biasanya, kamu bakal sering ketemu JSON saat berinteraksi dengan API web. Semoga ini membantu!