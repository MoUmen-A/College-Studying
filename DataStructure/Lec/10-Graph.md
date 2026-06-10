# CCS2401 — Data Structures & Algorithms
## 11 – Graphs
**Dr. Ahmed Said**

---

## Graphs

A graph is the **most general of all the collections** because it allows arbitrary relationships to exist among its elements.

> 📌 Extracted from image: Directed graph with vertices labeled a, b, c, d, e, f, g, h and directed edges between them forming a complex network.

---

## Directed VS Undirected Graphs

Two Types of Graphs:
1. **Directed**
2. **Undirected**

> 📌 Extracted from image: **Directed Graphs** — Three examples (labeled 1, 2, 3) showing vertices A, B, C with arrows indicating directed edges in different configurations.
>
> **Undirected Graphs** — Three examples (labeled 4, 5, 6) showing vertices A, B, C with lines (no arrowheads) indicating undirected edges in different configurations.

---

## Graph Terminology

A Graph **G = (V, E)** consists of a set of **vertices**, V, and a set of **edges**, E.

> 📌 Extracted from image: Graph with vertices A, B, C, D. Edge labeled 10 from A→B; edge labeled 1 from A→C; edge labeled 1 from C→D; edge labeled 1 from D→B. "Vertex" label pointing to A; "Edge" label pointing to the A→B edge.

Each edge is a **pair (v, w)**, where v, w ∈ V.

Vertices are sometimes called **nodes**.  
Edges are sometimes called **arcs**.

Sometimes an edge has a third component, known as either a **weight** or a **cost**.

> 📌 Extracted from image: Same graph as above with numeric labels on edges (10, 1, 1, 1) highlighted as "Weight / Cost".

Two vertices are said to be **adjacent**, if there is an edge between the two vertices.

- A & C are adjacent vertices, as there is a common edge
- A & B
- C & D

The **degree** of a vertex is the number of edges coming out of it.

In a **directed graph** you can sometimes use the terms:
- **In Degree**: the number of edges pointing to the vertex.
- **Out Degree**: the number of edges coming out of a vertex.

> 📌 Extracted from image: Graph with vertices A, B, C, D. Vertex A has "Out Degree = 2" (edges going to B and C). Vertex B has "In Degree = 2" (edges coming from A and D).

---

## Trees as Graphs

Every tree is a graph with some restrictions:
- The tree is **Directed**.
- There are **no cycles**.
- There is a **directed path from the root to every node**.

> 📌 Extracted from image: Binary tree with root node 4, children 2 and 7, and leaf nodes 1, 3, 5, 9. All edges are directed downward (parent → child).

---

## Graph Applications

Graphs are used to represent elements that share connections, for example:
- Google Maps
- GPS Navigation Systems
- Social media (Social Graphs)
- Knowledge Graphs
- Computer networks
- Transportation networks
- Databases
- …

---

## Implementation

> 📌 Extracted from image: Undirected graph with vertices 1, 2, 3, 4, 5, 6 and various edges connecting them.

### Graph ADT Functions

- `insertVertex(v)`
- `removeVertex(v)`
- `insertEdge(v1, v2, w)`
- `removeEdge(e)`
- `numVertices()`
- `numEdges()`
- `areAdjacent(v1, v2)`
- `traverse()`

---

## Representation of Graph

How to store a graph in the computer's memory? What technique will we use?

There are two major ways to do that:
1. **Adjacency Matrix** (Sequential representation)
2. **Adjacency List** (Linked list representation)

> 📌 Extracted from image: Directed graph with vertices 1–6. Two arrows point left (toward "Adjacency List") and right (toward "Adjacency Matrix"), illustrating the two representation approaches.

---

## 1 – Adjacency Matrix

One of the easiest ways to implement a graph is to use a **two-dimensional matrix**.

- Each of the rows and columns represent a vertex in the graph.
- The value stored in the cell at the intersection of row v and column w indicates if there is an edge from vertex v to vertex w. When two vertices are connected by an edge, they are said to be **adjacent**.
- If the graph is **weighted**, a value in a cell represents the **weight** of the edge from vertex v to vertex w.

> 📌 Extracted from image (Directed Graph): Vertices 1, 2, 3, 4, 5. Edges include: 1→2, 1→4, 2→3, 3→2, 4→2, 5→2, and a self-loop on 4.

