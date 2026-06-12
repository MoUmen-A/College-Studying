# PHP Questions Bank

### Section 1 — Topic summary
- Syntax rules: Variables, statement terminators.
- Associative array sorting: `asort`, `ksort`, `arsort`, `krsort`, `rsort`.
- Form processing: GET vs POST superglobals (`$_POST`).
- Iteration: `foreach` loops for associative arrays.

### Section 2 — Tone analysis
PHP questions test the precise differences between the various sorting functions, ensuring students know how keys and values are affected. Tracing questions require students to manually simulate associative array ordering.

### Section 3 — Question bank

### Q1 — MCQ | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**
In PHP, which function is used to sort an associative array according to the key in a descending order?
A. `asort()`
B. `ksort()`
C. `krsort()`
D. `rsort()`

**Guide answer:**
C. `krsort()`

**Key points to include for Full Marks:**
- Select C.

**Common mistakes to avoid:**
- Choosing `ksort()` which sorts ascending instead of descending.

### Q2 — Code Tracing / Output Prediction | Bloom's: Apply / Analyse | Difficulty: Medium | Marks: 5

**Question:**
What will be the output of the following PHP code snippet?
```php
<?php
$colors = array("Red" => 10, "Blue" => 30, "Green" => 20);
asort($colors);
foreach($colors as $key => $val) {
    echo "$key:$val, ";
}
?>
```

**Guide answer:**
Output: `Red:10, Green:20, Blue:30, `
Explanation: `asort()` sorts the associative array in ascending order according to the value.

**Key points to include for Full Marks:**
- Provide exact formatting with spaces and commas.

**Common mistakes to avoid:**
- Sorting by key (`Blue:30, Green:20, Red:10`) instead of value.

### Q3 — MCQ | Bloom's: Understand | Difficulty: Easy | Marks: 2

**Question:**
Which of the following is NOT a valid PHP variable name?
A. `$if`
B. `if`
C. `$_if`

**Guide answer:**
B. `if`

**Key points to include for Full Marks:**
- Variables must begin with `$ `.

**Common mistakes to avoid:**
- Choosing `$if` thinking keywords cannot be variables (they can, if prefixed with `$`).

### Q4 — True / False + justify | Bloom's: Analyse | Difficulty: Medium | Marks: 2

**Question:**
In PHP, an associative array can be traversed using both `for` and `foreach` statements. (If false, correct the statement).

**Guide answer:**
False. An associative array uses named keys rather than numerical indices, so it should be traversed using a `foreach` loop.

**Key points to include for Full Marks:**
- State False, identify `foreach` as the correct loop.

**Common mistakes to avoid:**
- Merely saying false without providing the correct `foreach` alternative.

### Q5 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**
In PHP, the function ______ returns true if the specified key has data in the array.

**Guide answer:**
`array_key_exists()` (or `isset()`)

**Key points to include for Full Marks:**
- Write `array_key_exists()`.

**Common mistakes to avoid:**
- Confusing with generic JS methods like `has()`.

### Section 4 — Study tips & weak areas (Guide to Full Mark)
To get the full mark in PHP questions:
- **Array Sorting Functions:** Memorize the matrix of sort functions. Starts with 'k' = sorts by key. Starts with 'a' = sorts associative by value. Contains 'r' = reverse/descending. 
- **Variable Syntax:** Don't forget the `$ ` symbol. A very common mistake in written exams is writing variable names like Java/JS without the dollar sign.
- **Statement Endings:** Always include the semicolon `;` at the end of PHP lines!

### Section 5 — Coverage gap analysis
- Need further coverage of PHP session variables (`$_SESSION`) and multidimensional arrays.
