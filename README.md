EasyDatabase
============
## PHP5 Module by PentaSource
visit [PentaSource.de] (http://pentasource.de/) for more information

### About the project
Every Developer wants to focus on the code that makes his project unique. PentaSource's PHP Modules assist them by making every-day code easier to implement.

EasyDatabase is a project that easily lets you manage your database connection to any MySQL server. Sending queries never was easier before.

### How to use
#### Setup
Download the ```inc``` folder and copy it into your website's root directory.
Then, in your index.php (or whatever entry point you're using), paste this to include the DatabaseSystem:
```php
require_once 'inc/DatabaseSystem.class.php';
```
Open the ```DatabaseSystem.class.php```. Edit the variables ```$db_host```, ```$db_user```, ```$db_pass``` and ```$db_name``` as appropriate and save your changes.

#### Executing a query

Once you've done that, it's extremely easy to execute a query. Just copy the following:
```php
DatabaseSystem::query($statement);
```
where $statement is the string containing your query. This function returns false if the query failed or a ```mysql_result```-object.

To fetch an associative result containing the selected rows, just extend your code like this:
```php
$array = DatabaseSystem::query($statement)->fetch_array(MYSQL_ASSOC);
```

If you have inserted a new row into a database, you can get the AutoIncrement-Id of that row by using:
```php
$insertId = DatabaseSystem::getLastInsertId();
```

You can also debug your query by echoing the last error from a query:
```php
echo DatabaseSystem::getLastError();
//or
echo DatabaseSystem::getLastErrorNo();
```

Also good for debugging is to check if you can establish a connection:
```php
$isConnected = DatabaseSystem::testConnection();

if ($isConnected) {
	//connection successful
} else {
	//error
}
```

One last thing: If you ever need to handle user input (like in a signin form), you have to make sure that all special characters are escaped so that any sort of SQLInjection is prevented. A safe way to do that is by using this:
```php
$escapedString = DatabaseSystem::escapeString($unescapedString);
```
