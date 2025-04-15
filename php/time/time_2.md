Oke, kita lanjut ke:

---

### 📅 **Kelompok 2 – Membuat dan Memanipulasi Tanggal/Waktu**

Berikut contoh penggunaan fungsi-fungsinya:

```php
<?php
// mktime() – buat timestamp dari komponen waktu
$timestamp = mktime(14, 30, 0, 4, 15, 2025); // 15 April 2025, jam 14:30
echo "Timestamp dari mktime: $timestamp\n";
echo "Format tanggal: " . date('Y-m-d H:i:s', $timestamp) . "\n";

// strtotime() – parsing string waktu ke timestamp
$str = "next Monday";
$nextMonday = strtotime($str);
echo "Next Monday: " . date('Y-m-d', $nextMonday) . "\n";

// date_create() – buat objek DateTime
$dt = date_create('2025-04-15 12:00:00');
echo "DateTime awal: " . date_format($dt, 'Y-m-d H:i:s') . "\n";

// date_modify() – ubah waktu
date_modify($dt, '+1 day');
echo "Setelah tambah 1 hari: " . date_format($dt, 'Y-m-d H:i:s') . "\n";

// date_add() – tambah interval
$interval = date_interval_create_from_date_string('2 hours');
date_add($dt, $interval);
echo "Setelah tambah 2 jam: " . date_format($dt, 'Y-m-d H:i:s') . "\n";

// date_sub() – kurangi interval
$interval2 = date_interval_create_from_date_string('30 minutes');
date_sub($dt, $interval2);
echo "Setelah kurang 30 menit: " . date_format($dt, 'Y-m-d H:i:s') . "\n";

// date_create_from_format() – buat DateTime dari format custom
$customDate = date_create_from_format('d-m-Y H:i', '20-04-2025 09:15');
echo "Custom Date: " . date_format($customDate, 'Y-m-d H:i:s') . "\n";
?>
```

---

### Penjelasan Singkat:
- `mktime()`: Buat timestamp dari bagian-bagian waktu.
- `strtotime()`: Parsing teks seperti "tomorrow", "next month".
- `date_create()`: Objek waktu yang fleksibel.
- `date_modify()`, `date_add()`, `date_sub()`: Manipulasi waktu secara dinamis.
- `date_create_from_format()`: Berguna saat parsing input pengguna dengan format non-standar.

---

Kalau sudah paham bagian ini, kita bisa lanjut ke **Kelompok 3: Format dan Konversi Tanggal/Waktu**. Lanjut?