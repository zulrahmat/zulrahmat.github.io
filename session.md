```php
<?php

$session = service('session', $config);
$session = session();
```

### Mengambil Data
```php
$item = $session->get('item');
$item = $session->item;
$item = session('item');

# mengambil array
$userData = $_SESSION;

# or
$userData = $session->get();
```

### Menambah Data
```php
$session->set($array);

$newdata = [
    'username'  => 'johndoe',
    'email'     => 'johndoe@some-site.com',
    'logged_in' => true,
];

$session->set($newdata);

# menambah data seession
$session->set('some_name', 'some_value');

# push nilai baru ke session data
$session->push('hobbies', ['sport'=>'tennis']);
```

### Menghapus Data
```php
unset($_SESSION['some_name']);

#multiple
unset(
    $_SESSION['some_name'],
    $_SESSION['another_name'],
);

$session->remove('some_name');

$array_item = ['username', 'email'];
$session->remove($array_item);

```

### Flash Data
```php
# mark sebagai flash data
$session->markFlashData('item');
$session->markFlashData(['item', 'item2']);

# menambah ke flash data
$_SESSION['item'] = 'value';
$session->markAsFlashdata('item');

$session->setFlashData('item', 'value');

# mengambil flash data
$session->getFlashData();
$session->getFlashData('item');

```

### Menutup Session
```php
$session->destroy();
```