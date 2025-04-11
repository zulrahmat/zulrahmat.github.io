### $builder->where() - simple key value
```php
# simple key value
$builder->where('name', $name);
// Produces: WHERE name = 'Joe'
```

### $builder->where() - multiple key value
```php
$builder->where('name', $name);
$builder->where('title', $title);
$builder->where('status', $status);
// WHERE name = 'Joe' AND title = 'boss' AND status = 'active'
```

### $builder->where() - custom operator
```php
$builder->where('name !=', $name);
$builder->where('id <', $id);
// Produces: WHERE name != 'Joe' AND id < 45
```

### $builder->where() - associative array
```php
$array = ['name' => $name, 'title' => $title, 'status' => $status];
$builder->where($array);
// Produces: WHERE name = 'Joe' AND title = 'boss' AND status = 'active'
```
### $builder->where() - array with custom operator
```php
$array = ['name !=' => $name, 'id <' => $id, 'date >' => $date];
$builder->where($array);
```

### $builder->where() - custom string
```php
$where = "name='Joe' AND status='boss' OR status='active'";
$builder->where($where);
```

### $builder->orWhere()
```php
$builder->where('name !=', $name);
$builder->orWhere('id >', $id);
// Produces: WHERE name != 'Joe' OR id > 50
```
### $builder->whereIn() ###
```php
$names = ['Frank', 'Todd', 'James'];
$builder->whereIn('username', $names);
// Produces: WHERE username IN ('Frank', 'Todd', 'James')
```
### $builder->orWhereIn()
```php
$names = ['Frank', 'Todd', 'James'];
$builder->orWhereIn('username', $names);
// Produces: OR username IN ('Frank', 'Todd', 'James')
```
### $builder->whereNotIn()
```php
$names = ['Frank', 'Todd', 'James'];
$builder->whereNotIn('username', $names);
// Produces: WHERE username NOT IN ('Frank', 'Todd', 'James')
```
### $builder->orWhereNotIn()
```php
$names = ['Frank', 'Todd', 'James'];
$builder->orWhereNotIn('username', $names);
// Produces: OR username NOT IN ('Frank', 'Todd', 'James')
```