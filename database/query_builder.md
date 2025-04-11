### Buat Koneksi
```php
$db      = \Config\Database::connect();
$builder = $db->table('users');
```
### GET
```php
$builder = $db->table('mytable');
$query   = $builder->get();  // Produces: SELECT * FROM mytable

# menggunakan limit
$query = $builder->get(10, 20);
/*
 * Executes: SELECT * FROM mytable LIMIT 20, 10
 * (in MySQL. Other databases have slightly different syntax)
 */
```

### Get Compiled Select
```php
$sql = $builder->getCompiledSelect();
echo $sql;
// Prints string: SELECT * FROM mytable

echo $builder->limit(10, 20)->getCompiledSelect(false);
/*
 * Prints string: SELECT * FROM mytable LIMIT 20, 10
 * (in MySQL. Other databases have slightly different syntax)
 */

echo $builder->select('title, content, date')->getCompiledSelect();
// Prints string: SELECT title, content, date FROM mytable LIMIT 20, 10
```

## Where
### `$builder->getWhere()`
```php
$query = $builder->getWhere(['id' => $id], $limit, $offset);
```
### Select
```php
$builder->select('title, content, date');
$query = $builder->get();
// Executes: SELECT title, content, date FROM mytable
```
### Select Max
```php
$builder->selectMax('age');
$query = $builder->get();
// Produces: SELECT MAX(age) as age FROM mytable

$builder->selectMax('age', 'member_age');
$query = $builder->get();
// Produces: SELECT MAX(age) as member_age FROM mytable
```
### Select Min
```php
$builder->selectMin('age');
$query = $builder->get();
// Produces: SELECT MIN(age) as age FROM mytable
```
### Select Avg
```php
$builder->selectAvg('age');
$query = $builder->get();
// Produces: SELECT AVG(age) as age FROM mytable
```
### Select Sum
```php
$builder->selectSum('age');
$query = $builder->get();
// Produces: SELECT SUM(age) as age FROM mytable
```
### Select Count
```php
$builder->selectCount('age');
$query = $builder->get();
// Produces: SELECT COUNT(age) as age FROM mytable
```
### Select Sub Query
```php
$subquery = $db->table('countries')->select('name')->where('id', 1);
$builder  = $db->table('users')->select('name')->selectSubquery($subquery, 'country');
$query    = $builder->get();
// Produces: SELECT `name`, (SELECT `name` FROM `countries` WHERE `id` = 1) `country` FROM `users`
```
### From
```php
$builder = $db->table('users');
$builder->select('title, content, date');
$builder->from('mytable');
$query = $builder->get();
// Produces: SELECT title, content, date FROM users, mytable
```
### Subquery
```php
$subquery = $db->table('users');
$builder  = $db->table('jobs')->fromSubquery($subquery, 'alias');
$query    = $builder->get();
// Produces: SELECT * FROM `jobs`, (SELECT * FROM `users`) `alias`
```
### Subquery via newQuery
```php
$subquery = $db->table('users')->select('id, name');
$builder  = $db->newQuery()->fromSubquery($subquery, 't');
$query    = $builder->get();
// Produces: SELECT * FROM (SELECT `id`, `name` FROM users) `t`
```
### Join
```php
$builder = $db->table('blogs');
$builder->select('*');
$builder->join('comments', 'comments.id = blogs.id');
$query = $builder->get();
/*
 * Produces:
 * SELECT * FROM blogs JOIN comments ON comments.id = blogs.id
 */
```