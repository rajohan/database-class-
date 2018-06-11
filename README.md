# Database.php

#### Initiating
##### Initiate a database connection by creating a new Database() object.

```php 
require_once('Database.php');
$db = new Database(); 
```

#### Select
##### Select rows from a database table

##### Usage:
```php
$db->select(string $table, array $where=[], string $columns="*", string $whereMode="AND", 
            string $order="",string $limit="", array $dataTypes=[], string $returnType="object", 
            string $returnClass="");
```
##### Arguments:

string $table &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - Database Table.  
array  $where &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - Optional: Array holding the filters/'WHERE' clause for the query.  
string $columns &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - Optional: the column to select (SELECT count(*) FROM ...), defaults to *.  
string $whereMode   - Optional: Add an 'AND' or 'OR' after each item in the $where array, defaults to AND.  
string $order       - Optional: string holding the 'ORDER BY' clause.  
string $limit       - Optional: string holding the 'LIMIT' clause.  
array  $dataTypes   - Optional: Pass in data types as an array in equal order to the $where.  
                        - Options: int/integer, bool/boolean, str/string.  
                        - Data type will default to string if nothing is passed in (PDO::PARAM_STR).  
string $returnType  - Optional: Choose data type to get returned result as.  
                        - Options: obj/object, class, array/arr/assoc. Defaults to object (PDO::FETCH_OBJ).  
                        - Remember to set $returnClass if class is chosen or return type will be set to object.  
string $returnClass - Optional: Class to return data as when class is chosen as $returnType.  

return mixed        - Returns as object, class or array based on $returnType choice.  

##### Example:

$db->select("users", array("id" => 55, "firstName" => "Raymond"), "*", "OR", "ORDER BY ID ASC", "LIMIT 5",
            array("int", "str"), "Class", "TestClass");

#### Insert
##### Insert data into a database table

##### Usage:

$db->insert(string $table, Array $columnsData, Array $dataTypes=[]);

##### Arguments:

string $table       - Database Table.
array  $columnsData - Array of columns and data to insert to the assign columns.
array  $dataTypes   - Optional: Pass in data types as an array in equal order to $columnsData.
                        - Options: int/integer, bool/boolean, str/string.
                        - Data type will default to string if nothing is passed in (PDO::PARAM_STR).

return boolean      - True = Success, False = Error.

##### Example:

$db->insert("users",
            Array("firstName" => "Raymond",
                  "lastName" => "Johannessen",
                  "email" => "mail@rajohan.no"),
            Array("str", "str", "str"));


#### Update
##### Update one or more rows of a database table

##### Arguments:

string $table       - Database Table.
array  $columnsData - Array of columns and data to insert to the assign columns.
array  $where       - Optional: Array holding the filters/'WHERE' clause for the query.
string $whereMode   - Optional: Add an 'AND' or 'OR' after each item in the $where array, defaults to AND.
array  $dataTypes   - Optional: Pass in data types as an array in equal order to $columnsData.
                        - Options: int/integer, bool/boolean, str/string.
                        - Data type will default to string if nothing is passed in (PDO::PARAM_STR).

return boolean      - True = Success, False = Error.

##### Usage:

$db->update(string $table, array $columnsData, array $where=[], string $whereMode="AND", Array $dataTypes=[]);

##### Example:


$db->update("users",
            Array("firstName" => "Raymond",
                  "lastName" => "Johannessen",
                  "email" => "mail@rajohan.no"),
            Array("id" => 1,
                  "username" => "Rajohan"),
            "OR",
            Array("str", "str", "str", "int", "str"));


#### Delete
##### Remove one or more rows from a database table

##### Arguments:

string $table       - Database Table.
array  $where       - Optional: Array holding the filters/'WHERE' clause for the query.
string $whereMode   - Optional: Add an 'AND' or 'OR' after each item in the $where array, defaults to AND.
array  $dataTypes   - Optional: Pass in data types as an array in equal order to $where.
                        - Options: int/integer, bool/boolean, str/string.
                        - Data type will default to string if nothing is passed in (PDO::PARAM_STR).

return boolean      - True = Success, False = Error.

##### Usage:

$db->delete(string $table, array $where=[], string $whereMode="AND", Array $dataTypes=[]);

##### Example:

$db->delete("users",
            Array("id" => 1,
                  "username" => "Rajohan"),
            "OR",
            Array("int", "str"));


#### Count
##### Get row count from a database table

##### Arguments:

string $table     - Database Table.
array  $where     - Optional: Array holding the filters/'WHERE' clause for the query.
string $whereMode - Optional: Add an 'AND' or 'OR' after each item in the $where array, defaults to AND.
string $columns   - Optional: the column to select (SELECT count(*) FROM ...), defaults to *.
array  $dataTypes - Optional: Pass in data types as an array in equal order to the $where.
                      - Options: int/integer, bool/boolean, str/string.
                      - Data type will default to string if nothing is passed in (PDO::PARAM_STR).

return integer    - Row count.

##### Usage:

$db->count(string $table, Array $where=[], $whereMode="AND", string $columns="*", Array $dataTypes=[]);

Example:

$db->count("users",
           Array("id" => 1,
           "firstName" => "Raymond"),
           "OR",
           "*",
           Array("int", "str"));

#### Id
##### Last inserted row's id

##### Usage:
$db->id();

#### Sql
##### Get last used query

##### Usage:
$db->sql();

#### CloseConnection
##### Close the database connection

##### Usage:
$db->closeConnection();

#### Licensed under the MIT License.
