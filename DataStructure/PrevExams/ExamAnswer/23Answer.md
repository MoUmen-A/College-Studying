# Exam Answers — CCS2401 Data Structures & Algorithms
**Course:** CCS2401 — Data Structures & Algorithms | Dr. Ahmed Said  
**Calibrated against:** `DSA-instruction.md`

---

# 23‑Spring Exam Answers

## Question 1 — True / False [10 Points]

| # | Statement | Answer | Correction |
|---|-----------|--------|------------|
| 1 | On social media sites, we use **directed graphs** to track user data (recommendations, etc.) | ✓ | — |
| 2 | **Queue** data structure is used to evaluate expressions in infix, postfix, and prefix notations | ✗ | **Stack** is used for expression evaluation (operators are pushed/popped based on precedence). |
| 3 | **Web browsers** use a stack to keep track of visited web pages | ✓ | — |
| 4 | **Circular Queue** is used to enable undo and redo operations | ✗ | **Two Stacks** are used for undo/redo (one for undo history, one for redo history). |
| 5 | **AVL tree** can be used in navigation systems where both forward and backward traversal is required | ✗ | **Doubly Linked List** supports forward and backward traversal. AVL tree is a self‑balancing BST used for fast search. |
| 6 | **BST** is used to store function calls and their states | ✗ | A **Stack** (call stack) stores function calls and their states, enabling recursive function calls. |
| 7 | **Queues** can be used to manage and allocate resources such as printers or CPU processing time | ✓ | — |
| 8 | The **breadth‑first search** algorithm uses a **stack** to explore nodes in a graph | ✗ | BFS uses a **Queue**. DFS uses a Stack. |
| 9 | **BST** is used for storing hierarchical data like folder structure, XML/HTML | ✓ | — |
| 10 | **BST** is used to implement efficient search algorithms | ✓ | — |

---

## Question 2 — Polynomial Representation [10 Points]

### 2.1 PolyList Implementation

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

struct term {
    float coeff;
    int   pow;
};

class polyList {
private:
    term *poly;
    int   last;
    int   capacity;

public:
    polyList(int size) {
        poly     = new term[size];
        last     = -1;
        capacity = size;
    }

    // a) Insert a new term at the end
    void insertAtEnd(float coeff, int pow) {
        if (last + 1 >= capacity) return; // overflow guard
        last++;
        poly[last].coeff = coeff;
        poly[last].pow   = pow;
    }

    // b) Display the polynomial (e.g. 5.6x^2 + 7x + 89)
    void display() const {
        for (int i = 0; i <= last; i++) {
            if (poly[i].pow == 0)
                cout << poly[i].coeff;
            else if (poly[i].pow == 1)
                cout << poly[i].coeff << "x";
            else
                cout << poly[i].coeff << "x^" << poly[i].pow;
            if (i != last) cout << " + ";
        }
        cout << endl;
    }

    // c) Differentiate the polynomial (6x^2+7x+89 -> 12x+7)
    void differentiate() {
        for (int i = 0; i <= last; i++) {
            if (poly[i].pow == 0) {
                // constant term becomes 0, remove it
                for (int j = i; j < last; j++) poly[j] = poly[j + 1];
                last--;
                i--;
            } else {
                poly[i].coeff *= poly[i].pow;
                poly[i].pow--;
            }
        }
    }

    // d) Return the order (highest exponent)
    int order() const {
        int maxPow = 0;
        for (int i = 0; i <= last; i++)
            maxPow = max(maxPow, poly[i].pow);
        return maxPow;
    }
};

