Berikut adalah contoh untuk **Fitur Fungsi** yang terdapat pada nomor 3:

### 1. **Function Declaration**:  
   Untuk mendeklarasikan fungsi menggunakan kata kunci `function`:
   ```javascript
   function greet(name) {
     return "Hello, " + name + "!";
   }
   console.log(greet("Alice")); // Output: Hello, Alice!
   ```

### 2. **Arrow Function**:  
   Sintaksis singkat untuk mendeklarasikan fungsi, lebih ringkas dan tidak memiliki `this` sendiri:
   ```javascript
   const greet = (name) => "Hello, " + name + "!";
   console.log(greet("Bob")); // Output: Hello, Bob!
   ```

### 3. **Function Expression**:  
   Fungsi yang dideklarasikan dalam variabel. Fungsi ini tidak dapat dipanggil sebelum deklarasinya.
   ```javascript
   const greet = function(name) {
     return "Hello, " + name + "!";
   };
   console.log(greet("Charlie")); // Output: Hello, Charlie!
   ```

### 4. **IIFE (Immediately Invoked Function Expression)**:  
   Fungsi yang langsung dijalankan setelah dideklarasikan, sering digunakan untuk membungkus kode agar tidak mengganggu scope global.
   ```javascript
   (function() {
     console.log("Ini adalah IIFE!");
   })();
   // Output: Ini adalah IIFE!
   ```

### 5. **Parameter Default**:  
   Menentukan nilai default untuk parameter fungsi jika argumen tidak diberikan.
   ```javascript
   function greet(name = "Guest") {
     return "Hello, " + name + "!";
   }
   console.log(greet("David")); // Output: Hello, David!
   console.log(greet());        // Output: Hello, Guest!
   ```

### 6. **Rest Parameters**:  
   Menyimpan argumen tambahan dalam sebuah array.
   ```javascript
   function sum(...numbers) {
     return numbers.reduce((total, num) => total + num, 0);
   }
   console.log(sum(1, 2, 3, 4)); // Output: 10
   ```

### 7. **Spread Operator**:  
   Digunakan untuk memecah array atau objek menjadi elemen individu.
   ```javascript
   function greet(name, age) {
     console.log("Hello, " + name + "! You are " + age + " years old.");
   }

   const person = ["Alice", 25];
   greet(...person);  // Output: Hello, Alice! You are 25 years old.
   ```

Semoga contoh-contoh ini memberikan gambaran yang jelas tentang cara penggunaan fungsi di JavaScript!