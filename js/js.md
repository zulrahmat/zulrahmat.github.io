- [Clipboard API](clipboard.md)
- [Json](json.md)
- [Storage](storage.md)
- [Fetch](fetch.md)
- [Clipboard](clipboard.md)



Berikut adalah daftar fitur JavaScript yang dikelompokkan berdasarkan fungsinya:

### [1. **Fitur Pengelolaan Data**](js_1.md)
   - **Variabel**: `let`, `const`, `var` (untuk mendeklarasikan variabel)
   - **Tipe Data**: `string`, `number`, `boolean`, `undefined`, `null`, `symbol`, `bigint`, `object`
   - **Array**: `Array()`, `push()`, `pop()`, `shift()`, `unshift()`, `slice()`, `splice()`, `map()`, `filter()`, `reduce()`
   - **Object**: `Object()`, `Object.keys()`, `Object.values()`, `Object.entries()`, `hasOwnProperty()`
   - **Set dan Map**:
     - `Set()`, `add()`, `delete()`, `has()`, `clear()`
     - `Map()`, `set()`, `get()`, `has()`, `delete()`, `clear()`
   
### [2. **Pengendalian Alur Program (Control Flow)**](js_2.md)
   - **Percabangan**: `if`, `else`, `else if`, `switch`
   - **Perulangan**: `for`, `for...of`, `for...in`, `while`, `do...while`
   - **Penghentian Loop**: `break`, `continue`, `return`
   - **Exception Handling**: `try`, `catch`, `finally`, `throw`

### [3. **Fitur Fungsi**](js_3.md)
   - **Function Declaration**: `function namaFungsi() {}`
   - **Arrow Function**: `(parameter) => {}`  
   - **Function Expression**: `const fungsi = function() {};`
   - **IIFE (Immediately Invoked Function Expression)**: `(function() { /* kode */ })();`
   - **Parameter Default**: `function example(a = 5) {}`
   - **Rest Parameters**: `function example(...args) {}`
   - **Spread Operator**: `...args`

### [4. **Manipulasi DOM (Document Object Model)**](js_4.md)
   - **Memilih Elemen**: `document.getElementById()`, `document.getElementsByClassName()`, `document.querySelector()`, `document.querySelectorAll()`
   - **Menambah/Modifikasi Elemen**: `createElement()`, `appendChild()`, `removeChild()`, `insertBefore()`, `setAttribute()`, `getAttribute()`, `innerHTML`, `textContent`
   - **Event Handling**: `addEventListener()`, `removeEventListener()`, `event.target`

### [5. **Asynchronous Programming**](js_5.md)
   - **Callback**: Fungsi yang dipanggil setelah operasi selesai
   - **Promises**: `new Promise()`, `then()`, `catch()`, `finally()`
   - **Async/Await**: `async function`, `await`
   - **setTimeout() dan setInterval()**: Fungsi untuk penundaan dan interval waktu

### [6. **Operasi Array**](js_6.md)
   - **Array Methods**: `map()`, `filter()`, `reduce()`, `forEach()`, `sort()`, `find()`, `findIndex()`
   - **Destructuring Array**: `const [a, b] = [1, 2];`
   - **Array.from() dan Array.isArray()**

### [7. **Operasi Object**](js_7.md)
   - **Destructuring Object**: `const {name, age} = person;`
   - **Object Methods**: `Object.assign()`, `Object.freeze()`, `Object.seal()`
   - **Computed Property Names**: `const obj = { [key]: value };`
   - **Object Destructuring**: `const {name} = person;`

### [8. **Modularisasi Kode**](js_8.md)
   - **Export dan Import**: `export { functionName };` dan `import { functionName } from './module';`
   - **Module System**: CommonJS, ES6 Modules

### [9. **Fitur ES6 dan Versi Terbaru**](js_9.md)
   - **Let dan Const** (Variabel dengan scope blok)
   - **Arrow Functions** (Sintaksis singkat untuk fungsi)
   - **Template Literals**: `` `Hello ${name}!` ``
   - **Destructuring**: Menarik nilai dari array atau objek
   - **Classes**: Sintaksis kelas untuk objek dan pewarisan
   - **Iterators dan Generators**: `for...of`, `function*`, `yield`

### [10. **Fitur untuk Pengelolaan Waktu dan Tanggal**](js_10.md)
   - **Date Object**: `new Date()`, `Date.now()`, `getDate()`, `getFullYear()`, `setMonth()`
   - **Intl.DateTimeFormat**: Format tanggal dan waktu
   - **setTimeout() dan setInterval()**

### 11. **Fitur Web APIs**
   - **Geolocation API**: `navigator.geolocation.getCurrentPosition()`
   - **Fetch API**: `fetch()`, `Response.json()`, `then()`, `catch()`
   - **LocalStorage / SessionStorage**: `localStorage.setItem()`, `localStorage.getItem()`
   - **WebSockets**: `new WebSocket()`, `onopen`, `onmessage`

### 12. **Fitur Browser**
   - **Browser Object Model (BOM)**: `window`, `navigator`, `screen`, `history`, `location`
   - **Cookies**: `document.cookie`
   - **Event Loop dan Stack**: Asynchronous event handling

### 13. **Fitur Lainnya**
   - **Regular Expressions (RegEx)**: `/pattern/`, `test()`, `exec()`, `match()`, `replace()`
   - **JSON**: `JSON.parse()`, `JSON.stringify()`
   - **SetTimeout**: Untuk menunda eksekusi kode
   - **Eval()**: Mengeksekusi string sebagai kode JavaScript (sering dihindari karena masalah keamanan)

Semoga daftar ini membantu kamu dalam memahami fitur-fitur JavaScript!