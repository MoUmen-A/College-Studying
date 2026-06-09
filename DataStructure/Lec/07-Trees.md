# CCS2401 — Data Structures & Algorithms
## 07 - Trees
**Dr. Ahmed Said**

---

## Linear vs. Non-linear Data Structures

**Linear**
- Stacks
- Queues
- Lists
- …

**Non-Linear**
- Trees
- Graphs

---

## Trees

- Trees are a **natural data structure** for representing specific data.
  - Family trees
  - Organizational chart of a corporation, showing who supervises who
  - Folder (directory) structure on a hard drive

- A tree is a **nonlinear**, two-dimensional data structure.
  - Tree nodes contain **two** or more links.
  - A tree provides a way of storing hierarchical data.
  - A **node** or a **vertex** is a container of data.
  - The top node of the tree is identified as the **root** node.

> 📌 Extracted from image: Diagram showing a DFS Namespace folder tree with root "DFS Namespace" branching into: Profiles, Home, Local, Global — each with further sub-folders (User 1, User 2, User 3 / Sales, IT, Marketing, Management / HR, IT).

---

## Terminologies

- An **edge** is a link from a **parent** node to a **child** (successor) node:
  - D is the parent of I & J.
  - F, G & H are children of C.

- A **leaf** node has no children:
  - K, L & M are leaf nodes.

- **Siblings** of a tree are nodes that share the same parent node.
  - They are also called "brother" or "sister" nodes.

- **Inner Node** — any node of a tree that has child nodes.

> 📌 Extracted from image: Tree diagram with nodes A (root), B, C, D, E (children of B), F, G, H (children of C), I, J (children of D), K, L (children of E), M (child of H). Labels shown: Root = A, Edge (A→B), Parent = D, Child = I & J, Siblings = F, G, H (same parent C), Leaf Nodes = K, L, M, I, J.  
> *Note: "In any tree, there must be **only one** root node."*

---

## Terminologies (Cont.)

- **Path** refers to the sequence of nodes along the edges of a tree.
  - v₀, v₁, … , vₙ, where there is an edge from one node to the next.
  - Path from A to M is: A, C, H, M.
  - Trees can **never** have cycles (loops).

> 📌 Extracted from image: Same tree diagram with the path A → C → H → M highlighted in red.

---

## Terminologies (Cont.)

- The **descendants** of a node V are:
  - Children, grand children, grand grand children, … etc. of V.
  - All nodes reached by a path from node V to the leaf nodes.
  - The descendants of C are F, G, H & M.

- The **ancestors** of a node V are:
  - Parent, grand parent, … etc. of V.
  - All nodes found on the path from root node to node V.
  - Ancestors of L are E, B, and A.

- A **subtree** is a section of a tree structure that consists of a node and all its descendants.

> 📌 Extracted from image: Tree diagram highlighting the subtree rooted at C (containing C, F, G, H, M) with a bounding box labeled "Subtree".

---

## Terminology (Practice Example)

> 📌 Extracted from image: Tree with root 0; children of 0 are 1 and 2; children of 1 are 3; children of 3 are 4 and 8; children of 2 are 5, 6, 7.

- **Root:** 0 (has no parent)
- **Path from 0 to 6:** 0 – 2 – 6
- **Ascendants vs descendants:**
  - Ascendants of 3: 1, 0
  - Descendants of 1: 5, 3, 4, 8
- **Leaves:** 5, 4, 6, 7, 8 (have no children)
- **Subtrees**
- **Inner Nodes:** 1, 2 & 3

---

## Terminologies (Cont.) — Level, Depth, Height

- The **level** of a node V is the number of vertices in the path from root to V:
  - Root node A is at level 0.
  - Leaf nodes I, J & K are at level 3.
  - Leaf nodes D, F, H are at level 2.

- The **depth** of a node is the number of edges from the root to the node.

- The **height** of a node is the number of edges from the node to the **deepest** leaf.
  - The maximum level of the tree: 3
  - An empty tree has height 0.