> 📌 Extracted from image (Undirected Graph — unweighted): Vertices A, B, C, D, E, F. Edges: A–B, A–E, B–E, B–F, F–D.

> 📌 Extracted from image (Undirected Graph — weighted): Same graph as above with weights: A–B = 2, A–E = 5, B–E = 3, B–F = 4, F–D = 3.

---

## 2 – Adjacency List

In an adjacency list implementation, we keep a **master list of all the vertices** in the Graph object, and then each vertex object maintains a list of the other vertices it is connected to.

For better performance, the original list of nodes can be implemented as a **hash table**.

> 📌 Extracted from image (Undirected Graph — Adjacency List): Vertices 0–4. Adjacency list:
> - 0 → 1 → 2 → 3 → 4
> - 1 → 0 → 3
> - 2 → 0 → 3 → 4
> - 3 → 0 → 1 → 2 → 4
> - 4 → 0 → 2 → 3
>
> Head (an array of pointers) points to each linked list row.

> 📌 Extracted from image (Directed Graph — Adjacency List): Vertices M, N, P, R, T, Z. Directed edges shown with arrows between vertices forming a diamond-like pattern.

> 📌 Extracted from image (Directed Weighted Graph — Adjacency List):
>
> Graph with edges and weights:
> - M → N (weight 2), P → M (weight 6), N → Z (weight 5), T → Z (weight 4), Z → P (weight 8), Z → R (weight 6)
>
> Adjacency list representation:
> ```
> M → (N, 2)
> N → (Z, 5)
> P → (M, 6)
> R
> T → (Z, 4)
> Z → (P, 8) → (R, 6)
> ```

---

## Adjacency List vs. Adjacency Matrix

### Adjacency Matrix
- Can answer fast questions regarding if a specific edge between two vertices belongs to the graph.
- Can also have quick insertions and deletions of edges.
- Uses excessive space, especially for graphs with many vertices.
- Slow to iterate over the edges.

### Adjacency List
- More space efficient especially for **sparse graphs**.
- Fast to iterate over all edges.
- Finding the presence or absence of a specific edge is slightly slower than the matrix, because you must search through the appropriate list to find the edge.

---

## Traversal

**Visit all nodes.**  
It should be started for each connected component individually.

> 📌 Extracted from image: Graph with 8 vertices (0–7). Vertices 0, 1, 2, 3, 4 form one connected component (shown inside a dashed box). Vertices 5 and 6 form another connected component. Vertex 7 is isolated.

---

## Depth First vs. Breadth First Search

> 📌 Extracted from image:
>
> **Depth-first search** (left diagram): Traversal goes deep along one branch before backtracking. Order follows the tree path downward.
>
> **Breadth-first search** (right diagram): Traversal visits all neighbors at the current depth level before moving deeper. Level-by-level traversal shown with dashed horizontal arrows.

---

## Depth First Search (DFS) Algorithm

```
1.  Initialize all vertices as "unvisited".
2.  Let S be a stack.
3.  Push the root on S.
4.  While S not empty, do
5.  begin
6.      Let n <- Pop S.
7.      If n is marked as "unvisited", then
8.      begin
9.          Mark n as "visited", and output n to the terminal.
10.         For each vertex v in Adj[n], do
11.             If v is marked as "unvisited", then
12.                 push v on S.
13.     end
14. end
```

---

## DFS Example

> 📌 Extracted from image: Undirected graph with vertices A, B, I, C, D, E, F, G, H.
> Edges: A–B, A–I, B–I, I–C, I–G, C–D, C–E, C–F, D–E, E–H, E–F, G–F.

Step-by-step DFS execution (starting from A):

| Step | Current | Stack |
|------|---------|-------|
| Initial | — | — |
| 1 | — | A |
| 2 | A | B, I |
| 3 | B | I |
| 4 | I | C, G |
| 5 | C | D, E, F, G |
| 6 | D | E, F, G |
| 7 | E | H, F, G |
| 8 | H | G, F, G |
| 9 | G | F, G |
| 10 | F | G |
| 11 | G (already visited) | — |

**Visited order:** A, B, I, C, D, E, H, G, F

> 📌 Note: Another valid DFS solution: A, I, G, H, E, C, F, D (order depends on adjacency list ordering).

