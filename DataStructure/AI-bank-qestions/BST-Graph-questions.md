# Question Bank — BST & Graphs
**Generated from:** `08-BST.md` · `11-Graph.md`
**Calibrated against:** `23-spring.txt` · `25-spring`
**Course:** CCS2401 — Data Structures & Algorithms | Dr. Ahmed Said

---

## Section 1 — Topic Summary

### Binary Search Tree (BST)
- A BST stores data in ordered fashion: left subtree < root ≤ right subtree.
- Average time complexity for search, insert, delete: **O(log N)**. Worst case (degenerate/skewed): **O(N)**.
- **Insertion**: compare and recurse left (<) or right (≥) until null position found.
- **Search**: compare at each node; stop if equal, go left if less, go right if greater, return false if null.
- **Deletion — 3 cases**:
  1. Leaf node → simply remove.
  2. One child → bypass: parent points to child directly.
  3. Two children → replace with **in-order successor** (leftmost node in right subtree) OR **in-order predecessor** (rightmost node in left subtree), then delete that node.
- **Traversals**: InOrder (sorted output), PreOrder (Root→L→R), PostOrder (L→R→Root).
- **InOrder predecessor**: immediately visited before a node in InOrder traversal.
- **InOrder successor**: immediately visited after a node in InOrder traversal.
- C++ implementation uses recursive private helpers (`insert`, `remove`, `search`, `findInOrderSuccessor`).

### Graphs
- A Graph **G = (V, E)**: set of vertices V and edges E. Edges can be directed/undirected and weighted.
- **Terminology**: adjacent vertices, degree, in-degree (directed), out-degree (directed), weight/cost.
- **Trees as graphs**: directed, acyclic, with a directed path from root to every node.
- **Representations**:
  - Adjacency Matrix: 2D array, O(V²) space. Fast edge lookup. Slow to iterate edges.
  - Adjacency List: array of linked lists. O(V+E) space. Best for sparse graphs. Slower edge lookup.
- **DFS**: uses a **Stack**. Goes deep before backtracking. Good for full-tree searches. Space: O(d·k).
- **BFS**: uses a **Queue**. Level-by-level traversal. Good when depth varies. Space: O(k^d).
- **Dijkstra's Algorithm**: single-source shortest path. Works on directed/undirected weighted graphs (non-negative weights).
  - Table tracks: Vertex | Visited | Distance | Predecessor.
  - Always select the unvisited vertex with the smallest current distance.
  - Complexity: O(V²) with adjacency matrix; O((V+E) log V) with adjacency list + heap.

---

## Section 2 — Tone Analysis

**From `23-spring.txt`** (2023 exam):
- Q1: True/False (10 items, 1 mark each) — test real-world application matching (e.g., "BFS uses a stack" is False).
- Q2: Mixed — polynomial array-based list implementation in C++ + stack-based decimal-to-binary conversion.
- Q3: Full graph question — adjacency matrix, Dijkstra manual table, DFS sequence.
- Q4: Mixed — link-based queue implementation + AVL tree insertions/deletions with drawing.

**From `25-spring`** (2025 exam):
- Q1: 6 MCQ (1-2 marks each) + tree construction from two traversals + code-completion task.
- Q2: 4 independent coding functions (BST cousin check, stack transformation, queue reversed print, doubly linked list deletion).
- Q3: Full AVL question — 10 insertions + 3 deletions with rotation annotation (LL/RR/LR/RL, S/D/N) + intermediate drawings.
- Q4: Graph traversals (DFS + BFS) from adjacency list + Dijkstra manual table.

**Key calibration rules derived from both exams**:
- Code questions always provide a declaration/skeleton and ask for member function implementation.
- Dijkstra must show the full table step by step.
- DFS/BFS must trace through the correct visited order.
- True/False items focus on application matching (which data structure does what).
- Tree construction from PreOrder + InOrder appears frequently.

---

## Section 3 — Question Bank

---

### 1. Multiple Choice (MCQ)

---

#### Q1 — MCQ | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**
In a Binary Search Tree, when deleting a node that has **two children**, which of the following replacements is always correct?

- A) Replace it with its left child directly.
- B) Replace it with its right child directly.
- C) Replace it with its in-order successor (leftmost node in the right subtree), then delete that node.
- D) Swap it with the root and delete the root.

**Guide answer:**
**C** — The in-order successor is always either a leaf or has at most one (right) child, making it safe to remove after copying its value up. Replacing with the left or right child directly breaks BST ordering.

**Key points to include for Full Marks:**
- State that the in-order successor is the **leftmost node in the right subtree**.
- Mention that the in-order predecessor (rightmost node in left subtree) is equally valid.

**Common mistakes to avoid:**
Choosing A or B — directly promoting a child breaks the BST property for the entire subtree.

---

#### Q2 — MCQ | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**
Which data structure does the **Breadth-First Search (BFS)** algorithm use internally?

- A) Stack
- B) Priority Queue
- C) Queue
- D) Linked List

**Guide answer:**
**C** — BFS processes nodes level by level, enqueuing all neighbors before moving deeper. DFS uses a Stack.

