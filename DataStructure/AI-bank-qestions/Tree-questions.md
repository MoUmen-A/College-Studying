# Trees (General) - Exam Questions
**Generated from:** `07-Trees.md`
**Calibrated against:** `23-spring.txt` · `25-spring`
**Course:** CCS2401 — Data Structures & Algorithms | Dr. Ahmed Said

---

## Section 1 — Topic Summary

### Trees
- **Non-linear** data structure. Hierarchical. No cycles.
- Key terminology: root, leaf, edge, parent, child, sibling, inner node, path, ancestors, descendants, subtree.
- **Level** of node = number of vertices from root to node (root = level 0).
- **Depth** = number of edges from root to node (= level).
- **Height** = number of edges from node to its deepest leaf.
- Maximum nodes in binary tree of height h: **2^(h+1) − 1**.
- **Types of binary trees**: Full (0 or 2 children), Complete (all levels filled except last, left-aligned), Perfect (all internal nodes have 2 children, all leaves at same level), Balanced (left and right subtree heights differ by ≤ 1), Degenerate/Skewed (like a linked list).
- **Traversals**:
  - **In-order**: Left → Root → Right → sorted output for BST.
  - **Pre-order**: Root → Left → Right → useful for copying/displaying tree.
  - **Post-order**: Left → Right → Root → useful for deleting tree.
- **Expression Trees**: leaves = operands, internal nodes = operators. Pre-order → prefix, Post-order → postfix, In-order → infix.
- **Tree construction from traversals**: Preorder[0] = root. Find root in Inorder → split into left and right subtrees. Recurse.

---

## Section 2 — Tone Analysis

From **`23-spring.txt`** and **`25-spring`**, the exam style for these topics is:
- **MCQ (Q1 in 25-spring)**: Tree construction from two traversals appears frequently.
- **Code completion (Q1.3 in 25-spring)**: A function with a missing line/lines — identify and fill.
- Questions are grouped by data structure; expect multi-part questions combining linked list + tree or queue + stack.

---

## Section 3 — Question Bank

---

### 1. Multiple Choice (MCQ)

---

#### Q4 — MCQ | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
Which of the following correctly describes a **Perfect Binary Tree**?

- A) Every node has 0 or 2 children.
- B) All levels are completely filled and all leaves are at the same depth.
- C) All levels are filled except the last, and last-level nodes are left-aligned.
- D) The height difference between left and right subtrees is at most 1.

**Guide answer:**
**B** — A **Perfect Binary Tree** has all internal nodes with exactly 2 children and all leaves at the same depth/level. Option A describes a **Full** Binary Tree. Option C describes a **Complete** Binary Tree. Option D describes a **Balanced** Binary Tree.

**Key points to include for Full Marks:**
- Know all five binary tree types and their exact definitions.

**Common mistakes to avoid:**
Confusing Perfect (B) with Full (A) — the most common trap. Memorize: Perfect = symmetric, all leaves same level.

---

#### Q5 — MCQ | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
What is the maximum number of nodes in a **binary tree of height h = 3**?

- A) 7
- B) 8
- C) 15
- D) 16

**Guide answer:**
**C** — Formula: max nodes = **2^(h+1) − 1** = 2^(3+1) − 1 = 2^4 − 1 = **15**.

**Key points to include for Full Marks:**
- State the formula explicitly: 2^(h+1) − 1.
- This is the node count of a **Perfect Binary Tree** of height h.

**Common mistakes to avoid:**
Using 2^h = 8 (that's the number of nodes at level h only, not the total).

---

#### Q6 — MCQ | Bloom's: Analyse | Difficulty: Medium | Marks: 2

**Question:**
Consider the following binary tree:
```
        4
       / \
      2   6
     / \ / \
    1  3 5  7
```
What is the **Post-order** traversal result?

- A) 1, 2, 3, 4, 5, 6, 7
- B) 4, 2, 1, 3, 6, 5, 7
- C) 1, 3, 2, 5, 7, 6, 4
- D) 4, 6, 7, 5, 2, 3, 1

**Guide answer:**
**C** — Post-order: Left → Right → Root.
- Left subtree of 4: post-order → 1, 3, 2
- Right subtree of 4: post-order → 5, 7, 6
- Root: 4
- **Result: 1, 3, 2, 5, 7, 6, 4**

A is In-order. B is Pre-order.

**Key points to include for Full Marks:**
- Apply recursively: process each subtree fully before the root.
- Post-order always ends with the root.

---

### 2. Fill-in-the-blank

