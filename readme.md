# PHP Berkeley Class
A PHP Class to ease the pain of dealing with old berkeley files. It allows to easily interact with old berkeley data files using an iterator interface and named fields or columns. It implements insertion, update, deletion, search, regex search, truncation and optimization of berkeley database files.


## Instalation
```
git clone https://github.com/flaab/php-berkeley-class.git
```

## Usage

```
// Require the library
require_once('berkeley.php');

// Path to berkeley file
$file = 'database.db';

// Separator between fields
$separator = '|';

// Instance the library
$db = new Berkeley($file, $separator);

// Get amount of rows
$rows = db->cardinality();  // Integer containing number of rows

// Set fetch mode as array or string
$db->set_fetch_mode(DBA_ARRAY); // or $db->set_fetch_mode(DBA_STRING);

// Iterate all records
foreach($db as $record)
{
    // Dump record. 
    // $record will be array if DBA_ARRAY was set previously.
    // $record will be string if DBA_STRING was set previously.
    var_dump($record); 
}

// Insert a new record and get the id or false
$id = $db->insert(array('lorem','ipsum','dolor','sit','amet');
if(!$id) trigger_error("Failed to insert new record into file', E_USER_ERROR);

// Update recently created with new content
$db->update($id, 'John Doe|johndoe@gmail.com|Client|10');

// The above is the same as...
$db->update($id, array('John','Doe','johndoe@gmail.com','Client','10'));

// Get a specific row, for instance row 50.
$row = $db->fetch(45);

// Search for all Johns in the file.
// Can be plain text or a regular expression.
$search = $db->search('/^John$/');

// Iterate all search results and delete them from the db
foreach($search as $record)
    $db->delete($record[0]);

// If we set field names, we'll get associative arrays in our queries instead of numbered arrays
$db->set_fields(array('fullname','email','type','orders'));

// Optimize the berkeley file for efficiency
$db->optimize();

// We can also delete the database from the hard drive. Careful!
// $db->drop();

// We can also delete all rows but keep the file
// $db->truncate();

// Disconnect
$db->disconnect();
```


## Author
- **Arturo Lopez Perez** - Main and sole developer (so far).


## License
This project is licensed under the MIT License - see the LICENSE file for details
