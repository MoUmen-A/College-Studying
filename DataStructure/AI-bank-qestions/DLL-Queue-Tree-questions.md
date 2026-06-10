# Question Bank — Doubly Linked List, Queues & Trees
**Generated from:** `04-Doubly-Linked-List.md` · `06-Queues.txt` · `07-Trees.md`
**Calibrated against:** `23-spring.txt` · `25-spring`
**Course:** CCS2401 — Data Structures & Algorithms | Dr. Ahmed Said

---

## Section 1 — Topic Summary

### Doubly Linked List
- Each node has `data`, `next` (successor pointer), and `prev` (predecessor pointer).
- `head` → first node (prev = NULL). `tail` → last node (next = NULL).
- Advantage over singly linked list: **bidirectional traversal** (can go forward and backward).
- Key operations: `InsertAtStart`, `InsertAtEnd`, `InsertAt(x, p)`, `InsertAfter(x, p)`, `Delete(p)`, `Locate(x)`, `Retrieve(p)`, `PrintList`.
- **InsertAtStart**: new node's `next = head`; `head->prev = newNode`; `head = newNode`. Handle empty list (set tail = head).
- **InsertAtEnd**: new node's `prev = tail`; `tail->next = newNode`; `tail = newNode`. Handle empty list (set head = tail).
- **Delete(p)**: update `p->prev->next` and `p->next->prev`; update head/tail if needed; then `delete p`.
- Application functions: `Sum()`, `Reverse()`, `Split()` (odd/even).

### Queues
- **FIFO** — First In, First Out. Insertion at **rear** (enqueue); deletion from **front** (dequeue).
- Operations: `enqueue`, `dequeue`, `front`, `isEmpty`, `isFull`, `length`.
- **Linked-list implementation**: front and rear pointers. Enqueue adds to rear; dequeue removes from front.
  - Both enqueue and dequeue: **O(1)** time and space.
- **Array implementation** — Naïve: shift elements on dequeue → O(n) — **inefficient**.
- **Circular Array**: rear = (rear + 1) % MAX_SIZE; front = (front + 1) % MAX_SIZE. Avoids wasted space.
  - Use a `size` counter to distinguish full from empty.
- Real-world uses: print queues, CPU scheduling, bank counters, BFS traversal.

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
- **True/False (Q1)**: Real-world application matching ("Queue is used to undo/redo" — False, that's a Stack).
- **Code completion (Q1.3 in 25-spring)**: A function with a missing line/lines — identify and fill. *Very likely to appear.*
- **Independent coding functions (Q2 in 25-spring)**: 3–5 marks each — write a standalone method from scratch (e.g., `PrintReversed()`, `NewDelete()`, `MoveNegEnd()`).
- **Link-based ADT Implementation (Q4.1 in 23-spring)**: "Implement the link-based ADT Queue" — full class, constructor, enqueue, dequeue.
- Questions are grouped by data structure; expect multi-part questions combining linked list + tree or queue + stack.

---

## Section 3 — Question Bank

---

### 1. Multiple Choice (MCQ)

---

#### Q1 — MCQ | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**
Which of the following is the **main advantage** of a Doubly Linked List over a Singly Linked List?

- A) It uses less memory per node.
- B) It allows traversal in **both** forward and backward directions.
- C) It allows random access to elements in O(1).
- D) Insertion at the end is faster.

**Guide answer:**
**B** — Each node in a doubly linked list has both `next` and `prev` pointers, enabling bidirectional traversal (e.g., rewind in media players). Singly linked lists only support forward traversal.

**Key points to include for Full Marks:**
- Name both pointers: `next` (successor) and `prev` (predecessor).
- Give a real-world example: rewind/replay for media files.

**Common mistakes to avoid:**
A is wrong — doubly linked list uses **more** memory (extra `prev` pointer per node). C is wrong — linked lists never support O(1) random access.

---

#### Q2 — MCQ | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**
A queue follows which order for insertion and deletion?

- A) LIFO — Last In, First Out
- B) FIFO — First In, First Out
- C) Random order
- D) FILO — First In, Last Out

**Guide answer:**
**B** — A Queue is **First In, First Out**: elements are enqueued at the rear and dequeued from the front. LIFO describes a Stack.

