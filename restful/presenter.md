```php
$routes->presenter('photos');

// Equivalent to the following:
$routes->get('photos/new', 'Photos::new');
$routes->post('photos/create', 'Photos::create');
$routes->post('photos', 'Photos::create');   // alias
$routes->get('photos', 'Photos::index');
$routes->get('photos/show/(:segment)', 'Photos::show/$1');
$routes->get('photos/(:segment)', 'Photos::show/$1');  // alias
$routes->get('photos/edit/(:segment)', 'Photos::edit/$1');
$routes->post('photos/update/(:segment)', 'Photos::update/$1');
$routes->get('photos/remove/(:segment)', 'Photos::remove/$1');
$routes->post('photos/delete/(:segment)', 'Photos::delete/$1');
```

### Limit the routes made
```php
# only
$routes->presenter('photos', ['only' => ['index', 'show']]);

# except
$routes->presenter('photos', ['except' => 'new,edit']);
```

### method
```php
# GET /photos
public function index();

# GET /photos/new
public function new();

# POST /photos
# POST /photos/create
public function create();

# GET /photos/(:segment)
# GET /photos/show/(:segment)
public function show($id = null);

# GET /photos/(:segment)/edit
public function edit($id = null);

# PUT /photos/(:segment)
public function update($id = null);

# POST /photos/update/(:segment)
public function update($id = null);

# POST /photos/remove/(:segment)
public funtion remove($id = null);

# DELETE /photos/(:segment)
public function delete($id = null);


```