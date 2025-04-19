Berikut adalah contoh untuk **Pengendalian Alur Program (Control Flow)** yang terdapat pada nomor 2:

### 1. **Percabangan**
   - **`if`, `else`, `else if`**: Untuk percabangan atau pengkondisian
   ```javascript
   let age = 18;

   if (age >= 18) {
     console.log("Dewasa");
   } else {
     console.log("Anak-anak");
   }
   // Output: Dewasa
   ```

   - **`switch`**: Untuk percabangan dengan banyak kondisi
   ```javascript
   let day = 3;
   switch (day) {
     case 1:
       console.log("Senin");
       break;
     case 2:
       console.log("Selasa");
       break;
     case 3:
       console.log("Rabu");
       break;
     default:
       console.log("Hari tidak valid");
   }
   // Output: Rabu
   ```

### 2. **Perulangan**
   - **`for`**: Untuk perulangan dengan jumlah iterasi yang diketahui
   ```javascript
   for (let i = 0; i < 5; i++) {
     console.log(i);
   }
   // Output: 0 1 2 3 4
   ```

   - **`for...of`**: Untuk perulangan pada array atau iterable lainnya
   ```javascript
   const fruits = ['apple', 'banana', 'cherry'];

   for (let fruit of fruits) {
     console.log(fruit);
   }
   // Output: apple banana cherry
   ```

   - **`for...in`**: Untuk perulangan pada properti objek
   ```javascript
   const person = { name: 'Alice', age: 30 };

   for (let key in person) {
     console.log(key + ': ' + person[key]);
   }
   // Output: name: Alice
   //         age: 30
   ```

   - **`while`**: Untuk perulangan yang terus berjalan selama kondisi terpenuhi
   ```javascript
   let i = 0;
   while (i < 5) {
     console.log(i);
     i++;
   }
   // Output: 0 1 2 3 4
   ```

   - **`do...while`**: Untuk perulangan yang selalu dijalankan minimal satu kali
   ```javascript
   let i = 0;
   do {
     console.log(i);
     i++;
   } while (i < 5);
   // Output: 0 1 2 3 4
   ```

### 3. **Penghentian Loop**
   - **`break`**: Menghentikan perulangan secara langsung
   ```javascript
   for (let i = 0; i < 5; i++) {
     if (i === 3) {
       break; // Hentikan loop saat i mencapai 3
     }
     console.log(i);
   }
   // Output: 0 1 2
   ```

   - **`continue`**: Melewati iterasi saat kondisi tertentu terpenuhi
   ```javascript
   for (let i = 0; i < 5; i++) {
     if (i === 3) {
       continue; // Lewatkan iterasi ini
     }
     console.log(i);
   }
   // Output: 0 1 2 4
   ```

   - **`return`**: Menghentikan eksekusi fungsi dan mengembalikan nilai (jika ada)
   ```javascript
   function checkAge(age) {
     if (age < 18) {
       return "Anak-anak";
     }
     return "Dewasa";
   }
   console.log(checkAge(20)); // Output: Dewasa
   ```

### 4. **Exception Handling**
   - **`try`, `catch`, `finally`, `throw`**: Untuk menangani kesalahan dalam kode
   ```javascript
   try {
     let result = 10 / 0;
     if (!isFinite(result)) {
       throw new Error("Pembagian dengan nol");
     }
     console.log(result);
   } catch (error) {
     console.log("Terjadi kesalahan: " + error.message);
   } finally {
     console.log("Blok finally dijalankan.");
   }
   // Output: Terjadi kesalahan: Pembagian dengan nol
   //         Blok finally dijalankan.
   ```

   - **`throw`**: Untuk melemparkan kesalahan kustom
   ```javascript
   function checkNumber(num) {
     if (num < 0) {
       throw "Nomor tidak boleh negatif";
     }
     return num;
   }

   try {
     console.log(checkNumber(-5)); 
   } catch (error) {
     console.log("Kesalahan: " + error); // Output: Kesalahan: Nomor tidak boleh negatif
   }
   ```

Semoga contoh-contoh ini memberikan gambaran yang jelas tentang bagaimana pengendalian alur program di JavaScript bekerja!