Siap, kita lanjut ke:

---

### ⏱️ **Kelompok 4 – Fungsi Durasi dan Interval**

Fungsi-fungsi ini berguna untuk mengukur selisih waktu dan membuat interval durasi.

```php
<?php
// microtime(true) – hitung durasi eksekusi (benchmark sederhana)
$start = microtime(true);

// Simulasi proses
usleep(500000); // 0.5 detik

$end = microtime(true);
echo "Durasi eksekusi: " . ($end - $start) . " detik\n";

// hrtime() – high resolution time (lebih presisi, PHP 7.3+)
$startHigh = hrtime(true); // nanodetik

usleep(100000); // 0.1 detik

$endHigh = hrtime(true);
$diffNano = $endHigh - $startHigh;
echo "Durasi (hrtime): " . ($diffNano / 1e9) . " detik\n";

// date_diff() – hitung selisih antara dua DateTime
$date1 = date_create("2025-04-15 08:00:00");
$date2 = date_create("2025-04-16 10:30:00");
$diff = date_diff($date1, $date2);
echo "Selisih waktu: " . $diff->format('%d hari, %h jam, %i menit') . "\n";

// date_interval_create_from_date_string() – buat interval dari string
$interval = date_interval_create_from_date_string('3 days 4 hours');
print_r($interval);

// date_interval_format() – format objek interval
echo "Interval diformat: " . date_interval_format($interval, '%d hari, %h jam') . "\n";
?>
```

---

### Penjelasan Singkat:
- `microtime(true)`: Cocok untuk menghitung durasi proses.
- `hrtime(true)`: Presisi tinggi (nanodetik), ideal untuk profiling performa.
- `date_diff()`: Menghitung selisih antar waktu sebagai objek `DateInterval`.
- `date_interval_create_from_date_string()`: Buat interval durasi dari teks.
- `date_interval_format()`: Tampilkan isi `DateInterval` dengan format fleksibel.

---

Kalau udah mantap bagian ini, kita lanjut ke **Kelompok 5: Fungsi Zona Waktu** ya? Mau lanjut sekarang?