**Key points to include for Full Marks:**
- State enqueue = rear, dequeue = front.
- Contrast with Stack (LIFO).

---

#### Q3 — MCQ | Bloom's: Understand | Difficulty: Easy | Marks: 2

**Question:**
In a **Circular Queue** implemented with an array of size `MAX_SIZE`, after enqueuing an element the rear index is updated as:

- A) `rear = rear + 1`
- B) `rear = (rear - 1) % MAX_SIZE`
- C) `rear = (rear + 1) % MAX_SIZE`
- D) `rear = rear % MAX_SIZE + 1`

**Guide answer:**
**C** — The modulo operation `(rear + 1) % MAX_SIZE` ensures the index wraps around to 0 after reaching the last position, implementing the circular behavior.

**Key points to include for Full Marks:**
- The `% MAX_SIZE` is the key detail. Without it, the index goes out of bounds.
- Same logic applies to front: `front = (front + 1) % MAX_SIZE`.

**Common mistakes to avoid:**
A gives a linear (non-circular) queue — the rear eventually exceeds the array bounds.

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

#### Q7 — MCQ | Bloom's: Analyse | Difficulty: Hard | Marks: 2

**Question:**
Which statement about the **naïve array implementation of a queue** is TRUE?

- A) Enqueue is O(n) because elements must shift.
- B) Dequeue is O(n) because all remaining elements must shift one position forward.
- C) Both enqueue and dequeue are O(1).
- D) Dequeue is O(log n) using binary search.

**Guide answer:**
**B** — In the naïve implementation, the front index is fixed at 0. When dequeuing, **all remaining elements shift left by one**, making dequeue **O(n)**. Enqueue remains O(1) since it just places at rear. This is why the circular array implementation was introduced.

**Key points to include for Full Marks:**
- Naïve = fixed front → shift on dequeue → O(n).
- Circular array fixes this: both enqueue and dequeue become O(1).

---

### 2. Fill-in-the-blank

---

#### Q8 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
In a doubly linked list, the first node's `prev` pointer is set to ________, and the last node's `next` pointer is set to ________.

**Guide answer:** **nullptr (NULL)** ; **nullptr (NULL)**

---

#### Q9 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
In a queue, elements are **inserted** at the ________ and **removed** from the ________.

**Guide answer:** **rear (back/end)** ; **front**

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

#### Q13 — Short Answer | Bloom's: Understand | Difficulty: Easy | Marks: 3

**Question:**
List **four** real-world applications of queues and explain why the queue data structure fits each one.

**Guide answer:**

| Application | Why Queue? |
|-------------|-----------|
| **Print queue** | Print jobs are processed in the order they arrive (FIFO — first sent, first printed). |
| **CPU scheduling** | Processes waiting for CPU time are served in arrival order (FIFO). |
| **Bank counter / ticket systems** | Customers are served in the order they arrive. |
| **BFS graph traversal** | Nodes are explored level by level; each discovered neighbor is enqueued and processed in order. |

**Key points to include for Full Marks:**
- Each application must be linked to the FIFO property explicitly.
- At least 4 applications named.

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

#### Q15 — Short Answer | Bloom's: Understand | Difficulty: Medium | Marks: 4

**Question:**
Explain the **problem with the naïve array implementation** of a queue and how the **circular array** solves it. Draw a small example.

**Guide answer:**

**Problem with naïve implementation:**
The front index is fixed at 0. Every dequeue requires **shifting all remaining elements left by one position** → O(n) time. Eventually, even if there is space at the front, the rear cannot wrap back, wasting memory.

```
Naïve: after 2 dequeues from [5|6|7|8]:
[_|_|7|8]   Front=0 (fixed), Rear=3
→ But positions 0 and 1 are wasted
```

**Circular array solution:**
Both front and rear indices **wrap around** using modulo arithmetic:
- `rear = (rear + 1) % MAX_SIZE`
- `front = (front + 1) % MAX_SIZE`

```
Circular (size=4): [_|_|7|8] → Front=2, Rear=3
After Enqueue(9):  [9|_|7|8] → Rear wraps to 0
After Enqueue(10): [9|10|7|8] → Rear=1 (full, size=4)
```

A `size` counter distinguishes empty (size=0) from full (size=MAX_SIZE).