// e) Main function
int main() {
    polyList p(10);
    p.insertAtEnd(5.6f, 2);
    p.insertAtEnd(7.0f, 1);
    p.insertAtEnd(89.0f, 0);

    cout << "Polynomial: ";
    p.display();                               // 5.6x^2 + 7x + 89
    cout << "Order: " << p.order() << endl;   // 2

    p.differentiate();
    cout << "After differentiation: ";
    p.display();                               // 11.2x + 7
    cout << "New order: " << p.order() << endl; // 1

    return 0;
}
```

**Key points for full marks:**
- `insertAtEnd` must increment `last` before assigning (or use `poly[++last]`).
- `display()` must handle exponent = 0 (print constant only) and exponent = 1 (omit `^1`).
- `differentiate()` must **remove** constant terms (pow = 0 after differentiation → pow becomes −1 → remove).
- `order()` returns the maximum power in the list.

---

### 2.2 Stack‑based Decimal‑to‑Binary (x = 19)

```cpp
#include <stack>
using namespace std;

void Dec2Bin(int x) {
    stack<int> s;
    while (x > 0) {
        s.push(x % 2);
        x /= 2;
    }
    while (!s.empty()) {
        cout << s.top();
        s.pop();
    }
    cout << endl;
}
```

**Manual trace for x = 19:**

| Step | x | x % 2 | Push | Stack (bottom → top) |
|------|---|--------|------|----------------------|
| 1 | 19 | 1 | push 1 | [1] |
| 2 | 9 | 1 | push 1 | [1, 1] |
| 3 | 4 | 0 | push 0 | [1, 1, 0] |
| 4 | 2 | 0 | push 0 | [1, 1, 0, 0] |
| 5 | 1 | 1 | push 1 | [1, 1, 0, 0, 1] |
| 6 | 0 | — | stop | — |

**Pop all → Binary representation of 19 = `10011`**  
Verification: 1×16 + 0×8 + 0×4 + 1×2 + 1×1 = 19 ✓

---

## Question 3 — Directed Weighted Graph [10 Points]

**Graph edges:**
- A→B=2, A→C=7, A→E=12
- B→D=2
- C→B=3, C→D=1, C→E=2
- D→F=2
- E→A=4, E→G=7
- F→G=2
- G→D=1

### 3.1 Adjacency Matrix

|   | A | B | C | D | E | F | G |
|---|---|---|---|---|---|---|---|
| **A** | 0 | 2 | 7 | ∞ | 12 | ∞ | ∞ |
| **B** | ∞ | 0 | ∞ | 2 | ∞ | ∞ | ∞ |
| **C** | ∞ | 3 | 0 | 1 | 2 | ∞ | ∞ |
| **D** | ∞ | ∞ | ∞ | 0 | ∞ | 2 | ∞ |
| **E** | 4 | ∞ | ∞ | ∞ | 0 | ∞ | 7 |
| **F** | ∞ | ∞ | ∞ | ∞ | ∞ | 0 | 2 |
| **G** | ∞ | ∞ | ∞ | 1 | ∞ | ∞ | 0 |

*(∞ = no direct edge; 0 = self)*

---

### 3.2 Dijkstra's Algorithm (source = A)

| Step | Known Set | Selected | A | B | C | D | E | F | G |
|------|-----------|----------|---|---|---|---|---|---|---|
| Init | {} | — | **0** | ∞ | ∞ | ∞ | ∞ | ∞ | ∞ |
| 1 | {A} | A | 0 | **2** | **7** | ∞ | **12** | ∞ | ∞ |
| 2 | {A,B} | B | 0 | 2 | 7 | **4** | 12 | ∞ | ∞ |
| 3 | {A,B,D} | D | 0 | 2 | 7 | 4 | 12 | **6** | ∞ |
| 4 | {A,B,D,F} | F | 0 | 2 | 7 | 4 | 12 | 6 | **8** |
| 5 | {A,B,D,F,C} | C | 0 | 2 | 7 | 4 | **9** | 6 | 8 |
| 6 | {A,B,D,F,C,G} | G | 0 | 2 | 7 | 4 | 9 | 6 | 8 |
| 7 | {A,B,D,F,C,G,E} | E | 0 | 2 | 7 | 4 | 9 | 6 | 8 |

**Final shortest distances from A:**
- A → A = 0
- A → B = 2 (path: A→B)
- A → C = 7 (path: A→C)
- A → D = 4 (path: A→B→D)
- A → E = 9 (path: A→C→E)
- A → F = 6 (path: A→B→D→F)
- A → G = 8 (path: A→B→D→F→G)

### 3.3 Shortest path from A to F
**Path: A → B → D → F**  
**Length: 2 + 2 + 2 = 6**

### 3.4 Depth‑First Search from A (ascending edge order)
**DFS order: A, B, D, F, G, C, E**

---

## Question 4 — Queue Implementation & AVL Tree [10 Points]

### 4.1 Link‑based Queue Implementation

```cpp
struct QNode {
    int data;
    QNode* next;
    QNode(int d) : data(d), next(nullptr) {}
};

