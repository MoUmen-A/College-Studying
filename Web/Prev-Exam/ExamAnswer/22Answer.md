# Exam 22 Solutions
**Course:** Web Programming

---

### Question One — Multiple Choice | Bloom's: Remember | Difficulty: Easy | Marks: 5

**Question:**
1) All of the following are examples of HTML block-level element EXCEPT 
2) The HTML element that is used to embed a separate HTML document in an HTML page is: 
3) JavaScript is responsible for the ---------- phase in the web application. 
4) The PHP comment is ---------- 
5) In JavaScript, the function ---------- is used to display a dialog-box containing a message with [OK / Cancel] buttons

**Guide answer:**
1. **C. `<td>`** (The `<td>` element displays as a table-cell, not a standard block-level element like `<h1>`, `<p>`, or `<div>`).
2. **B. `<iframe>`**
3. **C. behavioral**
4. **D. all of them** (`#`, `//`, `/* */`)
5. **A. `confirm ( )`**

**Key points to include for Full Marks:**
- Ensure the correct letter option is selected.
- Understanding the semantic role of JS as behavioral compared to HTML (structural) and CSS (presentational).

**Common mistakes to avoid:**
- Misidentifying `alert()` (which only has OK) instead of `confirm()` for OK/Cancel options.

---

### Question Two (a) — Code Tracing | Bloom's: Apply / Analyse | Difficulty: Hard | Marks: 6

**Question:**
What is the output of the PHP and JS codes? Explain your answers.

**Guide answer:**

**PHP Trace:**
```
c = 1.5 <br>
b = 16
Not Identical
```
**Explanation:** 
- The function `Q2()` uses global variables `$a` ("10") and `$b` (15). 
- `$z = 15 / "10"` evaluates to `1.5` due to implicit type casting.
- `++$b` increments the global `$b` to 16.
- The `===` operator checks for strict equality. Since `$d` (10) is an integer and `$a` ("10") is a string, they are not identical.

**JavaScript Trace:**
```
1 <br>
r <br>
bPro <br>
11,32 <br>
29-5-3-8-11-32 <br>
-1
```
**Explanation:**
- `indexOf("a")`: The first "a" in "JavaScript" is at index 1.
- `charAt(6)`: The character at index 6 is "r".
- `slice(2,6)`: Extracts from index 2 up to (but not including) 6 -> "bPro".
- `slice(-2)`: Extracts the last 2 elements of the array -> `11,32`.
- `join("-")`: Joins array elements with a dash -> `29-5-3-8-11-32`.
- `lastIndexOf('M')`: The `toUpperCase()` function returns a new string but *does not modify* `B` in place because strings are immutable in JS. Therefore, `B` remains "WebProgramming", which does not contain the uppercase 'M', resulting in `-1`.

**Key points to include for Full Marks:**
- Explicitly mention PHP's strict type checking (`===`) for the `Not Identical` output.
- Explicitly mention that JS strings are immutable, leading to `-1`. *(Note: If the exam assumed strings mutate, pointing out the technical JS rule demonstrates full understanding and secures the mark).*

**Common mistakes to avoid:**
- Confusing `=` and `===` in PHP.
- Assuming `toUpperCase()` modifies the string in-place in JS and writing `10` as the last output.

---

### Question Two (b) — HTML Debugging | Bloom's: Analyse | Difficulty: Medium | Marks: 6

**Question:**
Each of the HTML statements contains errors. Explain the errors then correct them.

**Guide answer:**
1. `<input name="country" value="Your country here. ">`
   - **Error:** Missing the `type` attribute.
   - **Correction:** `<input type="text" name="country" value="Your country here.">`
2. `<checkbox name="color" value="purple">`
   - **Error:** `<checkbox>` is not a valid HTML tag.
   - **Correction:** `<input type="checkbox" name="color" value="purple">`
3. `<input type="radiobutton" value="Ahly">` \n `<input type="radiobutton" value="Zamalek">`
   - **Error:** `type` should be `radio` (not `radiobutton`). Also, for radio buttons to work as a mutually exclusive group, they must share the same `name` attribute.
   - **Correction:** `<input type="radio" name="team" value="Ahly"> <input type="radio" name="team" value="Zamalek">`
4. `<p style="red"> Hello! </p>`
   - **Error:** CSS syntax in the style attribute is incorrect. It needs a property name.
   - **Correction:** `<p style="color: red;"> Hello! </p>`
5. `<img text="Egypt Flag" width="100" length="60"> Egypt.jpg </img>`
   - **Error:** Uses `text` instead of `alt`; uses `length` instead of `height`; image source is outside the tag instead of using the `src` attribute; `<img>` is an empty element and should not have a closing tag.
   - **Correction:** `<img src="Egypt.jpg" alt="Egypt Flag" width="100" height="60">`
6. `<div style=color: circular-gradient (blue)> </div>`
   - **Error:** Missing quotes around the style string. Also, gradients are applied to `background` or `background-image`, not `color`. The correct function is `radial-gradient`.
   - **Correction:** `<div style="background: radial-gradient(blue, white);"> </div>`

