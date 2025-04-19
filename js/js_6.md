Berikut adalah contoh untuk **Fitur Operasi Array** yang terdapat pada nomor 6:

### 1. **Membuat dan Mengakses Array**
   Anda dapat membuat array menggunakan tanda kurung siku `[]` dan mengakses elemen array dengan indeks.
   ```javascript
   const fruits = ["Apple", "Banana", "Cherry"];
   console.log(fruits[0]); // Output: Apple
   console.log(fruits[1]); // Output: Banana
   ```

### 2. **Metode Array (Array Methods)**
   - **`push()`**: Menambahkan elemen ke akhir array.
   ```javascript
   const fruits = ["Apple", "Banana"];
   fruits.push("Cherry");
   console.log(fruits); // Output: ["Apple", "Banana", "Cherry"]
   ```

   - **`pop()`**: Menghapus elemen terakhir dari array.
   ```javascript
   const fruits = ["Apple", "Banana", "Cherry"];
   fruits.pop();
   console.log(fruits); // Output: ["Apple", "Banana"]
   ```

   - **`shift()`**: Menghapus elemen pertama dari array.
   ```javascript
   const fruits = ["Apple", "Banana", "Cherry"];
   fruits.shift();
   console.log(fruits); // Output: ["Banana", "Cherry"]
   ```

   - **`unshift()`**: Menambahkan elemen ke awal array.
   ```javascript
   const fruits = ["Banana", "Cherry"];
   fruits.unshift("Apple");
   console.log(fruits); // Output: ["Apple", "Banana", "Cherry"]
   ```

   - **`concat()`**: Menggabungkan dua atau lebih array.
   ```javascript
   const fruits1 = ["Apple", "Banana"];
   const fruits2 = ["Cherry", "Date"];
   const combinedFruits = fruits1.concat(fruits2);
   console.log(combinedFruits); // Output: ["Apple", "Banana", "Cherry", "Date"]
   ```

   - **`join()`**: Menggabungkan semua elemen array menjadi satu string dengan pemisah tertentu.
   ```javascript
   const fruits = ["Apple", "Banana", "Cherry"];
   const result = fruits.join(", ");
   console.log(result); // Output: Apple, Banana, Cherry
   ```

   - **`slice()`**: Mengambil sebagian array (membuat array baru tanpa mengubah array asli).
   ```javascript
   const fruits = ["Apple", "Banana", "Cherry", "Date"];
   const slicedFruits = fruits.slice(1, 3);
   console.log(slicedFruits); // Output: ["Banana", "Cherry"]
   ```

   - **`splice()`**: Menambahkan atau menghapus elemen dari array pada posisi tertentu.
   ```javascript
   const fruits = ["Apple", "Banana", "Cherry"];
   fruits.splice(1, 1, "Orange", "Grapes");
   console.log(fruits); // Output: ["Apple", "Orange", "Grapes", "Cherry"]
   ```

### 3. **Metode Iterasi Array**
   - **`forEach()`**: Menjalankan fungsi pada setiap elemen array.
   ```javascript
   const fruits = ["Apple", "Banana", "Cherry"];
   fruits.forEach((fruit) => {
     console.log(fruit);
   });
   // Output:
   // Apple
   // Banana
   // Cherry
   ```

   - **`map()`**: Membuat array baru dengan elemen yang telah dimodifikasi berdasarkan elemen asli.
   ```javascript
   const numbers = [1, 2, 3, 4];
   const doubledNumbers = numbers.map((number) => number * 2);
   console.log(doubledNumbers); // Output: [2, 4, 6, 8]
   ```

   - **`filter()`**: Membuat array baru dengan elemen yang memenuhi kondisi tertentu.
   ```javascript
   const numbers = [1, 2, 3, 4, 5];
   const evenNumbers = numbers.filter((number) => number % 2 === 0);
   console.log(evenNumbers); // Output: [2, 4]
   ```

   - **`reduce()`**: Menggabungkan elemen array menjadi satu nilai tunggal (misalnya total).
   ```javascript
   const numbers = [1, 2, 3, 4];
   const sum = numbers.reduce((accumulator, currentValue) => accumulator + currentValue, 0);
   console.log(sum); // Output: 10
   ```

   - **`some()`**: Mengecek apakah ada elemen yang memenuhi kondisi tertentu (mengembalikan boolean).
   ```javascript
   const numbers = [1, 2, 3, 4];
   const hasEven = numbers.some((number) => number % 2 === 0);
   console.log(hasEven); // Output: true
   ```

   - **`every()`**: Mengecek apakah semua elemen memenuhi kondisi tertentu (mengembalikan boolean).
   ```javascript
   const numbers = [2, 4, 6, 8];
   const allEven = numbers.every((number) => number % 2 === 0);
   console.log(allEven); // Output: true
   ```

   - **`find()`**: Mengembalikan elemen pertama yang memenuhi kondisi tertentu.
   ```javascript
   const numbers = [1, 2, 3, 4];
   const firstEven = numbers.find((number) => number % 2 === 0);
   console.log(firstEven); // Output: 2
   ```

   - **`findIndex()`**: Mengembalikan indeks elemen pertama yang memenuhi kondisi tertentu.
   ```javascript
   const numbers = [1, 2, 3, 4];
   const index = numbers.findIndex((number) => number === 3);
   console.log(index); // Output: 2
   ```

### 4. **Metode Array Lainnya**
   - **`includes()`**: Mengecek apakah array berisi elemen tertentu (mengembalikan boolean).
   ```javascript
   const fruits = ["Apple", "Banana", "Cherry"];
   console.log(fruits.includes("Banana")); // Output: true
   console.log(fruits.includes("Orange")); // Output: false
   ```

   - **`indexOf()`**: Mencari indeks elemen dalam array.
   ```javascript
   const fruits = ["Apple", "Banana", "Cherry"];
   const index = fruits.indexOf("Banana");
   console.log(index); // Output: 1
   ```

   - **`reverse()`**: Membalikkan urutan elemen dalam array.
   ```javascript
   const fruits = ["Apple", "Banana", "Cherry"];
   fruits.reverse();
   console.log(fruits); // Output: ["Cherry", "Banana", "Apple"]
   ```

   - **`sort()`**: Mengurutkan elemen array.
   ```javascript
   const numbers = [4, 2, 3, 1];
   numbers.sort();
   console.log(numbers); // Output: [1, 2, 3, 4]
   ```

### 5. **Destructuring Array**
   **Array Destructuring** memungkinkan Anda untuk mengekstrak elemen array ke dalam variabel.
   ```javascript
   const fruits = ["Apple", "Banana", "Cherry"];
   const [first, second] = fruits;
   console.log(first);  // Output: Apple
   console.log(second); // Output: Banana
   ```

Semoga contoh-contoh ini dapat membantu Anda memahami berbagai operasi yang dapat dilakukan dengan array di JavaScript!