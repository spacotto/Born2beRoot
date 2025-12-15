# About PHP
**PHP (Hypertext Preprocessor)** is a server-side **scripting language** for web development. PHP code runs on the server and generates HTML sent to the browser.

## Basic Syntax
PHP code is enclosed in `<?php ?>` tags:
```
<?php
  echo "Hello, World!";
?>
```
Statements end with semicolons. 
Comments use `//` for single lines or `/* */` for multiple lines, like C.

## Variables and Data Types
Variables start with `$` and don't require type declarations:
```
$name = "Alice";            // String
$age = 25;                  // Integer
$price = 19.99;             // Float
$isActive = true;           // Boolean
$items = [1, 2, 3];         // Array
$nothing = null;            // Null
```

## Strings
```
$single = 'Single quotes (literal)';
$double = "Double quotes with $variable interpolation";
$concat = "Hello " . "World";  // Concatenation

// Useful functions
strlen($str);           // Length
strtoupper($str);       // Uppercase
strtolower($str);       // Lowercase
substr($str, 0, 5);     // Substring
str_replace("old", "new", $str);
trim($str);             // Remove whitespace
```

## Arrays
```
// Indexed arrays
$fruits = ["apple", "banana", "orange"];
echo $fruits[0];  // "apple"

// Associative arrays (key-value pairs)
$person = [
  "name" => "John",
  "age" => 30,
  "city" => "Paris"
];
echo $person["name"];  // "John"

// Array functions
count($array);          // Length
array_push($array, $item);
array_pop($array);
in_array($item, $array);
array_merge($arr1, $arr2);
sort($array);
```

## Control Structures
### If Statements
```
if ($age >= 18) {
  echo "Adult";
} elseif ($age >= 13) {
  echo "Teen";
} else {
  echo "Child";
}

// Ternary operator
$status = ($age >= 18) ? "Adult" : "Minor";
```

### Switch
```
switch ($day) {
  case "Monday":
    echo "Start of week";
    break;
  case "Friday":
    echo "End of week";
    break;
  default:
    echo "Midweek";
}
```

### Loops
```
// For loop
for ($i = 0; $i < 10; $i++) {
  echo $i;
}

// While loop
while ($x < 5) {
  echo $x;
  $x++;
}

// Foreach (for arrays)
foreach ($fruits as $fruit) {
  echo $fruit;
}

// Foreach with keys
foreach ($person as $key => $value) {
  echo "$key: $value";
}
```

## Functions
```
function greet($name, $greeting = "Hello") {
  return "$greeting, $name!";
}

echo greet("Alice");              // "Hello, Alice!"
echo greet("Bob", "Welcome");     // "Welcome, Bob!"

// Anonymous functions
$multiply = function($a, $b) {
  return $a * $b;
};
echo $multiply(5, 3);  // 15
```

## Superglobals
PHP provides built-in arrays with global scope:
```
$_GET      // URL parameters (?name=value)
$_POST     // Form data (POST method)
$_REQUEST  // Both GET and POST
$_SERVER   // Server information
$_SESSION  // Session variables
$_COOKIE   // Cookies
$_FILES    // Uploaded files

// Examples
$name = $_GET['name'];
$email = $_POST['email'];
$userAgent = $_SERVER['HTTP_USER_AGENT'];
```

## Working with Forms
- HTML:
```
<form method="post" action="process.php">
  <input type="text" name="username">
  <input type="password" name="password">
  <button type="submit">Submit</button>
</form>
```
- PHP:
```
// process.php
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
  $username = $_POST['username'];
  $password = $_POST['password'];
  
  // Validate and process
}
```

## File Operations
```
// Read file
$content = file_get_contents('file.txt');

// Write file
file_put_contents('file.txt', 'Content');

// Check if file exists
if (file_exists('file.txt')) {
  // Do something
}

// Read line by line
$handle = fopen('file.txt', 'r');
while (($line = fgets($handle)) !== false) {
  echo $line;
}
fclose($handle);
```

