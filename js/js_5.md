Berikut adalah contoh untuk **Fitur Asynchronous Programming** yang terdapat pada nomor 5:

### 1. **Callback Functions**
   **Callback function** adalah fungsi yang diteruskan sebagai argumen ke fungsi lain dan dipanggil kembali setelah proses selesai.
   ```javascript
   function fetchData(callback) {
     setTimeout(() => {
       console.log("Data fetched!");
       callback(); // Menjalankan callback setelah data di-fetch
     }, 2000);
   }

   fetchData(() => {
     console.log("Callback function executed!");
   });
   // Output setelah 2 detik:
   // Data fetched!
   // Callback function executed!
   ```

### 2. **Promises**
   **Promise** adalah objek yang mewakili nilai yang akan tersedia di masa depan, baik dalam bentuk keberhasilan atau kegagalan.
   
   - **Membuat Promise**: 
   ```javascript
   const myPromise = new Promise((resolve, reject) => {
     let success = true;
     if (success) {
       resolve("Operation succeeded!");
     } else {
       reject("Operation failed.");
     }
   });

   myPromise
     .then((message) => {
       console.log(message); // Output: Operation succeeded!
     })
     .catch((message) => {
       console.log(message); // Output jika gagal: Operation failed.
     });
   ```

   - **Chaining Promises**:
     Anda dapat **chain** beberapa `then()` untuk menjalankan operasi secara berurutan.
   ```javascript
   const myPromise = new Promise((resolve, reject) => {
     resolve("Start of promise chain");
   });

   myPromise
     .then((message) => {
       console.log(message); // Output: Start of promise chain
       return "Next step in chain";
     })
     .then((message) => {
       console.log(message); // Output: Next step in chain
     });
   ```

   - **Handling Multiple Promises (Promise.all)**:
     `Promise.all()` digunakan untuk menjalankan beberapa promises secara paralel dan menunggu semua selesai.
   ```javascript
   const promise1 = new Promise((resolve, reject) => {
     setTimeout(() => resolve("First promise resolved!"), 1000);
   });

   const promise2 = new Promise((resolve, reject) => {
     setTimeout(() => resolve("Second promise resolved!"), 1500);
   });

   Promise.all([promise1, promise2])
     .then((messages) => {
       console.log(messages); // Output: [ 'First promise resolved!', 'Second promise resolved!' ]
     })
     .catch((error) => {
       console.log(error); // Output jika ada error
     });
   ```

### 3. **Async / Await**
   **`async`** dan **`await`** adalah sintaks baru di JavaScript yang memudahkan penulisan kode asynchronous dengan cara yang lebih sinkron.
   
   - **Membuat Fungsi `async`**:
     Fungsi yang dideklarasikan dengan `async` selalu mengembalikan sebuah promise.
   ```javascript
   async function fetchData() {
     return "Data fetched!";
   }

   fetchData().then((message) => {
     console.log(message); // Output: Data fetched!
   });
   ```

   - **Menggunakan `await`**:
     **`await`** hanya dapat digunakan di dalam fungsi `async`. Ini akan menunggu promise selesai sebelum melanjutkan eksekusi.
   ```javascript
   async function fetchData() {
     const result = await new Promise((resolve) => {
       setTimeout(() => resolve("Data fetched!"), 2000);
     });
     console.log(result); // Output: Data fetched!
   }

   fetchData();
   ```

   - **Error Handling dengan `try`/`catch`**:
     Anda dapat menangani error dalam kode asynchronous dengan `try`/`catch`.
   ```javascript
   async function fetchData() {
     try {
       const result = await new Promise((resolve, reject) => {
         setTimeout(() => reject("Error occurred!"), 2000);
       });
       console.log(result);
     } catch (error) {
       console.log(error); // Output: Error occurred!
     }
   }

   fetchData();
   ```

### 4. **Fetching Data Asynchronously (Fetch API)**
   `fetch()` adalah cara modern untuk membuat permintaan HTTP asynchronous (GET, POST, dll).
   
   - **Mengambil Data dengan `fetch()`**:
   ```javascript
   fetch('https://api.example.com/data')
     .then(response => response.json()) // Mengubah response ke format JSON
     .then(data => {
       console.log(data); // Menampilkan data yang diterima
     })
     .catch(error => {
       console.log(error); // Menangani error
     });
   ```

   - **Menggunakan `async/await` dengan `fetch()`**:
   ```javascript
   async function getData() {
     try {
       const response = await fetch('https://api.example.com/data');
       const data = await response.json();
       console.log(data);
     } catch (error) {
       console.log(error);
     }
   }

   getData();
   ```

### 5. **SetTimeout dan SetInterval**
   - **`setTimeout()`**: Menunda eksekusi fungsi setelah waktu tertentu.
   ```javascript
   setTimeout(() => {
     console.log("This will run after 2 seconds");
   }, 2000);
   // Output setelah 2 detik: This will run after 2 seconds
   ```

   - **`setInterval()`**: Menjalankan fungsi secara berulang pada interval waktu tertentu.
   ```javascript
   let count = 0;
   const intervalId = setInterval(() => {
     count++;
     console.log("Interval: " + count);
     if (count === 5) {
       clearInterval(intervalId); // Menghentikan interval setelah 5 kali
     }
   }, 1000);
   // Output akan muncul setiap detik: Interval: 1, Interval: 2, ...
   ```

### 6. **Promise.race**
   `Promise.race()` akan mengembalikan hasil dari promise yang pertama kali diselesaikan (resolve atau reject).
   ```javascript
   const promise1 = new Promise((resolve) => setTimeout(resolve, 1000, "First"));
   const promise2 = new Promise((resolve) => setTimeout(resolve, 500, "Second"));

   Promise.race([promise1, promise2])
     .then((message) => {
       console.log(message); // Output: Second (karena promise2 lebih cepat)
     })
     .catch((error) => {
       console.log(error);
     });
   ```

Semoga contoh-contoh ini membantu Anda memahami berbagai fitur **asynchronous programming** di JavaScript!