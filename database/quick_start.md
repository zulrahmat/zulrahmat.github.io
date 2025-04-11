[kembali](../README.md)

- [Membuat Koneksi ke database](#membuat-koneksi-ke-database)
- [Membuat Koneksi ke database ganda](#membuat-koneksi-ke-database-ganda)
- [Standard Query](#standard-query)
- [Standard Query Dengan Single Result](#standard-query-dengan-single-result)
- [Standard Query dengan Result Ganda](#standard-query-dengan-result-ganda)

### Membuat Koneksi ke database
```php
# initializing database
$db = \Config\Database::connect();
$db = db_connect();

# koneksi ke specifig group, yang mana group_name adalah nama group koneksi pada config 
$db = \Config\Database::connect('group_name');

# 
$db = \Config\Database::connect('group_name', false);
```

### Membuat Koneksi ke database ganda
```php
$db1 = \Config\Database::connect('group_one');
$db2 = \Config\Database::connect('group_two');
```

### Standard Query
```php
<?php

$query   = $db->query('SELECT name, title, email FROM my_table');

# result sebagai object
$results = $query->getResult();

foreach ($results as $row) {
    echo $row->title;
    echo $row->name;
    echo $row->email;
}

# result sebagai array
$results = $query->getResultArray();

foreach ($results as $row) {
    echo $row['title'];
    echo $row['name'];
    echo $row['email'];
}

echo 'Total Results: ' . count($results);
```
### Standard Query Dengan Single Result
```php
<?php

$query = $db->query('SELECT name FROM my_table LIMIT 1');

# result sebagai object
$row   = $query->getRow();
echo $row->name;

# result sebagai array
$row   = $query->getRowArray();
echo $row['name'];


```

### Standard Query dengan Result Ganda
```php
<?php

$query   = $db->query('SELECT name, title, email FROM my_table');
$results = $query->getResultArray();

foreach ($results as $row) {
    echo $row['title'];
    echo $row['name'];
    echo $row['email'];
}
```