# CCS2401 — Data Structures & Algorithms
## 09 - AVL Trees
**Dr. Ahmed Said**

---

## Binary Search Tree

- Review of 'insertion' and 'deletion' for BST
- Sequentially insert 3, 2, 1, 4, 5, 6 to a BST Tree
- If we continue to insert 7, 16, 15, 14, 13, 12, 11, 10, 8, 9 **?**

> 📌 Extracted from image: BST after inserting 3, 2, 1, 4, 5, 6:
> ```
>         3
>        / \
>       2   4
>      /     \
>     1       5
>              \
>               6
> ```

---

## What is the Complexity of the following BSTs?

> 📌 Extracted from image: Three BST examples shown:
>
> **Balanced BST (blue)** — O(log n):
> ```
>         10
>        /  \
>       8    12
>      / \  / \
>     7   9 11  13
> ```
>
> **Degenerate BST (grey, zigzag)** — O(n):
> ```
> 20 → 22 → 25 → 30 → 22 → 20
> (zigzag/degenerate shape)
> ```
>
> **Skewed BST (grey, right-skewed)** — O(n):
> ```
> 15
>   \
>    30
>   /
>  25
>  /
> 18
>  \
>   20
> ```
>
> - Balanced BST → **O(log n)**
> - Degenerate/Skewed BST → **O(n)** — Problem?

---

## Balance Binary Search Tree

- Worst case height of binary search tree: **N–1**
  - Insertion, deletion can be **O(N)** in the worst case
- We want a tree with small height
- Height of a binary tree with N node is at least **O(log N)**
- **Goal**: keep the height of a binary search tree **O(log N)**
- **Balanced Binary Search Trees** (Guaranteed a height of log(n) for n items.)
  - AVL Tree
  - Red-Black Tree

---

## AVL Trees

---

### AVL Trees

- **AVL** (Adelson-Velsky and Landis 1962) tree is a **self-balancing Binary Search Tree (BST)** where:
  - **The difference between heights of left and right subtrees cannot be more than one for all nodes.**
- The balance condition ensures that the depth of the tree is O(logN).
- **Condition**: for every node in the tree, the height of the left and right subtrees can differ by at most 1.

> 📌 Extracted from image: AVL tree example (valid):
> ```
>         12
>        /  \
>       8    18
>      /    /  \
>     5    11   17
>    /
>   4
> ```
> The above tree is AVL because the differences between the heights of left and right subtrees for every node are less than or equal to 1.

---

### AVL Trees — Valid vs Invalid Examples

