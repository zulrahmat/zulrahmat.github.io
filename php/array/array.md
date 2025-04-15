Di PHP, array memiliki banyak fungsi bawaan yang dapat digunakan untuk berbagai operasi, seperti manipulasi data dan pengelolaan struktur array. Berikut adalah kelompok fungsi-fungsi array yang umum digunakan:

### 1. **Fungsi untuk Membuat Array**
   - `array()`: Membuat array baru.
   - `range()`: Membuat array dengan nilai yang terurut dalam rentang tertentu.

### 2. **Fungsi untuk Mengakses Elemen Array**
   - `array_shift()`: Menghapus elemen pertama dari array dan mengembalikannya.
   - `array_pop()`: Menghapus elemen terakhir dari array dan mengembalikannya.
   - `array_slice()`: Mengambil potongan bagian dari array.
   - `array_splice()`: Memotong bagian dari array dan menggantinya dengan array lain.
   - `array_key_exists()`: Memeriksa apakah sebuah kunci ada dalam array.
   - `in_array()`: Memeriksa apakah sebuah nilai ada dalam array.

### 3. **Fungsi untuk Manipulasi Array**
   - `array_push()`: Menambahkan satu atau lebih elemen ke akhir array.
   - `array_unshift()`: Menambahkan satu atau lebih elemen ke awal array.
   - `array_merge()`: Menggabungkan dua atau lebih array.
   - `array_diff()`: Membandingkan dua array dan mengembalikan elemen yang ada di array pertama namun tidak ada di array lainnya.
   - `array_intersect()`: Mengembalikan elemen yang ada pada semua array yang dibandingkan.
   - `array_map()`: Menerapkan fungsi tertentu ke setiap elemen dalam array.
   - `array_walk()`: Menerapkan fungsi ke setiap elemen dalam array, memodifikasi array asli.
   - `array_filter()`: Memfilter elemen array berdasarkan kriteria tertentu.

### 4. **Fungsi untuk Mengurutkan Array**
   - `sort()`: Mengurutkan array secara menaik.
   - `rsort()`: Mengurutkan array secara menurun.
   - `asort()`: Mengurutkan array dengan mempertahankan asosiasi kunci.
   - `ksort()`: Mengurutkan array berdasarkan kunci.
   - `usort()`: Mengurutkan array menggunakan fungsi kustom untuk perbandingan.

### 5. **Fungsi untuk Mencari Nilai dalam Array**
   - `array_search()`: Mencari nilai dalam array dan mengembalikan kunci pertama yang ditemukan.
   - `array_rand()`: Mengambil kunci acak dari array.
   - `array_flip()`: Membalikkan array, menjadikan nilai sebagai kunci dan kunci sebagai nilai.

### 6. **Fungsi untuk Menghitung Elemen Array**
   - `count()`: Menghitung jumlah elemen dalam array.
   - `array_sum()`: Menghitung jumlah dari semua nilai dalam array.
   - `array_product()`: Menghitung hasil perkalian dari semua elemen array.

### 7. **Fungsi untuk Penggabungan dan Perbandingan Array**
   - `array_unique()`: Menghapus elemen duplikat dari array.
   - `array_diff_key()`: Membandingkan dua array berdasarkan kunci dan mengembalikan perbedaan.
   - `array_merge_recursive()`: Menggabungkan dua array secara rekursif (menggabungkan array yang memiliki kunci yang sama).

### 8. **Fungsi untuk Array Asosiatif**
   - `array_keys()`: Mengambil semua kunci dari array.
   - `array_values()`: Mengambil semua nilai dari array.
   - `array_change_key_case()`: Mengubah kapitalisasi kunci array (menjadi uppercase atau lowercase).

Ini hanya beberapa contoh fungsi array di PHP, dan ada banyak lagi yang bisa digunakan tergantung pada kebutuhan Anda. Fungsi-fungsi tersebut sangat membantu dalam memanipulasi dan mengelola data dalam bentuk array.