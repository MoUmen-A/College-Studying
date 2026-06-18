# COA Practice Exam 10: RPN, Stack Evaluation & Postfix/Infix Conversions

This exam focuses on Reverse Polish Notation (RPN), infix-to-postfix conversion, stack-based evaluation with trace tables, and zero-address instruction programming.

---

## Topic Summary

This exam covers the following core concepts from the COA course:

- **Reverse Polish Notation (RPN) / Postfix Notation:**
  - An algebraic notation where operators **follow** their operands (e.g., $A + B$ becomes $A\ B\ +$).
  - Eliminates the need for parentheses and operator precedence rules during parsing.
- **Infix to Postfix (RPN) Conversion:**
  - Evaluates operands and operators based on standard precedence ($*$, $/$ before $+$, $-$) and parentheses, working from left to right.
  - Operand order is always preserved (e.g., $A$ appears before $B$ in both infix and postfix).
- **Stack-Based RPN Evaluation:**
  - Operands are pushed onto a stack.
  - When an operator is encountered, the top two elements are popped, the operation is applied, and the result is pushed back.
  - Crucial: For non-commutative operations (subtraction, division), the first popped element is the **right** operand (divisor/subtractor) and the second popped element is the **left** operand (dividend/minuend).
- **Zero-Address Instruction Architectures:**
  - Instruction sets that do not use explicit memory addresses for arithmetic operations (e.g., `ADD`, `SUB`).
  - Rely on a hardware stack. Only `PUSH` and `POP` require memory addresses to move data between registers/memory and the stack.

---

## How to Solve Questions in This Exam

### Infix to Postfix Conversions (Q1, Q2, Q7)
1. **Parenthesize the infix expression completely** according to operator precedence.
   - E.g., $A + B * C \implies A + (B * C) \implies (A + (B * C))$.
2. **Move the operators to the right of their respective closing parentheses.**
   - E.g., $(A + (B\ C\ *)) \implies (A\ (B\ C\ *)\ +) \implies A\ B\ C\ *\ +$.
3. **Remove all parentheses** to obtain the final RPN expression.
4. **Always verify:** Check that the operands ($A, B, C, \dots$) remain in the exact same left-to-right order as in the original infix expression.

### Postfix (RPN) to Infix Conversions (Q3, Q4)
1. Scan the RPN expression from left to right.
2. If you see an operand, push it to a mental stack.
3. If you see a binary operator:
   - Pop the top element (call it $Y$).
   - Pop the next element (call it $X$).
   - Form the parenthesized infix string: $(X \text{ OP } Y)$.
   - Push this string back onto the stack.
4. The final item on the stack is the equivalent infix expression.

### RPN Stack Trace Tables (Q5, Q6, Q7)
1. Set up columns: `Step`, `Token`, `Action`, `Stack State (Bottom → Top)`.
2. For each number/variable: Action is `Push operand`, append to the right end of the stack list.
3. For each operator:
   - Action is `Pop Y, X; Push result`.
   - Perform the math: $X - Y$ for subtraction, $X / Y$ for division.
   - Update the stack list.
4. Write the final result clearly. Always perform a quick sanity check by evaluating the infix equivalent.

### Zero-Address Programming (Q8)
- Zero-address code directly mirrors the RPN representation of the expression.
- Convert the algebraic target expression to RPN.
- Replace operands with `PUSH Operand`.
- Replace operators with the corresponding zero-address instructions (`ADD`, `SUB`, `MUL`, `DIV`).
- Add a final `POP Destination` to store the result in the target variable.
- **Double check subtraction and division orders:**
  - To compute $C - D$, write:
    ```
    PUSH C
    PUSH D
    SUB
    ```
  - This ensures $D$ is at the top of the stack and $C$ is below it, so `SUB` computes $C - D$.

---

## Part 1: Infix to Postfix Conversions [10 Marks]

### Q1 — Application (Conversion) | Bloom's: Apply | Difficulty: Medium | Marks: 2

**Question:**
Convert the following infix expressions to Reverse Polish Notation (RPN / Postfix):

**(a)** $(A + B) * (C + D) - E$
**(b)** $A * (B + C * D) + E$

**Guide Answer:**

**(a)** $(A + B) * (C + D) - E$

Step-by-step using operator precedence and parentheses:
- $(A + B)$ → $A\ B\ +$
- $(C + D)$ → $C\ D\ +$
- $(A + B) * (C + D)$ → $A\ B\ +\ C\ D\ +\ *$
- Subtract $E$: $A\ B\ +\ C\ D\ +\ *\ E\ -$

**RPN:** $A\ B\ +\ C\ D\ +\ *\ E\ -$

**(b)** $A * (B + C * D) + E$

