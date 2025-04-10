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