---

#### Q10 — Fill-in-the-blank | Bloom's: Understand | Difficulty: Easy | Marks: 2

**Question:**
The three standard tree traversal methods are:
1. ________ traversal: visits Left subtree → Root → Right subtree. Result for BST: **sorted ascending**.
2. ________ traversal: visits Root → Left subtree → Right subtree. Useful for **copying** a tree.
3. ________ traversal: visits Left subtree → Right subtree → Root. Useful for **deleting** a tree.

**Guide answer:** **In-order** ; **Pre-order** ; **Post-order**

---

#### Q11 — Fill-in-the-blank | Bloom's: Understand | Difficulty: Medium | Marks: 3

**Question:**
For the binary tree:
```
        4
       / \
      2   6
     / \ / \
    1  3 5  7
```
- In-order result: ________
- Pre-order result: ________
- Post-order result: ________

**Guide answer:**
- In-order: **1, 2, 3, 4, 5, 6, 7**
- Pre-order: **4, 2, 1, 3, 6, 5, 7**
- Post-order: **1, 3, 2, 5, 7, 6, 4**

---

#### Q12 — Fill-in-the-blank | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
A ________ Binary Tree has all levels completely filled with nodes except the last level, where all nodes are as **left-aligned** as possible.
A ________ Binary Tree has every node with exactly 0 or 2 children.

**Guide answer:** **Complete** ; **Full**

---

### 3. Short Answer

---

#### Q14 — Short Answer | Bloom's: Understand | Difficulty: Easy | Marks: 3

**Question:**
Define the following tree terms and give an example from the tree below:
```
        A
       / \
      B   C
     / \   \
    D   E   F
```
(a) **Leaf node**  (b) **Height of node A**  (c) **Level of node E**

**Guide answer:**
**(a) Leaf node**: A node with **no children**. Examples: D, E, F.

**(b) Height of node A**: The number of edges from A to its deepest leaf. Deepest leaves are D, E, F at depth 2. **Height of A = 2**.

**(c) Level of node E**: The number of vertices in the path from root to E = A→B→E → **Level = 2**.

*(Note: Level is also equal to the depth of the node — number of edges from root to that node.)*

**Key points to include for Full Marks:**
- Level of root = 0 (this is fixed by the lecture definition).
- Height = edges to deepest leaf, not number of levels.
- Leaf = no children (both left and right are null).

**Common mistakes to avoid:**
Saying height = number of levels (off by 1 — height = levels − 1).

---

#### Q16 — Short Answer | Bloom's: Analyse | Difficulty: Medium | Marks: 4

**Question:**
Given **Preorder: CFHGBEADJI** and **Inorder: HFBGCAJDIE**, construct the binary tree. Draw the final tree.

*(This is exactly from the 25-spring exam — Q1.2)*

**Guide answer:**

**Step 1**: Preorder[0] = **C** → C is the root.

**Step 2**: Find C in Inorder: `HFBGC | AJDIE`
- Left subtree Inorder: `HFBG` (4 nodes)
- Right subtree Inorder: `AJDIE` (5 nodes)

**Step 3**: Left subtree Preorder (next 4 from Preorder after C): `FHGB`
- Preorder[0] = **F** → F is root of left subtree.
- Find F in `HFBG`: `H | BG` → Left of F = `H`, Right of F = `BG`
- Left of F: Preorder `H` → root = **H** (leaf)
- Right of F: Preorder `GB` → root = **G**; Inorder `BG`: Left of G = `B`, Right = empty
  - G's left = **B** (leaf)

**Step 4**: Right subtree Preorder (next 5): `EADJI`
- Preorder[0] = **E** → E is root of right subtree.
- Find E in `AJDIE`: `AJDI | E` → Left = `AJDI`, Right = empty
- Left of E: Preorder `ADJI` → root = **A**
  - Find A in `AJDI`: empty | `JDI` → Left of A = empty, Right = `JDI`
  - Right of A: Preorder `DJI` → root = **D**
    - Find D in `JDI`: `J | I` → Left = J (leaf), Right = I (leaf)

**Final Tree:**
```
              C
            /   \
           F     E
          / \   /
         H   G A
            /   \
           B     D
                / \
               J   I
```

**Key points to include for Full Marks:**
- Always take Preorder[0] as the root at each step.
- Split Inorder at the root → left/right subtrees.
- Count nodes in each subtree to correctly slice the Preorder array.
- Draw the final tree clearly.

---

### 4. True / False + Justify

---

