# Database Integration Questions Bank

### Section 1 — Topic summary
- MySQLi connection methods (`mysqli_connect`).
- Processing forms and linking PHP inputs to SQL queries.
- Using SQL commands (`INSERT`, `SELECT`, `UPDATE`) dynamically in PHP.
- Input validation (checking for empty fields, proper formats).

### Section 2 — Tone analysis
Focuses on full-scale application generation. Students must write long-form PHP code that connects to databases, handles errors gracefully, and executes SQL using superglobals securely.

### Section 3 — Question bank

### Q1 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**
In PHP, to send user information appended to the page URL, we use the ______ method in the HTML form.

**Guide answer:**
`GET`

**Key points to include for Full Marks:**
- Write `GET`.

**Common mistakes to avoid:**
- Answering `POST`, which sends data in the HTTP request body.

### Q2 — Application (code) | Bloom's: Evaluate / Create | Difficulty: Hard | Marks: 10

**Question:**
You have an HTML form that POSTs data to `insertStudent.php`. Write the script that connects to a MySQL database named `School` on `localhost` (`root`, no password), validates the `student_name` is not empty, inserts it into the `Students` table, and displays a success message.

**Guide answer:**
```php
<?php
$conn = mysqli_connect("localhost", "root", "", "School");
if ($_SERVER["REQUEST_METHOD"] == "POST" && !empty($_POST["student_name"])) {
    $name = $_POST["student_name"];
    $sql = "INSERT INTO Students (name) VALUES ('$name')";
    if (mysqli_query($conn, $sql)) {
        echo "A new student, $name is added successfully";
    }
}
mysqli_close($conn);
?>
```

**Key points to include for Full Marks:**
- Valid `mysqli_connect()`, validation using `!empty()`, and correctly formatted `INSERT` query.

**Common mistakes to avoid:**
- Forgetting to enclose the `$name` variable in single quotes within the SQL query string.

### Q3 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**
The PHP function used to execute an SQL statement against the active database connection is ______.

**Guide answer:**
`mysqli_query()`

**Key points to include for Full Marks:**
- Write `mysqli_query()`.

**Common mistakes to avoid:**
- Using deprecated `mysql_query()` or forgetting the connection parameter.

### Q4 — Application | Bloom's: Evaluate / Create | Difficulty: Hard | Marks: 10

**Question:**
Write a PHP snippet to fetch and display the data of all students in grade "6" from the `Students` table.

**Guide answer:**
```php
$sql = "SELECT * FROM Students WHERE grade = '6'";
$result = mysqli_query($conn, $sql);
while($row = mysqli_fetch_assoc($result)) {
    echo $row['name'] . "<br>";
}
```

**Key points to include for Full Marks:**
- Correct `SELECT` query structure with `WHERE` clause, and a loop using `mysqli_fetch_assoc`.

**Common mistakes to avoid:**
- Trying to print `$result` directly instead of fetching rows via a `while` loop.

### Q5 — Application | Bloom's: Evaluate | Difficulty: Hard | Marks: 8

**Question:**
Write the PHP validation code required to ensure a phone number submitted via `$_POST['phone']` is exactly 10 digits with no spaces.

**Guide answer:**
```php
$phone = $_POST['phone'];
if (preg_match('/^[0-9]{10}$/', $phone)) {
    echo "Valid";
} else {
    echo "Invalid Phone Number";
}
```

**Key points to include for Full Marks:**
- String length check and ensuring it contains only numbers.

**Common mistakes to avoid:**
- Using `is_numeric` without checking the exact string length of 10.

### Section 4 — Study tips & weak areas (Guide to Full Mark)
To get the full mark in Database Integration questions:
- **SQL String Wrapping:** In PHP, when inserting a variable into an SQL string, remember to wrap it in single quotes: `VALUES ('$name')`. Forgetting the single quotes will crash the SQL query.
- **Validation Before Insertion:** Never blindly insert `$_POST` variables into the database. Always check if they are set and not empty using `isset()` or `empty()`.
- **Database Connection Order:** Remember the order of parameters for `mysqli_connect()`: Host, Username, Password, Database Name.

### Section 5 — Coverage gap analysis
- Next topics should tackle `UPDATE` and `DELETE` queries.