---

## Breadth First Search (BFS) Algorithm

```
1.  Initialize all vertices as "unvisited".
2.  Let Q be a queue.
3.  Enqueue the root on Q.
4.  While Q not empty, do
5.  begin
6.      n <- Dequeue Q.
7.      If n is marked as "unvisited", then
8.      begin
9.          Mark n as "visited", and output n to the terminal.
10.         For each vertex v in Adj[n], do
11.             If v is marked "unvisited", then
12.                 enqueue v on Q.
13.     end
14. end
```

---

## BFS Example

> 📌 Extracted from image: Same graph as DFS example — vertices A, B, I, C, D, E, F, G, H.

Step-by-step BFS execution (starting from A):

| Step | Current | Queue (visited order) |
|------|---------|----------------------|
| Initial | — | — |
| 1 | — | A |
| 2 | A | A → enqueue B, I |
| 3 | B | A, B → dequeue B; I remains |
| 4 | I | A, B, I → enqueue G, C |
| 5 | C | A, B, I, C → enqueue F, E, D, G |
| 6 | G | A, B, I, C, G → enqueue H, F |
| 7 | D | A, B, I, C, G, D |
| 8 | E | A, B, I, C, G, D, E → enqueue H |
| 9 | F | A, B, I, C, G, D, E, F → enqueue H |
| 10 | H | A, B, I, C, G, D, E, F, H |

**Visited order:** A, B, I, C, G, D, E, F, H

---

## Space Requirements

Assuming:
- The longest path in the graph is of length **d**
- The highest number of out-edges is **k**

| Algorithm | Space Complexity |
|-----------|-----------------|
| DFS | O(d · k) — stack grows to at most this size |
| BFS | O(k^d) — queue can grow to this size |

---

## When to Use Each?

- **Breadth First Search** is generally the best approach when the **depth of the tree can vary**.
- **Depth First Search** is commonly used when you need to **search the entire tree**.
  - Easier to implement with recursion.
  - Needs less memory.

---

## Shortest Path

> 📌 Extracted from image: Undirected graph with vertices 1–6 and various edges.

---

## Single-Source Shortest Path Problem

The problem of **finding shortest paths from a source vertex v to all other vertices** in the graph.

**Dijkstra's algorithm** is a popular algorithm for solving many single-source shortest path problems.

It was conceived by Dutch computer scientist **Dijkstra in 1956**.

---

## Need for Dijkstra's Algorithm

The need for Dijkstra's algorithm arises in many applications where finding the shortest path between two points is crucial.

Can work for both:
- Directed Graphs
- Undirected Graphs

Used in:
- Routing protocols for computer networks
- Map systems to find the shortest path between a starting point and a destination (Google Maps, …)

---

## Dijkstra's Algorithm

```
1. Mark the source node with a current distance of 0 and the rest with infinity.
2. Set the non-visited node with the smallest current distance as the current node.
3. For each neighbor N of the current node, add the current distance of the adjacent
   node with the weight of the edge connecting them.
   - If it is smaller than the current distance of N, set it as the new current distance of N.
   - Update the predecessor node accordingly.
4. Mark the current node as visited.
5. Go to step 2 if there are any unvisited nodes.
```

---

## Dijkstra's Algorithm — Worked Example

**Find Shortest Path from a to f**

> 📌 Extracted from image: Weighted undirected graph with vertices a, b, c, d, e, f.
> Edges and weights:
> - a–b: 2
> - a–c: 4
> - b–c: 1
> - b–d: 4 (via cross edge, effective weight from b: 4)
> - b–e: 2
> - c–e: 3 (implied from slide)
> - d–f: 3
> - e–f: 2

### Initial State

Mark the source node with a current distance of 0 and the rest with infinity.

**Unvisited Nodes:** {a, b, c, d, e, f}

| V | Visited | Distance (Cost) | Predecessor |
|---|---------|-----------------|-------------|
| a | ✓ | 0 | — |
| b | ✗ | ∞ | |
| c | ✗ | ∞ | |
| d | ✗ | ∞ | |
| e | ✗ | ∞ | |
| f | ✗ | ∞ | |

### Step 1 — Process node a

Calculate distance to all adjacent nodes of a.

