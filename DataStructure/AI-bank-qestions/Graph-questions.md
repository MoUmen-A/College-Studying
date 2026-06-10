# Graphs - Exam Questions
**Generated from:** `11-Graph.md`
**Calibrated against:** `23-spring.txt` · `25-spring`
**Course:** CCS2401 — Data Structures & Algorithms | Dr. Ahmed Said

---

## Section 1 — Topic Summary

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
- Q3: Full graph question — adjacency matrix, Dijkstra manual table, DFS sequence.

**From `25-spring`** (2025 exam):
- Q4: Graph traversals (DFS + BFS) from adjacency list + Dijkstra manual table.

**Key calibration rules derived from both exams**:
- Dijkstra must show the full table step by step.
- DFS/BFS must trace through the correct visited order.
- True/False items focus on application matching (which data structure does what).

---

## Section 3 — Question Bank

---

### 1. Multiple Choice (MCQ)

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

### 2. Fill-in-the-blank

---

#### Q7 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
In Dijkstra's algorithm, we always select the **unvisited** node with the ________ current distance as the next node to process.

**Guide answer:** **smallest (minimum)**

---

#### Q9 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
BFS uses a ________ to track the next node to visit, while DFS uses a ________.

**Guide answer:** **Queue** ; **Stack**

---

#### Q11 — Fill-in-the-blank | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
In an adjacency matrix for a **directed** graph, the cell `matrix[v][w] = 1` (or the edge weight) means there is an edge **from** vertex ________ **to** vertex ________.  
For an **undirected** graph, the matrix is always ________.

**Guide answer:** **v** ; **w** ; **symmetric** (i.e., `matrix[v][w] == matrix[w][v]`)

---

### 3. Short Answer

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

### 5. Application (Code / Scenario)

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

## Section 4 — Study Tips & Weak Areas

| Weak Area | Why Students Lose Marks | How to Fix |
|-----------|------------------------|------------|
| **DFS vs BFS data structure** | Swapping Stack↔Queue | Mnemonic: **D**FS → **D**eep → **S**tack. **B**FS → **B**road → **Q**ueue (B looks like a Q). |
| **Dijkstra's table** | Forgetting to cross out old distances, skipping predecessor updates, processing wrong vertex | Always write the table fresh at each step. Select the **minimum unvisited** distance each time. |
| **Adjacency matrix for directed graph** | Making it symmetric (like undirected) | Directed = asymmetric. Only mark `matrix[from][to]`, NOT `matrix[to][from]`. |

---

## Section 5 — Coverage Gap Analysis

### Concepts in lectures not yet covered in this question bank:

| Concept | From Lecture | Suggested Question |
|---------|-------------|-------------------|
| **Graph ADT functions** (`insertVertex`, `removeVertex`, `areAdjacent`) | `11-Graph.md` | "Implement the `areAdjacent(v1, v2)` function for an adjacency matrix representation." |
| **Trees as a special case of graphs** | `11-Graph.md` | "State three properties that distinguish a tree from a general directed graph." |
| **Space complexity of DFS vs BFS** (d, k notation) | `11-Graph.md` | "If a graph has a maximum depth d=4 and max branching factor k=3, what is the maximum space used by DFS and BFS?" |
| **Dijkstra with adjacency list complexity** | `11-Graph.md` (Complexity table) | "Compare the time and space complexity of Dijkstra using adjacency matrix vs adjacency list. When is each preferred?" |
