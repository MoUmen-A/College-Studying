# Exam 26 Solutions
**Course:** Web Programming

---

### Question One — MCQ & True/False | Bloom's: Remember / Analyse | Difficulty: Medium | Marks: 15

**Question (a) Choose the Correct Answer:**
1. All the following are HTML container elements EXCEPT: A. `<img>`
2. In CSS, the "the child selector" combinator is denoted by: C. `>`
3. In JavaScript, the function shows a pop-up box to allow the user inputs some text: B. `prompt()`
4. In PHP, which of the following is not a valid variable name: B. `if`
5. In PHP, the function sorts an associative array according to key in a descending order: *(Note: Exam options listed `ksort()`, `ksort()`, `asort()`, `rsort()`. The technically correct answer missing from the options is `krsort()`. For grading purposes, students who pointed this out or chose the closest fit should be credited).*

**Question (b) True/False and correct:**
1. In HTML, the text attribute specifies an alternative text...
   **False.** The `alt` attribute specifies alternative text.
2. In HTML, the Anchor tag `<a>` is a block level element.
   **False.** It is an inline element.
3. The CSS universal selector is denoted by `#`.
   **False.** It is denoted by `*` (asterisk).
4. CSS is responsible for the structural phase in web application development.
   **False.** HTML is responsible for the structural phase; CSS handles the presentation phase.
5. The expression `("10" + "20")` is evaluated to 1020 in JavaScript; while in PHP it raises an error.
   **False.** In PHP, the `+` operator adds them mathematically, resulting in `30` (no error).
6. In JavaScript, the function names are not case-sensitive.
   **False.** JavaScript is strictly case-sensitive.
7. The condition `("1000" != 1000)` is evaluated to be false.
   **True.** Type coercion treats the string and number as equal values, so `!=` is false.
8. The semicolon is mandatory at the end of each statement in both PHP and JavaScript.
   **False.** It is mandatory in PHP, but optional (due to automatic semicolon insertion) in JavaScript.
9. The POST method sends the user information appended to the page URL...
   **False.** The GET method appends to the URL (separated by `&`). POST sends data in the HTTP body.
10. In PHP, an associative array can be traversed using both for and foreach statements.
    **False.** Associative arrays must be traversed using `foreach` since their keys are not sequential integers.

**Key points to include for Full Marks:**
- Explicit correction of every false statement.
- Recognizing the difference in type coercion between JS string concatenation and PHP arithmetic operators.

**Common mistakes to avoid:**
- Answering False without providing the correct replacement word.

---

### Question Two — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 15

**Guide answer:**
a) (1) `<ol>`, (2) `type="a"`
b) (3) Clickable (or takes up space in layout), (4) Can have alternative text (or isn't repeated by default).
c) (5) `<sup>`, (6) `<sub>`
d) (7) `inline`, (8) `internal`
e) (9) `target="example"`, (10) `href="#top"`
f) (11) `<link>`, (12) `<head>`
g) (13) `array_key_exists()` (or `isset()`), (14) `array_slice()`, (15) `array_pop()`

**Key points to include for Full Marks:**
- Correct spelling of tags (`<sup>` vs `<sub>`) and PHP functions.

**Common mistakes to avoid:**
- Swapping `<sup>` and `<sub>`.
- Confusing `inline` and `internal` CSS definitions.

---

### Question Three — Application (PHP & Database) | Bloom's: Create | Difficulty: Hard | Marks: 10

**Question:**
Design a register page HTML form. Write `insertStudent.php` to insert data. Display data of all students in grade 6.

**Guide answer:**
**1. HTML Form:**
```html
<form action="insertStudent.php" method="POST">
    Name: <input type="text" name="name" required>
    Password: <input type="password" name="password" required>
    Address: <input type="text" name="address" required>
    Grade: <input type="text" name="grade" required>
    <input type="submit" value="Register">
</form>
```

**2. `insertStudent.php` (Insert and display grade 6):**
```php
<?php
$conn = mysqli_connect("localhost", "root", "", "School");

if (!$conn) {
    die("Connection failed: " . mysqli_connect_error());
}

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $name = $_POST['name'];
    $password = $_POST['password']; // Consider hashing in real apps
    $address = $_POST['address'];
    $grade = $_POST['grade'];

    // Insert new student
    $sql_insert = "INSERT INTO Students (name, password, address, grade) VALUES ('$name', '$password', '$address', '$grade')";
    
    if (mysqli_query($conn, $sql_insert)) {
        echo "A new student, $name is added successfully<br><br>";
    } else {
        echo "Error: " . mysqli_error($conn);
    }
}

// Display students in grade "6"
echo "<h3>Students in Grade 6:</h3>";
$sql_select = "SELECT * FROM Students WHERE grade = '6'";
$result = mysqli_query($conn, $sql_select);

if (mysqli_num_rows($result) > 0) {
    while($row = mysqli_fetch_assoc($result)) {
        echo "Name: " . $row["name"] . " | Address: " . $row["address"] . "<br>";
    }
} else {
    echo "No students found in grade 6.";
}

mysqli_close($conn);
?>
```

**Key points to include for Full Marks:**
- **HTML Validation:** Using the `required` attribute inside the `<input>` tags to validate against blanks natively in HTML.
- **SQL Execution:** Properly structured `INSERT INTO` and `SELECT` statements with variables wrapped in single quotes.
- **Data Fetching:** Utilizing `mysqli_fetch_assoc` inside a loop to print the result set.

**Common mistakes to avoid:**
- Trying to insert without checking the connection or form submission method.
- Leaving out the `required` HTML5 attribute when the prompt specifically asks to "Validate using HTML attributes".
