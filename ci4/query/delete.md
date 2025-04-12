### delete
```php
$builder->delete(['id' => $id]);
// Produces: DELETE FROM mytable WHERE id = $id

# menggunakan where
$builder->where('id', $id);
$builder->delete();
/*
 * Produces:
 * DELETE FROM mytable
 * WHERE id = $id
 */
```
### getCompiledDelete()
```php

```
### emptyTable()
```php
$builder->emptyTable('mytable');
// Produces: DELETE FROM mytable
```
### truncate
```php
$builder->truncate();
/*
 * Produce:
 * TRUNCATE mytable
 */
```