**Key points to include for Full Marks:**
- Name the problem: O(n) dequeue due to shifting.
- State the circular fix: modulo operation on both front and rear.
- Mention `size` counter to detect empty vs full.

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

#### Q17 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 2

**Question:**
*"A Circular Queue data structure is used to enable undo and redo operations in applications like text editors."*
True or False? Justify and name the correct data structure.

*(Based directly on 23-spring Q1)*

**Guide answer:**
**FALSE.**
Undo/redo operations require remembering the **history** of actions and reversing them in last-in-first-out order. This is handled by a **Stack** (LIFO), not a Queue. Specifically, two stacks are used: one for undo history and one for redo history. A Circular Queue is used for resource management (CPU scheduling, print queues).

**Key points to include for Full Marks:**
- State FALSE and correct structure = **Stack**.
- Briefly explain why: undo reverses the most recent action → LIFO.
- Mention what Circular Queue IS used for.

---

#### Q18 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 2

**Question:**
*"Web browsers use a stack to keep track of the web pages you visit."*
True or False? Justify.

*(Taken directly from 23-spring Q1)*

**Guide answer:**
**TRUE.**
When you navigate to a new page, it is **pushed** onto the stack. When you press the **Back** button, the current page is **popped** off the stack and you return to the previous page. This is LIFO behavior — the most recently visited page is the first one returned to. A second stack handles the Forward button (redo stack).

**Key points to include for Full Marks:**
- Confirm TRUE and link the behavior to push/pop.
- Explain Back = pop, Forward = second stack.

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

#### Q20 — True/False | Bloom's: Analyse | Difficulty: Medium | Marks: 3

**Question:**
*"In a doubly linked list, deleting the head node requires no special handling beyond updating the `next` pointer."*
True or False? Justify with reference to what must actually be updated.

**Guide answer:**
**FALSE.**
When deleting the head node, the following must be handled:
1. Update `head = head->next` (move head forward).
2. If the new head is not null, set `newHead->prev = nullptr` (to remove the dangling backward pointer to the deleted node).
3. If the list becomes empty after deletion (only one node existed), also set `tail = nullptr`.
4. Call `delete` on the old head node to free memory.

Simply updating the `next` pointer of some external variable is insufficient — failing to clear `newHead->prev` leaves a dangling pointer, and forgetting to update `tail` on a single-node list leaves `tail` pointing to freed memory.

**Key points to include for Full Marks:**
- All 4 steps mentioned.
- Specifically mention the `prev = nullptr` fix and the empty-list edge case.

---

### 5. Application (Code / Scenario)

---

#### Q21 — Application | Bloom's: Apply | Difficulty: Easy | Marks: 4

**Question:**
Using the `DoublyList` class from the lecture, implement the function:

```cpp
ElementType Sum(DoublyList L)
```

that calculates and returns the **sum of all values** in the doubly linked list.

**Guide answer:**

```cpp
ElementType Sum(DoublyList L) {
    Position curr = L.First();   // start at head
    ElementType s = 0;
    while (curr != nullptr) {
        ElementType x = L.Retrieve(curr);
        s = s + x;
        curr = L.Next(curr);     // move to next node
    }
    return s;
}
```

**Trace example** — List: 10 → 20 → 40 → 55 → 70:
- s = 0 + 10 = 10
- s = 10 + 20 = 30
- s = 30 + 40 = 70
- s = 70 + 55 = 125
- s = 125 + 70 = 195
- curr = nullptr → return **195** ✓

**Key points to include for Full Marks:**
- Start with `L.First()` (not `head` directly — use the ADT interface).
- Use `L.Retrieve(curr)` to get data value.
- Use `L.Next(curr)` to advance (not `curr->next` — use the ADT interface).
- Null check: loop condition `curr != nullptr`.

**Common mistakes to avoid:**
- Accessing `curr->data` directly instead of `L.Retrieve(curr)` (bypasses ADT encapsulation).
- Starting with s = some non-zero value.
- Forgetting the loop termination condition.

---

#### Q22 — Application | Bloom's: Apply | Difficulty: Medium | Marks: 5

**Question:**
Implement the **`InsertAtEnd`** and **`Delete`** member functions for the `DoublyList` class. Your `Delete` must correctly handle all three cases: deleting the head, the tail, and a middle node.

