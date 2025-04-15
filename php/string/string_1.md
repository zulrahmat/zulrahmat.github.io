Berikut adalah contoh penggunaan fungsi-fungsi string PHP secara singkat dan sederhana, dimulai dari kelompok pertama:

### 1. **Fungsi Pengambilan Substring**
#### `substr()`
```php
$string = "Hello, World!";
$substring = substr($string, 7, 5); // Mengambil 5 karakter mulai dari indeks 7
echo $substring; // Output: World
```

#### `substr_replace()`
```php
$string = "Hello, World!";
$replace = substr_replace($string, "PHP", 7, 5); // Mengganti "World" dengan "PHP"
echo $replace; // Output: Hello, PHP!
```

#### `strstr()`
```php
$string = "Hello, World!";
$result = strstr($string, "World"); // Mengambil substring mulai dari "World"
echo $result; // Output: World!
```

#### `strrchr()`
```php
$string = "Hello, World!";
$result = strrchr($string, "o"); // Mengambil substring dari kemunculan terakhir "o"
echo $result; // Output: orld!
```

### 2. **Fungsi Pencarian dan Penggantian**
#### `strpos()`
```php
$string = "Hello, World!";
$position = strpos($string, "World"); // Mencari posisi pertama kemunculan "World"
echo $position; // Output: 7
```

#### `strrpos()`
```php
$string = "Hello, World!";
$position = strrpos($string, "o"); // Mencari posisi terakhir kemunculan "o"
echo $position; // Output: 8
```

#### `str_replace()`
```php
$string = "Hello, World!";
$replaced = str_replace("World", "PHP", $string); // Mengganti "World" dengan "PHP"
echo $replaced; // Output: Hello, PHP!
```

#### `str_ireplace()`
```php
$string = "Hello, world!";
$replaced = str_ireplace("world", "PHP", $string); // Mengganti "world" (case-insensitive) dengan "PHP"
echo $replaced; // Output: Hello, PHP!
```

### 3. **Fungsi Pembersihan dan Pemotongan String**
#### `trim()`
```php
$string = "  Hello, World!  ";
$trimmed = trim($string); // Menghapus spasi di awal dan akhir string
echo $trimmed; // Output: Hello, World!
```

#### `ltrim()`
```php
$string = "  Hello, World!";
$leftTrimmed = ltrim($string); // Menghapus spasi di sisi kiri string
echo $leftTrimmed; // Output: Hello, World!
```

#### `rtrim()`
```php
$string = "Hello, World!  ";
$rightTrimmed = rtrim($string); // Menghapus spasi di sisi kanan string
echo $rightTrimmed; // Output: Hello, World!
```

#### `chop()`
```php
$string = "Hello, World!  ";
$chopped = chop($string); // Alias dari rtrim, menghapus spasi di sisi kanan
echo $chopped; // Output: Hello, World!
```

### 4. **Fungsi Pengubahan Kasus (Case Conversion)**
#### `strtoupper()`
```php
$string = "Hello, World!";
$upper = strtoupper($string); // Mengubah seluruh string menjadi huruf besar
echo $upper; // Output: HELLO, WORLD!
```

#### `strtolower()`
```php
$string = "Hello, World!";
$lower = strtolower($string); // Mengubah seluruh string menjadi huruf kecil
echo $lower; // Output: hello, world!
```

#### `ucwords()`
```php
$string = "hello, world!";
$capitalized = ucwords($string); // Mengubah huruf pertama dari setiap kata menjadi huruf besar
echo $capitalized; // Output: Hello, World!
```

#### `ucfirst()`
```php
$string = "hello, world!";
$capitalized = ucfirst($string); // Mengubah huruf pertama dari string menjadi huruf besar
echo $capitalized; // Output: Hello, world!
```

#### `lcfirst()`
```php
$string = "Hello, World!";
$lowered = lcfirst($string); // Mengubah huruf pertama dari string menjadi huruf kecil
echo $lowered; // Output: hello, World!
```

### 5. **Fungsi Penghitungan Karakter dalam String**
#### `strlen()`
```php
$string = "Hello, World!";
$length = strlen($string); // Menghitung panjang string
echo $length; // Output: 13
```

#### `mb_strlen()`
```php
$string = "Hello, World!";
$length = mb_strlen($string); // Menghitung panjang string dengan multi-byte encoding
echo $length; // Output: 13
```

### 6. **Fungsi Pembagian String**
#### `explode()`
```php
$string = "apple,banana,cherry";
$array = explode(",", $string); // Memecah string berdasarkan koma
print_r($array); // Output: Array ( [0] => apple [1] => banana [2] => cherry )
```

#### `implode()`
```php
$array = ["apple", "banana", "cherry"];
$string = implode(",", $array); // Menggabungkan array menjadi string dengan koma
echo $string; // Output: apple,banana,cherry
```

### 7. **Fungsi Pengganti Karakter**
#### `strtr()`
```php
$string = "Hello, World!";
$translated = strtr($string, "HW", "hw"); // Mengganti H dengan h dan W dengan w
echo $translated; // Output: hello, world!
```

#### `str_split()`
```php
$string = "Hello";
$array = str_split($string, 2); // Membagi string menjadi array dengan panjang 2
print_r($array); // Output: Array ( [0] => He [1] => ll [2] => o )
```

### 8. **Fungsi Enkripsi dan Dekripsi String**
#### `md5()`
```php
$string = "Hello, World!";
$hash = md5($string); // Menghasilkan hash MD5 dari string
echo $hash; // Output: fc3ff98e8c6a0d3087d515c0473f8677
```

#### `sha1()`
```php
$string = "Hello, World!";
$hash = sha1($string); // Menghasilkan hash SHA1 dari string
echo $hash; // Output: d3486ae9136e7856bc42212385ea797094475802
```

#### `crypt()`
```php
$password = "secret";
$hashedPassword = crypt($password, "salt"); // Menghasilkan hash dari password dengan salt
echo $hashedPassword; // Output: salt$somethinghashed
```

### 9. **Fungsi Pencocokan Pola (Regular Expression)**
#### `preg_match()`
```php
$string = "Hello, World!";
$pattern = "/World/";
if (preg_match($pattern, $string)) {
    echo "Pattern found!"; // Output: Pattern found!
}
```

#### `preg_replace()`
```php
$string = "Hello, World!";
$pattern = "/World/";
$replace = preg_replace($pattern, "PHP", $string); // Mengganti "World" dengan "PHP"
echo $replace; // Output: Hello, PHP!
```

#### `preg_split()`
```php
$string = "apple,banana,cherry";
$pattern = "/,/";
$array = preg_split($pattern, $string); // Memecah string berdasarkan koma menggunakan regex
print_r($array); // Output: Array ( [0] => apple [1] => banana [2] => cherry )
```

Semoga contoh-contoh ini membantu! Kamu bisa mengembangkan penggunaannya lebih lanjut sesuai kebutuhan.