Berikut adalah materi terkait **Destructuring Object**, **Object Methods**, dan **Computed Property Names** di JavaScript:

### 1. **Destructuring Object**
   **Object destructuring** memungkinkan Anda untuk mengekstrak nilai dari objek dan menyimpannya dalam variabel dengan cara yang lebih bersih dan ringkas.

   - **Sintaks Dasar**:
     ```javascript
     const person = { name: "John", age: 30 };
     const { name, age } = person;
     console.log(name); // Output: John
     console.log(age);  // Output: 30
     ```

     Di sini, kita mengekstrak properti `name` dan `age` dari objek `person` dan menyimpannya ke dalam variabel dengan nama yang sama.

   - **Mengubah Nama Variabel**:
     Anda dapat mengganti nama variabel yang dihasilkan saat destructuring.
     ```javascript
     const person = { name: "John", age: 30 };
     const { name: fullName, age: yearsOld } = person;
     console.log(fullName); // Output: John
     console.log(yearsOld); // Output: 30
     ```

   - **Destructuring dengan Nilai Default**:
     Jika properti yang diambil tidak ada dalam objek, Anda dapat memberikan nilai default.
     ```javascript
     const person = { name: "John" };
     const { name, age = 25 } = person;
     console.log(name); // Output: John
     console.log(age);  // Output: 25 (karena tidak ada properti age dalam objek)
     ```

   - **Nested Destructuring**:
     Anda juga bisa mengekstrak nilai dari objek yang ada di dalam objek lain.
     ```javascript
     const person = { name: "John", address: { city: "New York", zip: 10001 } };
     const { name, address: { city, zip } } = person;
     console.log(name);  // Output: John
     console.log(city);  // Output: New York
     console.log(zip);   // Output: 10001
     ```

---

### 2. **Object Methods**
   JavaScript menyediakan berbagai metode untuk bekerja dengan objek. Berikut adalah beberapa metode yang sering digunakan:

   - **`Object.assign()`**:
     Digunakan untuk menyalin nilai dari satu atau lebih objek ke objek target.
     ```javascript
     const obj1 = { name: "John" };
     const obj2 = { age: 30 };
     const combined = Object.assign({}, obj1, obj2);
     console.log(combined); // Output: { name: "John", age: 30 }
     ```

     Anda bisa menyalin objek ke objek lain atau membuat salinan objek baru.

   - **`Object.freeze()`**:
     Membekukan objek, mencegah properti baru ditambahkan atau properti yang ada diubah.
     ```javascript
     const person = { name: "John", age: 30 };
     Object.freeze(person);
     person.age = 35; // Tidak akan mengubah nilai age
     console.log(person.age); // Output: 30
     ```

     Dengan `Object.freeze()`, objek menjadi tidak dapat dimodifikasi.

   - **`Object.seal()`**:
     Menyegel objek, yang berarti tidak bisa menambah properti baru, tetapi properti yang ada masih bisa diubah.
     ```javascript
     const person = { name: "John", age: 30 };
     Object.seal(person);
     person.age = 35; // Nilai age bisa diubah
     person.address = "New York"; // Tidak bisa menambah properti baru
     console.log(person); // Output: { name: "John", age: 35 }
     ```

     `Object.seal()` memungkinkan pengubahan properti yang ada, tetapi tidak bisa menambah atau menghapus properti.

---

### 3. **Computed Property Names**
   **Computed Property Names** memungkinkan Anda untuk menentukan nama properti objek secara dinamis. Anda dapat menggunakan ekspresi dalam tanda kurung kotak `[]` untuk menentukannya.

   - **Sintaks Dasar**:
     ```javascript
     const key = "name";
     const value = "John";
     const obj = { [key]: value };
     console.log(obj.name); // Output: John
     ```

     Di sini, `key` adalah variabel yang nilainya menjadi nama properti objek.

   - **Menggunakan Ekspresi**:
     Anda dapat menggunakan ekspresi di dalam tanda kurung kotak.
     ```javascript
     const obj = { 
       [`user${1 + 1}`]: "John" 
     };
     console.log(obj.user2); // Output: John
     ```

     Dalam contoh ini, nama properti dihitung sebagai `user2`, berdasarkan ekspresi `user${1 + 1}`.

---

### 4. **Object Destructuring**
   Merupakan metode untuk mengekstrak nilai dari objek dengan cara yang lebih ringkas.

   - **Sintaks Dasar**:
     ```javascript
     const person = { name: "John", age: 30 };
     const { name } = person;
     console.log(name); // Output: John
     ```

   Ini adalah cara untuk mengambil properti tertentu dari objek. Misalnya, dalam contoh ini, kita hanya mengambil properti `name` dari objek `person`.

---

### Ringkasan:

1. **Destructuring Object** memungkinkan Anda untuk mengekstrak nilai dari objek dengan cara yang ringkas dan jelas.
2. **Object Methods** seperti `Object.assign()`, `Object.freeze()`, dan `Object.seal()` memberikan kontrol lebih dalam mengelola objek di JavaScript.
3. **Computed Property Names** memungkinkan Anda untuk mendefinisikan nama properti objek secara dinamis, yang bisa berupa ekspresi.

Semoga penjelasan ini membantu!