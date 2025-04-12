```php
helper('cookie');

set_cookie('nama', 'zulrahmat', 3600); // 3600 = 1 jam
set_cookie('nama', 'zulrahmat', 86400); // simpan selama 1 hari
set_cookie('nama', 'zulrahmat', 0) //simpan sampai browser ditutup

# apabila array
set_cookie([
  'name'   => 'nama',
  'value'  => 'isi_cookie',
  'expire' => 3600, // dalam detik
  'path'   => '/',
  'secure' => false, // true jika menggunakan HTTPS
  'httponly' => true
]);
```
### Menambah Cookie pada response
```php
$response = service('response');
$response->setCookie('nama', 'isi_cookie', 3600);
```
### Mengambil Cookie
```php
$cookie = get_cookie('nama');
```
### Mengamil Cookie via request object
```php
$request = service('request');
$cookie = $request->getCookie('nama');
```
### Hapus Cookie
```php
delete_cookie('nama');

# hapus Response Object
$response = service('response');
$response->deleteCookie('nama');
```