Tentu! Berikut adalah contoh penggunaan fungsi array PHP secara singkat dan sederhana mulai dari nomor 1:

### 1. **Fungsi untuk Membuat Array**
   - `array()`: Membuat array baru.
   ```php
   $fruits = array("Apple", "Banana", "Cherry");
   print_r($fruits);
   ```

   - `range()`: Membuat array dengan nilai yang terurut dalam rentang tertentu.
   ```php
   $numbers = range(1, 5); // Array(1, 2, 3, 4, 5)
   print_r($numbers);
   ```

### 2. **Fungsi untuk Mengakses Elemen Array**
   - `array_shift()`: Menghapus elemen pertama dari array dan mengembalikannya.
   ```php
   $fruits = array("Apple", "Banana", "Cherry");
   $first = array_shift($fruits); // Menghapus 'Apple'
   echo $first; // Output: Apple
   print_r($fruits); // Output: Array ( [0] => Banana [1] => Cherry )
   ```

   - `array_pop()`: Menghapus elemen terakhir dari array dan mengembalikannya.
   ```php
   $fruits = array("Apple", "Banana", "Cherry");
   $last = array_pop($fruits); // Menghapus 'Cherry'
   echo $last; // Output: Cherry
   print_r($fruits); // Output: Array ( [0] => Apple [1] => Banana )
   ```

   - `array_slice()`: Mengambil potongan bagian dari array.
   ```php
   $fruits = array("Apple", "Banana", "Cherry", "Date");
   $slice = array_slice($fruits, 1, 2); // Mengambil 2 elemen mulai dari index 1
   print_r($slice); // Output: Array ( [0] => Banana [1] => Cherry )
   ```

   - `array_splice()`: Memotong bagian dari array dan menggantinya dengan array lain.
   ```php
   $fruits = array("Apple", "Banana", "Cherry");
   array_splice($fruits, 1, 1, "Orange"); // Mengganti "Banana" dengan "Orange"
   print_r($fruits); // Output: Array ( [0] => Apple [1] => Orange [2] => Cherry )
   ```

   - `array_key_exists()`: Memeriksa apakah sebuah kunci ada dalam array.
   ```php
   $person = ["name" => "John", "age" => 30];
   if (array_key_exists("age", $person)) {
       echo "Age exists!";
   }
   ```

   - `in_array()`: Memeriksa apakah sebuah nilai ada dalam array.
   ```php
   $fruits = ["Apple", "Banana", "Cherry"];
   if (in_array("Banana", $fruits)) {
       echo "Banana is in the array!";
   }
   ```

### 3. **Fungsi untuk Manipulasi Array**
   - `array_push()`: Menambahkan satu atau lebih elemen ke akhir array.
   ```php
   $fruits = ["Apple", "Banana"];
   array_push($fruits, "Cherry", "Date");
   print_r($fruits); // Output: Array ( [0] => Apple [1] => Banana [2] => Cherry [3] => Date )
   ```

   - `array_unshift()`: Menambahkan satu atau lebih elemen ke awal array.
   ```php
   $fruits = ["Apple", "Banana"];
   array_unshift($fruits, "Mango");
   print_r($fruits); // Output: Array ( [0] => Mango [1] => Apple [2] => Banana )
   ```

   - `array_merge()`: Menggabungkan dua atau lebih array.
   ```php
   $fruits1 = ["Apple", "Banana"];
   $fruits2 = ["Cherry", "Date"];
   $allFruits = array_merge($fruits1, $fruits2);
   print_r($allFruits); // Output: Array ( [0] => Apple [1] => Banana [2] => Cherry [3] => Date )
   ```

   - `array_diff()`: Membandingkan dua array dan mengembalikan elemen yang ada di array pertama namun tidak ada di array lainnya.
   ```php
   $array1 = [1, 2, 3, 4];
   $array2 = [3, 4, 5, 6];
   $result = array_diff($array1, $array2);
   print_r($result); // Output: Array ( [0] => 1 [1] => 2 )
   ```

   - `array_intersect()`: Mengembalikan elemen yang ada pada semua array yang dibandingkan.
   ```php
   $array1 = [1, 2, 3, 4];
   $array2 = [3, 4, 5, 6];
   $result = array_intersect($array1, $array2);
   print_r($result); // Output: Array ( [2] => 3 [3] => 4 )
   ```

### 4. **Fungsi untuk Mengurutkan Array**
   - `sort()`: Mengurutkan array secara menaik.
   ```php
   $numbers = [4, 1, 3, 2];
   sort($numbers);
   print_r($numbers); // Output: Array ( [0] => 1 [1] => 2 [2] => 3 [3] => 4 )
   ```

   - `rsort()`: Mengurutkan array secara menurun.
   ```php
   $numbers = [4, 1, 3, 2];
   rsort($numbers);
   print_r($numbers); // Output: Array ( [0] => 4 [1] => 3 [2] => 2 [3] => 1 )
   ```

### 5. **Fungsi untuk Mencari Nilai dalam Array**
   - `array_search()`: Mencari nilai dalam array dan mengembalikan kunci pertama yang ditemukan.
   ```php
   $fruits = ["Apple", "Banana", "Cherry"];
   $key = array_search("Banana", $fruits);
   echo $key; // Output: 1
   ```

   - `array_rand()`: Mengambil kunci acak dari array.
   ```php
   $fruits = ["Apple", "Banana", "Cherry"];
   $randomKey = array_rand($fruits);
   echo $fruits[$randomKey]; // Output: (random fruit)
   ```

   - `array_flip()`: Membalikkan array, menjadikan nilai sebagai kunci dan kunci sebagai nilai.
   ```php
   $array = ["a" => 1, "b" => 2];
   $flipped = array_flip($array);
   print_r($flipped); // Output: Array ( [1] => a [2] => b )
   ```

### 6. **Fungsi untuk Menghitung Elemen Array**
   - `count()`: Menghitung jumlah elemen dalam array.
   ```php
   $fruits = ["Apple", "Banana", "Cherry"];
   echo count($fruits); // Output: 3
   ```

   - `array_sum()`: Menghitung jumlah dari semua nilai dalam array.
   ```php
   $numbers = [1, 2, 3, 4];
   echo array_sum($numbers); // Output: 10
   ```

   - `array_product()`: Menghitung hasil perkalian dari semua elemen array.
   ```php
   $numbers = [1, 2, 3, 4];
   echo array_product($numbers); // Output: 24
   ```

### 7. **Fungsi untuk Penggabungan dan Perbandingan Array**
   - `array_unique()`: Menghapus elemen duplikat dari array.
   ```php
   $numbers = [1, 2, 2, 3, 3, 4];
   $uniqueNumbers = array_unique($numbers);
   print_r($uniqueNumbers); // Output: Array ( [0] => 1 [1] => 2 [3] => 3 [5] => 4 )
   ```

### 8. **Fungsi untuk Array Asosiatif**
   - `array_keys()`: Mengambil semua kunci dari array.
   ```php
   $person = ["name" => "John", "age" => 30];
   print_r(array_keys($person)); // Output: Array ( [0] => name [1] => age )
   ```

   - `array_values()`: Mengambil semua nilai dari array.
   ```php
   $person = ["name" => "John", "age" => 30];
   print_r(array_values($person)); // Output: Array ( [0] => John [1] => 30 )
   ```

Itulah beberapa contoh penggunaan fungsi array di PHP. Setiap fungsi memiliki kegunaan tertentu dalam manipulasi dan pengelolaan array.