> 📌 Extracted from image:
>
> **(1) Valid AVL Tree ✓**
> ```
>       5
>      / \
>     2   8
>    / \ /
>   1  4 7
>      |
>      3
> ```
>
> **(2) Invalid AVL Tree ✗**
> ```
>       7
>      / \
>     2   8
>    / \
>   1   4
>      / \
>     3   5
> ```
> (Node 7's left subtree has height 3, right subtree has height 1 → difference = 2 > 1. **Not AVL.**)

---

### The AVL Balance Condition

- Left and right subtrees of every node have heights differing by at most 1
- **Mathematical Definition:**
  - For every node x, $-1 \leq \text{balance}(x) \leq 1$ where

$$\text{balance}(\text{node}) = \text{height}(\text{node.left}) - \text{height}(\text{node.right})$$

---

### An AVL Tree?

To check if this tree is an AVL, we calculate the heights and balances for each node.

> 📌 Extracted from image: Tree with height (h) and balance (b) annotations per node:
> ```
>                  6        [h:4, b:2]
>                 / \
>         [h:3,b:2] 4    8  [h:1, b:0]
>                  / \ / \
>       [h:2,b:-2] 1  5  7   11  [all b:0]
>                   \
>              [h:-1] (null)
>                     3   [h:1, b:1]
>                      \
>                   0   2
> ```
> Node annotations:
> - Node 6: h:4, b:2
> - Node 4: h:3, b:2
> - Node 8: h:1, b:0
> - Node 1: h:2, b:-2
> - Node 5: b:0
> - Node 7: b:0
> - Node 11: b:0
> - Node 3: h:1, b:1
> - Node 2: b:0
>
> **This tree is NOT an AVL tree** — nodes 6 and 4 have |balance| = 2.

---

> 📌 Extracted from image (Animation slide): Numbers 1–20 shown as circular nodes in a row, representing nodes to be sequentially inserted into an AVL tree for a class demonstration.

---

## Operations on an AVL Tree

1. **Insertion**
2. **Deletion**
3. **Searching** [It is similar to performing a search in BST]

---

## Insertion in AVL

- Basically, follows insertion strategy of binary search tree
  - But **this may cause violation of AVL tree property**
- So, **Restore the destroyed balance condition** if needed

> 📌 Extracted from image: Three-step diagram:
>
> **Original AVL tree:**
> ```
>       5
>      / \
>     2   8
>    / \ /
>   1  4 7
>      |
>      3
> ```
>
> **Insert 6 → AVL Property violated:**
> ```
>       5
>      / \
>     2   8
>    / \ /
>   1  4 7
>      |  \
>      3   6  ← inserted
> ```
>
> **Restore AVL property:**
> ```
>       5
>      / \
>     2   7
>    / \ / \
>   1  4 6   8
>      |
>      3
> ```

---

## Insertion: Observations

- After an insertion, only nodes that are on the path **from the insertion point to the root** might have their balance altered
- Because only those nodes have their subtrees altered
- **Rebalance** the tree **at the deepest node** guarantees that the entire tree satisfies the AVL property

> 📌 Extracted from image: Two diagrams illustrating:
> - Left: path from inserted node 6 up to root 5 is highlighted green. Caption: "Node 5, 8, 7 might have balance altered"
> - Right: after rebalancing node 7 (the deepest violating node), tree is AVL again. Caption: "Rebalance node 7 guarantees the whole tree be AVL"

---

## Inserting Node: Rebalancing Cases

### 1. Left-Left (LL) Case
- Occurs when a new node is inserted into the left subtree of the left child of an imbalanced node.

> 📌 Extracted from image:
> ```
> 30
>  /
> 20
>  /
> 10  ← Inserted
> ```

### 2. Left-Right (LR) Case
- Occurs when a new node is inserted into the right subtree of the left child, creating a zigzag imbalance.

> 📌 Extracted from image:
> ```
> 30
>  /
> 10
>  \
>  20  ← Inserted
> ```

### 3. Right-Right (RR) Case
- Occurs when a new node is inserted into the right subtree of the right child of an imbalanced node.

> 📌 Extracted from image:
> ```
> 10
>  \
>  20
>   \
>   30  ← Inserted
> ```

### 4. Right-Left (RL) Case
- Occurs when a new node is inserted into the left subtree of the right child, causing a zigzag imbalance.

> 📌 Extracted from image:
> ```
> 10
>  \
>  30
>  /
> 20  ← Inserted
> ```

> *Cases 1 & 3 and Cases 2 & 4 are mirror image symmetries with respect to the inserted node's parent.*

---

## Rotations

- **Rebalance** of AVL tree are done with simple modification to tree, known as **Rotation**
- Insertion occurs on the **"outside"** (i.e., **Left-Left** or **Right-Right**) is fixed by **single rotation** of the tree
- Insertion occurs on the **"inside"** (i.e., **Left-Right** or **Right-Left**) is fixed by **double rotation** of the tree

---

## Rotating the Subtrees in an AVL Tree

An AVL tree may rotate in one of the following two ways to keep itself balanced:

1. Left Rotation
2. Right Rotation

---

### AVL — Left Rotation

When a node is added into the **R**ight subtree of the **R**ight subtree **"Outside"**, if the tree gets out of balance, we do a **single left rotation**.

> 📌 Extracted from image: Three-step left rotation diagram:
>
> **Before (RR imbalance, balance factors shown):**
> ```
> 1  [-2]
>  \
>   2  [-1]
>    \
>     3  [0]
> ```
>
> **Rotation in progress** (dotted arrows showing node 1 rotating left):
> ```
>   1 [-2] ←
>    \
>     2 [-1] ←
>      \
>       3 [0]
> ```
>
> **After (balanced):**
> ```
>     2  [0]
>    / \
>  1[0]  3[0]
> ```

---

### Right Rotation

If a node is added to the **L**eft subtree of the **L**eft subtree **"Outside"**, the AVL tree may get out of balance; we do a **single right rotation**.

> 📌 Extracted from image: Three-step right rotation diagram:
>
> **Before (LL imbalance):**
> ```
>     3  [+2]
>    /
>   2  [+1]
>  /
> 1  [0]
> ```
>
> **Rotation in progress** (dotted arrows showing node 3 rotating right):
>
> **After (balanced):**
> ```
>     2  [0]
>    / \
>  1[0]  3[0]
> ```

---

### Left-Right (LR) Rotation

A **Left-Right rotation** is a combination in which first **Left** rotation takes place, after that **Right** rotation executes.

- **Grandchild becomes the new subtree root**

> 📌 Extracted from image: Four-step LR rotation diagram:
>
> **Initial state (LR imbalance):**
> ```
>   3  [+2]   ← Grandparent
>  /
> 1  [-1]     ← Parent
>  \
>   2  [0]    ← Grandchild
> ```
>
> **Step 1 — Left rotate at Parent (1):**
> ```
>   3  [+2]
>  /
> 1 ←
>  \
>   2 [0]
> ```
> → After LL Rotation:
> ```
>   3  [+2]
>  /
> 2  [+1]
>  /
> 1  [0]
> ```
>
> **Step 2 — Right rotate at Grandparent (3):**
>
> → After RR Rotation (final balanced tree):
> ```
>     2  [0]
>    / \
>  1[0]  3[0]
> ```

---

### Right-Left (RL) Rotation

A **Right-Left rotation** is a combination in which first **Right** rotation takes place, after that **Left** rotation executes.

> 📌 Extracted from image: Four-step RL rotation diagram:
>
> **Initial state (RL imbalance):**
> ```
> 1  [-2]
>  \
>   3  [+1]
>  /
> 2  [0]
> ```
>
> **Step 1 — Right rotate at 3:**
> → After RR Rotation:
> ```
> 1  [-2]
>  \
>   2  [-1]
>    \
>     3  [0]
> ```
>
> **Step 2 — Left rotate at 1:**
> → After LL Rotation (final balanced tree):
> ```
>     2  [0]
>    / \
>  1[0]  3[0]
> ```

---

## Insertion Algorithm

1. First, insert the new key as a new leaf just as in ordinary **B**inary **S**earch **T**ree
2. Then trace the path from the new leaf towards the root.
   - For each node x encountered, **check if heights of left(x) and right(x) differ by at most 1**
3. If **yes**, proceed to parent(x)
4. If **not**, restructure by doing either a single rotation or a double rotation

**Note**: once we perform a rotation at a node x, we won't need to perform any rotation at any ancestor of x.

---

## PART II — Walk-through: 16 inserts, 9 rotations.

We will insert these keys one by one and watch the tree rebalance itself after each one.

**Insertion sequence:** 3, 2, 1, 4, 5, 6, 7, 16, 15, 14, 13, 12, 11, 10, 8, 9

---

### Step 1 / 16 — Insert 3 • STILL BALANCED

First node becomes the root.

> 📌 Extracted from image:
> ```
> 3  [BF: 0]
> ```

---

### Step 2 / 16 — Insert 2 • STILL BALANCED

2 < 3. Travel left, attach as left child.

> 📌 Extracted from image:
> ```
>   3  [+1]
>  /
> 2  [0]
> ```

---

### Step 3 / 16 — Insert 1 • IMBALANCE · LL

**BEFORE:** BF(3) hit +2
**AFTER:** Rebalanced · root = 2

Inserted 1 on the left-left path of 3. Balance factor of 3 hit +2. One **right rotation** around 3 restores balance.

> 📌 Extracted from image:
>
> Before:
> ```
>     3  [+2]
>    /
>   2  [+1]
>  /
> 1  [0]
> ```
> → LL: **Right rotate** at 3 →
>
> After:
> ```
>     2  [0]
>    / \
>  1[0]  3[0]
> ```

---

### Step 4 / 16 — Insert 4 • STILL BALANCED

4 > 3. Travel right, attach as right child.

> 📌 Extracted from image:
> ```
>     2  [-1]
>    / \
>  1[0]  3[-1]
>           \
>            4[0]
> ```

---

### Step 5 / 16 — Insert 5 • IMBALANCE · RR

**BEFORE:** BF(3) hit −2
**AFTER:** Rebalanced · root = 2

Inserted 5 on the right-right path of 3. Balance factor of 3 hit −2. One **left rotation** around 3 restores balance.

> 📌 Extracted from image:
>
> Before:
> ```
>     2  [-2]
>    / \
>  1[0]  3[-2]
>           \
>            4[-1]
>              \
>               5[0]
> ```
> → RR: **Left rotate** at 3 →
>
> After:
> ```
>       2  [-1]
>      / \
>    1[0]  4[0]
>          / \
>        3[0]  5[0]
> ```

---

### Step 6 / 16 — Insert 6 • IMBALANCE · RR

**BEFORE:** BF(2) hit −2
**AFTER:** Rebalanced · root = 4

Inserted 6 on the right-right path of 2. Balance factor of 2 hit −2. One **left rotation** around 2 restores balance.

> 📌 Extracted from image:
>
> Before:
> ```
>       2  [-2]
>      / \
>    1[0]  4[-1]
>          / \
>        3[0]  5[-1]
>                \
>                 6[0]
> ```
> → RR: **Left rotate** at 2 →
>
> After:
> ```
>         4  [0]
>        / \
>       2   5[-1]
>      / \     \
>    1[0] 3[0]  6[0]
> ```

---

### Step 7 / 16 — Insert 7 • IMBALANCE · RR

**BEFORE:** BF(5) hit −2
**AFTER:** Rebalanced · root = 4

Inserted 7 on the right-right path of 5. Balance factor of 5 hit −2. One **left rotation** around 5 restores balance.

> 📌 Extracted from image:
>
> Before:
> ```
>         4  [-1]
>        / \
>       2   5[-2]
>      / \     \
>    1[0] 3[0]  6[-1]
>                 \
>                  7[0]
> ```
> → RR: **Left rotate** at 5 →
>
> After:
> ```
>         4  [0]
>        / \
>       2   6[0]
>      / \ / \
>    1  3 5   7
> ```

---

### Step 8 / 16 — Insert 16 • STILL BALANCED

16 > 7. Travel right, attach as right child.

> 📌 Extracted from image:
> ```
>           4  [-1]
>          / \
>         2   6[-1]
>        / \ / \
>       1  3 5  7[-1]
>                 \
>                  16[0]
> ```

---

### Step 9 / 16 — Insert 15 • IMBALANCE · RL

**BEFORE:** BF(7) hit −2
**AFTER:** Rebalanced · root = 4

Inserted 15 on the right-left path of 7. The zig-zag shape needs a double rotation: right-rotate 7's right child, then left-rotate 7.

> 📌 Extracted from image (3 sub-steps shown):
>
> Before:
> ```
>           4  [-1]
>          / \
>         2   6[-2]
>        / \ / \
>       1  3 5  7[-2]
>                 \
>                  16[+1]
>                 /
>                15[0]
> ```
>
> Step 1 — Right rotate at 16 (7's right child):
> ```
>   7  [-2]
>     \
>      15[-1]
>        \
>         16[0]
> ```
>
> Step 2 — Left rotate at 7:
>
> After (RL double rotation complete):
> ```
>           4  [-1]
>          / \
>         2   6[-1]
>        / \ / \
>       1  3 5  15[0]
>              / \
>             7   16
> ```

---

### Step 10 / 16 — Insert 14 • IMBALANCE · RL

**BEFORE:** BF(6) hit −2
**AFTER:** Rebalanced · root = 4

Inserted 14 on the right-left path of 6. The zig-zag shape needs a double rotation: right-rotate 6's right child, then left-rotate 6.

> 📌 Extracted from image (3 sub-steps):
>
> Before:
> ```
>         4  [-2]
>        / \
>       2   6[-2]
>      / \ / \
>     1  3 5  15[+1]
>            /  \
>           7[-1] 16[0]
>            \
>             14[0]
> ```
>
> After (final balanced result):
> ```
>         4  [-1]
>        / \
>       2   7[0]
>      / \ / \
>     1  3 6  15[+1]
>         / \  / \
>        5  (5 moved) 14  16
> ```
> *(See image for exact final structure with BFs.)*

---

### Step 11 / 16 — Insert 13 • IMBALANCE · RR

**BEFORE:** BF(4) hit −2
**AFTER:** Rebalanced · root = 7

Inserted 13 on the right-right path of 4. Balance factor of 4 hit −2. One **left rotation** around 4 restores balance.

> 📌 Extracted from image:
>
> After:
> ```
>             7  [0]
>            / \
>           4   15[+1]
>          / \ / \
>         2  6 14  16
>        / \/ \
>       1  3 5  13
> ```

---

### Step 12 / 16 — Insert 12 • IMBALANCE · LL

**BEFORE:** BF(14) hit +2
**AFTER:** Rebalanced · root = 7

Inserted 12 on the left-left path of 14. Balance factor of 14 hit +2. One **right rotation** around 14 restores balance.

> 📌 Extracted from image:
>
> After:
> ```
>             7  [0]
>            / \
>           4   15[+1]
>          / \ / \
>         2  6 13  16
>        / \/ \  \
>       1  3 5  12  14
> ```

---

### Step 13 / 16 — Insert 11 • IMBALANCE · LL

**BEFORE:** BF(15) hit +2
**AFTER:** Rebalanced · root = 7

Inserted 11 on the left-left path of 15. Balance factor of 15 hit +2. One **right rotation** around 15 restores balance.

> 📌 Extracted from image:
>
> After:
> ```
>               7  [0]
>              / \
>             4   13[0]
>            / \ / \
>           2  6 12  15
>          / \/ \ / \ / \
>         1  3 5 11 12 14 16
> ```

---

### Step 14 / 16 — Insert 10 • IMBALANCE · LL

**BEFORE:** BF(12) hit +2
**AFTER:** Rebalanced · root = 7

Inserted 10 on the left-left path of 12. Balance factor of 12 hit +2. One **right rotation** around 12 restores balance.

> 📌 Extracted from image:
>
> After:
> ```
>               7  [0]
>              / \
>             4   13[0]
>            / \ / \
>           2  6 11  15
>          / \/ \ / \ / \
>         1  3 5 10 12 14 16
> ```

---

### Step 15 / 16 — Insert 8 • STILL BALANCED

8 > 10. Travel right, attach as right child. *(Note: 8 < 10, travel left — see image.)*

> 📌 Extracted from image: Tree after inserting 8 (balance factors shown, still balanced):
> ```
>               7  [-1]
>              / \
>             4   13[+1]
>            / \ / \
>           2  6 11[+1] 15[0]
>          / \/ \ / \ / \
>         1  3 5 10[+1] 12 14 16
>                 /
>                8[0]
> ```

---

### Step 16 / 16 — Insert 9 • IMBALANCE · LR

**BEFORE:** BF(10) hit +2
**AFTER:** Rebalanced · root = 7

Inserted 9 on the left-right path of 10. The zig-zag shape needs a double rotation: left-rotate 10's left child, then right-rotate 10.

> 📌 Extracted from image:
>
> Before:
> ```
>   10  [+2]
>  /
> 8  [-1]
>  \
>   9  [0]
> ```
> → LR: **Left then Right** at 10 →
>
> After (final tree):
> ```
>               7  [-1]
>              / \
>             4   13[+1]
>            / \ / \
>           2  6 11  15[0]
>          / \/ \ / \ / \
>         1  3 5 9  12 14 16
>               / \
>              8   10
> ```

---

## Final Tree

### Height = 5.

A plain BST on this sequence would reach depth 9 in places. The AVL tree keeps every root-to-leaf path within $\log_2(16+1) \approx \mathbf{4.09}$.

> 📌 Extracted from image: Final AVL tree after all 16 insertions:
> ```
>                     7  [-1]
>                    / \
>                   4   13[+1]
>                  / \ / \
>                 2  6 11[+1] 15[0]
>                / \/ \ / \  / \
>               1  3 5 9 12 14 16
>                     / \
>                    8   10
> ```
> All balance factors are within {-1, 0, +1}. **Height = 5.**

---

## Single Rotation Fails to fix LR & RL Cases

### Left Right (LR) Case

**Facts:**
- The new key is inserted in the subtree B or C
- The AVL-property is violated at k₃
- k₃–k₁–k₂ forms a zig-zag shape

> 📌 Extracted from image: General LR case diagram:
>
> Before:
> ```
>       k3
>      /  \
>     k1   D
>    /  \
>   A    k2
>       / \
>      B   C
> ```
>
> After (double rotation):
> ```
>        k2
>       /  \
>      k1   k3
>     / \ / \
>    A  B C  D
> ```

**Solution:**
- We cannot leave **k3** as the root
- The only alternative is to place **k2** as the new root

---

### Right Left (RL) Case — symmetric to LR case

**Facts:**
- The new key is inserted in the subtree B or C
- The AVL-property is violated at k₁
- k₁–k₃–k₂ forms a zig-zag shape

> 📌 Extracted from image: General RL case diagram:
>
> Before:
> ```
>     k1
>    /  \
>   A    k3
>       /  \
>      k2   D
>     / \
>    B   C
> ```
>
> After (double rotation):
> ```
>        k2
>       /  \
>      k1   k3
>     / \ / \
>    A  B C  D
> ```

**Solution:**
- We cannot leave **k1** as the root
- The only alternative is to place **k2** as the new root

---

## Applications of AVL Tree

- **AVL Trees** can self-balance themselves and therefore provides time complexity as **O(Log n)** for search, insert and delete.
- **AVL** Tree is used as a first example self balancing BST in DSA as it is **easier to understand and implement compared to Red Black Tree**.
- Applications where insertions and deletions are **less common** but **frequent data lookups** along with other operations of BST like sorted traversal, floor, ceil, min and max.
- **Red Black tree** is more commonly implemented in language libraries like `map` in C++, `set` in C++, `TreeMap` in Java and `TreeSet` in Java.
- **AVL Trees** can be used in a real time environment where predictable and consistent performance is required.

*End of Lecture 09 — AVL Trees*