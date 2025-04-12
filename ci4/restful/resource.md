```php
$routes->resource('photos');

# alternative
$routes->resource('photos', ['controller' => 'Gallery']);
// Would create routes like:
$routes->get('photos', '\App\Controllers\Gallery::index');


//equavalent
$routes->get('photos/new', 'Photos::new');
$routes->post('photos', 'Photos::create');
$routes->get('photos', 'Photos::index');
$routes->get('photos/(:segment)', 'Photos::show/$1');
$routes->get('photos/(:segment)/edit', 'Photos::edit/$1');
$routes->put('photos/(:segment)', 'Photos::update/$1');
$routes->patch('photos/(:segment)', 'Photos::update/$1');
$routes->delete('photos/(:segment)', 'Photos::delete/$1');
```

### Limit Routes
```php
# valid limit index, show, create, update, new, edit and delete
$routes->resource('photos', ['only' => ['index', 'show']]);

# except
$routes->resource('photos', ['except' => ['index', 'show']]);
```

### method
```php
# GET /photos
public function index();

# GET /photos/new
public function new();

# POST /photos
public function create();

# GET /photos/(:segment)
public function show($id = null);

# GET /photos/(:segment)/edit
public function edit($id = null);

# PUT /photos/(:segment)
public function update($id = null);

# POST /photos/(:segment)
public function update($id = null);

# DELETE /photos/(:segment)
public function delete($id = null);
```