Berikut ringkasan topik dari URL **CodeIgniter Email Library** (https://codeigniter.com/user_guide/libraries/email.html):

### **1. Pengantar**  
- Library Email CodeIgniter memudahkan pengiriman email dengan dukungan protokol **SMTP**, **Sendmail**, dan **mail()** (PHP bawaan).  
- Mendukung fitur seperti **enkripsi (TLS/SSL)**, multiple recipient, attachment, dan HTML/CSS.

### **2. Konfigurasi Email**  
- File konfigurasi: **app/Config/Email.php**.  
- Pengaturan utama:  
  - Protokol (`$protocol`: SMTP, mail, sendmail).  
  - SMTP Host, Port, Username, Password.  
  - Enkripsi (`$SMTPCrypto`: TLS/SSL).  
  - Pengaturan charset, word wrapping, dll.  

### **3. Mengirim Email**  
- **Contoh dasar**:  
  ```php
  $email = \Config\Services::email();
  $email->setFrom('pengirim@example.com', 'Nama Pengirim');
  $email->setTo('penerima@example.com');
  $email->setSubject('Subjek Email');
  $email->setMessage('Isi pesan');
  $email->send();
  ```

### **4. Fitur Lanjutan**  
- **Attachment**:  
  ```php
  $email->attach('/path/to/file.pdf');
  ```
- **CC/BCC**:  
  ```php
  $email->setCC('cc@example.com');
  $email->setBCC('bcc@example.com');
  ```
- **Email Alternatif (HTML/Teks)**:  
  ```php
  $email->setMailType('html'); // atau 'text'
  ```
- **Batch Mode**: Untuk mengirim ke banyak penerima.  

### **5. Debugging**  
- Cek error dengan:  
  ```php
  if (!$email->send()) {
      echo $email->printDebugger();
  }
  ```

### **6. Customisasi**  
- Override konfigurasi runtime:  
  ```php
  $email->initialize(['mailType' => 'html']);
  ```

### **7. Catatan Penting**  
- Pastikan server email (SMTP) dikonfigurasi dengan benar.  
- Untuk pengiriman massal, pertimbangkan antrian (queue) agar tidak timeout.

### **Kesimpulan**  
Library Email CodeIgniter menyederhanakan pengiriman email dengan fitur lengkap dan fleksibilitas konfigurasi. Cocok untuk aplikasi kecil hingga menengah.  

Jika butuh detail lebih lanjut, lihat dokumentasi resmi atau contoh kode di URL tersebut.