```cpp
class DoublyList {
private:
    Position head;
    Position tail;
    int counter;
public:
    void InsertAtEnd(ElementType x);
    void Delete(Position p);
    // ... other members
};
```

**Guide answer:**

```cpp
void DoublyList::InsertAtEnd(ElementType x) {
    Position newNode = new Node;
    newNode->data = x;
    newNode->next = nullptr;
    newNode->prev = tail;          // link back to current tail
    if (tail != nullptr) {
        tail->next = newNode;      // current tail points forward to new node
    }
    tail = newNode;                // update tail
    if (head == nullptr) {
        head = tail;               // empty list: head = tail = new node
    }
    counter++;
}

void DoublyList::Delete(Position p) {
    if (p == nullptr) return;      // nothing to delete

    // Update tail if deleting the last node
    if (p == tail) {
        tail = p->prev;
    }
    // Update head if deleting the first node
    if (p == head) {
        head = p->next;
    }
    // Stitch neighbors together
    if (p->prev != nullptr) {
        p->prev->next = p->next;   // bypass p going forward
    }
    if (p->next != nullptr) {
        p->next->prev = p->prev;   // bypass p going backward
    }
    delete p;
    counter--;
}
```

**Key points to include for Full Marks:**
- `InsertAtEnd`: set `newNode->prev = tail` AND `tail->next = newNode`. Handle empty list.
- `Delete`: update BOTH `head` and `tail` if needed (check both separately, not else-if).
- Null-guard `p->prev != nullptr` before accessing `p->prev->next`.
- Null-guard `p->next != nullptr` before accessing `p->next->prev`.
- Call `delete p` and decrement `counter`.

**Common mistakes to avoid:**
- Using `else if` for head/tail checks — a one-node list is BOTH head and tail; both must be updated.
- Forgetting `delete p` → memory leak.
- Not handling the empty list in `InsertAtEnd` (tail was null → head also needs to be set).

---

#### Q23 — Application | Bloom's: Apply | Difficulty: Medium | Marks: 5

**Question:**
Implement the **link-based Queue ADT** — write the complete class with: constructor, `enqueue`, `dequeue`, and `isEmpty`.

*(23-spring Q4.1 — implement the link-based ADT Queue)*

**Guide answer:**

```cpp
class Node {
public:
    int data;
    Node* next;
    Node(int d) : data(d), next(nullptr) {}
};

class Queue {
private:
    Node* front;
    Node* rear;
    int size;
public:
    Queue() : front(nullptr), rear(nullptr), size(0) {}

    bool isEmpty() {
        return size == 0;
    }

    void enqueue(int data) {
        Node* newNode = new Node(data);
        if (isEmpty()) {
            front = rear = newNode;   // first element: both front and rear
        } else {
            rear->next = newNode;     // link new node at the back
            rear = newNode;           // advance rear
        }
        size++;
    }

    int dequeue() {
        if (isEmpty()) {
            return -1;                // queue is empty — error sentinel
        }
        Node* temp = front;
        front = front->next;          // move front forward
        int data = temp->data;
        delete temp;
        size--;
        if (isEmpty()) {
            rear = nullptr;           // list is now empty; reset rear
        }
        return data;
    }

    int length() {
        return size;
    }

    ~Queue() {
        while (!isEmpty()) dequeue(); // clean up all nodes
    }
};
```

**Key points to include for Full Marks:**
- `enqueue`: handle empty queue (front = rear = newNode). Otherwise: `rear->next = newNode`, `rear = newNode`.
- `dequeue`: save `front`, advance `front = front->next`, `delete temp`. If now empty, reset `rear = nullptr`.
- Destructor: loop `dequeue()` until empty to free all memory.
- `isEmpty()` checks `size == 0`.

**Common mistakes to avoid:**
- In dequeue: forgetting to set `rear = nullptr` when queue becomes empty → `rear` dangling pointer.
- In enqueue: forgetting to advance `rear = newNode` after linking.
- Memory leak: no destructor or forgetting `delete temp`.

---

#### Q24 — Application | Bloom's: Apply | Difficulty: Medium | Marks: 5

**Question:**
Write a member function `void queueList::PrintReversed()` that prints the elements of a queue in **reversed order** without destroying the contents of the queue. For example, if 5, 6, 2, 7, 3 were inserted, the function prints: `3 7 2 6 5`.