**Key points to include for Full Marks:**
- Explicitly contrast: BFS = Queue (FIFO), DFS = Stack (LIFO).

**Common mistakes to avoid:**
Confusing BFS with DFS. A very common exam trap: "BFS uses a stack" — this is **False** (23-spring Q1 included exactly this).

---

#### Q3 — MCQ | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
Consider a BST built by inserting: `8, 3, 10, 1, 6, 14, 4, 7, 13` (in this order).
What is the **in-order traversal** output of this BST?

- A) 8, 3, 1, 6, 4, 7, 10, 14, 13
- B) 1, 3, 4, 6, 7, 8, 10, 13, 14
- C) 1, 4, 7, 6, 3, 13, 14, 10, 8
- D) 8, 10, 14, 13, 3, 6, 7, 4, 1

**Guide answer:**
**B** — In-order traversal of any BST always produces a **sorted ascending** sequence. The BST built from those values has sorted output: 1, 3, 4, 6, 7, 8, 10, 13, 14.

**Key points to include for Full Marks:**
- Explicitly state the rule: InOrder traversal of a BST = sorted ascending order.

**Common mistakes to avoid:**
Option A is the insertion order, not the traversal result. Option C looks like PostOrder.

---

#### Q4 — MCQ | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
For a **directed weighted graph** with V vertices and E edges, what is the time complexity of Dijkstra's algorithm using an **adjacency matrix** representation?

- A) O(E log V)
- B) O(V + E)
- C) O(V²)
- D) O(V · E)

**Guide answer:**
**C** — With an adjacency matrix, finding the minimum distance vertex at each step requires scanning all V vertices → O(V) per step, repeated V times → **O(V²)** total. Using an adjacency list + min-heap gives O((V+E) log V).

**Key points to include for Full Marks:**
- Know both complexities: matrix = O(V²), list+heap = O((V+E) log V).

**Common mistakes to avoid:**
Choosing A — that is the adjacency list + heap version. Choosing B — that is plain BFS/DFS complexity.

---

#### Q5 — MCQ | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
Which of the following statements about **Adjacency Matrix vs. Adjacency List** is **FALSE**?

- A) Adjacency Matrix allows fast edge lookup between two specific vertices.
- B) Adjacency List is more space-efficient for sparse graphs.
- C) Adjacency Matrix is more space-efficient for sparse graphs.
- D) Adjacency List is faster to iterate over all edges.

**Guide answer:**
**C** — Adjacency Matrix always uses O(V²) space regardless of edge count, making it wasteful for sparse graphs. Adjacency List uses O(V+E), which is far more efficient when E << V².

**Key points to include for Full Marks:**
- Define sparse graph: few edges relative to V².
- Matrix = O(V²) space; List = O(V+E) space.

**Common mistakes to avoid:**
Confusing fast edge lookup (Matrix advantage) with space efficiency (List advantage).

---

#### Q6 — MCQ | Bloom's: Analyse | Difficulty: Hard | Marks: 2

**Question:**
After inserting `40, 20, 66, 1, 32, 51, 78` into a BST, node `66` is deleted. Which node **replaces** `66` using the in-order successor method?

- A) 78
- B) 51
- C) 32
- D) 40

**Guide answer:**
**B** — The in-order successor of 66 is the leftmost node in its right subtree. The right subtree of 66 has root 78, and 78 has no left child — so **78** ... wait, let's trace the tree carefully:

```
         40
        /  \
       20   66
      / \   / \
     1  32 51  78
```

In-order successor of 66 = leftmost node in right subtree of 66 = go right to 78, then go left → 78 has no left child → in-order successor = **78**.

Wait — re-check: right subtree of 66 is rooted at 78. 78 has no left child. So in-order successor = 78.

**Corrected Answer: A (78)**

The tree structure has 78 as the only right child of 66, with no left sub-child → `findInOrderSuccessor(66->right)` returns 78. After deletion, 66 is replaced by 78, and 78 is removed from its original position.

**Key points to include for Full Marks:**
- Trace `findInOrderSuccessor`: go right once (to 78), then go as far **left** as possible. Since 78 has no left child, 78 is the in-order successor.
- After copying 78 into node 66's position, delete 78 from the right subtree.

**Common mistakes to avoid:**
Going left from 66 instead of right to find the successor (that finds the predecessor instead).

---

### 2. Fill-in-the-blank

---

#### Q7 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
In Dijkstra's algorithm, we always select the **unvisited** node with the ________ current distance as the next node to process.

**Guide answer:** **smallest (minimum)**

---

#### Q8 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
The in-order successor of a node in a BST is the ________ node in its **right subtree**.

**Guide answer:** **leftmost**

---

#### Q9 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
BFS uses a ________ to track the next node to visit, while DFS uses a ________.

**Guide answer:** **Queue** ; **Stack**

---

#### Q10 — Fill-in-the-blank | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
The **in-order traversal** of any Binary Search Tree always produces values in ________ order. For the BST with root 63 and values {16, 25, 41, 46, 53, 55, 63, 64, 65, 70, 74}, the in-order predecessor of node 63 is ________ and its in-order successor is ________.

