Di PHP, fungsi manipulasi string dibagi dalam beberapa kategori berdasarkan fungsinya. Berikut adalah beberapa kelompok fungsi manipulasi string yang dapat kamu pelajari:

### [1. **Fungsi Pengambilan Substring**](string_1.md)
- **`substr($string, $start, $length)`**  
  Mengambil bagian dari string mulai dari posisi tertentu.
- **`substr_replace($string, $replacement, $start, $length)`**  
  Mengganti bagian dari string dengan substring baru.
- **`strstr($haystack, $needle)`**  
  Mengambil bagian dari string setelah menemukan substring pertama.
- **`strrchr($haystack, $needle)`**  
  Mengambil bagian dari string setelah menemukan substring terakhir.

### [2. **Fungsi Pencarian dan Penggantian**](string_1.md)
- **`strpos($haystack, $needle)`**  
  Mencari posisi pertama kemunculan substring dalam string.
- **`strrpos($haystack, $needle)`**  
  Mencari posisi terakhir kemunculan substring dalam string.
- **`str_replace($search, $replace, $subject)`**  
  Mencari dan mengganti semua kemunculan substring.
- **`str_ireplace($search, $replace, $subject)`**  
  Mencari dan mengganti semua kemunculan substring, tanpa memperhatikan huruf besar/kecil.
  
### [3. **Fungsi Pembersihan dan Pemotongan String**](string_1.md)
- **`trim($string)`**  
  Menghapus spasi atau karakter lain di awal dan akhir string.
- **`ltrim($string)`**  
  Menghapus spasi atau karakter lain di sisi kiri string.
- **`rtrim($string)`**  
  Menghapus spasi atau karakter lain di sisi kanan string.
- **`chop($string)`**  
  Alias dari `rtrim()`.

### [4. **Fungsi Pengubahan Kasus (Case Conversion)**](string_1.md)
- **`strtoupper($string)`**  
  Mengubah seluruh string menjadi huruf besar.
- **`strtolower($string)`**  
  Mengubah seluruh string menjadi huruf kecil.
- **`ucwords($string)`**  
  Mengubah huruf pertama dari setiap kata menjadi huruf besar.
- **`ucfirst($string)`**  
  Mengubah huruf pertama dari string menjadi huruf besar.
- **`lcfirst($string)`**  
  Mengubah huruf pertama dari string menjadi huruf kecil.

### [5. **Fungsi Penghitungan Karakter dalam String**](string_1.md)
- **`strlen($string)`**  
  Menghitung panjang string (jumlah karakter).
- **`mb_strlen($string, $encoding)`**  
  Menghitung panjang string dalam encoding multi-byte.

### [6. **Fungsi Pembagian String**](string_1.md)
- **`explode($delimiter, $string)`**  
  Memecah string menjadi array berdasarkan pemisah tertentu.
- **`implode($glue, $array)`**  
  Menggabungkan array menjadi string dengan pemisah tertentu.

### [7. **Fungsi Pengganti Karakter**](string_1.md)
- **`strtr($string, $from, $to)`**  
  Mentransformasikan karakter dalam string dengan mengganti karakter tertentu.
- **`str_split($string, $length)`**  
  Membagi string menjadi array dengan panjang tertentu.

### [8. **Fungsi Enkripsi dan Dekripsi String**](string_1.md)
- **`md5($string)`**  
  Menghitung hash MD5 dari string.
- **`sha1($string)`**  
  Menghitung hash SHA1 dari string.
- **`crypt($string, $salt)`**  
  Menghasilkan hash untuk password dengan salt.

### [9. **Fungsi Pencocokan Pola (Regular Expression)**](string_1.md)
- **`preg_match($pattern, $subject)`**  
  Mencocokkan pola dalam string.
- **`preg_replace($pattern, $replacement, $subject)`**  
  Mengganti pola dalam string.
- **`preg_split($pattern, $subject)`**  
  Memecah string berdasarkan pola regex.

Dengan menguasai fungsi-fungsi ini, kamu dapat melakukan banyak manipulasi string di PHP, mulai dari pencarian, penggantian, pemotongan, hingga pengubahan karakter.