**Key points to include for Full Marks:**
- Identifying all 4 distinct errors in statement #5.
- Mentioning the shared `name` attribute requirement for radio buttons.

**Common mistakes to avoid:**
- Correcting `radiobutton` to `radio` but forgetting to add the `name` attribute to group them.

---

### Question Three — Application (PHP) | Bloom's: Create | Difficulty: Hard | Marks: 11

**Question:**
Write a PHP script to connect to a DB, validate GPA, insert data, and display CS students with GPA > 3.1.

**Guide answer:**
```php
<?php
// (a) Connect to the database
$conn = mysqli_connect("localhost", "root", "", "university");
if (!$conn) {
    die("Connection failed: " . mysqli_connect_error());
}

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $sid = $_POST['sid'];
    $name = $_POST['name'];
    $mail = $_POST['mail'];
    $dept = $_POST['dept'];
    $gpa = $_POST['gpa'];

    // (b) Validate the input of gpa
    if (is_numeric($gpa) && $gpa > 0 && $gpa < 4) {
        // (c) Insert the entered data
        $sql_insert = "INSERT INTO students (sid, name, mail, dept, gpa) VALUES ('$sid', '$name', '$mail', '$dept', '$gpa')";
        if (mysqli_query($conn, $sql_insert)) {
            echo "Student inserted successfully.<br>";
        } else {
            echo "Error: " . mysqli_error($conn) . "<br>";
        }
    } else {
        echo "Invalid GPA. It must be a positive number less than 4.<br>";
    }
}

// (d) Display all students with gpa > 3.1 in CS department (deptId = 10)
$sql_select = "SELECT * FROM students WHERE gpa > 3.1 AND dept = '10'";
$result = mysqli_query($conn, $sql_select);

echo "<h3>CS Students with GPA > 3.1:</h3>";
if (mysqli_num_rows($result) > 0) {
    while($row = mysqli_fetch_assoc($result)) {
        echo "ID: " . $row['sid'] . " - Name: " . $row['name'] . " - GPA: " . $row['gpa'] . "<br>";
    }
} else {
    echo "No matching students found.";
}

mysqli_close($conn);
?>
```

**Key points to include for Full Marks:**
- Explicit check for `$gpa > 0 && $gpa < 4`.
- Correct SQL syntax combining two conditions `WHERE gpa > 3.1 AND dept = '10'`.
- Proper use of `mysqli_fetch_assoc` loop to print results.

**Common mistakes to avoid:**
- Inserting data without wrapping PHP string variables in single quotes inside the SQL statement.

---

### Question Four — Application (JavaScript & HTML) | Bloom's: Create | Difficulty: Hard | Marks: 12

**Question:**
Write HTML and JS to calculate a receipt based on checkboxes and inputs. Use `confirm()`. If OK, display total. If Cancel, clear inputs.

**Guide answer:**
```html
<!-- HTML Design -->
<form id="receiptForm">
    <input type="checkbox" id="a"> Item A Qty: <input type="number" id="x"><br>
    <input type="checkbox" id="b"> Item B Qty: <input type="number" id="y"><br>
    <input type="checkbox" id="c"> Item C Qty: <input type="number" id="z"><br>
    
    <button type="button" onclick="calculateTotal()">Total</button>
    <span id="totalDisplay" style="margin-left: 10px; font-weight: bold;"></span>
</form>

<!-- JavaScript -->
<script>
function calculateTotal() {
    let total = 0;
    
    // Assume fixed prices for calculation (e.g., A=10, B=20, C=30)
    if (document.getElementById("a").checked) {
        total += Number(document.getElementById("x").value) * 10;
    }
    if (document.getElementById("b").checked) {
        total += Number(document.getElementById("y").value) * 20;
    }
    if (document.getElementById("c").checked) {
        total += Number(document.getElementById("z").value) * 30;
    }
    
    // Confirmation dialog
    let userAgrees = confirm("Your total is " + total + ". Do you confirm?");
    
    if (userAgrees) {
        // Display total after the button
        document.getElementById("totalDisplay").innerHTML = "Total: " + total;
    } else {
        // Clear input quantities
        document.getElementById("x").value = "";
        document.getElementById("y").value = "";
        document.getElementById("z").value = "";
        document.getElementById("totalDisplay").innerHTML = "";
    }
}
</script>
```

**Key points to include for Full Marks:**
- Using `.checked` to verify boolean checkbox state.
- Wrapping the prompt in an `if (confirm(...))` block to branch behavior.
- Clearing the `.value` of all text inputs in the `else` (Cancel) block.
- Casting `.value` (which is a string) to `Number()` before mathematical operations.

**Common mistakes to avoid:**
- Using `alert()` instead of `confirm()`, making it impossible to handle the OK/Cancel logic.
- Trying to set `.innerHTML` of input elements instead of modifying `.value`.
