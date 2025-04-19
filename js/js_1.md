Berikut adalah contoh untuk **Fitur Pengelolaan Data** yang terdapat pada nomor 1:

### 1. **Variabel**
   - **`let`**: Untuk mendeklarasikan variabel yang bisa diubah nilainya
   ```javascript
   let x = 5;
   x = 10; // nilai dapat diubah
   console.log(x); // Output: 10
   ```

   - **`const`**: Untuk mendeklarasikan variabel yang tidak bisa diubah nilainya
   ```javascript
   const y = 20;
   // y = 25; // Error: Assignment to constant variable.
   console.log(y); // Output: 20
   ```

   - **`var`**: Variabel yang memiliki scope fungsi (lebih lama, tidak dianjurkan di ES6 ke atas)
   ```javascript
   var z = 30;
   if (true) {
     var z = 40; // Variabel z akan terubah karena var memiliki scope fungsi
   }
   console.log(z); // Output: 40
   ```

### 2. **Tipe Data**
   - **`string`**
   ```javascript
   let name = "John Doe";
   console.log(name); // Output: John Doe
   ```

   - **`number`**
   ```javascript
   let age = 25;
   console.log(age); // Output: 25
   ```

   - **`boolean`**
   ```javascript
   let isActive = true;
   console.log(isActive); // Output: true
   ```

   - **`undefined`** (Variabel yang tidak diinisialisasi)
   ```javascript
   let x;
   console.log(x); // Output: undefined
   ```

   - **`null`**
   ```javascript
   let value = null;
   console.log(value); // Output: null
   ```

   - **`symbol`**
   ```javascript
   const sym = Symbol('description');
   console.log(sym); // Output: Symbol(description)
   ```

   - **`bigint`**
   ```javascript
   const bigNumber = 1234567890123456789012345678901234567890n;
   console.log(bigNumber); // Output: 1234567890123456789012345678901234567890n
   ```

   - **`object`**
   ```javascript
   let person = {
     name: "Alice",
     age: 30
   };
   console.log(person); // Output: { name: 'Alice', age: 30 }
   ```

### 3. **Array**
   - **Membuat array dan manipulasi dasar**
   ```javascript
   let fruits = ['apple', 'banana', 'cherry'];
   fruits.push('date');  // Menambah elemen di akhir array
   console.log(fruits); // Output: ['apple', 'banana', 'cherry', 'date']

   fruits.pop(); // Menghapus elemen terakhir
   console.log(fruits); // Output: ['apple', 'banana', 'cherry']
   ```

### 4. **Object**
   - **Membuat objek dan mengakses properti**
   ```javascript
   let person = {
     name: "Bob",
     age: 35
   };

   console.log(person.name); // Output: Bob
   console.log(person['age']); // Output: 35
   ```

   - **Menambah atau mengubah properti objek**
   ```javascript
   person.age = 36; // Mengubah nilai properti
   person.city = "New York"; // Menambah properti baru
   console.log(person); // Output: { name: 'Bob', age: 36, city: 'New York' }
   ```

### 5. **Set dan Map**
   - **Set**: Koleksi elemen yang unik
   ```javascript
   let numbers = new Set([1, 2, 3, 3, 4]);
   numbers.add(5); // Menambah elemen baru
   numbers.delete(2); // Menghapus elemen
   console.log(numbers); // Output: Set { 1, 3, 4, 5 }
   ```

   - **Map**: Koleksi pasangan key-value
   ```javascript
   let map = new Map();
   map.set('name', 'Alice');
   map.set('age', 28);
   console.log(map.get('name')); // Output: Alice
   ```

Semoga contoh-contoh ini membantu untuk memahami fitur pengelolaan data di JavaScript!