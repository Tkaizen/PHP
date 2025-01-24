Sure! Here's the third part of the PHP tutorial series in markdown format for your GitHub repo:

```markdown
# PHP Tutorials - Part 3: Working with Databases in PHP

Welcome to the third part of our PHP tutorial series! In this tutorial, we'll focus on working with databases in PHP, one of the most crucial aspects of dynamic web development.

## Table of Contents
1. [Introduction to MySQL and PHP](#introduction-to-mysql-and-php)
2. [Connecting to a MySQL Database](#connecting-to-a-mysql-database)
3. [Performing CRUD Operations](#performing-crud-operations)
4. [Prepared Statements](#prepared-statements)
5. [Using PDO for Database Interaction](#using-pdo-for-database-interaction)
6. [Conclusion](#conclusion)

---

## 1. Introduction to MySQL and PHP

MySQL is one of the most popular relational database management systems. PHP provides multiple ways to interact with MySQL, including the `mysqli` extension and PDO (PHP Data Objects).

In this tutorial, we will focus on using PDO for its flexibility and support for multiple database types.

---

## 2. Connecting to a MySQL Database

Before we can start querying our database, we need to establish a connection to the MySQL server.

### Simple MySQL Connection Using PDO

```php
<?php
$host = '127.0.0.1';
$db = 'tutorial_db';
$user = 'root';
$pass = 'password';

try {
    $pdo = new PDO("mysql:host=$host;dbname=$db", $user, $pass);
    // Set the PDO error mode to exception
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    echo "Connected successfully!";
} catch (PDOException $e) {
    echo "Connection failed: " . $e->getMessage();
}
```

### Breakdown:
- **PDO Constructor**: `"mysql:host=$host;dbname=$db"` — Specifies the MySQL host and database name.
- **Exception Handling**: Using `try-catch` ensures that we gracefully handle any connection errors.

---

## 3. Performing CRUD Operations

CRUD (Create, Read, Update, Delete) operations are the basic functions for managing data in a database.

### 3.1 Create - Inserting Data

```php
<?php
$sql = "INSERT INTO users (name, email) VALUES (:name, :email)";
$stmt = $pdo->prepare($sql);

$name = 'John Doe';
$email = 'john.doe@example.com';

$stmt->bindParam(':name', $name);
$stmt->bindParam(':email', $email);

$stmt->execute();
echo "New record created successfully!";
```

### 3.2 Read - Fetching Data

```php
<?php
$sql = "SELECT * FROM users";
$stmt = $pdo->prepare($sql);
$stmt->execute();

$results = $stmt->fetchAll(PDO::FETCH_ASSOC);
foreach ($results as $row) {
    echo $row['name'] . " - " . $row['email'] . "<br>";
}
```

### 3.3 Update - Modifying Data

```php
<?php
$sql = "UPDATE users SET name = :name WHERE id = :id";
$stmt = $pdo->prepare($sql);

$id = 1;
$name = 'Jane Doe';

$stmt->bindParam(':id', $id);
$stmt->bindParam(':name', $name);

$stmt->execute();
echo "Record updated successfully!";
```

### 3.4 Delete - Removing Data

```php
<?php
$sql = "DELETE FROM users WHERE id = :id";
$stmt = $pdo->prepare($sql);

$id = 1;
$stmt->bindParam(':id', $id);

$stmt->execute();
echo "Record deleted successfully!";
```

---

## 4. Prepared Statements

Prepared statements are an important concept in database interaction because they help prevent SQL injection attacks. When you prepare a statement, you define the SQL structure first and then bind values to it.

### Why Use Prepared Statements?

- **Security**: Prevents SQL injection by separating SQL logic from user input.
- **Performance**: Prepared statements can be executed multiple times without re-parsing the query.

Here’s how we use a prepared statement for an insert operation:

```php
<?php
$sql = "INSERT INTO users (name, email) VALUES (?, ?)";
$stmt = $pdo->prepare($sql);
$stmt->execute([$name, $email]);
```

In this case, the question marks (`?`) are placeholders that get replaced with the values we pass in the `execute` method.

---

## 5. Using PDO for Database Interaction

PDO (PHP Data Objects) is a database access layer that provides a uniform method for interacting with different types of databases.

### Advantages of PDO:
- **Supports Multiple Databases**: PDO works with MySQL, PostgreSQL, SQLite, and others.
- **Flexible Error Handling**: Can throw exceptions or handle errors with other methods.
- **Prepared Statements**: Built-in support for preventing SQL injection.

### Example: Fetching Data Using PDO

```php
<?php
$sql = "SELECT id, name, email FROM users";
$stmt = $pdo->query($sql);

while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {
    echo $row['id'] . " - " . $row['name'] . " - " . $row['email'] . "<br>";
}
```

### Example: Using Named Placeholders in Prepared Statements

```php
<?php
$sql = "UPDATE users SET name = :name WHERE id = :id";
$stmt = $pdo->prepare($sql);

$stmt->bindParam(':id', $id);
$stmt->bindParam(':name', $name);

$stmt->execute();
```

In this example, we use named placeholders like `:id` and `:name` instead of question marks, which can improve readability.

---

## 6. Conclusion

In this part of the tutorial, we covered how to interact with MySQL databases using PDO in PHP. We explored connecting to a database, performing CRUD operations, using prepared statements for security, and leveraging PDO's advantages for flexible and secure database interactions.

In the next tutorial, we’ll explore object-oriented programming (OOP) in PHP and how to structure your applications for better maintainability.

---

Feel free to [open an issue](https://github.com/your-repo/issues) or [contribute to this repository](https://github.com/your-repo/pulls) if you have any suggestions or improvements!

---

### Next Steps
- [Part 1: Introduction to PHP](https://github.com/your-repo/part1)
- [Part 2: Advanced Concepts in PHP](https://github.com/your-repo/part2)
- [Part 4: Object-Oriented Programming in PHP](https://github.com/your-repo/part4)
```

This tutorial introduces working with MySQL using PDO, focusing on CRUD operations, security, and flexibility. It builds upon the previous tutorials and gives the user a solid understanding of how to interact with databases in PHP.

Let me know if you'd like any adjustments!
