Mantap, kita lanjut ke:

---

### 🔄 **Kelompok 3 – Format dan Konversi Tanggal/Waktu**

Berikut contoh penggunaan fungsi-fungsinya:

```php
<?php
// date_format() – format objek DateTime
$dt = date_create('2025-04-15 14:00:00');
echo "Format DateTime: " . date_format($dt, 'l, d F Y H:i:s') . "\n";

// strftime() – format waktu sesuai lokal (CATATAN: deprecated sejak PHP 8.1)
setlocale(LC_TIME, 'en_US.UTF-8');
echo "strftime (gaya lama): " . strftime("%A, %d %B %Y") . "\n";

// idate() – ambil bagian tertentu dari waktu (angka)
echo "Tahun sekarang: " . idate("Y") . "\n";
echo "Bulan sekarang: " . idate("m") . "\n";
echo "Tanggal sekarang: " . idate("d") . "\n";

// date_parse() – parsing string ke array bagian tanggal
$parsed = date_parse("2025-04-15 16:30:00");
print_r($parsed);

// date_parse_from_format() – parsing dengan format khusus
$parsed2 = date_parse_from_format("d/m/Y H:i", "22/04/2025 08:15");
print_r($parsed2);

// checkdate() – cek validitas tanggal (misal tanggal palsu)
echo "Apakah 30 Februari valid? " . (checkdate(2, 30, 2025) ? "Ya" : "Tidak") . "\n";
echo "Apakah 29 Februari 2024 valid? " . (checkdate(2, 29, 2024) ? "Ya" : "Tidak") . "\n";
?>
```

---

### Penjelasan Singkat:
- `date_format()` – Menampilkan tanggal dari objek `DateTime`.
- `strftime()` – Format lama berbasis lokal, hati-hati deprecated di PHP 8.1.
- `idate()` – Ambil bagian numerik dari tanggal seperti tahun, bulan, hari.
- `date_parse()` – Pecah string waktu jadi bagian-bagian (year, month, dll).
- `date_parse_from_format()` – Sama seperti `date_parse()` tapi dengan format custom.
- `checkdate()` – Untuk validasi input tanggal (berguna saat menerima input user).

---

Kalau sudah oke, selanjutnya kita masuk ke **Kelompok 4: Fungsi Durasi dan Interval**. Lanjut bro?