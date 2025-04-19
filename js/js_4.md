Berikut adalah contoh untuk **Fitur Manipulasi DOM** yang terdapat pada nomor 4:

### 1. **Mengakses Elemen DOM**
   - **`document.getElementById()`**: Mengambil elemen berdasarkan ID.
   ```javascript
   const element = document.getElementById("myElement");
   console.log(element); // Output: elemen dengan ID "myElement"
   ```

   - **`document.getElementsByClassName()`**: Mengambil elemen berdasarkan kelas.
   ```javascript
   const elements = document.getElementsByClassName("myClass");
   console.log(elements); // Output: koleksi elemen dengan kelas "myClass"
   ```

   - **`document.getElementsByTagName()`**: Mengambil elemen berdasarkan tag HTML.
   ```javascript
   const elements = document.getElementsByTagName("p");
   console.log(elements); // Output: koleksi elemen <p>
   ```

   - **`document.querySelector()`**: Mengambil elemen pertama yang sesuai dengan selector CSS.
   ```javascript
   const element = document.querySelector(".myClass");
   console.log(element); // Output: elemen pertama dengan kelas "myClass"
   ```

   - **`document.querySelectorAll()`**: Mengambil semua elemen yang sesuai dengan selector CSS.
   ```javascript
   const elements = document.querySelectorAll(".myClass");
   console.log(elements); // Output: NodeList dari semua elemen dengan kelas "myClass"
   ```

### 2. **Memanipulasi Konten dan Atribut Elemen**
   - **Mengubah Konten Elemen**
     Anda dapat mengubah konten teks atau HTML dari elemen menggunakan properti `textContent` atau `innerHTML`.
   ```javascript
   const element = document.getElementById("myElement");
   element.textContent = "Ini adalah teks baru!";
   element.innerHTML = "<b>Ini adalah teks baru dalam tag HTML!</b>";
   ```

   - **Menambah dan Mengubah Atribut Elemen**
     Untuk menambah atau mengubah atribut elemen, Anda bisa menggunakan `setAttribute()`.
   ```javascript
   const link = document.querySelector("a");
   link.setAttribute("href", "https://www.example.com");
   console.log(link.getAttribute("href")); // Output: https://www.example.com
   ```

   - **Mengambil Nilai dari Input**
     Anda bisa mengambil nilai dari elemen input dengan menggunakan properti `value`.
   ```javascript
   const input = document.getElementById("myInput");
   console.log(input.value); // Output: Nilai input dari elemen dengan ID "myInput"
   ```

### 3. **Menambah dan Menghapus Elemen DOM**
   - **Menambah Elemen Baru**
     Untuk menambah elemen baru ke DOM, gunakan `createElement()` untuk membuat elemen dan `appendChild()` untuk menambahkannya.
   ```javascript
   const newElement = document.createElement("div");
   newElement.textContent = "Ini adalah elemen baru";
   document.body.appendChild(newElement);
   ```

   - **Menghapus Elemen**
     Untuk menghapus elemen dari DOM, gunakan `removeChild()` pada elemen induk.
   ```javascript
   const element = document.getElementById("myElement");
   element.parentNode.removeChild(element);
   ```

### 4. **Menangani Event**
   - **Menambahkan Event Listener**
     Untuk menangani event seperti klik, Anda dapat menggunakan `addEventListener()` untuk menambahkan event listener pada elemen.
   ```javascript
   const button = document.getElementById("myButton");
   button.addEventListener("click", function() {
     alert("Tombol diklik!");
   });
   ```

   - **Event Propagation**
     Anda bisa menangani event pada elemen tertentu dan kemudian mencegah event tersebut diteruskan ke elemen lainnya.
   ```javascript
   const parent = document.getElementById("parent");
   parent.addEventListener("click", function(event) {
     alert("Klik pada parent!");
     event.stopPropagation(); // Mencegah event diteruskan ke elemen lain
   });

   const child = document.getElementById("child");
   child.addEventListener("click", function() {
     alert("Klik pada child!");
   });
   ```

   - **Event Delegation**
     Ini adalah teknik di mana Anda menangani event pada elemen induk yang lebih umum dan memeriksa elemen target yang diklik.
   ```javascript
   document.getElementById("parent").addEventListener("click", function(event) {
     if (event.target && event.target.matches("button.className")) {
       alert("Tombol dengan className diklik!");
     }
   });
   ```

### 5. **Mengubah Gaya CSS Elemen**
   Anda dapat mengubah gaya CSS elemen menggunakan properti `style`.
   ```javascript
   const element = document.getElementById("myElement");
   element.style.color = "red";
   element.style.backgroundColor = "yellow";
   element.style.fontSize = "20px";
   ```

### 6. **Animasi dengan CSS dan JavaScript**
   - **Animasi CSS**
     Anda bisa menambahkan animasi CSS ke elemen dengan menggunakan kelas dan `@keyframes` di CSS.
   ```css
   @keyframes example {
     from { background-color: red; }
     to { background-color: yellow; }
   }

   #myElement {
     animation: example 2s infinite;
   }
   ```

   - **Animasi JavaScript**
     Anda bisa membuat animasi menggunakan JavaScript, seperti dengan mengubah gaya secara bertahap.
   ```javascript
   let element = document.getElementById("myElement");
   let pos = 0;
   function move() {
     if (pos === 200) {
       clearInterval(id);
     } else {
       pos++;
       element.style.left = pos + "px";
     }
   }
   let id = setInterval(move, 10); // Animasi bergerak ke kanan
   ```

Semoga contoh-contoh ini memberikan gambaran tentang bagaimana memanipulasi DOM di JavaScript!