Step-by-step:
- Inner: $C * D$ → $C\ D\ *$
- Parenthesis: $B + C * D$ → $B\ C\ D\ *\ +$
- Multiply by $A$: $A * (B + C * D)$ → $A\ B\ C\ D\ *\ +\ *$
- Add $E$: $A\ B\ C\ D\ *\ +\ *\ E\ +$

**RPN:** $A\ B\ C\ D\ *\ +\ *\ E\ +$

**Key Points to Include for Full Marks:**
- Correct operator precedence: $*$ and $/$ before $+$ and $-$.
- Parentheses override precedence.
- Operand order is preserved (left to right).

**Common Mistakes to Avoid:**
- Changing operand order.
- Applying addition before multiplication when no parentheses dictate it.

---

### Q2 — Application (Conversion) | Bloom's: Apply | Difficulty: Hard | Marks: 3

**Question:**
Convert the following infix expressions to RPN:

**(a)** $A / B + C * D - E * F / G$
**(b)** $(A + B) * ((C - D) / (E + F))$
**(c)** $A * B * C + D / E - F$

**Guide Answer:**

**(a)** $A / B + C * D - E * F / G$

Apply left-to-right evaluation with precedence (* and / before + and -):
- $A / B$ → $A\ B\ /$
- $C * D$ → $C\ D\ *$
- $E * F$ → $E\ F\ *$
- $E * F / G$ → $E\ F\ *\ G\ /$
- $(A / B) + (C * D)$ → $A\ B\ /\ C\ D\ *\ +$
- Result minus $(E * F / G)$: $A\ B\ /\ C\ D\ *\ +\ E\ F\ *\ G\ /\ -$

**RPN:** $A\ B\ /\ C\ D\ *\ +\ E\ F\ *\ G\ /\ -$

**(b)** $(A + B) * ((C - D) / (E + F))$

- $(A + B)$ → $A\ B\ +$
- $(C - D)$ → $C\ D\ -$
- $(E + F)$ → $E\ F\ +$
- $(C - D) / (E + F)$ → $C\ D\ -\ E\ F\ +\ /$
- $(A + B) * ((C - D) / (E + F))$ → $A\ B\ +\ C\ D\ -\ E\ F\ +\ /\ *$

**RPN:** $A\ B\ +\ C\ D\ -\ E\ F\ +\ /\ *$

**(c)** $A * B * C + D / E - F$

Left-to-right association for same-precedence operators:
- $A * B$ → $A\ B\ *$
- $A * B * C$ → $A\ B\ *\ C\ *$
- $D / E$ → $D\ E\ /$
- $(A * B * C) + (D / E)$ → $A\ B\ *\ C\ *\ D\ E\ /\ +$
- Result minus $F$: $A\ B\ *\ C\ *\ D\ E\ /\ +\ F\ -$

**RPN:** $A\ B\ *\ C\ *\ D\ E\ /\ +\ F\ -$

**Key Points to Include for Full Marks:**
- Left-to-right associativity for operators of equal precedence.
- Correct handling of nested parentheses.

---

### Q3 — Application (Conversion) | Bloom's: Apply | Difficulty: Medium | Marks: 2

**Question:**
Convert the following RPN expressions to standard Infix notation:

**(a)** $A\ B\ +\ C\ *\ D\ E\ -\ /$
**(b)** $A\ B\ C\ +\ D\ *\ +$

**Guide Answer:**

**(a)** $A\ B\ +\ C\ *\ D\ E\ -\ /$

Stack trace:
- Push A, Push B → $[A, B]$
- $+$: Pop B, A → $A + B$ → Push $(A + B)$
- Push C → $[(A + B), C]$
- $*$: Pop C, $(A + B)$ → $(A + B) * C$ → Push result
- Push D, Push E → $[(A + B) * C, D, E]$
- $-$: Pop E, D → $D - E$ → Push $(D - E)$
- $/$: Pop $(D - E)$, $(A + B) * C$ → $\frac{(A + B) * C}{D - E}$

**Infix:** $(A + B) * C / (D - E)$

**(b)** $A\ B\ C\ +\ D\ *\ +$

Stack trace:
- Push A, Push B, Push C
- $+$: Pop C, B → $B + C$
- Push D
- $*$: Pop D, $(B + C)$ → $(B + C) * D$
- $+$: Pop $(B + C) * D$, A → $A + (B + C) * D$

**Infix:** $A + (B + C) * D$

**Key Points to Include for Full Marks:**
- Correct operand popping order (second popped is left operand).
- Appropriate parentheses in infix result.

---

### Q4 — Application (Conversion) | Bloom's: Apply | Difficulty: Hard | Marks: 3

**Question:**
Convert the following RPN expressions to Infix:

