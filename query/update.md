### update()
```php
$data = [
    'title' => $title,
    'name'  => $name,
    'date'  => $date,
];

$builder->where('id', $id);
$builder->update($data);
/*
 * Produces:
 * UPDATE mytable
 * SET title = '{$title}', name = '{$name}', date = '{$date}'
 * WHERE id = $id
 */
```
### replace()
```php
$data = [
    'title' => 'My title',
    'name'  => 'My Name',
    'date'  => 'My date',
];

$builder->replace($data);
// Executes: REPLACE INTO mytable (title, name, date) VALUES ('My title', 'My name', 'My date')
```
### set()
```php
$builder->set('name', $name);
$builder->insert();
// Produces: INSERT INTO mytable (`name`) VALUES ('{$name}')
```