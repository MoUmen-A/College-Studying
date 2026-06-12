# Exam 25 Solutions
**Course:** Web Programming

---

### Question One — Fill in the spaces | Bloom's: Remember | Difficulty: Easy | Marks: 10

**Question:**
1. ...... is the HTML semantic element typically used for information appearing at the end of a document.
2. ...... are the HTML elements used to display titles and subtitles.
3. ...... is the HTML attribute used to specify what an image represents if the image cannot be displayed.
4. ...... is the HTML element used to mark up a part of text in a document.
5. ...... is the HTML element used to describe the content of a table.
6. ...... is the HTML element used to include and display a web page within another web page.
7. ...... is the HTML element used to identify items in a list.
8. ...... is the HTML attribute that is used to specify the address of a hyperlink.
9. ...... is the HTML entity that is used for non-breaking spaces.
10. ...... is the HTML attribute that is used to specify the amount of space between table cells.

**Guide answer:**
1. `<footer>`
2. `<h1>` to `<h6>` (or heading tags)
3. `alt`
4. `<span>` (or `<mark>`)
5. `<caption>`
6. `<iframe>`
7. `<li>`
8. `href`
9. `&nbsp;`
10. `cellspacing`

**Key points to include for Full Marks:**
- Exact spelling of attributes and tags.
- Recognizing the `&nbsp;` entity format correctly.

**Common mistakes to avoid:**
- Writing `text` instead of `alt` for image fallback.
- Confusing `cellspacing` with `cellpadding`.

---

### Question Two — Code Tracing | Bloom's: Apply / Analyse | Difficulty: Hard | Marks: 10

**Question:**
Determine the text color of each HTML element given the provided internal style sheet.

**Guide answer:**
- **Container**: `navy` (Inherited from `div.container { color: navy; }`).
- **Unique**: `teal` (The element is `<p id="unique">`, but the CSS defines a class `.unique`. Thus it doesn't match. It only matches `div p { color: teal; }`).
- **Special**: `red` (Matches `p.special { color: red; }`, which has higher specificity than `div p`).
- **Normal Span**: `violet` (Preceded by `p.special`. Matches both `p ~ span` and `p + span`. `p + span` is written last in CSS, so it wins).
- **Another Span**: `blue` (Preceded by a span, but follows a paragraph `p.special`. Only matches `p ~ span { color: blue; }`).
- **Heading**: `navy` (It is an `<h2>` inside the container. Inherits from `div.container`).
- **Nested**: `teal` (Matches `h2 ~ p` (cyan) and `div p` (teal). Both have 0,0,2 specificity. `div p` is declared last, so it overrides `h2 ~ p`).
- **Em**: `magenta` (Assuming standard tag reading, the word "Em" is inside `<p class="highlight">`. Matches `.highlight { color: magenta; }`).
- **Text**: `magenta` (Also inside `<p class="highlight">`).
- **Standalone**: `purple` (Matches `.unique { color: purple; }`).

**Key points to include for Full Marks:**
- Recognizing that `.unique` in CSS targets a class, not an ID, so the `<p id="unique">` relies on `div p`.
- Correct application of the cascading rule where specificities are tied (last rule wins: `p + span` over `p ~ span`, and `div p` over `h2 ~ p`).

**Common mistakes to avoid:**
- Mistaking `#unique` with `.unique`.
- Misinterpreting adjacent sibling `+` vs general sibling `~`.

---

### Question Three — Application (PHP) | Bloom's: Create | Difficulty: Hard | Marks: 10

**Question:**
Write a PHP program to update a profile. (a) Design form and check login. (b) Validate email and 10-digit phone number. (c) Update database and redirect to Confirm page.

**Guide answer:**
```php
<?php
session_start();

// (a) Check if user is logged in
if (!isset($_SESSION["user"])) {
    die("Please login first.");
}

$error = "";
$username = $_SESSION["user"];

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $email = $_POST["email"];
    $phone = $_POST["phone"];
    
    // (b) Validation
    if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
        $error .= "Invalid email format. ";
    }
    if (!preg_match('/^[0-9]{10}$/', $phone)) {
        $error .= "Phone number must be exactly 10 digits. ";
    }
    
    // (c) Update and redirect
    if (empty($error)) {
        $conn = mysqli_connect("localhost", "root", "", "Users");
        $sql = "UPDATE UserProfile SET Email='$email', PhoneNumber='$phone' WHERE Name='$username'";
        if (mysqli_query($conn, $sql)) {
            header("Location: Confirm.php");
            exit();
        }
    }
}
?>

<!-- HTML Form -->
<form method="POST">
    Email: <input type="text" name="email"> 
    Phone: <input type="text" name="phone">
    <span style="color:red;"><?php echo $error; ?></span>
    <input type="submit" value="Update Profile">
</form>
```

**Key points to include for Full Marks:**
- `session_start()` and `isset($_SESSION["user"])` to check login state.
- `preg_match` or string length evaluation for the 10-digit requirement.
- Valid SQL `UPDATE` statement.
- Using `header("Location: ...")` for the redirect.

**Common mistakes to avoid:**
- Forgetting to start the session before accessing `$_SESSION`.
- Executing the SQL query without wrapping variables in quotes.

---

### Question Four — Application & Tracing (JavaScript) | Bloom's: Apply / Create | Difficulty: Hard | Marks: 10

**Question:**
(a) JavaScript receipt total from checkboxes and textboxes.
(b) Array operation outputs.

**Guide answer:**
**(a) JavaScript Script:**
```javascript
function calculateTotal() {
    let total = 0;
    
    let beefChecked = document.getElementById("beefChx").checked;
    let chickenChecked = document.getElementById("chickenChx").checked;
    
    if (beefChecked) {
        let beefQty = Number(document.getElementById("beefTxt").value);
        total += beefQty * 50; // Assuming 50 is the price of beef
    }
    if (chickenChecked) {
        let chickenQty = Number(document.getElementById("chickenTxt").value);
        total += chickenQty * 40; // Assuming 40 is the price of chicken
    }
    
    alert("Total receipt value is: " + total);
}
```
*(Prices are assumed based on a standard receipt mockup)*.

**(b) Array Output Trace:**
```javascript
let a=[7,3,12,100,32,30]; 
let b=[29,3,5,3,11,32];

console.log(a.sort()); 
// Output: [100, 12, 3, 30, 32, 7] (Sorted alphabetically as strings)

console.log(a.join(':')); 
// Output: "100:12:3:30:32:7"

console.log(b.find((element) => element > 10)); 
// Output: 29 (First element > 10)

console.log(b.slice(-2)); 
// Output: [11, 32] (Last two elements)

console.log(b.indexOf(3,2)); 
// Output: 3 (Searches for value 3 starting at index 2)
```

**Key points to include for Full Marks:**
- **JS Form:** Using `.checked` to verify checkboxes, casting `.value` to Number before multiplication.
- **Trace:** Recognizing that `.sort()` default behavior converts numbers to strings (`100` before `12`).

**Common mistakes to avoid:**
- Sorting `a` numerically instead of alphabetically.
- Returning an array instead of a single value for `.find()`.
