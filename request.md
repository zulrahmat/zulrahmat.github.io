### Request

```php

echo $request->getIPAddress();

if( ! $request->isValidIP($ip)) {
    echo 'valid';
} else {
    echo 'tidak valid';
}

```