**Guide answer:** **ascending (sorted)** ; **55** ; **64**

**Key points to include for Full Marks:**
- Predecessor = node visited immediately **before** in in-order.
- Successor = node visited immediately **after** in in-order.

---

#### Q11 — Fill-in-the-blank | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
In an adjacency matrix for a **directed** graph, the cell `matrix[v][w] = 1` (or the edge weight) means there is an edge **from** vertex ________ **to** vertex ________.  
For an **undirected** graph, the matrix is always ________.

**Guide answer:** **v** ; **w** ; **symmetric** (i.e., `matrix[v][w] == matrix[w][v]`)

---

### 3. Short Answer

---

#### Q12 — Short Answer | Bloom's: Understand | Difficulty: Easy | Marks: 3

**Question:**
Explain the **three cases** of deleting a node from a BST. For each case, state what action is taken.

**Guide answer:**

| Case | Condition | Action |
|------|-----------|--------|
| 1 | Node is a **leaf** (no children) | Simply remove the node; set the parent's pointer to `nullptr`. |
| 2 | Node has **one child** | Bypass the node: set the parent's pointer to point directly to the node's single child. |
| 3 | Node has **two children** | Find the in-order successor (leftmost node in right subtree). Copy its value into the current node. Delete the in-order successor node (which has at most one child — Case 2). |

**Key points to include for Full Marks:**
- All three cases must be named and correctly described.
- For Case 3, explicitly state "in-order successor" (or "in-order predecessor") and "leftmost in right subtree".
- Mention that directly promoting a child in Case 3 **breaks BST property**.

**Common mistakes to avoid:**
Saying "just delete and reconnect" for Case 3 without specifying the successor mechanism.

---

#### Q13 — Short Answer | Bloom's: Understand | Difficulty: Easy | Marks: 3

**Question:**
What is the difference between **in-degree** and **out-degree** of a vertex in a directed graph? Give an example using a vertex with in-degree = 2 and out-degree = 1.

**Guide answer:**
- **In-degree**: the number of edges **pointing to** (entering) a vertex.
- **Out-degree**: the number of edges **going out of** (leaving) a vertex.

Example: Consider vertex B with edges A→B, C→B (in-degree = 2) and B→D (out-degree = 1).

```
A ──→ B ──→ D
C ──→ B
```

**Key points to include for Full Marks:**
- Clear definition of both terms using directionality.
- A correct example diagram or description.

---

#### Q14 — Short Answer | Bloom's: Analyse | Difficulty: Medium | Marks: 4

**Question:**
What is the **worst-case time complexity** of searching in a BST, and when does it occur? How does this compare to the average case?

**Guide answer:**
- **Worst case: O(N)** — occurs when the BST degenerates into a **skewed (linear) tree**, e.g., inserting sorted values like 1, 2, 3, 4, 5 produces a right-skewed tree where every node has only a right child. Search then becomes equivalent to linear list traversal.
- **Average case: O(log N)** — occurs with a balanced tree, where each comparison eliminates half of the remaining nodes.

```
Skewed tree (worst case):     Balanced tree (avg case):
1                                   5
 \                                /   \
  2                              3     7
   \                            / \   / \
    3                          1   4 6   8
     \
      4
```

**Key points to include for Full Marks:**
- State O(N) worst case and O(log N) average.
- Explain **why** worst case happens (degenerate/skewed structure from sorted insertions).

**Common mistakes to avoid:**
Saying worst case is always O(log N) — that only holds for balanced trees.

---

#### Q15 — Short Answer | Bloom's: Analyse | Difficulty: Medium | Marks: 4

**Question:**
Compare **DFS** and **BFS** graph traversal in terms of: (a) underlying data structure used, (b) traversal order characteristic, (c) space complexity, (d) best use case.

**Guide answer:**

| Criterion | DFS | BFS |
|-----------|-----|-----|
| Data structure | **Stack** (or recursion call stack) | **Queue** |
| Traversal order | Goes **deep** along one path before backtracking | Visits all neighbors at current level (**level-by-level**) |
| Space complexity | O(d · k) where d = max depth, k = max degree | O(k^d) — can be much larger |
| Best use case | Searching the entire tree/graph; easier to implement recursively | When the target is likely close to the source (shallow depth); when depth varies |

**Key points to include for Full Marks:**
- All 4 criteria addressed.
- Correct data structures (Stack for DFS, Queue for BFS).
- Correct space formulas from the lecture.

---

### 4. True / False + Justify

---

#### Q16 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 2

**Question:**
*"The Depth-First Search algorithm uses a Queue to track which nodes to visit next."*  
True or False? Justify your answer.

**Guide answer:**
**FALSE.**  
DFS uses a **Stack** (LIFO). It pushes unvisited neighbors onto the stack and pops the top to visit next, achieving the "go deep first" behavior.  
BFS is the algorithm that uses a **Queue** (FIFO) to achieve level-by-level traversal.

