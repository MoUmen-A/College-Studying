# CSS Questions Bank

### Section 1 — Topic summary
- Combinators: Child (`>`), adjacent sibling (`+`), general sibling (`~`), descendant (space).
- Specificity calculations for conflicting styles (ID vs Class vs Element).
- Inline, internal, and external style sheets.

### Section 2 — Tone analysis
Heavy focus on code tracing. Students are expected to manually "render" the CSS rules onto an HTML tree to determine exact colors or formats applied, mirroring the challenging trace questions in previous exams.

### Section 3 — Question bank

### Q1 — MCQ | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**
In CSS, which combinator is used to select an element that is placed immediately after another specific element (adjacent sibling)?
A. `>`
B. `+`
C. `~`
D. ` ` (space)

**Guide answer:**
B. `+`

**Key points to include for Full Marks:**
- Select option B.

**Common mistakes to avoid:**
- Confusing `+` (adjacent sibling) with `~` (general sibling).

### Q2 — Code Tracing / Output Prediction | Bloom's: Apply / Analyse | Difficulty: Hard | Marks: 5

**Question:**
Determine the text color of the `span` element with the text "Target Span" when the provided internal style sheet is applied. Explain why.
```html
<body>
    <div class="content">
        <p>Paragraph 1</p>
        <p class="special">Paragraph 2</p>
        <span>Target Span</span>
    </div>
</body>
<style>	
    div span { color: blue; }	
    p.special + span { color: red; }	
    .content p ~ span { color: green; }	
</style>	
```

**Guide answer:**
The text color of "Target Span" will be **green**. 
Explanation: `p.special + span` and `.content p ~ span` have the same specificity (0,1,2). The one that appears last in the CSS rule set takes precedence. Therefore, `.content p ~ span` applies.

**Key points to include for Full Marks:**
- State the final color (green) and mention specificity/cascading order.

**Common mistakes to avoid:**
- Misunderstanding specificity and assuming `.special` being closer in the DOM matters more than cascading order.

### Q3 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**
The ...... CSS is used to apply a style to a single HTML element, while the internal CSS is used to define a style for a single HTML page.

**Guide answer:**
`inline`

**Key points to include for Full Marks:**
- Write `inline`.

**Common mistakes to avoid:**
- Writing `external` or confusing it with `internal`.

### Q4 — True / False + justify | Bloom's: Analyse | Difficulty: Medium | Marks: 2

**Question:**
The CSS universal selector is denoted by `#`. (If false, correct the statement).

**Guide answer:**
False. The CSS universal selector is denoted by `*`. The `#` symbol is used to denote an ID selector.

**Key points to include for Full Marks:**
- State False and correct `#` to `*`.

**Common mistakes to avoid:**
- Saying it is false without providing the correct `*` symbol.

### Q5 — Code Tracing | Bloom's: Apply | Difficulty: Hard | Marks: 5

**Question:**
Determine the text color of the `em` element below:
```html
<body>
  <p>Nested<em>Text</em></p>
</body>
<style>
  p > em { color: green; }
  p em { color: red; }
</style>
```

**Guide answer:**
The color is **red**. Both selectors have the same specificity (0,0,2). Because `p em` is declared last, it overrides `p > em`.

**Key points to include for Full Marks:**
- State red and reference the cascading rule.

**Common mistakes to avoid:**
- Assuming child combinator `>` gives extra specificity points over descendant combinator space.

### Section 4 — Study tips & weak areas (Guide to Full Mark)
To get the full mark in CSS Code Tracing:
- **Count Specificity:** Use the (ID, Class, Element) formula. ID = 100, Class = 10, Element = 1. Highest number wins.
- **Tie-Breakers:** If specificities are equal, the rule written **last** in the `<style>` block wins.
- **Combinator meaning:** Know the difference between `+` (next immediate sibling) and `~` (any following sibling). Misinterpreting these leads to incorrect trace colors.

### Section 5 — Coverage gap analysis
- Need to expand on linking external stylesheets and testing pseudo-classes like `:hover`.
