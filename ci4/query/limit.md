### limit()
```php
$builder->limit(10);
// Produces: LIMIT 10

$builder->limit(10, 20);
// Produces: LIMIT 20, 10 (in MySQL. Other databases have slightly different syntax)
```
### countAllResults()
```php
echo $builder->countAllResults(); // Produces an integer, like 25
$builder->like('title', 'match');
$builder->from('my_table');
echo $builder->countAllResults(); // Produces an integer, like 17
```
### countAll()
```php
echo $builder->countAll(); // Produces an integer, like 25
```
