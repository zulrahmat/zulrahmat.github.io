Berikut adalah daftar **fungsi-fungsi waktu di PHP** yang sudah **dikelompokkan berdasarkan tujuannya** agar lebih mudah dipahami dan digunakan:

---

### [🕰️ **1. Fungsi Mendapatkan Waktu Saat Ini**](time_1.md)
Digunakan untuk mendapatkan waktu saat ini dalam berbagai format.
| Fungsi | Keterangan |
|--------|------------|
| `time()` | Mengembalikan waktu sekarang dalam format Unix Timestamp |
| `microtime()` | Mengembalikan waktu dengan presisi mikrodetik |
| `date($format)` | Mengembalikan waktu sekarang dalam format tertentu |
| `gmdate($format)` | Seperti `date()`, tapi dalam waktu UTC |
| `getdate()` | Mengembalikan array detail tanggal dan waktu saat ini |
| `localtime()` | Mengembalikan array waktu lokal (mirip `getdate()`) |

---

### [📅 **2. Fungsi Membuat dan Memanipulasi Tanggal/Waktu**](time_2.md)
Digunakan untuk membuat waktu khusus dan melakukan manipulasi.
| Fungsi | Keterangan |
|--------|------------|
| `mktime()` | Membuat Unix Timestamp dari elemen waktu (jam, menit, dsb.) |
| `gmmktime()` | Versi GMT dari `mktime()` |
| `strtotime($string)` | Mengubah string waktu ke Unix Timestamp |
| `date_create()` | Membuat objek `DateTime` |
| `date_modify()` | Mengubah `DateTime` dengan operasi waktu |
| `date_add()` | Menambahkan interval ke `DateTime` |
| `date_sub()` | Mengurangi interval dari `DateTime` |
| `date_time_set()` | Mengatur jam dan menit objek `DateTime` |
| `date_date_set()` | Mengatur tanggal pada objek `DateTime` |
| `date_timestamp_set()` | Mengatur timestamp dari `DateTime` |
| `date_create_from_format()` | Membuat `DateTime` dari string dengan format tertentu |

---

### [🔄 **3. Fungsi Format dan Konversi Tanggal/Waktu**](time_3.md)
Untuk mengubah tanggal/waktu ke string atau sebaliknya.
| Fungsi | Keterangan |
|--------|------------|
| `date_format()` | Mengubah `DateTime` menjadi string format tertentu |
| `strftime()` | Format waktu seperti `date()`, dengan format lokal |
| `idate()` | Mengembalikan bagian numerik dari tanggal seperti tahun, bulan |
| `date_parse()` | Menguraikan string tanggal menjadi array |
| `date_parse_from_format()` | Menguraikan string tanggal dengan format tertentu |
| `checkdate()` | Mengecek validitas tanggal (bulan, hari, tahun) |

---

### [⏱️ **4. Fungsi Durasi dan Interval**](time_4.md)
Berhubungan dengan durasi, interval waktu, dan perbedaan waktu.
| Fungsi | Keterangan |
|--------|------------|
| `microtime(true)` | Waktu sekarang dalam float detik (berguna untuk benchmarking) |
| `hrtime()` | Mendapatkan waktu resolusi tinggi (untuk pengukuran presisi) |
| `date_diff()` | Menghitung selisih antara dua objek `DateTime` |
| `date_interval_create_from_date_string()` | Membuat `DateInterval` dari string |
| `date_interval_format()` | Format interval waktu |

---

### [🌍 **5. Fungsi Zona Waktu**](time_5.md)
Untuk mengatur dan mendapatkan informasi zona waktu.
| Fungsi | Keterangan |
|--------|------------|
| `date_default_timezone_set($timezone)` | Mengatur timezone default |
| `date_default_timezone_get()` | Mendapatkan timezone default |
| `timezone_open()` | Membuat objek `DateTimeZone` |
| `timezone_name_get()` | Mendapatkan nama timezone dari objek |
| `date_timezone_get()` | Mendapatkan timezone dari `DateTime` |
| `timezone_identifiers_list()` | Daftar semua identifier timezone |
| `timezone_location_get()` | Informasi lokasi dari timezone |
| `timezone_offset_get()` | Selisih offset dari timezone terhadap UTC |
| `timezone_name_from_abbr()` | Mendapatkan nama timezone dari singkatan |

---

Kalau kamu mau contoh penggunaan tiap fungsi atau penjelasan lebih lanjut di bagian tertentu (misalnya `DateTime`, `strtotime`, dll), tinggal bilang aja ya!