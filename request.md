### Request
```php

$request = service('request');

# "POST"
echo $request->getPost('foo');
echo $request->getGet('foo');
echo $request->getCookie('foo');
echo $request->getServer('foo');


# check $_POST lalu $_GET
echo $request->getPostGet('foo');

# check $_GET lalu $_POST
echo $request->getGetPost('foo');

```

### JSON
```php
# mengambil JSON
echo $request->getJSON();

# mengambil json variabel
$data = $request->getJsonVar('foo');
echo $request->getJsonVar('fizz.buzz');

# sebagai associative array
echo $request->getJsonVar('fizz', true);
```
### Raw Input
```php
# var
echo $request->getEnv('foo');
echo $request->getVar('foo');
```

```php
echo $request->getIPAddress(); 
# "0.0.0.0"

echo $request->getMethod();

if( ! $request->isValidIP($ip)) {
    echo 'valid';
} else {
    echo 'tidak valid';
}

```
### Filter Data
```php
$email = $request->getPost('email', FILTER_SANITIZE_EMAIL);
```
### Modifikasi Header
```php
var_dump($request->headers());

/*
 * Outputs:
 * [
 *     'Host'          => CodeIgniter\HTTP\Header,
 *     'Cache-Control' => CodeIgniter\HTTP\Header,
 *     'Accept'        => CodeIgniter\HTTP\Header,
 * ]
 */

# cek jika ada header
if ($request->hasHeader('DNT')) {
    // Don't track something...
}

```

### Request URL
```php
$uri = $request->getUri();

echo $uri->getScheme();         // http
echo $uri->getAuthority();      // snoopy:password@example.com:88
echo $uri->getUserInfo();       // snoopy:password
echo $uri->getHost();           // example.com
echo $uri->getPort();           // 88
echo $uri->getPath();           // /path/to/page
echo $uri->getRoutePath();      // path/to/page
echo $uri->getQuery();          // foo=bar&bar=baz
print_r($uri->getSegments());   // Array ( [0] => path [1] => to [2] => page )
echo $uri->getSegment(1);       // path
echo $uri->getTotalSegments();  // 3
```
### Upload File
```php
$file = $request->getFile('userfile');
$files = $request->getFileMultiple('userfile');
```