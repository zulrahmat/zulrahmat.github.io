### orderBy()
```php
$builder->orderBy('title', 'DESC');
// Produces: ORDER BY `title` DESC
```
### orderBy() - string
```php
$builder->orderBy('title DESC, name ASC');
// Produces: ORDER BY `title` DESC, `name` ASC
```

### orderBy() - Multiple value
```php
$builder->orderBy('title', 'DESC');
$builder->orderBy('name', 'ASC');
// Produces: ORDER BY `title` DESC, `name` ASC
```
