### Routing

```php

$routes->get('/', 'Home::index');
$routes->post('products', 'Product::feature');
$routes->put('products/1', 'Product::feature');
$routes->delete('products/1', 'Product::feature');

# call $Users->list()
$routes->get('users', 'Users::list');

# calls $Users->list(1,23)
$routes->get('users/1/23', 'Users::list/1/23');

# menggunakan match
$routes->match(['GET', 'PUT'], 'products', 'Product::feature');
```

### Named Route
```php
$routes->get('users/profile', 'Users::profile', ['as'=>'profile']);
```

### Placeholder
```php
# match any integer
$routes->get('product/(:num)', 'Catalog::productLookup/$1');

# match semua karakter sampai ke akhir URI
$routes->get('product/(:any)', 'Catalog::productLookup/$1');

# match di antara karakter /
$routes->get('product/(:segment)/edit', 'Catalog::productLookup/$1');

# match huruf alpha
$routes->get('product/(:alpha)/edit', 'Catalog::productLookup/$1');

# match huruf alpha numeric
$routes->get('product/(:alphanum)/edit', 'Catalog::productLookup/$1');

# match hash
$routes->get('product/(:hash)/edit', 'Catalog::productLookup/$1');
```

### Namespace
```php
// Routes to \App\Controllers\Api\Users::update()
$routes->post('api/users', 'Api\Users::update');

// Routes to \Acme\Blog\Controllers\Home::list()
$routes->get('blog', '\Acme\Blog\Controllers\Home::list');

// Routes to \Admin\Users::index()
$routes->get('admin/users', 'Users::index', ['namespace' => 'Admin']);
```

### Grouping Route
```php
# admin
$routes->group('admin', static function ($routes) {
    $routes->get('users', 'Admin\Users::index');
    $routes->get('blog', 'Admin\Blog::index');
});

# api
$routes->group('api', ['namespace'=>'App\API\v1'], static function ($routes) {
    $routes->resource('users');
})
```

### Redirect Route
```php
# redirect ke named route
$routes->addRedirect('users/about', 'profile');

# redirect ke URI
$routes->addRedirect('users/about', 'users/profile');
```