| V | Visited | Distance (Cost) | Predecessor |
|---|---------|-----------------|-------------|
| a | ✓ | 0 | — |
| b | ✗ | 2 | a |
| c | ✗ | 4 | a |
| d | ✗ | ∞ | |
| e | ✗ | ∞ | |
| f | ✗ | ∞ | |

### Step 2 — Mark b as visited (lowest unvisited distance = 2)

| V | Visited | Distance (Cost) | Predecessor |
|---|---------|-----------------|-------------|
| a | ✓ | 0 | — |
| b | ✓ | 2 | a |
| c | ✗ | 4 | a |
| d | ✗ | ∞ | |
| e | ✗ | ∞ | |
| f | ✗ | ∞ | |

### Step 3 — Process node b; update neighbors c, d, e

- c: 2 + 1 = 3 < 4 → update
- d: 2 + 4 = 6 → update
- e: 2 + 2 = 4 → update

| V | Visited | Distance (Cost) | Predecessor |
|---|---------|-----------------|-------------|
| a | ✓ | 0 | — |
| b | ✓ | 2 | a |
| c | ✗ | 3 | b |
| d | ✗ | 6 | b |
| e | ✗ | 4 | b |
| f | ✗ | ∞ | |

### Step 4 — Mark c as visited (lowest unvisited distance = 3)

| V | Visited | Distance (Cost) | Predecessor |
|---|---------|-----------------|-------------|
| a | ✓ | 0 | — |
| b | ✓ | 2 | a |
| c | ✓ | 3 | b |
| d | ✗ | 6 | b |
| e | ✗ | 4 | b |
| f | ✗ | ∞ | |

### Step 5 — Process node c; check neighbor e

- e via c: 3 + 3 = 6 > 4 (current) → **no update needed**

### Step 6 — Mark e as visited (lowest unvisited distance = 4)

| V | Visited | Distance (Cost) | Predecessor |
|---|---------|-----------------|-------------|
| a | ✓ | 0 | — |
| b | ✓ | 2 | a |
| c | ✓ | 3 | b |
| d | ✗ | 6 | b |
| e | ✓ | 4 | b |
| f | ✗ | ∞ | |

### Step 7 — Process node e; update neighbor f

- f: 4 + 2 = 6 → update

| V | Visited | Distance (Cost) | Predecessor |
|---|---------|-----------------|-------------|
| a | ✓ | 0 | — |
| b | ✓ | 2 | a |
| c | ✓ | 3 | b |
| d | ✗ | 6 | b |
| e | ✓ | 4 | b |
| f | ✗ | 6 | e |

### Step 8 — Mark d and f as visited (both cost = 6); algorithm stops

| V | Visited | Distance (Cost) | Predecessor |
|---|---------|-----------------|-------------|
| a | ✓ | 0 | — |
| b | ✓ | 2 | a |
| c | ✓ | 3 | b |
| d | ✓ | 6 | b |
| e | ✓ | 4 | b |
| f | ✓ | 6 | e |

All nodes are visited — algorithm stops.

### Result

**The shortest path from a to f is: a → b → e → f** (total cost = **6**)

---

## Implementation of Dijkstra's Algorithm

There are several ways to implement Dijkstra's algorithm; the most common ones are:

1. **Array-based Implementation** — uses Adjacency Matrix
2. **Priority Queue (Heap-based Implementation)** — uses Adjacency List

---

## Complexity Analysis of Dijkstra's Algorithm

| Implementation | Time Complexity | Space Complexity |
|----------------|----------------|-----------------|
| Adjacency Matrix | $O(V^2)$ | $O(V^2)$ |
| Adjacency List | $O((V + E) \log V)$ | $O(V + E)$ |

Where **V** is the number of vertices and **E** is the number of edges.

---

## Assignment

**Traverse the graph using:**
- DFS
- BFS

**Find the Shortest Path from 0 to 6 using Dijkstra.**

> 📌 Extracted from image: Undirected weighted graph with 7 vertices (0, 1, 2, 3, 4, 5, 6).
>
> Edges and weights:
> - 0–2: 6
> - 0–1: 2
> - 2–3: 8
> - 1–3: 5
> - 3–4: 10
> - 3–5: 15
> - 4–6: 2
> - 5–6: 6
>
> Find: shortest path from vertex **0** to vertex **6**.

---

*End of Lecture 11 — Graphs*