## Classes and Objects
```
class User {
  public $name;
  private $email;
  
  public function __construct($name, $email) {
    $this->name = $name;
    $this->email = $email;
  }
  
  public function getEmail() {
    return $this->email;
  }
  
  public function greet() {
    return "Hello, {$this->name}";
  }
}

$user = new User("Alice", "alice@example.com");
echo $user->name;           // "Alice"
echo $user->greet();        // "Hello, Alice"
echo $user->getEmail();     // "alice@example.com"
```
### Inheritance
```
class Admin extends User {
  private $role = "admin";
  
  public function getRole() {
    return $this->role;
  }
}

$admin = new Admin("Bob", "bob@example.com");
echo $admin->greet();   // Inherited method
echo $admin->getRole(); // "admin"
```

## Database (MySQL with PDO)
```
// Connect
try {
  $pdo = new PDO('mysql:host=localhost;dbname=mydb', 'username', 'password');
  $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch (PDOException $e) {
  die("Connection failed: " . $e->getMessage());
}

// Select
$stmt = $pdo->query("SELECT * FROM users");
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {
  echo $row['name'];
}

// Insert with prepared statements (prevents SQL injection)
$stmt = $pdo->prepare("INSERT INTO users (name, email) VALUES (?, ?)");
$stmt->execute([$name, $email]);

// Update
$stmt = $pdo->prepare("UPDATE users SET name = ? WHERE id = ?");
$stmt->execute([$newName, $userId]);

// Delete
$stmt = $pdo->prepare("DELETE FROM users WHERE id = ?");
$stmt->execute([$userId]);
```

## Sessions and Cookies
```
// Sessions
session_start();  // Always call first

$_SESSION['user_id'] = 123;
$_SESSION['username'] = 'alice';

echo $_SESSION['username'];

session_destroy();  // End session

// Cookies
setcookie('username', 'alice', time() + 86400);  // Expires in 1 day
echo $_COOKIE['username'];
```

## Error Handling
```
// Try-catch
try {
  $result = riskyOperation();
} catch (Exception $e) {
  echo "Error: " . $e->getMessage();
} finally {
  // Always executes
}

// Custom error handling
set_error_handler(function($errno, $errstr) {
  echo "Error: $errstr";
});
```

## Common Security Practices
```
// Validate and sanitize input
$email = filter_var($_POST['email'], FILTER_VALIDATE_EMAIL);
$name = htmlspecialchars($_POST['name'], ENT_QUOTES, 'UTF-8');

// Use prepared statements for database queries (shown above)

// Hash passwords
$hashedPassword = password_hash($password, PASSWORD_DEFAULT);

// Verify passwords
if (password_verify($inputPassword, $hashedPassword)) {
  // Password correct
}

// Prevent XSS
echo htmlspecialchars($userInput, ENT_QUOTES, 'UTF-8');

// CSRF protection: use tokens in forms
$_SESSION['csrf_token'] = bin2hex(random_bytes(32));
```

## Useful Built-in Functions
```
// Type checking
is_string($var);
is_int($var);
is_array($var);
is_null($var);
isset($var);
empty($var);

// Math
abs(-5);        // 5
round(3.7);     // 4
rand(1, 10);    // Random number
max(1, 5, 3);   // 5
min(1, 5, 3);   // 1

// Date and time
date('Y-m-d');              // "2025-12-04"
date('H:i:s');              // "14:30:00"
time();                     // Unix timestamp
strtotime('next Monday');
```

## Including Files
```
include 'file.php';        // Include file, warning if not found
require 'file.php';        // Include file, fatal error if not found
include_once 'file.php';   // Include only once
require_once 'file.php';   // Require only once (common for classes)
```

## Modern PHP Features
### Type Declarations (PHP 7+)
```
function add(int $a, int $b): int {
  return $a + $b;
}

function getUser(int $id): ?User {  // Nullable return type
  return $user ?? null;
}
```

### Null Coalescing Operator
```
$username = $_GET['name'] ?? 'Guest';  // Default if not set
```

### Arrow Functions (PHP 7.4+)
```
$numbers = [1, 2, 3, 4];
$squared = array_map(fn($n) => $n * $n, $numbers);
```

## Running PHP
```
# Built-in server (development only)
php -S localhost:8000

# Run a script
php script.php

# Check version
php -v
```
