# HTML / HTML5 Questions Bank

### Section 1 — Topic summary
- HTML5 structural tags and semantic elements (e.g., `<footer>`, `<header>`).
- Distinguishing block-level elements (`<p>`, `<h1>`, `<div>`) from inline elements (`<a>`, `<span>`, `<img>`).
- Form elements, list tags (`<ol>`, `<ul>`), table structures (`<caption>`, `<th>`, `<td>`), and core attributes (`href`, `alt`, `src`, `title`).

### Section 2 — Tone analysis
Questions are styled after straightforward knowledge retrieval, identifying the purpose of tags, and correcting misconceptions about block/inline properties as seen in past exams.

### Section 3 — Question bank

### Q1 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**
...... is the HTML element used to describe the content of a table.

**Guide answer:**
`<caption>`

**Key points to include for Full Marks:**
- Explicitly state the `<caption>` tag.

**Common mistakes to avoid:**
- Writing `<thead>` or `<th>` instead.

### Q2 — True / False + justify | Bloom's: Understand / Analyse | Difficulty: Medium | Marks: 3

**Question:**
The Anchor tag `<a>` is a block level element that automatically creates a new line before and after itself. (If false, correct the statement).

**Guide answer:**
False. The Anchor tag `<a>` is an inline element, which only takes up as much width as necessary and does not force line breaks.

**Key points to include for Full Marks:**
- Identify as False and correctly label it an inline element.

**Common mistakes to avoid:**
- Correcting it to say it's a structural tag without mentioning "inline".

### Q3 — Multiple choice (MCQ) | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**
Which attribute is used to specify what an image represents if the image cannot be displayed?
A. `title`
B. `alt`
C. `src`
D. `href`

**Guide answer:**
B. `alt`

**Key points to include for Full Marks:**
- Select B or write `alt`.

**Common mistakes to avoid:**
- Choosing `title` which provides a tooltip, not an alternative text replacement.

### Q4 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**
...... is the HTML semantic element typically used for information appearing at the end of a document.

**Guide answer:**
`<footer>`

**Key points to include for Full Marks:**
- Write `<footer>`.

**Common mistakes to avoid:**
- Using `<div>` without the semantic `footer` tag when specifically asked for the semantic element.

### Q5 — Application | Bloom's: Apply | Difficulty: Medium | Marks: 5

**Question:**
Write the HTML code to create an ordered list (using letters A, B, C) containing three items: "HTML", "CSS", "JS". 

**Guide answer:**
```html
<ol type="A">
  <li>HTML</li>
  <li>CSS</li>
  <li>JS</li>
</ol>
```

**Key points to include for Full Marks:**
- Use `<ol>` with the `type="A"` attribute, and correctly nest `<li>` tags.

**Common mistakes to avoid:**
- Using `<ul>` instead of `<ol>`, or forgetting to wrap items in `<li>`.

### Section 4 — Study tips & weak areas (Guide to Full Mark)
To get the full mark in HTML questions:
- **Exact Tag Names:** Do not confuse similar tags (e.g., `<title>` vs the `title=""` attribute).
- **Inline vs Block:** Memorize which elements force line breaks (`<p>`, `<div>`, `<h1>`) versus which flow with text (`<a>`, `<span>`, `<img>`). This often appears in True/False questions.
- **Attributes:** Always associate attributes with their primary element (`src` for `<img>`, `href` for `<a>`). 

### Section 5 — Coverage gap analysis
- Next exams may feature image maps (`<map>`, `<area>`) and specific input types in forms, which need further exploration.