class Queue {
    QNode* front;
    QNode* rear;
    int    count;
public:
    Queue() : front(nullptr), rear(nullptr), count(0) {}

    bool isEmpty() const { return front == nullptr; }

    void enqueue(int x) {
        QNode* newNode = new QNode(x);
        if (rear) rear->next = newNode;
        rear = newNode;
        if (!front) front = rear;
        count++;
    }

    int dequeue() {
        if (isEmpty()) throw std::underflow_error("Queue is empty");
        int val = front->data;
        QNode* temp = front;
        front = front->next;
        if (!front) rear = nullptr;
        delete temp;
        count--;
        return val;
    }

    int getFront() const { return front->data; }
    int size()     const { return count; }
};
```

---

### 4.2 AVL Tree Manipulations

**Starting AVL tree:**
```
         40
        /  \
      20    60
     /  \   / \
   10   30 50  150
       /  \      \
      25  35     160
```

#### a) Insert 37 into the AVL tree

37 > 35, so insert as right child of 35.

After insertion, check balance factors upward:
- Node 30: left‑height=1 (25), right‑height=2 (35→37) → BF = -1 → **balanced**
- Node 20: left‑height=1 (10), right‑height=3 (30→35→37) → BF = -2 → **IMBALANCED** (RR case because 37 > 30 > 20)

Apply **RR Single Rotation** at node 20:

```
         40
        /  \
      30    60
     /  \   / \
   20   35 50  150
   / \    \      \
  10  25  37     160
```

#### b) Insert 33 into the original AVL tree

33 goes: 40→20→30→25→35 (33 < 35, left child of 35).

Check balance upward:
- Node 35: BF = 1 (left=1,right=0) → balanced
- Node 30: left‑height=2 (25→33), right‑height=1 (35) → BF = 1 → balanced
- Node 20: left‑height=1 (10), right‑height=3 (30→25→33) → BF = -2 → **IMBALANCED**
  - Right child 30, inserted in 30's **left** subtree (25→33) → **RL Double Rotation** at node 20

Apply **RL Double Rotation** at 20:

```
         40
        /  \
      30    60
     /  \   / \
   20   35 50  150
   / \  /        \
  10  25 33      160
```

#### c) Delete 40 from the original BST (no rebalancing needed for plain BST deletion)

Node 40 has two children → find **in‑order successor** (leftmost in right subtree of 40).  
Right subtree of 40 is rooted at 60; go left → 50 → 50 has no left child → **in‑order successor = 50**.

Copy 50 to root, delete original 50:

```
         50
        /  \
      20    60
     /  \     \
   10   30    150
       /  \      \
      25  35     160
```

#### d) Traversals of the original BST (before deletions)

**Inorder (L → Root → R):**  
`10, 20, 25, 30, 35, 40, 50, 60, 150, 160`

**Preorder (Root → L → R):**  
`40, 20, 10, 30, 25, 35, 60, 50, 150, 160`

**Postorder (L → R → Root):**  
`10, 25, 35, 30, 20, 50, 160, 150, 60, 40`

---
---