> 📌 Extracted from image: Tree with levels labeled:
> - Level 0: A
> - Level 1: B, C
> - Level 2: D, E, F, G, H
> - Level 3: I, J, K

---

## Terminology — Worksheet

- The level of the root is defined to be 0.
- The level of each node is defined to be 1 + the level of its parent.
- The depth of a node is the number of edges from the root to the node. *(Equal to the level of that node.)*
- The height of a node is the number of edges from the node to the deepest leaf. *(Treat that node as the root of a small tree.)*

**Practice:** Give the level, depth and height for each of the red nodes. How many nodes are on each level?

| Node | Level | Depth | Height |
|------|-------|-------|--------|
| A    | 0     | 0     | 3      |
| B    | 2     | 2     | 1      |
| C    | 3     | 3     | 0      |

**Nodes per level:** 1, 2, 4, 8

---

## Types of Trees

```
Tree
├── Binary Tree
├── Ternary
└── N-ary Tree
```

> 📌 Extracted from image: Three tree diagrams side by side — Binary Tree (max 2 children per node), Ternary Tree (max 3 children), N-ary Tree (variable/many children).

---

## Binary Trees

### Binary Tree

- A **binary tree** is a tree in which **no node can have more than two children**.
- The most common tree type is a binary tree.
- Every node has at most 2 children, called the **left child** and **right child**.
- A binary tree can be defined **recursively** as:
  - Root node
  - Left subtree: left child and all its descendants
  - Right subtree: right child and all its descendants

> 📌 Extracted from image: Binary tree with root A; left subtree rooted at B (with children D and E; D has children H and I; E has children J and K); right subtree rooted at C (with children F and G; F has child L).

---

### Types of Binary Trees

- **Full** (binary)
- **Complete**
- **Degenerate** or Skewed
- **Perfect**
- **Balanced**

> 📌 Extracted from image: Five tree diagrams labeled Full, Complete, Degenerate, Perfect, Balanced respectively.

---

### Types: Full Binary Tree

- **Full Binary Tree** is a Binary Tree in which every node has **0 or 2 children**.

> 📌 Extracted from image: Left side (green) — valid Full Binary Trees where every node has 0 or 2 children. Right side (red) — invalid examples where some nodes have exactly 1 child.

---

### Types: Complete Binary Tree

- **Complete Binary Tree**: has all levels completely filled with nodes **except the last level**, and in the last level, **all the nodes are as left side as possible**.

> 📌 Extracted from image: Left side (green) — valid Complete Binary Trees. Right side (red) — invalid examples (last-level nodes not left-aligned or upper levels not fully filled).

---

### Types: Perfect Binary Tree

- **Perfect Binary Tree** is a Binary Tree in which **all internal nodes have 2 children**, and **all the leaf nodes are at the same depth or same level**.

> 📌 Extracted from image: Left side (green) — valid Perfect Binary Trees (symmetric, all leaves at same level). Right side (red) — invalid examples where leaf depths differ.

---

### Types: Balanced Binary Tree

- **Balanced Binary Tree** is a Binary tree in which the **level or height** of the left and the right sub-trees of every node **may differ by at most 1**.

> 📌 Extracted from image: Left side (green) — valid Balanced Binary Trees. Right side (red) — invalid examples with height difference > 1 between subtrees.

---

### A Degenerate (Skewed) Binary Tree

- All skewed (left or right) binary trees are degenerate, but **not all degenerate binary trees are skewed**.
- A degenerate tree can have **a mix of left and right children**, while a skewed tree is **strictly one-sided**.
- Skewed Tree is similar to a **Linked List**.

> 📌 Extracted from image: A right-skewed tree with nodes 1 → 2 → 3 → 4 → 5, each node only having a right child, resembling a linked list.

---

## Tree Traversal

- A tree traversal is a specific order in which to trace the nodes of a tree.
- There are 3 common methods:

1. **In-order:**
   - Visit nodes in the following order: left subtree → root → right subtree.
   - This traversal method results in the nodes being visited in **ascending order**.

