# JavaScript Questions Bank

### Section 1 — Topic summary
- Array manipulation (`sort`, `slice`, `join`, `find`, `indexOf`).
- Popup boxes (`alert`, `prompt`, `confirm`).
- Type coercion vs strict comparisons (`==` vs `===`), string concatenations (`+`).
- DOM interactions (`getElementById`, manipulating inputs).

### Section 2 — Tone analysis
Exams aggressively test output prediction for built-in array methods and exact string/number math logic. Application questions expect fully functional code blocks that retrieve values from forms and process them.

### Section 3 — Question bank

### Q1 — True / False + justify | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
In JavaScript, the function `prompt()` is used to show a pop-up box displaying a message with only an "OK" button. (If false, correct the statement).

**Guide answer:**
False. The function `prompt()` allows user input. The function that displays a message with only an "OK" button is `alert()`.

**Key points to include for Full Marks:**
- Correct to `alert()`.

**Common mistakes to avoid:**
- Misidentifying `confirm()` as the one with only an "OK" button.

### Q2 — Application (code) | Bloom's: Evaluate / Create | Difficulty: Hard | Marks: 8

**Question:**
Write a JavaScript script that calculates a total price. Assume you have two input fields with IDs `price1` and `price2`, and a button. When the user clicks the button, the script should retrieve the values from the two inputs, add them together, and display the result in an alert box. Ensure that the inputs are properly converted to numbers before addition.

**Guide answer:**
```javascript
function calculateTotal() {
    let p1 = Number(document.getElementById("price1").value);
    let p2 = Number(document.getElementById("price2").value);
    alert("The total price is: " + (p1 + p2));
}
```

**Key points to include for Full Marks:**
- Fetching values by ID, casting using `Number()` or `parseInt()`, and utilizing `alert()`.

**Common mistakes to avoid:**
- Forgetting to extract `.value` from the element, or forgetting to cast the string to a number, leading to concatenation.

### Q3 — MCQ | Bloom's: Understand | Difficulty: Easy | Marks: 2

**Question:**
The expression `("10" + "20")` is evaluated to what in JavaScript?
A. 30
B. "1020"
C. Error
D. 10+20

**Guide answer:**
B. "1020"

**Key points to include for Full Marks:**
- Select B (due to string concatenation).

**Common mistakes to avoid:**
- Selecting A (30), forgetting that the `+` operator concatenates when strings are involved.

### Q4 — Code Tracing | Bloom's: Apply | Difficulty: Hard | Marks: 5

**Question:**
Write the output of the following JavaScript snippet:
```javascript
let b = [29, 3, 5, 11, 32];
console.log(b.slice(-2));
console.log(b.indexOf(3, 2));
```

**Guide answer:**
Line 1: `[11, 32]` (slice extracts the last two elements).
Line 2: `-1` (searches for value 3 starting from index 2; it's not found).

**Key points to include for Full Marks:**
- Exact array format and correct `-1` value.

**Common mistakes to avoid:**
- Misunderstanding `indexOf` parameters and looking for index 3 starting at 2.

### Q5 — True / False + justify | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
The condition `("1000" != 1000)` is evaluated to be true. (If false, correct the statement).

**Guide answer:**
False. The `!=` operator performs type coercion, making string "1000" equal to number 1000, so they are not different (evaluates to false).

**Key points to include for Full Marks:**
- State False, explain type coercion.

**Common mistakes to avoid:**
- Confusing `!=` with `!==` which does not coerce types.

### Section 4 — Study tips & weak areas (Guide to Full Mark)
To get the full mark in JavaScript questions:
- **String vs Number Addition:** ALWAYS remember that reading a value from an HTML input returns a string. If you use `+` without parsing (e.g., `parseInt()`), it will concatenate, causing logic errors and mark deductions.
- **Array Sorting:** The default `sort()` method converts items to strings and sorts alphabetically. e.g. `[100, 20]` sorts to `[100, 20]`.
- **Negative slices:** `slice(-2)` grabs the last two elements. Know your array method definitions!

### Section 5 — Coverage gap analysis
- Need more questions involving loops over objects and JSON parsing, if covered in further lectures.
