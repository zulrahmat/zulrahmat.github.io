### Request


```php

$request = service('request');

echo $request->getIPAddress(); 
# "0.0.0.0"

echo $request->getMethod();
# "POST"

echo $request->getPost('foo');
echo $request->getGet('foo');
echo $request->getCookie('foo');
echo $request->getServer('foo');

# check $_POST lalu $_GET
echo $request->getPostGet('foo');

# check $_GET lalu $_POST
echo $request->getGetPost('foo');







if( ! $request->isValidIP($ip)) {
    echo 'valid';
} else {
    echo 'tidak valid';
}

```