**Key points to include for Full Marks:**
- State DFS = Stack, BFS = Queue explicitly.
- Briefly explain why (LIFO → deep-first; FIFO → level-by-level).

---

#### Q17 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 2

**Question:**
*"In-order traversal of a Binary Search Tree always produces the node values in ascending sorted order."*  
True or False? Justify your answer.

**Guide answer:**
**TRUE.**  
By the BST property (left subtree < node ≤ right subtree), in-order traversal visits: left subtree (all smaller values) → root → right subtree (all larger values). Applying this recursively produces values in ascending sorted order.

**Key points to include for Full Marks:**
- Reference the BST property explicitly.
- State that in-order = Left → Root → Right.

---

#### Q18 — True/False | Bloom's: Analyse | Difficulty: Medium | Marks: 3

**Question:**
*"An Adjacency Matrix is always the best representation for a graph because it allows fast edge lookup."*  
True or False? Justify your answer.

**Guide answer:**
**FALSE.**  
While an adjacency matrix does allow **O(1)** edge lookup, it always requires **O(V²)** space, which is wasteful for **sparse graphs** (graphs with few edges, E << V²). For sparse graphs, an **Adjacency List** is more space-efficient at O(V+E) and faster to iterate over all edges. The adjacency matrix is only preferred when the graph is dense or when frequent edge-existence queries are needed.

**Key points to include for Full Marks:**
- Acknowledge the advantage of matrix (O(1) edge lookup).
- State the disadvantage: O(V²) space waste for sparse graphs.
- Mention Adjacency List as the preferred alternative for sparse graphs.

---

#### Q19 — True/False | Bloom's: Analyse | Difficulty: Hard | Marks: 3

**Question:**
*"When deleting a node with two children from a BST, we can replace it with its right child directly without violating the BST property."*  
True or False? Justify with a concrete counter-example.

**Guide answer:**
**FALSE.**  
Replacing the deleted node with its right child directly can violate the BST property. Consider deleting node **31** from:

```
      31
     /  \
    3    95
        /  \
       78   (none)
        \
        81
```

If we promote 95 directly to root, then 3 is in the left subtree of 95 — valid. But 78 and 81, which were children of 95, are now in the right subtree of 3 via the new root 95. The structure remains valid **in this specific case**, but promoting the **left child** directly would break ordering. More importantly, if the right child has a left subtree, some of those left-subtree values may be **smaller than the deleted node**, which would then incorrectly appear in the right subtree — a BST violation.

**Correct approach**: Copy the in-order successor's value into the deleted node, then delete the in-order successor.

**Key points to include for Full Marks:**
- State that direct promotion is wrong in general.
- Provide or describe a counter-example.
- State the correct solution: in-order successor replacement.

---

### 5. Application (Code / Scenario)

---

#### Q20 — Application | Bloom's: Apply | Difficulty: Easy | Marks: 5

**Question:**
Using the BST class declaration below (from `bst.h`), **implement** the private helper function `findInOrderSuccessor(Node* node)` that finds and returns the in-order successor node starting from a given subtree root. Then explain in one sentence how it is used in the `remove` function when deleting a node with two children.

```cpp
class Node {
public:
    int data;
    Node* left;
    Node* right;
    Node(int value);
};

class BinarySearchTree {
    Node* root;
    Node* findInOrderSuccessor(Node* node);
    // ... other members
};
```

**Guide answer:**

```cpp
Node* BinarySearchTree::findInOrderSuccessor(Node* node) {
    Node* current = node;
    // The in-order successor is the leftmost node in the given subtree
    while (current && current->left != nullptr)
        current = current->left;
    return current;
}
```

**Usage in `remove`**: When deleting a node with two children, `findInOrderSuccessor(node->right)` is called to get the smallest node in the right subtree; its `data` is copied into the node to be deleted, and then that successor node is recursively deleted from the right subtree.

**Key points to include for Full Marks:**
- Loop goes **left** until `left == nullptr` (not right).
- Returns `current`, not `current->data` (must return the node pointer).
- One-sentence explanation of how it fits in `remove`.

**Common mistakes to avoid:**
- Going right instead of left inside the loop — that finds the maximum, not the minimum.
- Forgetting the null-guard `current &&` in the while condition.

---

#### Q21 — Application | Bloom's: Apply | Difficulty: Medium | Marks: 6

**Question:**
Write a `main` function that uses the `BinarySearchTree` class to:
1. Insert the values: `40, 20, 66, 1, 32, 51, 78` (in this order).
2. Traverse the tree using **in-order**, **pre-order**, and **post-order**.
3. Remove value `66`.
4. Traverse again using **in-order** and show how the output changes.

**Guide answer:**