2. **Pre-order:**
   - Visit nodes in the following order: root → left subtree → right subtree.
   - This method is useful for **creating a copy of the tree**.

3. **Post-order:**
   - Visit nodes in the following order: left subtree → right subtree → root.
   - This method is used to **delete the tree**.

---

### Tree Traversal — In-order

**Order: left subtree → root → right subtree**

> 📌 Extracted from image: Binary tree used for traversal examples:
> ```
>         4
>        / \
>       2   6
>      / \ / \
>     1  3 5  7
> ```

Steps:
1. Visit the left subtree of 4 (root) → subtree rooted at 2.
2. Visit the left subtree of 2 → node 1.
3. Visit 2 (root of this subtree).
4. Visit the right subtree of 2 → node 3.
5. Visit 4 (root).
6. Visit the right subtree of 4 → subtree rooted at 6.
7. Visit the left subtree of 6 → node 5.
8. Visit 6 (root of this subtree).
9. Visit the right subtree of 6 → node 7.

**In-order traversal result: 1, 2, 3, 4, 5, 6, 7**

> *For a Binary Search Tree, in-order traversal prints out a sorted list.*

---

### Tree Traversal — Pre-order

**Order: root → left subtree → right subtree**

Steps:
1. Visit 4 (root).
2. Visit the left subtree of 4 → subtree rooted at 2.
3. Visit 2 (root of this subtree).
4. Visit the left subtree of 2 → node 1.
5. Visit the right subtree of 2 → node 3.
6. Visit the right subtree of 4 → subtree rooted at 6.
7. Visit 6 (root of this subtree).
8. Visit the left subtree of 6 → node 5.
9. Visit the right subtree of 6 → node 7.

**Pre-order traversal result: 4, 2, 1, 3, 6, 5, 7**

> *Useful for displaying folders and subfolders.*

---

### Tree Traversal — Post-order

**Order: left subtree → right subtree → root**

Steps:
1. Visit the left subtree of 4 → subtree rooted at 2.
2. Visit the left subtree of 2 → node 1.
3. Visit the right subtree of 2 → node 3.
4. Visit 2 (root of this subtree).
5. Visit the right subtree of 4 → subtree rooted at 6.
6. Visit the left subtree of 6 → node 5.
7. Visit the right subtree of 6 → node 7.
8. Visit 6 (root of this subtree).
9. Visit 4 (root).

**Post-order traversal result: 1, 3, 2, 5, 7, 6, 4**

> *Useful for deleting tree nodes.*

---

## Application: Expression Tree

For the expression: **A \* B / (C + D \* E)**

> 📌 Extracted from image: Expression tree structure:
> ```
>          /
>         / \
>        *   +
>       / \ / \
>      A  B C  *
>              / \
>             D   E
> ```

- **Pre-order** (visit order numbered 1–9): / → * → A → B → + → C → * → D → E  
  Result: `/ * A B + C * D E`

- **Post-order** (visit order numbered 1–9): A → B → * → C → D → E → * → + → /  
  Result: `A B * C D E * + /`

- **In-order** (visit order numbered 1–9): A → * → B → / → C → + → D → * → E  
  Result: `A * B / C + D * E`

---

## Assignment

Show the result of traversal for this Binary Tree using the following methods:

1. In-Order
2. Pre-Order
3. Post-Order

> 📌 Extracted from image: Binary Search Tree:
> ```
>              63
>             /  \
>           41    74
>          /  \   /
>        16   53  65
>          \  /\ / \
>          25 46 55 64 70
> ```

---

## Binary Tree Structure

```cpp
class Node {
    int data;
    Node *left;
    Node *right;
};
```

> 📌 Extracted from image: Diagram showing Binary Tree memory representation:
> - **Root Node** contains: `data | left | right`
> - `left` pointer leads to left child node: `data | left | right` (both pointers → NULL)
> - `right` pointer leads to right child node: `data | left | right` (both pointers → NULL)
> - Caption: "Binary Tree Representation"

---

*End of Lecture 07 — Trees*