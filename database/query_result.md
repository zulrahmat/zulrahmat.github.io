**1. Mengambil Semua Hasil Query:**

### **`getResult()`** ###
Mengembalikan semua baris hasil sebagai array objek.

  *Contoh penggunaan:*
  
```php
  $query = $db->query('SELECT * FROM users');
  $results = $query->getResult();
  foreach ($results as $row) {
      echo $row->name;
  }
  ```

### **`getResultArray()`** ###
Mengembalikan semua baris hasil sebagai array asosiatif.

  *Contoh penggunaan:*
  
```php
  $query = $db->query('SELECT * FROM users');
  $results = $query->getResultArray();
  foreach ($results as $row) {
      echo $row['name'];
  }
  ```
**2. Mengambil Baris Tertentu dari Hasil Query:**

- **`getRow()`**: Mengembalikan satu baris hasil sebagai objek. Jika parameter angka diberikan, mengembalikan baris ke-n (dimulai dari 0).

  *Contoh penggunaan:*
  
```php
  $query = $db->query('SELECT * FROM users');
  $row = $query->getRow(); // Baris pertama
  echo $row->name;
  ```

### **`getRowArray()`** ### 
Serupa dengan `getRow()`, tetapi mengembalikan baris sebagai array asosiatif.

  *Contoh penggunaan:*
  
```php
  $query = $db->query('SELECT * FROM users');
  $row = $query->getRowArray();
  echo $row['name'];
```

### **`getUnbufferedRow()`** ### 
Mengembalikan satu baris hasil tanpa memuat semua hasil ke dalam memori, berguna untuk menangani set data besar.

  *Contoh penggunaan:*
  
```php
  $query = $db->query('SELECT * FROM users');
  while ($row = $query->getUnbufferedRow()) {
      echo $row->name;
  }
  ```

**3. Metode Navigasi Hasil Query:**

- **`getFirstRow()`**: Mengambil baris pertama dari hasil query.
- **`getLastRow()`**: Mengambil baris terakhir dari hasil query.
- **`getNextRow()`**: Mengambil baris berikutnya dari posisi saat ini.
- **`getPreviousRow()`**: Mengambil baris sebelumnya dari posisi saat ini.

*Catatan:* Metode-metode ini secara default mengembalikan objek. Untuk mendapatkan array asosiatif, berikan parameter `'array'`.

*Contoh penggunaan:*

```php
$row = $query->getFirstRow('array');
echo $row['name'];
```
