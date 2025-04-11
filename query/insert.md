### insert()
```php
$data = [
    'id'          => new RawSql('DEFAULT'),
    'title'       => 'My title',
    'name'        => 'My Name',
    'date'        => '2022-01-01',
    'last_update' => new RawSql('CURRENT_TIMESTAMP()'),
];

$builder->insert($data);
/* Produces:
    INSERT INTO mytable (id, title, name, date, last_update)
    VALUES (DEFAULT, 'My title', 'My name', '2022-01-01', CURRENT_TIMESTAMP())
*/
```
### insertBatch()
```php
$data = [
    [
        'title' => 'My title',
        'name'  => 'My Name',
        'date'  => 'My date',
    ],
    [
        'title' => 'Another title',
        'name'  => 'Another Name',
        'date'  => 'Another date',
    ],
];

$builder->insertBatch($data);
/*
 * Produces:
 * INSERT INTO mytable (title, name, date)
 *      VALUES ('My title', 'My name', 'My date'),
 *      ('Another title', 'Another name', 'Another date')
 */
```
### insert from query
```php
use CodeIgniter\Database\RawSql;

$query = 'SELECT user2.name, user2.email, user2.country
          FROM user2
          LEFT JOIN user ON user.email = user2.email
          WHERE user.email IS NULL';

$sql = $builder
    ->ignore(true)
    ->setQueryAsData(new RawSql($query), null, 'name, country, email')
    ->insertBatch();
/* MySQLi produces:
    INSERT IGNORE INTO `db_user` (`name`, `country`, `email`)
    SELECT user2.name, user2.email, user2.country
    FROM user2
    LEFT JOIN user ON user.email = user2.email
    WHERE user.email IS NULL
*/
```
### getCompiledInsert()
Compiles the insertion query just like $builder->insert() but does not run the query. This method simply returns the SQL query as a string.
```php
$data = [
    'title' => 'My title',
    'name'  => 'My Name',
    'date'  => 'My date',
];

$sql = $builder->set($data)->getCompiledInsert();
echo $sql;
// Produces string: INSERT INTO mytable (`title`, `name`, `date`) VALUES ('My title', 'My name', 'My date')

echo $builder->set('title', 'My Title')->getCompiledInsert(false);
// Produces string: INSERT INTO mytable (`title`) VALUES ('My Title')

echo $builder->set('content', 'My Content')->getCompiledInsert();
// Produces string: INSERT INTO mytable (`title`, `content`) VALUES ('My Title', 'My Content')
```