```cpp
#include <iostream>
#include "bst.h"
using namespace std;

int main() {
    BinarySearchTree bst;

    // Step 1: Insert values
    bst.Insert(40);
    bst.Insert(20);
    bst.Insert(66);
    bst.Insert(1);
    bst.Insert(32);
    bst.Insert(51);
    bst.Insert(78);

    // Step 2: Traversals before deletion
    cout << "In-order:   "; bst.Traverse("inorder");    // 1 20 32 40 51 66 78
    cout << "Pre-order:  "; bst.Traverse("preorder");   // 40 20 1 32 66 51 78
    cout << "Post-order: "; bst.Traverse("postorder");  // 1 32 20 51 78 66 40

    // Step 3: Remove 66
    bst.Remove(66);

    // Step 4: In-order after deletion (66 removed, 78 becomes in-order successor)
    cout << "In-order after removing 66: "; bst.Traverse("inorder"); // 1 20 32 40 51 78

    return 0;
}
```

**Tree structure after all insertions:**
```
         40
        /  \
       20   66
      / \   / \
     1  32 51  78
```

**After deleting 66** (in-order successor = 78, no left child of 78's right subtree):
```
         40
        /  \
       20   78
      / \   /
     1  32 51
```

**Key points to include for Full Marks:**
- Correct insertion order matters — the tree shape depends on it.
- In-order before deletion: `1 20 32 40 51 66 78` (sorted).
- In-order after deletion: `1 20 32 40 51 78` (66 gone, still sorted).
- All three traversal types attempted before deletion.

**Common mistakes to avoid:**
- Calling `bst.Traverse("inorder")` without the exact matching string — the implementation is case-sensitive.
- Forgetting the `#include` and `using namespace std;`.

---

#### Q22 — Application | Bloom's: Analyse | Difficulty: Medium | Marks: 6

**Question:**
Given the following directed weighted graph, apply **Dijkstra's algorithm** to find the shortest path from vertex **0** to all other vertices. Show your work in a step-by-step table.

```
Vertices: 0, 1, 2, 3, 4, 5, 6
Edges (undirected, weighted):
  0–1: 2      0–2: 6
  1–3: 5      2–3: 8
  3–4: 10     3–5: 15
  4–6: 2      5–6: 6
```

**Guide answer:**

Initial state — source = 0, all others = ∞:

| Vertex | Visited | Distance | Predecessor |
|--------|---------|----------|-------------|
| 0 | ✓ | 0 | — |
| 1 | ✗ | ∞ | |
| 2 | ✗ | ∞ | |
| 3 | ✗ | ∞ | |
| 4 | ✗ | ∞ | |
| 5 | ✗ | ∞ | |
| 6 | ✗ | ∞ | |

**Step 1 — Process 0** (neighbors: 1, 2):

| Vertex | Visited | Distance | Predecessor |
|--------|---------|----------|-------------|
| 0 | ✓ | 0 | — |
| 1 | ✗ | **2** | 0 |
| 2 | ✗ | **6** | 0 |
| 3 | ✗ | ∞ | |
| 4 | ✗ | ∞ | |
| 5 | ✗ | ∞ | |
| 6 | ✗ | ∞ | |

**Step 2 — Visit 1** (smallest unvisited = 1, dist=2). Process neighbors: 3 → 2+5=7:

| Vertex | Visited | Distance | Predecessor |
|--------|---------|----------|-------------|
| 0 | ✓ | 0 | — |
| 1 | ✓ | 2 | 0 |
| 2 | ✗ | 6 | 0 |
| 3 | ✗ | **7** | 1 |
| 4 | ✗ | ∞ | |
| 5 | ✗ | ∞ | |
| 6 | ✗ | ∞ | |

**Step 3 — Visit 2** (smallest unvisited = 2, dist=6). Process neighbors: 3 → 6+8=14 > 7 → no update:

| Vertex | Visited | Distance | Predecessor |
|--------|---------|----------|-------------|
| 0 | ✓ | 0 | — |
| 1 | ✓ | 2 | 0 |
| 2 | ✓ | 6 | 0 |
| 3 | ✗ | 7 | 1 |
| 4 | ✗ | ∞ | |
| 5 | ✗ | ∞ | |
| 6 | ✗ | ∞ | |

**Step 4 — Visit 3** (smallest unvisited = 3, dist=7). Process neighbors: 4 → 7+10=17; 5 → 7+15=22:

| Vertex | Visited | Distance | Predecessor |
|--------|---------|----------|-------------|
| 0 | ✓ | 0 | — |
| 1 | ✓ | 2 | 0 |
| 2 | ✓ | 6 | 0 |
| 3 | ✓ | 7 | 1 |
| 4 | ✗ | **17** | 3 |
| 5 | ✗ | **22** | 3 |
| 6 | ✗ | ∞ | |

**Step 5 — Visit 4** (smallest unvisited = 4, dist=17). Process neighbors: 6 → 17+2=19:

| Vertex | Visited | Distance | Predecessor |
|--------|---------|----------|-------------|
| 0 | ✓ | 0 | — |
| 1 | ✓ | 2 | 0 |
| 2 | ✓ | 6 | 0 |
| 3 | ✓ | 7 | 1 |
| 4 | ✓ | 17 | 3 |
| 5 | ✗ | 22 | 3 |
| 6 | ✗ | **19** | 4 |

**Step 6 — Visit 6** (smallest unvisited = 6, dist=19). Process neighbors: 5 → 19+6=25 > 22 → no update:

**Step 7 — Visit 5** (dist=22). No unvisited neighbors. Done.

**Final shortest paths from vertex 0:**

| Destination | Shortest Distance | Path |
|-------------|-----------------|------|
| 1 | 2 | 0 → 1 |
| 2 | 6 | 0 → 2 |
| 3 | 7 | 0 → 1 → 3 |
| 4 | 17 | 0 → 1 → 3 → 4 |
| 5 | 22 | 0 → 1 → 3 → 5 |
| 6 | 19 | 0 → 1 → 3 → 4 → 6 |

**Key points to include for Full Marks:**
- Show the **initial state** with source=0 and all others=∞.
- Show the table **after every step** with updated distances.
- Cross out (or note) old distance values when they are updated.
- State the **final shortest path** by tracing predecessors.
- Process exactly **V steps** (one per vertex).

**Common mistakes to avoid:**
- Processing a vertex without first marking it visited.
- Forgetting to check ALL neighbors of the current vertex.
- Not tracing the predecessor chain to state the actual path.

---

#### Q23 — Application | Bloom's: Apply | Difficulty: Medium | Marks: 5

**Question:**
Given the graph represented by the following adjacency list, perform:

**(a)** DFS starting from vertex 50 (visit neighbors in **increasing** numerical order).  
**(b)** BFS starting from vertex 50 (visit neighbors in **increasing** numerical order).

```
Vertex:  Neighbors
50    →  [20, 65, 80]
20    →  [10, 50, 40]
10    →  [20]
40    →  [20]
65    →  [50, 70]
70    →  [65]
80    →  [50, 90]
90    →  [80]
```

*(This is taken directly from the 25-spring exam — Q4.1)*

**Guide answer:**

**DFS from 50** (Stack-based, visit neighbors in increasing order — push in **reverse** increasing order so smallest is popped first):

Stack trace:

| Step | Visited | Stack |
|------|---------|-------|
| Start | — | [50] |
| Pop 50, push unvisited neighbors {20,65,80} in reverse → push 80,65,20 | 50 | [80, 65, 20] |
| Pop 20, push unvisited {10,40} → push 40,10 | 50,20 | [80, 65, 40, 10] |
| Pop 10, push unvisited {} | 50,20,10 | [80, 65, 40] |
| Pop 40, push unvisited {} | 50,20,10,40 | [80, 65] |
| Pop 65, push unvisited {70} | 50,20,10,40,65 | [80, 70] |
| Pop 70, push unvisited {} | 50,20,10,40,65,70 | [80] |
| Pop 80, push unvisited {90} | 50,20,10,40,65,70,80 | [90] |
| Pop 90 | 50,20,10,40,65,70,80,90 | [] |

**DFS order: 50, 20, 10, 40, 65, 70, 80, 90**

**BFS from 50** (Queue-based):

| Step | Current | Queue | Visited |
|------|---------|-------|---------|
| Enqueue 50 | — | [50] | — |
| Dequeue 50; enqueue unvisited {20,65,80} | 50 | [20,65,80] | 50 |
| Dequeue 20; enqueue unvisited {10,40} | 20 | [65,80,10,40] | 50,20 |
| Dequeue 65; enqueue unvisited {70} | 65 | [80,10,40,70] | 50,20,65 |
| Dequeue 80; enqueue unvisited {90} | 80 | [10,40,70,90] | 50,20,65,80 |
| Dequeue 10 | 10 | [40,70,90] | 50,20,65,80,10 |
| Dequeue 40 | 40 | [70,90] | 50,20,65,80,10,40 |
| Dequeue 70 | 70 | [90] | 50,20,65,80,10,40,70 |
| Dequeue 90 | 90 | [] | 50,20,65,80,10,40,70,90 |

**BFS order: 50, 20, 65, 80, 10, 40, 70, 90**

**Key points to include for Full Marks:**
- Show the full stack/queue state at every step.
- Skip already-visited nodes when pushing/enqueuing.
- Visit neighbors in the **specified order** (increasing numerical).
- State the final visited order clearly.

---

#### Q24 — Application | Bloom's: Create | Difficulty: Hard | Marks: 8

**Question:**
Using the BST class below, write the **complete `remove` member function** (both the public wrapper and the private recursive helper) that correctly handles all three deletion cases. Your implementation must use `findInOrderSuccessor`.

```cpp
class BinarySearchTree {
    Node* root;
    Node* remove(Node* node, int data);
    Node* findInOrderSuccessor(Node* node);
public:
    void Remove(int data);
};
```

**Guide answer:**

```cpp
void BinarySearchTree::Remove(int data) {
    root = remove(root, data);
}

Node* BinarySearchTree::remove(Node* node, int data) {
    // Base case: value not found
    if (node == nullptr)
        return node;

    // Navigate to the node to delete
    if (data < node->data)
        node->left = remove(node->left, data);
    else if (data > node->data)
        node->right = remove(node->right, data);
    else {
        // Case 1 & 2: node has zero or one child
        if (node->left == nullptr) {
            Node* temp = node->right;
            delete node;
            return temp;                  // right child (or nullptr) takes place
        } else if (node->right == nullptr) {
            Node* temp = node->left;
            delete node;
            return temp;                  // left child takes place
        }

        // Case 3: node has two children → find in-order successor
        Node* temp = findInOrderSuccessor(node->right);
        node->data = temp->data;          // copy successor's value
        node->right = remove(node->right, temp->data); // delete successor
    }
    return node;
}

Node* BinarySearchTree::findInOrderSuccessor(Node* node) {
    Node* current = node;
    while (current && current->left != nullptr)
        current = current->left;
    return current;
}
```

**Key points to include for Full Marks:**
- Public `Remove` calls private `remove` on `root` and **reassigns root** (`root = remove(root, data)`).
- Base case: `if (node == nullptr) return node;` — handles missing value.
- Case 1 (no left child): `return node->right;` (could be null → leaf case covered).
- Case 2 (no right child): `return node->left;`.
- Case 3: find successor with `findInOrderSuccessor(node->right)`, copy data, recursively delete successor.
- **`delete node;`** must be called before returning to avoid memory leak.

**Common mistakes to avoid:**
- Forgetting to `delete node` in Cases 1 and 2 (memory leak).
- Not reassigning `node->left` or `node->right` after the recursive call (the return value of `remove` must be stored).
- Using `findInOrderSuccessor(node)` instead of `findInOrderSuccessor(node->right)`.

---

### 6. Compare & Contrast

---

#### Q25 — Compare & Contrast | Bloom's: Analyse | Difficulty: Medium | Marks: 5

**Question:**
Compare **DFS** and **BFS** traversal algorithms. Your comparison must address: underlying data structure, traversal strategy, space complexity, and recommended use case. Use a table format.

**Guide answer:**

| Criterion | DFS (Depth-First Search) | BFS (Breadth-First Search) |
|-----------|--------------------------|---------------------------|
| Data Structure | **Stack** (or recursion stack) | **Queue** |
| Strategy | Goes **deep** along one path; backtracks when dead-end | Explores all neighbors at current depth (**level by level**) |
| Space Complexity | O(d · k) — d = max depth, k = max branching factor | O(k^d) — can be exponentially larger |
| Memory | Generally uses **less memory** | Can use **more memory** for wide/shallow graphs |
| Best Use Case | Searching the entire graph/tree; cycle detection; topological sort | Finding shortest path (unweighted); when solution is close to source |
| Implementation | Easier to implement **recursively** | Typically implemented **iteratively** |

**Key points to include for Full Marks:**
- All criteria addressed.
- Correct data structures.
- Correct space complexity formulas from the lecture.
- Meaningful use-case differentiation.

---

#### Q26 — Compare & Contrast | Bloom's: Evaluate | Difficulty: Hard | Marks: 5

**Question:**
Compare **Adjacency Matrix** vs. **Adjacency List** representations of a graph. For each, state its space complexity, time complexity for edge lookup, time complexity for iterating all edges, and when you would choose it.

**Guide answer:**

| Criterion | Adjacency Matrix | Adjacency List |
|-----------|-----------------|----------------|
| Space Complexity | **O(V²)** — always, regardless of edges | **O(V + E)** — proportional to actual structure |
| Edge Lookup (u→v exists?) | **O(1)** — direct array access `matrix[u][v]` | **O(degree(u))** — must search u's list |
| Iterating All Edges | **O(V²)** — must scan entire matrix | **O(V + E)** — only follows existing links |
| Best For | **Dense graphs** (E ≈ V²); frequent specific edge queries | **Sparse graphs** (E << V²); frequent traversal of all edges |
| Example | Routing table with many connections | Social network (most people aren't connected to everyone) |

**Key points to include for Full Marks:**
- Space: Matrix = O(V²), List = O(V+E).
- Edge lookup: Matrix wins; List slower.
- Iteration: List wins; Matrix is wasteful.
- Define sparse vs dense in context.

---

### 7. Essay / Long Answer

---

#### Q27 — Essay | Bloom's: Create | Difficulty: Hard | Marks: 10

**Question:**
Design and implement a complete C++ BST class that supports:
- Insert, Search, Remove (all three cases)
- InOrder, PreOrder, PostOrder traversals

Then, given the following insertion sequence: `60, 41, 74, 16, 53, 65, 46, 55, 63, 70, 42, 48, 64`

**(a)** Draw the resulting BST after all insertions.  
**(b)** State the InOrder, PreOrder, and PostOrder traversal results.  
**(c)** Show the BST after deleting: 53, 60 (apply both deletions sequentially on the same tree).  
**(d)** What is the in-order traversal of the final tree?

**Guide answer:**

**(a) BST after all insertions:**

```
                  60
                /    \
              41       74
             /  \     /
            16   53  65
                / \   / \
               46  55 63  70
              / \    \
             42  48   64
```
*(Verification: Each node's left subtree < node ≤ right subtree — BST property holds.)*

**(b) Traversal results:**
- **InOrder** (L→Root→R): `16, 41, 42, 46, 48, 53, 55, 60, 63, 64, 65, 70, 74`
- **PreOrder** (Root→L→R): `60, 41, 16, 53, 46, 42, 48, 55, 74, 65, 63, 64, 70`
- **PostOrder** (L→R→Root): `16, 42, 48, 46, 55, 53, 41, 64, 63, 70, 65, 74, 60`

**(c) Delete 53** (two children → in-order successor of 53 = leftmost in right subtree = 55, since 55 has no left child):
- Copy 55 into node 53's position. Delete original 55.

```
                  60
                /    \
              41       74
             /  \     /
            16   55  65
                /   / \
               46  63  70
              / \    \
             42  48   64
```

**Delete 60** (two children → in-order successor of 60 = leftmost in right subtree of 60 = go right to 74, then left to 65, then left to 63 → 63 has no left child → successor = 63):
- Copy 63 into root. Delete original 63.

```
                  63
                /    \
              41       74
             /  \     /
            16   55  65
                /     \
               46      70
              / \
             42  48
```

**(d) InOrder of final tree:**
`16, 41, 42, 46, 48, 55, 63, 65, 70, 74`

**Key points to include for Full Marks:**
- Correct tree drawing after all insertions (verify BST property).
- All three traversal sequences correct.
- Deletion of 53: correctly identify in-order successor (55), copy value, delete original 55.
- Deletion of 60: correctly trace in-order successor (63), copy value, delete original 63.
- Final in-order is still sorted — use this to self-verify.

**Common mistakes to avoid:**
- Not tracing ALL the way left to find the in-order successor (e.g., stopping at 74 or 65 instead of finding 63).
- Forgetting that in-order always = sorted output, so you can cross-check your traversal result.
- Not updating the tree diagram after each deletion before performing the next.

---

## Section 4 — Study Tips & Weak Areas

| Weak Area | Why Students Lose Marks | How to Fix |
|-----------|------------------------|------------|
| **In-order successor** | Going left instead of right first, or stopping too early | Memorize: "go right once, then go as far **left** as possible". The `findInOrderSuccessor` function loops `while(current->left != nullptr)`. |
| **3 deletion cases** | Merging Case 1 and 2, or mishandling Case 3 by promoting a child directly | Practice with concrete trees. Always identify: how many children does the node have? |
| **DFS vs BFS data structure** | Swapping Stack↔Queue | Mnemonic: **D**FS → **D**eep → **S**tack. **B**FS → **B**road → **Q**ueue (B looks like a Q). |
| **Dijkstra's table** | Forgetting to cross out old distances, skipping predecessor updates, processing wrong vertex | Always write the table fresh at each step. Select the **minimum unvisited** distance each time. |
| **Adjacency matrix for directed graph** | Making it symmetric (like undirected) | Directed = asymmetric. Only mark `matrix[from][to]`, NOT `matrix[to][from]`. |
| **Traversal verification** | Computing InOrder wrong | For BST: InOrder MUST be sorted. If it's not, your tree or traversal is wrong. |
| **Memory management in remove()** | Forgetting `delete node` in Cases 1 and 2 | Always call `delete` before `return temp`. |

---

## Section 5 — Coverage Gap Analysis

### Concepts in lectures not yet covered in this question bank:

| Concept | From Lecture | Suggested Question |
|---------|-------------|-------------------|
| BST **search trace** (step-by-step table) | `08-BST.md` (Search section) | "Trace the search for value 48 in the given BST. Show each node visited and the decision made." |
| **Building BST from a sequence** (drawing step-by-step) | `08-BST.md` (Assignment 1) | "Insert the values 100, 200, 90, 150, 125, 88, 99, 210 into an empty BST. Draw the tree after each insertion." |
| **Graph ADT functions** (`insertVertex`, `removeVertex`, `areAdjacent`) | `11-Graph.md` | "Implement the `areAdjacent(v1, v2)` function for an adjacency matrix representation." |
| **Trees as a special case of graphs** | `11-Graph.md` | "State three properties that distinguish a tree from a general directed graph." |
| **Space complexity of DFS vs BFS** (d, k notation) | `11-Graph.md` | "If a graph has a maximum depth d=4 and max branching factor k=3, what is the maximum space used by DFS and BFS?" |
| **Dijkstra with adjacency list complexity** | `11-Graph.md` (Complexity table) | "Compare the time and space complexity of Dijkstra using adjacency matrix vs adjacency list. When is each preferred?" |

### Lecture files not yet uploaded:
The following lecture numbers appear to be missing from `d:\Gam3a\Exam-Creation\DataStructure\Lec\`:
- Lectures 01, 02, 03 (likely: Arrays, Linked Lists basics, Stacks)
- Lecture 05 (likely: Singly Linked List or Circular Linked List)
- Lectures 09, 10 (likely: AVL Trees, Heap/Priority Queue)

> **Recommendation**: Upload these lectures to the `Lec\` folder. When you do, re-run this instruction file with the new materials and questions for those topics will be auto-generated — especially AVL rotations (LL/RR/LR/RL) which appear in **both** previous exams (23-spring Q4 and 25-spring Q3).