*(Taken directly from 25-spring Q2.3)*

**Guide answer:**

```cpp
void Queue::PrintReversed() {
    // Use a stack to reverse the queue
    Stack<int> s;  // or: std::stack<int> s;

    // Step 1: Dequeue everything into a stack (and a temp queue to restore)
    Queue temp;
    while (!isEmpty()) {
        int val = dequeue();
        s.push(val);
        temp.enqueue(val);
    }

    // Step 2: Restore original queue from temp
    while (!temp.isEmpty()) {
        enqueue(temp.dequeue());
    }

    // Step 3: Print from stack (reversed order)
    while (!s.empty()) {
        cout << s.top() << " ";
        s.pop();
    }
    cout << endl;
}
```

**Alternatively (simpler — using only a stack and re-enqueue from stack):**

```cpp
void Queue::PrintReversed() {
    std::stack<int> s;
    Node* curr = front;
    // Traverse without dequeuing — just read values into stack
    while (curr != nullptr) {
        s.push(curr->data);
        curr = curr->next;
    }
    // Print stack (reversed order), queue untouched
    while (!s.empty()) {
        cout << s.top() << " ";
        s.pop();
    }
    cout << endl;
}
```

**Key points to include for Full Marks:**
- Queue contents must be **preserved** (do not permanently dequeue and not restore).
- Stack used as auxiliary structure to reverse the order.
- Traversal approach: iterate node-by-node without modifying the queue, push each value to stack, then pop.
- Print all elements separated by spaces.

**Common mistakes to avoid:**
- Permanently dequeuing without restoring — this destroys the queue (violates the requirement).
- Printing in original order instead of reversed — stack reversal is the key mechanism.

---

#### Q25 — Application | Bloom's: Analyse | Difficulty: Hard | Marks: 6

**Question:**
Using ADT Doubly Linked List, implement `void NewDelete(DoublyList& L)` that **deletes all nodes with values greater than the average** of all values in the list. You must first implement `float avg(DoublyList L)`.

*(Taken directly from 25-spring Q2.4)*

**Guide answer:**

```cpp
float avg(DoublyList L) {
    Position curr = L.First();
    float sum = 0;
    int count = 0;
    while (curr != nullptr) {
        sum += L.Retrieve(curr);
        count++;
        curr = L.Next(curr);
    }
    if (count == 0) return 0;
    return sum / count;
}

void NewDelete(DoublyList& L) {
    float average = avg(L);
    Position curr = L.First();
    while (curr != nullptr) {
        Position nextNode = L.Next(curr);  // save next BEFORE potential deletion
        if (L.Retrieve(curr) > average) {
            L.Delete(curr);                // deletes the node
        }
        curr = nextNode;                   // move to saved next
    }
}
```

**Trace example** — List: 10 → 20 → 40 → 55 → 70
- avg = (10+20+40+55+70)/5 = 195/5 = **39.0**
- 10 ≤ 39 → keep
- 20 ≤ 39 → keep
- 40 > 39 → **delete**
- 55 > 39 → **delete**
- 70 > 39 → **delete**
- Result: 10 → 20

**Key points to include for Full Marks:**
- `avg()` must traverse the full list and divide correctly (use `float`, not `int` division).
- In `NewDelete`: save `nextNode = L.Next(curr)` **BEFORE** deleting `curr` — after deletion, `curr` is freed memory.
- Use `L.Delete(curr)` through the ADT interface.
- Handle empty list in `avg()` (return 0, avoid division by zero).

**Common mistakes to avoid:**
- Not saving `nextNode` before deletion → accessing freed memory → undefined behavior (most common mark deduction).
- Integer division in avg: `sum / count` where both are `int` truncates the result — declare sum as `float`.
- Deleting nodes while iterating without advance-pointer save.

---

#### Q26 — Application | Bloom's: Create | Difficulty: Hard | Marks: 8

**Question:**
Implement the **Circular Array Queue** — write the complete class with: constructor, `enqueue`, `dequeue`, `isEmpty`, `isFull`.

**Guide answer:**

