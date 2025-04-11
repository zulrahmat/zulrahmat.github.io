```php
<?php

return redirect()->to('admin/home');

# redirect ke route yang bernama user_gallery
return redirect()->route('user_gallery');

# redirect name_route
return redirect('name_route');
```
### Redirect Back
```php
# kembalikan ke halaman sebelumnya
return redirect()->back();

# kembali dengan nilai input yang lama
return redirect()->back()->withInput();

# redirect dengan flash data
return redirect()->back()->with('foo', 'message');

# redirect with cookie
return redirect()->back()->withCookies();

# redirect with header
return redirect()->back()->withHeaders();

# redirect with status code
return redirect()->back(302);
return redirect()->to('admin/home', 301);

```

### Force File Download
```php
$data = "Here is some text";
$name = "mytext.txt";

return $this->response->download($name, $data);

// konten photo.jpg akan secara otomatis
return $this->response->download('/path/to/photo.jpg', null);

return $this->response
            ->download('awkwardEncryptFileName.fakeExt', null)
            ->setFileName('expenses.csv');

```

### Open File In Browser
```php
$data = "Here is some text";
$name = "mytext.txt";

return $this->response->download($name, $data)->inline();
```

### Method
```php

# method

# mengambil status code
echo  $response->getStatusCode();


# set status code
$response->setStatusCode(404);
$response->setStatusCode(230, 'Tardis Initiated');

# mengambil status code dari response ini
echo $response->getReasonPhase();

# set tipe konten 
$response->setContentType('text/plain');
$response->setContentType('text/html');
$response->setContentType('application/json');

# cek cookie
if($response->hasCookie($name)) {
    // ...
}

# mengambil cookie
$cookie = $response->getCookie($name);
$cookies = $response->getCookies();

# delete cookie
$response->deleteCookie($name);

```