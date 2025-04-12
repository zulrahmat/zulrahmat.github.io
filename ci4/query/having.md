### having()
```php
$builder->having('user_id = 45'); // Produces: HAVING user_id = 45
$builder->having('user_id', 45); // Produces: HAVING user_id = 45
```
### having() - multi value
```php
# with multi value
$builder->having([
    'title =' => 'My Title', 
    'id <' => $id
]);
// Produces: HAVING title = 'My Title', id < 45
```

### orHaving()
```php
$builder->orHaving('user_id = 45');
```

### havingIn()
```php
$groups = [1, 2, 3];
$builder->havingIn('group_id', $groups);
// Produces: HAVING group_id IN (1, 2, 3)
```
### orHavingIn()
```php
$groups = [1, 2, 3];
$builder->orHavingIn('group_id', $groups);
// Produces: OR group_id IN (1, 2, 3)
```
### havingNotIn()
```php
$groups = [1, 2, 3];
$builder->havingNotIn('group_id', $groups);
// Produces: HAVING group_id NOT IN (1, 2, 3)
```
### orHavingNotIn()
```php
$groups = [1, 2, 3];
$builder->havingNotIn('group_id', $groups);
// Produces: OR group_id NOT IN (1, 2, 3)
```
### havingLike()
```php
$builder->havingLike('title', 'match');
// Produces: HAVING `title` LIKE '%match%' ESCAPE '!'
```

### havingLike() - multiple value
```php
$builder->havingLike('title', 'match');
$builder->havingLike('body', 'match');
// HAVING `title` LIKE '%match%' ESCAPE '!' AND  `body` LIKE '%match% ESCAPE '!'
```

### havingLike() - match
```php
$builder->havingLike('title', 'match', 'before'); // Produces: HAVING `title` LIKE '%match' ESCAPE '!'
$builder->havingLike('title', 'match', 'after');  // Produces: HAVING `title` LIKE 'match%' ESCAPE '!'
$builder->havingLike('title', 'match', 'both');   // Produces: HAVING `title` LIKE '%match%' ESCAPE '!'
```
### orHavingLike()
```php
$builder->havingLike('title', 'match');
$builder->orHavingLike('body', $match);
// HAVING `title` LIKE '%match%' ESCAPE '!' OR  `body` LIKE '%match%' ESCAPE '!'
```
### notHavingLike()
```php
$builder->notHavingLike('title', 'match');
// HAVING `title` NOT LIKE '%match% ESCAPE '!'
```
### orNotHavingLike()
```php
$builder->havingLike('title', 'match');
$builder->orNotHavingLike('body', 'match');
// HAVING `title` LIKE '%match% OR  `body` NOT LIKE '%match%' ESCAPE '!'
```