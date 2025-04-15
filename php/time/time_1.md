Berikut adalah **contoh kode singkat untuk fungsi-fungsi waktu PHP - Kelompok 1: Mendapatkan Waktu Saat Ini**:

---

### 🕰️ **Kelompok 1 – Fungsi Mendapatkan Waktu Saat Ini**

```php
<?php
// time() – Unix timestamp sekarang
echo "Timestamp sekarang: " . time() . "\n";

// microtime() – waktu dalam mikrodetik (default string)
echo "Microtime (string): " . microtime() . "\n";

// microtime(true) – waktu mikrodetik dalam float
echo "Microtime (float): " . microtime(true) . "\n";

// date() – format tanggal dan waktu sekarang
echo "Tanggal sekarang: " . date('Y-m-d H:i:s') . "\n";

// gmdate() – UTC time
echo "GMT sekarang: " . gmdate('Y-m-d H:i:s') . "\n";

// getdate() – array lengkap waktu sekarang
print_r(getdate());

// localtime() – array waktu lokal (default timestamp sekarang)
print_r(localtime());
?>
```

---

Keluaran contoh (kurang lebih seperti ini, tergantung waktu eksekusi):

```
Timestamp sekarang: 1713194550
Microtime (string): 0.12345600 1713194550
Microtime (float): 1713194550.123456
Tanggal sekarang: 2025-04-15 13:22:30
GMT sekarang: 2025-04-15 06:22:30
Array
(
    [seconds] => 30
    [minutes] => 22
    [hours] => 13
    [mday] => 15
    [wday] => 2
    [mon] => 4
    [year] => 2025
    [yday] => 104
    [weekday] => Tuesday
    [month] => April
    [0] => 1713194550
)
Array
(
    [0] => 30
    [1] => 22
    [2] => 13
    [3] => 15
    [4] => 3
    [5] => 125
    [6] => 2
    [7] => 0
    [8] => 0
)
```

---

Kalau kamu setuju, kita bisa lanjut ke **Kelompok 2: Membuat dan Memanipulasi Tanggal/Waktu** selanjutnya. Mau lanjut?