```cpp
const int MAX_SIZE = 100;

class Queue {
private:
    int data[MAX_SIZE];
    int front;
    int rear;
    int size;
public:
    Queue() : front(-1), rear(-1), size(0) {}

    bool isEmpty() { return size == 0; }

    bool isFull() { return size == MAX_SIZE; }

    int length() { return size; }

    void enqueue(int val) {
        if (isFull()) {
            cout << "Queue is full." << endl;
            return;
        }
        rear = (rear + 1) % MAX_SIZE;    // circular advance
        data[rear] = val;
        if (front == -1) front = 0;      // first element: initialize front
        size++;
    }

    int dequeue() {
        if (isEmpty()) {
            cout << "Queue is empty." << endl;
            return -1;
        }
        int val = data[front];
        front = (front + 1) % MAX_SIZE;  // circular advance
        size--;
        if (isEmpty()) {
            front = rear = -1;           // reset to initial state
        }
        return val;
    }
};
```

**Key points to include for Full Marks:**
- `enqueue`: `rear = (rear + 1) % MAX_SIZE` — the modulo is the core circular mechanism.
- `dequeue`: `front = (front + 1) % MAX_SIZE`. Reset both to -1 when queue becomes empty.
- `isFull`: check `size == MAX_SIZE` (NOT `rear + 1 == front` — that's ambiguous without size counter).
- `isEmpty`: check `size == 0`.

**Common mistakes to avoid:**
- Forgetting `% MAX_SIZE` → goes out of bounds.
- Using `rear == front` to detect full/empty — ambiguous without a size counter.
- Not resetting front/rear to -1 when empty — leaves stale index state.

---

### 6. Compare & Contrast

---

#### Q27 — Compare & Contrast | Bloom's: Analyse | Difficulty: Medium | Marks: 5

**Question:**
Compare **Singly Linked List**, **Doubly Linked List**, and **Array-based List** across: traversal direction, insertion/deletion ease, memory usage, and random access.

**Guide answer:**

| Criterion | Array-based List | Singly Linked List | Doubly Linked List |
|-----------|-----------------|-------------------|-------------------|
| Traversal | Forward only | Forward only | **Both forward & backward** |
| Insertion/Deletion | Hard — requires shifting elements; O(n) | Easy — update pointers; O(1) at known position | Easy — update pointers; O(1) at known position |
| Memory per node | Minimal (data only) | Moderate (data + 1 pointer) | Higher (data + 2 pointers: prev + next) |
| Random access (get i-th) | **O(1)** — direct index | O(n) — must traverse | O(n) — must traverse |
| Requires knowing size? | Yes (fixed capacity) | No (dynamic) | No (dynamic) |
| Can go backward? | Yes (by index) | **No** | **Yes** |

**Key points to include for Full Marks:**
- All 4 criteria addressed for all 3 structures.
- Highlight doubly linked list's unique backward traversal advantage.
- Note the extra memory cost of the `prev` pointer in doubly linked lists.

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

### 7. Essay / Long Answer

---

#### Q29 — Essay | Bloom's: Create | Difficulty: Hard | Marks: 10

**Question:**
**(a)** Implement the `void Split(DoublyList L, DoublyList& lOdd, DoublyList& lEven)` function that splits a doubly linked list into two: one containing **odd-indexed** elements and one containing **even-indexed** elements (0-indexed: index 0 is even, index 1 is odd, etc.).

**(b)** Then, implement `List Merge(List L1, List L2)` that merges two doubly linked lists by alternating elements: L1[0], L2[0], L1[1], L2[1], … If one list runs out, append the rest of the other.

**(c)** Write a `main` function that: creates a list with values 10, 20, 30, 40, 50; splits it; prints lEven and lOdd; then merges them back and prints the result.

**Guide answer:**

**(a) Split by Index:**

```cpp
void Split(DoublyList L, DoublyList& lOdd, DoublyList& lEven) {
    Position curr = L.First();
    int index = 0;
    while (curr != nullptr) {
        int x = L.Retrieve(curr);
        if (index % 2 == 0)
            lEven.InsertAtEnd(x);   // index 0, 2, 4, ... → even
        else
            lOdd.InsertAtEnd(x);    // index 1, 3, 5, ... → odd
        index++;
        curr = L.Next(curr);
    }
}
```

**(b) Merge alternating:**

```cpp
DoublyList Merge(DoublyList L1, DoublyList L2) {
    DoublyList result;
    Position p1 = L1.First();
    Position p2 = L2.First();
    while (p1 != nullptr || p2 != nullptr) {
        if (p1 != nullptr) {
            result.InsertAtEnd(L1.Retrieve(p1));
            p1 = L1.Next(p1);
        }
        if (p2 != nullptr) {
            result.InsertAtEnd(L2.Retrieve(p2));
            p2 = L2.Next(p2);
        }
    }
    return result;
}
```

**(c) Main function:**

```cpp
int main() {
    DoublyList L, lEven, lOdd;
    L.InsertAtEnd(10);
    L.InsertAtEnd(20);
    L.InsertAtEnd(30);
    L.InsertAtEnd(40);
    L.InsertAtEnd(50);

    Split(L, lOdd, lEven);

    cout << "Even-indexed: "; lEven.PrintList(); // 10 -> 30 -> 50
    cout << "Odd-indexed:  "; lOdd.PrintList();  // 20 -> 40

    DoublyList merged = Merge(lEven, lOdd);
    cout << "Merged: "; merged.PrintList();       // 10 -> 20 -> 30 -> 40 -> 50
    return 0;
}
```

**Expected output:**
```
Even-indexed: 10 -> 30 -> 50
Odd-indexed:  20 -> 40
Merged: 10 -> 20 -> 30 -> 40 -> 50
```

**Key points to include for Full Marks:**
- Split: use an `index` counter and `% 2` to separate by position (not by value).
- Merge: advance both pointers simultaneously; handle unequal lengths by continuing with the longer list.
- ADT interface: use `InsertAtEnd`, `Retrieve`, `Next`, `First` throughout — do not access `->data` directly.
- Main: correct insertion order and correct output traces.

**Common mistakes to avoid:**
- Splitting by value (`x % 2`) instead of by index — the question asks for index-based split.
- Stopping Merge when the shorter list ends — must continue with the remaining elements.
- Forgetting `lEven` and `lOdd` must be passed by **reference** (`DoublyList&`) to retain changes.

---

#### Q30 — Essay | Bloom's: Create | Difficulty: Hard | Marks: 10

**Question:**
Design and implement a **Circular Array Queue** that also supports a **Palindrome Checker** function. The palindrome checker:
1. Reads a string character by character into the queue.
2. Uses both the queue and a stack to compare characters.
3. Returns `true` if the string is a palindrome, `false` otherwise.

Test it with: `"rotator"` (palindrome) and `"data"` (not palindrome).

*(Adapted from 06-Queues.txt assignment)*

**Guide answer:**

```cpp
#include <iostream>
#include <stack>
#include <string>
using namespace std;

const int MAX_SIZE = 100;

class Queue {
private:
    char data[MAX_SIZE];
    int front, rear, size;
public:
    Queue() : front(-1), rear(-1), size(0) {}
    bool isEmpty() { return size == 0; }
    bool isFull()  { return size == MAX_SIZE; }

    void enqueue(char c) {
        if (isFull()) return;
        rear = (rear + 1) % MAX_SIZE;
        data[rear] = c;
        if (front == -1) front = 0;
        size++;
    }

    char dequeue() {
        if (isEmpty()) return '\0';
        char c = data[front];
        front = (front + 1) % MAX_SIZE;
        size--;
        if (isEmpty()) { front = rear = -1; }
        return c;
    }
};

bool isPalindrome(const string& str) {
    Queue q;
    stack<char> s;

    // Step 1: Load all characters into both queue and stack
    for (char c : str) {
        q.enqueue(c);
        s.push(c);
    }

    // Step 2: Compare front of queue with top of stack
    while (!q.isEmpty()) {
        char fromQueue = q.dequeue();  // reads front-to-back
        char fromStack = s.top();      // reads back-to-front
        s.pop();
        if (fromQueue != fromStack)
            return false;
    }
    return true;
}

int main() {
    string s1 = "rotator";
    string s2 = "data";
    cout << s1 << " is " << (isPalindrome(s1) ? "" : "not ") << "a palindrome." << endl;
    cout << s2 << " is " << (isPalindrome(s2) ? "" : "not ") << "a palindrome." << endl;
    return 0;
}
```

**Expected output:**
```
rotator is a palindrome.
data is not a palindrome.
```

**Why it works:**
- Queue reads characters **front-to-back** (original order).
- Stack reads characters **back-to-front** (reversed order).
- If every front-queue character matches every top-stack character → string reads the same forwards and backwards → palindrome.

**Key points to include for Full Marks:**
- Both queue AND stack loaded simultaneously in one pass.
- Dequeue from queue (front) compared against pop from stack (back).
- Correct circular array implementation (modulo on front and rear).
- Test both cases (palindrome and non-palindrome).

---

## Section 4 — Study Tips & Weak Areas

| Weak Area | Why Students Lose Marks | Fix |
|-----------|------------------------|-----|
| **Delete in doubly linked list** | Forgetting to update both `head` AND `tail`; not null-guarding `p->prev` and `p->next` | Always check: is p the head? is p the tail? Then stitch: `p->prev->next = p->next` AND `p->next->prev = p->prev`. |
| **Advance pointer before deletion** | Using `curr = L.Next(curr)` AFTER `L.Delete(curr)` — curr is freed memory | Always: `Position next = L.Next(curr); L.Delete(curr); curr = next;` |
| **Circular queue modulo** | Writing `rear = rear + 1` instead of `rear = (rear + 1) % MAX_SIZE` | The `% MAX_SIZE` is mandatory — without it the index goes out of bounds. |
| **Binary tree types** | Confusing Full / Complete / Perfect | Mnemonic: Full = 0 or 2 children; Complete = left-packed; Perfect = symmetric all-same-level leaves. |
| **Tree construction from traversals** | Not recursively splitting Inorder after each root identification | Pre-order[0] = root. Find root in Inorder. Count left-subtree nodes. Slice Pre-order accordingly. |
| **Post-order traversal** | Putting root in the middle instead of at the end | Post = Left, Right, **Root**. Root is ALWAYS last. |
| **avg() with int division** | `(10+20)/2 = 15` (correct) but `(10+25)/2 = 17` instead of 17.5 — truncation error | Always declare sum as `float`. |
| **Queue's rear after empty** | Not resetting `rear = nullptr` (or -1) after dequeuing the last element | In dequeue: `if (isEmpty()) { rear = nullptr; front = nullptr; }` |

---

## Section 5 — Coverage Gap Analysis

### Concepts in lectures not yet covered in this question bank:

| Concept | From Lecture | Suggested Question |
|---------|-------------|-------------------|
| `InsertAfter(x, p)` implementation | `04-Doubly-Linked-List.md` | "Implement `InsertAfter(x, p)` that inserts value x immediately after position p. Handle the case when p is the tail." |
| `Locate(x)` + `Retrieve(p)` usage pattern | `04-Doubly-Linked-List.md` | "Write a function that finds and deletes the first occurrence of value x from a doubly linked list." |
| Queue **Palindrome Checker** (standalone) | `06-Queues.txt` assignment | Already covered in Q30 above. |
| **Queue Reverse** (without extra data structure) | `06-Queues.txt` assignment | "Write a function to reverse a queue without using any other data structure. Hint: use recursion." |
| **Expression Tree** traversal (postfix/prefix derivation) | `07-Trees.md` | "Given the expression `A * B / (C + D * E)`, build the expression tree and derive its prefix (pre-order) and postfix (post-order) representations." |
| **Level, Depth, Height** calculation worksheet | `07-Trees.md` | "For each node in the given tree, calculate its level, depth, and height." |
| **Degenerate/Skewed tree** worst case | `07-Trees.md` | "Inserting 1, 2, 3, 4, 5 in order into a BST produces a skewed tree. Draw it and state why this is the worst case for search." |

### 🔔 Reminder — Lecture files still missing:
The following lectures are NOT yet in `d:\Gam3a\Exam-Creation\DataStructure\Lec\`:
- **Lectures 01, 02, 03** — likely Arrays, Stacks, Singly Linked List basics.
- **Lectures 05** — likely Circular Linked List or Stack applications.
- **Lectures 09, 10** — likely **AVL Trees** and Heap/Priority Queue.

> **AVL Trees appear in BOTH previous exams** (23-spring Q4 and 25-spring Q3 — full 10-mark questions). Upload the AVL lecture immediately and re-run to generate AVL rotation questions (LL, RR, LR, RL insertions/deletions with full step-by-step drawings).