#### Q19 — True/False | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
*"A Complete Binary Tree with n internal nodes has (n + 1) leaf nodes."*
True or False? Justify with a small example.

*(From 25-spring Q1.d)*

**Guide answer:**
**FALSE.**

In a **Complete Binary Tree**, the formula `leaves = internal nodes + 1` does NOT always hold. This formula applies to **Full Binary Trees** (where every node has 0 or 2 children), not to Complete Binary Trees. In a Complete Binary Tree, the last level may be partially filled from left to right, which can break the formula.

Example with 3 internal nodes (A, B, C) → 4 leaf nodes:
```
        A           Internal: A, B, C (n=3)
       / \          Leaves: D, E, F, G (n+1=4)
      B   C
     / \ / \
    D  E F  G
```

**Key points to include for Full Marks:**
- State TRUE and the formula: leaves = n + 1.
- Provide a concrete example.

---

### 6. Compare & Contrast

---

#### Q28 — Compare & Contrast | Bloom's: Evaluate | Difficulty: Hard | Marks: 5

**Question:**
Compare **Full**, **Complete**, **Perfect**, and **Balanced** Binary Trees. For each, state the defining property and give a 3-level example or counter-example.

**Guide answer:**

| Type | Defining Property | 3-Level Example |
|------|-----------------|----------------|
| **Full** | Every node has **0 or 2** children (never 1) | Root has 2 children; left child has 2 children; right child is a leaf ✓ |
| **Complete** | All levels full except last; last level **left-aligned** | Level 0: 1 node; Level 1: 2 nodes; Level 2: 3 nodes (leftmost 3 of 4 positions filled) ✓ |
| **Perfect** | All internal nodes have **exactly 2** children; all leaves at the **same depth** | Height-2 tree with 7 nodes: 1 root, 2 children, 4 grandchildren ✓ |
| **Balanced** | For every node, \|height(left) − height(right)\| ≤ **1** | AVL tree maintains this property automatically |

**Key relationships:**
- Every **Perfect** tree is also **Complete** and **Full** and **Balanced**.
- Every **Full** tree is NOT necessarily Complete or Perfect.
- A **Degenerate** tree is the worst case — like a linked list; height = n−1.

**Key points to include for Full Marks:**
- All four definitions correct and distinct.
- At least one example/counter-example.
- Mention that Perfect ⊂ Complete ⊂ "possible full" hierarchy.

---

## Section 4 — Study Tips & Weak Areas

| Weak Area | Why Students Lose Marks | Fix |
|-----------|------------------------|-----|
| **Binary tree types** | Confusing Full / Complete / Perfect | Mnemonic: Full = 0 or 2 children; Complete = left-packed; Perfect = symmetric all-same-level leaves. |
| **Tree construction from traversals** | Not recursively splitting Inorder after each root identification | Pre-order[0] = root. Find root in Inorder. Count left-subtree nodes. Slice Pre-order accordingly. |
| **Post-order traversal** | Putting root in the middle instead of at the end | Post = Left, Right, **Root**. Root is ALWAYS last. |

---

## Section 5 — Coverage Gap Analysis

### Concepts in lectures not yet covered in this question bank:

| Concept | From Lecture | Suggested Question |
|---------|-------------|-------------------|
| **Expression Tree** traversal (postfix/prefix derivation) | `07-Trees.md` | "Given the expression `A * B / (C + D * E)`, build the expression tree and derive its prefix (pre-order) and postfix (post-order) representations." |
| **Level, Depth, Height** calculation worksheet | `07-Trees.md` | "For each node in the given tree, calculate its level, depth, and height." |
| **Degenerate/Skewed tree** worst case | `07-Trees.md` | "Inserting 1, 2, 3, 4, 5 in order into a BST produces a skewed tree. Draw it and state why this is the worst case for search." |

### 🔔 Reminder — Lecture files still missing:
The following lectures are NOT yet in `d:\Gam3a\Exam-Creation\DataStructure\Lec\`:
- **Lectures 01, 02, 03** — likely Arrays, Stacks, Singly Linked List basics.
- **Lectures 05** — likely Circular Linked List or Stack applications.
- **Lectures 09, 10** — likely **AVL Trees** and Heap/Priority Queue.

> **AVL Trees appear in BOTH previous exams** (23-spring Q4 and 25-spring Q3 — full 10-mark questions). Upload the AVL lecture immediately and re-run to generate AVL rotation questions (LL, RR, LR, RL insertions/deletions with full step-by-step drawings).
