### Join
```php
$builder = $db->table('users');
$builder->select('users.name, orders.total');
$builder->join('orders', 'orders.user_id = users.id');
$query = $builder->get();
$results = $query->getResult();

/*
 * Produces:
 * SELECT * FROM blogs JOIN comments ON comments.id = blogs.id
 */
```
### Inner Join (default)
```php
$builder->join('orders', 'orders.user_id=users.id');
```
### Left Join
```php
$builder->join('orders', 'orders.user_id = users.id', 'left');
```
### Right Join
```php
$builder->join('orders', 'orders.user_id = users.id', 'right');
```
### Multi Join
```php
$builder->join('orders', 'orders.user_id = users.id');
$builder->join('products', 'products.id = orders.product_id');
```