**(a)** $A\ B\ C\ *\ +\ D\ E\ F\ +\ *\ -$
**(b)** $A\ B\ +\ C\ D\ -\ *\ E\ F\ +\ /$

**Guide Answer:**

**(a)** $A\ B\ C\ *\ +\ D\ E\ F\ +\ *\ -$

- Push A, B, C
- $*$: Pop C, B → $B * C$
- $+$: Pop $(B * C)$, A → $A + B * C$
- Push D, E, F
- $+$: Pop F, E → $E + F$
- $*$: Pop $(E + F)$, D → $D * (E + F)$
- $-$: Pop $D * (E + F)$, $(A + B * C)$ → $(A + B * C) - D * (E + F)$

**Infix:** $(A + B * C) - D * (E + F)$

**(b)** $A\ B\ +\ C\ D\ -\ *\ E\ F\ +\ /$

- Push A, B
- $+$: Pop B, A → $A + B$
- Push C, D
- $-$: Pop D, C → $C - D$
- $*$: Pop $(C - D)$, $(A + B)$ → $(A + B) * (C - D)$
- Push E, F
- $+$: Pop F, E → $E + F$
- $/$ : Pop $(E + F)$, $(A + B) * (C - D)$ → $\frac{(A + B) * (C - D)}{E + F}$

**Infix:** $(A + B) * (C - D) / (E + F)$

---

## Part 2: Stack Evaluation with Trace Tables [15 Marks]

### Q5 — Application (Stack Trace) | Bloom's: Apply | Difficulty: Medium | Marks: 5

**Question:**
Evaluate the RPN expression using a trace table. Show the Current Token, Action, and Stack State at every step.

**Expression:** $5\ 3\ +\ 4\ 2\ -\ *$

**Guide Answer:**

| Step | Token | Action | Stack (Bottom → Top) |
|:---:|:---:|:---|:---|
| 0 | — | Initialize | `[ ]` (empty) |
| 1 | `5` | Push operand | `[ 5 ]` |
| 2 | `3` | Push operand | `[ 5, 3 ]` |
| 3 | `+` | Pop 3, 5; Push $5 + 3 = 8$ | `[ 8 ]` |
| 4 | `4` | Push operand | `[ 8, 4 ]` |
| 5 | `2` | Push operand | `[ 8, 4, 2 ]` |
| 6 | `-` | Pop 2, 4; Push $4 - 2 = 2$ | `[ 8, 2 ]` |
| 7 | `*` | Pop 2, 8; Push $8 \times 2 = 16$ | `[ 16 ]` |

**Final Result:** $16$

**Verification (Infix):** $(5 + 3) * (4 - 2) = 8 * 2 = 16$ ✓

**Key Points to Include for Full Marks:**
- Complete trace table with every step.
- Correct pop order (first popped = right operand, second popped = left operand).
- Final result matches infix evaluation.

---

### Q6 — Application (Stack Trace) | Bloom's: Apply | Difficulty: Hard | Marks: 5

**Question:**
Evaluate the following RPN expression step by step with a full trace table:

**Expression:** $8\ 2\ /\ 3\ +\ 7\ 2\ *\ 1\ -\ *$

**Values:** Use the numeric values directly.

**Guide Answer:**

| Step | Token | Action | Stack (Bottom → Top) |
|:---:|:---:|:---|:---|
| 0 | — | Initialize | `[ ]` |
| 1 | `8` | Push operand | `[ 8 ]` |
| 2 | `2` | Push operand | `[ 8, 2 ]` |
| 3 | `/` | Pop 2, 8; Push $8 / 2 = 4$ | `[ 4 ]` |
| 4 | `3` | Push operand | `[ 4, 3 ]` |
| 5 | `+` | Pop 3, 4; Push $4 + 3 = 7$ | `[ 7 ]` |
| 6 | `7` | Push operand | `[ 7, 7 ]` |
| 7 | `2` | Push operand | `[ 7, 7, 2 ]` |
| 8 | `*` | Pop 2, 7; Push $7 \times 2 = 14$ | `[ 7, 14 ]` |
| 9 | `1` | Push operand | `[ 7, 14, 1 ]` |
| 10 | `-` | Pop 1, 14; Push $14 - 1 = 13$ | `[ 7, 13 ]` |
| 11 | `*` | Pop 13, 7; Push $7 \times 13 = 91$ | `[ 91 ]` |

**Final Result:** $91$

**Verification (Infix):** $(8 / 2 + 3) * (7 * 2 - 1) = (4 + 3) * (14 - 1) = 7 * 13 = 91$ ✓

**Key Points to Include for Full Marks:**
- All intermediate computations shown.
- Correct division (8/2 not 2/8) and subtraction (14-1 not 1-14).
- Stack state after every operation.

