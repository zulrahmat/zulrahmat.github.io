### like()
```php
$builder->like('title', 'match');
// Produces: WHERE `title` LIKE '%match%' ESCAPE '!'
```
### like() - multiple
```php
$builder->like('title', 'match');
$builder->like('body', 'match');
// WHERE `title` LIKE '%match%' ESCAPE '!' AND  `body` LIKE '%match%' ESCAPE '!'
```
### like() - match
```php
$builder->like('title', 'match', 'before'); // Produces: WHERE `title` LIKE '%match' ESCAPE '!'
$builder->like('title', 'match', 'after');  // Produces: WHERE `title` LIKE 'match%' ESCAPE '!'
$builder->like('title', 'match', 'both');   // Produces: WHERE `title` LIKE '%match%' ESCAPE '!'
```
### like() - array
```php
$array = ['title' => $match, 'page1' => $match, 'page2' => $match];
$builder->like($array);
/*
 * WHERE `title` LIKE '%match%' ESCAPE '!'
 *     AND  `page1` LIKE '%match%' ESCAPE '!'
 *     AND  `page2` LIKE '%match%' ESCAPE '!'
 */
```
### orLike()
```php
$builder->like('title', 'match');
$builder->orLike('body', $match);
// WHERE `title` LIKE '%match%' ESCAPE '!' OR  `body` LIKE '%match%' ESCAPE '!'
```
### notLike()
```php
$builder->notLike('title', 'match'); // WHERE `title` NOT LIKE '%match% ESCAPE '!'
```
### orNotLike()
```php
$builder->like('title', 'match');
$builder->orNotLike('body', 'match');
// WHERE `title` LIKE '%match% OR  `body` NOT LIKE '%match%' ESCAPE '!'
```