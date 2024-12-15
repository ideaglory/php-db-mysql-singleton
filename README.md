# Database PHP Singleton Class

This repository provides a PHP class to handle MySQL database connections and queries using the `mysqli` extension. It implements the Singleton design pattern to ensure only one instance of the database connection exists throughout the application lifecycle. This class is easy to integrate and includes methods for common database operations.

## Features

- **Singleton Design Pattern**: Ensures a single database connection instance.
- **Automatic Parameter Binding**: Prevents SQL injection by binding parameters securely.
- **Fetch Methods**: Fetch all rows or a single row.
- **Transaction Management**: Includes `beginTransaction`, `commit`, and `rollback` methods.
- **Last Insert ID**: Retrieve the last inserted record ID.
- **Character Set Support**: Defaults to `utf8mb4`, configurable via constants.

## Class Overview

### Constants
Define the following constants in the class to configure your database:
- `DB_HOST`: The database host (e.g., `localhost`).
- `DB_USERNAME`: The database username.
- `DB_PASSWORD`: The database password.
- `DB_DATABASE`: The database name.
- `DB_CHARSET`: The character set for the connection (default: `utf8mb4`).

### Methods

#### `getInstance()`
Creates or retrieves the singleton instance of the database class.

#### `query($sql, $params = [])`
Prepares and executes a SQL query with optional parameter binding.

#### `fetchAll($sql, $params = [])`
Executes a query and returns all rows as an associative array.

#### `fetchOne($sql, $params = [])`
Executes a query and returns a single row as an associative array.

#### `lastInsertId()`
Returns the ID of the last inserted row.

#### `beginTransaction()`
Starts a database transaction.

#### `commit()`
Commits the current transaction.

#### `rollback()`
Rolls back the current transaction.

#### `close()`
Closes the database connection and resets the singleton instance.

## Usage

### Initialization
The database configuration is defined using constants within the class. No parameters are required when calling `getInstance()`.

```php
// Initialize the singleton instance
$db = Database::getInstance();
```

### Insert Example
```php
$db->query("INSERT INTO users (name, email) VALUES (?, ?)", ['John Doe', 'john@example.com']);

// Get the last inserted ID
echo $db->lastInsertId();
```

### Fetch All Rows Example
```php
$users = $db->fetchAll("SELECT * FROM users");
print_r($users);
```

### Fetch One Row Example
```php
$user = $db->fetchOne("SELECT * FROM users WHERE id = ?", [1]);
print_r($user);
```

### Transaction Example
```php
try {
    $db->beginTransaction();

    $db->query("INSERT INTO accounts (name, balance) VALUES (?, ?)", ['John', 1000]);
    $db->query("INSERT INTO accounts (name, balance) VALUES (?, ?)", ['Jane', 2000]);

    $db->commit();
} catch (Exception $e) {
    $db->rollback();
    echo "Transaction failed: " . $e->getMessage();
}
```

### Closing the Connection
```php
$db->close();
```

## Installation

1. Clone this repository or download the `Database` class file.
2. Update the constants in the class with your database configuration.
3. Include the class file in your project:

```php
require_once 'Database.php';
```

## Requirements

- PHP 7.4 or higher
- MySQL
- `mysqli` extension enabled

## Contributing
Feel free to fork this repository and submit pull requests for improvements or bug fixes.

## License
This project is licensed under the MIT License. See the LICENSE file for details.

## Author
Created by [IdeaGlory](https://ideaglory.com).
