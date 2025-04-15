Gas terus! 🚀 Kita lanjut ke:

---

### 🌍 **Kelompok 5 – Fungsi Zona Waktu**

Fungsi-fungsi ini digunakan untuk mendapatkan, mengatur, dan bekerja dengan *timezone* (zona waktu), penting banget untuk aplikasi global atau multi-region.

```php
<?php
// date_default_timezone_get() – ambil zona waktu default saat ini
echo "Zona waktu default: " . date_default_timezone_get() . "\n";

// date_default_timezone_set() – set zona waktu default
date_default_timezone_set("Asia/Jakarta");
echo "Setelah diset ke Asia/Jakarta: " . date('Y-m-d H:i:s') . "\n";

// timezone_identifiers_list() – daftar semua nama zona waktu yang valid
$zonaList = timezone_identifiers_list();
echo "Contoh zona waktu: " . implode(", ", array_slice($zonaList, 0, 5)) . "...\n";

// timezone_name_get() – ambil nama timezone dari objek DateTimeZone
$tz = new DateTimeZone("Europe/London");
echo "Nama timezone: " . timezone_name_get($tz) . "\n";

// timezone_offset_get() – ambil offset (selisih dari UTC dalam detik)
$dt = new DateTime("now", $tz);
echo "Offset dari UTC (London): " . timezone_offset_get($tz, $dt) . " detik\n";

// timezone_open() – buat objek DateTimeZone dari string nama zona
$tzObj = timezone_open("America/New_York");
print_r($tzObj);
?>
```

---

### Penjelasan Singkat:
- `date_default_timezone_get()`: Lihat default timezone yang sedang aktif.
- `date_default_timezone_set()`: Set timezone default agar semua waktu sesuai lokasi tertentu.
- `timezone_identifiers_list()`: Dapatkan semua zona waktu yang dikenali PHP (berguna untuk dropdown).
- `timezone_name_get()`: Ambil nama zona dari objek `DateTimeZone`.
- `timezone_offset_get()`: Selisih waktu dari UTC dalam detik.
- `timezone_open()`: Buat objek zona waktu dari string.

---

Kalau kamu udah paham semua lima kelompok fungsi waktu di PHP ini, next kita bisa latihan bikin **fungsi utilitas tanggal/waktu**, atau bikin fitur seperti:
- konversi tanggal lokal ke UTC,
- kalkulator usia,
- kalender dinamis, dll.

Mau lanjut ke latihan atau ada bagian yang mau diulas ulang dulu?