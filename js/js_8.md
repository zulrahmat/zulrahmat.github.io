Berikut adalah materi tentang **Export dan Import** serta **Module System** secara singkat dan sederhana:

### 1. **Export dan Import**

   - **Export** digunakan untuk mengekspor fungsi, variabel, atau objek dari sebuah file/module agar bisa digunakan di file/module lain.
     - **Contoh Export:**
       ```javascript
       // file1.js
       export function greet() {
         console.log("Hello, World!");
       }
       ```
     
   - **Import** digunakan untuk mengambil fungsi, variabel, atau objek yang diekspor dari file/module lain.
     - **Contoh Import:**
       ```javascript
       // file2.js
       import { greet } from './file1';
       greet(); // Output: Hello, World!
       ```

---

### 2. **Module System**

   - **CommonJS**: Digunakan di Node.js, menggunakan `module.exports` untuk mengekspor dan `require()` untuk mengimpor.
     - **Contoh CommonJS:**
       ```javascript
       // file1.js (CommonJS)
       function greet() {
         console.log("Hello from CommonJS!");
       }
       module.exports = greet;
       ```

       ```javascript
       // file2.js (CommonJS)
       const greet = require('./file1');
       greet(); // Output: Hello from CommonJS!
       ```

   - **ES6 Modules**: Sistem module yang lebih modern dengan `export` dan `import`.
     - **Contoh ES6 Modules**:
       ```javascript
       // file1.js (ES6 Module)
       export function greet() {
         console.log("Hello from ES6 Module!");
       }
       ```

       ```javascript
       // file2.js (ES6 Module)
       import { greet } from './file1';
       greet(); // Output: Hello from ES6 Module!
       ```

---

**Ringkasan**:
- **Export** dan **Import** memungkinkan Anda untuk berbagi kode antar file.
- **CommonJS** digunakan di Node.js, sementara **ES6 Modules** adalah standar modern untuk pengelolaan modul di JavaScript.