---

### Q7 — Application (Stack Trace) | Bloom's: Apply | Difficulty: Hard | Marks: 5

**Question:**
Given the expression:
$$Y = \frac{(A - B) \times C}{D + E \times F}$$

With values: $A = 10, B = 4, C = 3, D = 2, E = 5, F = 2$

**(a)** Convert the expression to RPN. (1 Mark)
**(b)** Evaluate the RPN expression with a complete trace table. (3 Marks)
**(c)** Verify the result by evaluating the original infix expression. (1 Mark)

**Guide Answer:**

**(a) RPN Conversion:**
- Numerator: $(A - B) * C$ → $A\ B\ -\ C\ *$
- Denominator: $D + E * F$ → $D\ E\ F\ *\ +$
- Division: $A\ B\ -\ C\ *\ D\ E\ F\ *\ +\ /$

**RPN:** $A\ B\ -\ C\ *\ D\ E\ F\ *\ +\ /$

Substituting values: $10\ 4\ -\ 3\ *\ 2\ 5\ 2\ *\ +\ /$

**(b) Trace Table:**

| Step | Token | Action | Stack (Bottom → Top) |
|:---:|:---:|:---|:---|
| 0 | — | Initialize | `[ ]` |
| 1 | `10` | Push operand | `[ 10 ]` |
| 2 | `4` | Push operand | `[ 10, 4 ]` |
| 3 | `-` | Pop 4, 10; Push $10 - 4 = 6$ | `[ 6 ]` |
| 4 | `3` | Push operand | `[ 6, 3 ]` |
| 5 | `*` | Pop 3, 6; Push $6 \times 3 = 18$ | `[ 18 ]` |
| 6 | `2` | Push operand | `[ 18, 2 ]` |
| 7 | `5` | Push operand | `[ 18, 2, 5 ]` |
| 8 | `2` | Push operand | `[ 18, 2, 5, 2 ]` |
| 9 | `*` | Pop 2, 5; Push $5 \times 2 = 10$ | `[ 18, 2, 10 ]` |
| 10 | `+` | Pop 10, 2; Push $2 + 10 = 12$ | `[ 18, 12 ]` |
| 11 | `/` | Pop 12, 18; Push $18 / 12 = 1.5$ | `[ 1.5 ]` |

**Final Result:** $1.5$

**(c) Verification (Infix):**
$$Y = \frac{(10 - 4) \times 3}{2 + 5 \times 2} = \frac{6 \times 3}{2 + 10} = \frac{18}{12} = 1.5$$

Result matches ✓

**Key Points to Include for Full Marks:**
- Correct RPN string.
- Complete trace table with all 11 steps.
- Verification against original expression.
- Correct pop order for non-commutative operators (- and /).

---

## Part 3: Zero-Address Instruction Sequences [5 Marks]

### Q8 — Application (Design) | Bloom's: Apply | Difficulty: Hard | Marks: 5

**Question:**
A stack-based computer uses zero-address instructions with the following operations:
- `PUSH X` — Push the value of variable X onto the stack.
- `ADD` — Pop two values, push their sum.
- `SUB` — Pop two values (top is subtracted from second-to-top), push result.
- `MUL` — Pop two values, push their product.
- `DIV` — Pop two values (top divides second-to-top), push result.
- `POP X` — Pop the top value and store it in variable X.

Write the zero-address instruction sequence for:
**(a)** $X = A * B + C * D$ (2 Marks)
**(b)** $Y = (A + B) / (C - D)$ (3 Marks)

**Guide Answer:**

**(a)** $X = A * B + C * D$

```
PUSH A
PUSH B
MUL          ; Stack: [A*B]
PUSH C
PUSH D
MUL          ; Stack: [A*B, C*D]
ADD          ; Stack: [A*B + C*D]
POP X        ; X = A*B + C*D
```

Total: **8 instructions**.

**(b)** $Y = (A + B) / (C - D)$

```
PUSH A
PUSH B
ADD          ; Stack: [A+B]
PUSH C
PUSH D
SUB          ; Stack: [A+B, C-D]
DIV          ; Stack: [(A+B)/(C-D)]
POP Y        ; Y = (A+B)/(C-D)
```

Total: **8 instructions**.

**Key Points to Include for Full Marks:**
- Correct ordering of PUSH operations before each operator.
- SUB and DIV: top of stack is the right operand (subtractor/divisor).
- Final POP to store the result.
- Show stack comments for clarity.

**Common Mistakes to Avoid:**
- Pushing operands in wrong order for SUB (PUSH C then PUSH D means SUB computes C - D, which is correct).
- Forgetting the final POP to store the result.
