# Question Bank — Queues
**Source lecture:** [`06-Queues.txt`](file:///d:/Gam3a/Exam-Creation/DataStructure/Lec/06-Queues.txt)
**Calibrated against:** [`23-spring.txt`](file:///d:/Gam3a/Exam-Creation/DataStructure/PrevExams/23-spring.txt) · [`25-spring`](file:///d:/Gam3a/Exam-Creation/DataStructure/PrevExams/25-spring)
**Course:** CCS2401 — Data Structures & Algorithms | Dr. Ahmed Said

---

## Section 1 — Topic Summary

- **Queue** = FIFO (First In, First Out). Like a checkout line at a store.
- **Operations**: `enqueue` (insert at rear), `dequeue` (remove from front), `front()`, `isEmpty()`, `isFull()`, `length()`.
- **Linked-list implementation**: `front` and `rear` node pointers. Both enqueue and dequeue are **O(1)**.
  - `enqueue`: create new node, `rear->next = newNode`, `rear = newNode`. If empty: `front = rear = newNode`.
  - `dequeue`: save `front`, advance `front = front->next`, delete old node. If now empty: `rear = nullptr`.
- **Array implementation — Naïve**: front fixed at index 0. Dequeue shifts all elements left → **O(n)**. Inefficient.
- **Circular Array**: `rear = (rear + 1) % MAX_SIZE`; `front = (front + 1) % MAX_SIZE`. Both O(1). Use `size` counter to distinguish full vs empty.
- **Applications**: print queue, CPU scheduling, bank counters, BFS traversal.

---

## Section 2 — Tone Analysis

From past exams:
- **23-spring Q4.1**: "Implement the link-based ADT Queue" — full class with constructor, enqueue, dequeue (10 marks shared with AVL).
- **25-spring Q2.3**: `PrintReversed()` — print queue elements in reverse without destroying the queue (3–5 marks).
- **23-spring Q1**: True/False items on queue vs stack applications.
- **23-spring Q2.2**: Stack-based Dec2Bin — stack/queue application question.
- Expect: full ADT implementation, application functions, and True/False on FIFO vs LIFO.

---

## Section 3 — Question Bank

### 1. Multiple Choice (MCQ)

---

#### Q1 — MCQ | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**
A queue follows which order for insertion and deletion?

- A) LIFO — Last In, First Out
- B) FIFO — First In, First Out
- C) Random order
- D) FILO — First In, Last Out

**Guide answer:**
**B** — Queue is FIFO: elements enter at the rear and leave from the front. Like a checkout line — first customer in is first served.

**Key points to include for Full Marks:**
- Enqueue = rear, Dequeue = front.
- Contrast with Stack (LIFO).

**Common mistakes to avoid:**
D (FILO) is another name for LIFO = Stack, not Queue.

---

#### Q2 — MCQ | Bloom's: Understand | Difficulty: Easy | Marks: 2

**Question:**
In a **Circular Queue** using an array of size `MAX_SIZE`, the rear index is updated on enqueue as:

- A) `rear = rear + 1`
- B) `rear = (rear - 1) % MAX_SIZE`
- C) `rear = (rear + 1) % MAX_SIZE`
- D) `rear = rear % MAX_SIZE + 1`

**Guide answer:**
**C** — The modulo operation `% MAX_SIZE` wraps the index back to 0 after reaching the last array position, implementing circular behavior.

**Key points to include for Full Marks:**
- Same formula applies to front on dequeue: `front = (front + 1) % MAX_SIZE`.
- Without `%`, the index goes out of bounds.

---

#### Q3 — MCQ | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
What is the **problem** with the naïve (non-circular) array implementation of a queue?

- A) Enqueue is O(n) because elements must shift.
- B) Dequeue is O(n) because all remaining elements shift one position forward.
- C) Both enqueue and dequeue are O(1).
- D) The queue cannot store more than 2 elements.

**Guide answer:**
**B** — In the naïve implementation, the front index is fixed at 0. Dequeue removes the front element and shifts **all remaining elements** left by one → **O(n)**. Enqueue is O(1) since it just places at rear. The circular array fixes this.

**Key points to include for Full Marks:**
- Name the fix: circular array with modulo arithmetic makes both O(1).

---

#### Q4 — MCQ | Bloom's: Analyse | Difficulty: Medium | Marks: 2

**Question:**
What will be the contents of the stack after the following operations (top shown last)?

`push(2), push(4), pop(), push(6), push(8)`

- A) [2, 4, 6, 8]
- B) [2, 6, 8]
- C) [2, 6]
- D) [8, 6, 2]

*(From 25-spring Q1.c — Stack/Queue operations)*

**Guide answer:**
**B** — Trace:
1. push(2) → [2]
2. push(4) → [2, 4]
3. pop() → remove 4 → [2]
4. push(6) → [2, 6]
5. push(8) → **[2, 6, 8]**

**Key points to include for Full Marks:**
- pop() removes the most recently pushed element (LIFO for stacks).
- Bottom of stack = 2, top = 8.

---

### 2. Fill-in-the-blank

---

#### Q5 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
In a queue, elements are **inserted** at the ________ and **removed** from the ________.

**Guide answer:** **rear (back/end)** ; **front**

---

#### Q6 — Fill-in-the-blank | Bloom's: Understand | Difficulty: Easy | Marks: 2

**Question:**
In a circular array queue, the formula to **wrap around** the rear index when enqueuing is:

`rear = (________ + 1) % ________`

**Guide answer:** **rear** ; **MAX_SIZE**

---

#### Q7 — Fill-in-the-blank | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
In the linked-list queue implementation, after dequeuing the last remaining element, we must reset ________ to `nullptr` to avoid a ________ pointer.

**Guide answer:** **rear** (and front) ; **dangling**

---

### 3. Short Answer

---

#### Q8 — Short Answer | Bloom's: Understand | Difficulty: Easy | Marks: 3

**Question:**
List **four** real-world applications of queues and explain why the queue (FIFO) structure fits each.

**Guide answer:**

| Application | Why Queue (FIFO)? |
|-------------|-------------------|
| **Print queue** | Jobs are printed in the order they are sent — first submitted, first printed. |
| **CPU scheduling** | Processes wait in a queue and are served in arrival order. |
| **Bank counter** | Customers are served in the order they arrive in line. |
| **BFS traversal** | Nodes are explored level by level; discovered neighbors are processed in order of discovery. |

**Key points to include for Full Marks:**
- Each application must explicitly link to the **FIFO** property.
- At least 4 distinct applications.

---

#### Q9 — Short Answer | Bloom's: Analyse | Difficulty: Medium | Marks: 4

**Question:**
Explain the **problem with the naïve array queue** and how the **circular array** solves it. Include a small diagram.

**Guide answer:**

**Problem — Naïve array:**
Front is always at index 0. Each dequeue requires shifting all elements left → **O(n)** per dequeue. Also, once the rear reaches the end of the array, space at the front (freed by dequeue) cannot be reused.

```
Naïve: [_|_|7|8]  → front always 0 → shift needed
        ^     ^
       front  rear
```

**Solution — Circular array:**
Both `front` and `rear` wrap around using: `index = (index + 1) % MAX_SIZE`. Freed space at the beginning can be reused when rear wraps around.

```
Circular: [_|_|7|8]  → front=2, rear=3
Enqueue(9): [9|_|7|8] → rear wraps to 0
```

Use a `size` counter to distinguish full (`size == MAX_SIZE`) from empty (`size == 0`).

**Key points to include for Full Marks:**
- Naïve problem: O(n) dequeue due to shifting.
- Circular fix: modulo arithmetic, O(1) dequeue.
- `size` counter needed to tell full from empty.

---

### 4. True / False + Justify

---

#### Q10 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 2

**Question:**
*"A Circular Queue data structure is used to enable undo and redo operations in text editors."*
True or False?

*(Directly from 23-spring Q1)*

**Guide answer:**
**FALSE.**
Undo/redo uses a **Stack** (LIFO): the most recent action is undone first. Two stacks are used — one for undo history, one for redo. Circular queues are used for resource management (CPU scheduling, print queues).

**Key points to include for Full Marks:**
- FALSE → correct structure = Stack.
- Explain why: undo = reverse most recent action → LIFO.

---

#### Q11 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 2

**Question:**
*"Queues can be used to manage and allocate resources, such as printers or CPU processing time."*
True or False?

*(Directly from 23-spring Q1)*

**Guide answer:**
**TRUE.**
Printer jobs and CPU processes are scheduled in FIFO order — the first job submitted is the first to be processed. A queue naturally enforces this fairness policy.

---

#### Q12 — True/False | Bloom's: Analyse | Difficulty: Medium | Marks: 3

**Question:**
*"In a linked-list queue, after dequeuing the last element, setting `front = nullptr` alone is sufficient to maintain a valid empty queue."*
True or False?

**Guide answer:**
**FALSE.**
If only `front` is set to `nullptr` but `rear` still points to the deleted (freed) node, `rear` becomes a **dangling pointer**. The next enqueue would attempt `rear->next = newNode`, accessing freed memory → **undefined behavior**. Both must be reset:
```cpp
if (isEmpty()) {
    rear = nullptr;
    front = nullptr;
}
```

**Key points to include for Full Marks:**
- Both `front` AND `rear` must be set to `nullptr`.
- Explain the dangling pointer risk on `rear`.

---

### 5. Application (Code / Scenario)

---

#### Q13 — Application | Bloom's: Apply | Difficulty: Medium | Marks: 6

**Question:**
Implement the **link-based Queue ADT**: complete class with constructor, destructor, `enqueue`, `dequeue`, `isEmpty`, and `length`.

*(23-spring Q4.1: "Implement the link-based ADT Queue")*

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

    ~Queue() {
        while (!isEmpty()) dequeue();   // free all nodes
    }

    bool isEmpty() { return size == 0; }

    int length() { return size; }

    void enqueue(int data) {
        Node* newNode = new Node(data);
        if (isEmpty()) {
            front = rear = newNode;     // first element
        } else {
            rear->next = newNode;       // link at back
            rear = newNode;             // advance rear
        }
        size++;
    }

    int dequeue() {
        if (isEmpty()) return -1;       // error sentinel
        Node* temp = front;
        int data = temp->data;
        front = front->next;            // advance front
        delete temp;                    // free memory
        size--;
        if (isEmpty()) {
            rear = nullptr;             // reset rear when empty
            front = nullptr;
        }
        return data;
    }
};
```

**Key points to include for Full Marks:**
- `enqueue`: handle empty queue (`front = rear = newNode`). Otherwise: `rear->next = newNode; rear = newNode`.
- `dequeue`: save front, advance, delete, decrement. **Reset `rear = nullptr` when empty.**
- Destructor: loop dequeue until empty → prevents memory leak.
- Both operations are **O(1)**.

**Common mistakes to avoid:**
- Forgetting `rear = nullptr` when queue becomes empty.
- Missing destructor → memory leak.
- Not advancing `rear = newNode` after linking.

---

#### Q14 — Application | Bloom's: Apply | Difficulty: Medium | Marks: 5

**Question:**
Write a member function `void Queue::PrintReversed()` that prints the queue elements in **reversed order** without destroying the queue contents. If the queue contains 5, 6, 2, 7, 3, print: `3 7 2 6 5`.

*(Directly from 25-spring Q2.3)*

**Guide answer:**

```cpp
void Queue::PrintReversed() {
    // Traverse the internal linked list and push values onto a stack
    std::stack<int> s;
    Node* curr = front;
    while (curr != nullptr) {
        s.push(curr->data);
        curr = curr->next;
    }
    // Pop from stack → reversed order
    while (!s.empty()) {
        cout << s.top() << " ";
        s.pop();
    }
    cout << endl;
}
```

**Why it works:**
- Traverse queue front→rear → pushes values in original order onto a stack.
- Pop from stack → LIFO reversal → prints in reversed order.
- Queue is **never modified** — no dequeue called.

**Key points to include for Full Marks:**
- Queue contents must be **preserved** — do not permanently dequeue.
- Stack is the auxiliary structure that reverses the order.
- Traverse the internal linked list directly (no dequeue) to avoid modifying the queue.

**Common mistakes to avoid:**
- Dequeuing without restoring → destroys the queue.
- Printing in original order instead of reversed.

---

#### Q15 — Application | Bloom's: Apply | Difficulty: Hard | Marks: 7

**Question:**
Implement the **Circular Array Queue**: complete class with constructor, `enqueue`, `dequeue`, `isEmpty`, `isFull`.

**Guide answer:**

```cpp
const int MAX_SIZE = 100;

class Queue {
private:
    int data[MAX_SIZE];
    int front, rear, size;
public:
    Queue() : front(-1), rear(-1), size(0) {}

    bool isEmpty() { return size == 0; }
    bool isFull()  { return size == MAX_SIZE; }
    int length()   { return size; }

    void enqueue(int val) {
        if (isFull()) {
            cout << "Queue is full." << endl;
            return;
        }
        rear = (rear + 1) % MAX_SIZE;   // circular advance
        data[rear] = val;
        if (front == -1) front = 0;      // first element
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
        if (isEmpty()) front = rear = -1; // reset
        return val;
    }
};
```

**Key points to include for Full Marks:**
- `enqueue`: `rear = (rear + 1) % MAX_SIZE` — modulo is mandatory.
- `dequeue`: `front = (front + 1) % MAX_SIZE`. Reset to -1 when empty.
- `isFull`: use `size == MAX_SIZE` (not `rear + 1 == front` — ambiguous without counter).
- `isEmpty`: use `size == 0`.

**Common mistakes to avoid:**
- Forgetting `% MAX_SIZE` → index out of bounds.
- Using `rear == front` to detect full/empty — ambiguous without size counter.
- Not resetting front/rear to -1 when empty.

---

#### Q16 — Application | Bloom's: Create | Difficulty: Hard | Marks: 8

**Question:**
Implement a **Palindrome Checker** using a queue and a stack. The function reads a string character by character, loads into both structures, then compares. Returns `true` if palindrome. Test with `"rotator"` and `"data"`.

*(From 06-Queues.txt assignment)*

**Guide answer:**

```cpp
#include <iostream>
#include <stack>
#include <string>
using namespace std;

bool isPalindrome(const string& str) {
    Queue q;           // your linked-list or circular-array queue
    stack<char> s;

    // Load all characters into both queue and stack
    for (char c : str) {
        q.enqueue(c);
        s.push(c);
    }

    // Compare front-of-queue (forward) vs top-of-stack (backward)
    while (!q.isEmpty()) {
        char fromQueue = q.dequeue();  // front → back (original order)
        char fromStack = s.top();      // top → bottom (reversed order)
        s.pop();
        if (fromQueue != fromStack)
            return false;
    }
    return true;
}

int main() {
    cout << "rotator: " << (isPalindrome("rotator") ? "palindrome" : "not") << endl;
    cout << "data: "    << (isPalindrome("data") ? "palindrome" : "not")    << endl;
    return 0;
}
```

**Output:**
```
rotator: palindrome
data: not
```

**Why it works:**
Queue reads characters **front→back** (original order). Stack reads **top→bottom** (reversed). If every pair matches → string is a palindrome.

**Key points to include for Full Marks:**
- Both queue and stack loaded in one pass.
- Queue dequeue = forward reading; stack pop = backward reading.
- Handle both test cases.

---

### 6. Compare & Contrast

---

#### Q17 — Compare & Contrast | Bloom's: Analyse | Difficulty: Medium | Marks: 5

**Question:**
Compare **Stack** vs **Queue** across: ordering principle, primary operations, underlying data structure (for BFS/DFS), and two real-world applications each.

**Guide answer:**

| Criterion | Stack | Queue |
|-----------|-------|-------|
| Ordering | **LIFO** — Last In, First Out | **FIFO** — First In, First Out |
| Insert | `push` (top) | `enqueue` (rear) |
| Remove | `pop` (top) | `dequeue` (front) |
| Graph traversal | Used in **DFS** | Used in **BFS** |
| Applications | Undo/redo, browser back button, expression evaluation, function call stack | Print queue, CPU scheduling, bank counter, BFS traversal |

**Key points to include for Full Marks:**
- All rows filled for both structures.
- DFS = Stack, BFS = Queue — frequently tested.
- At least 2 real-world applications per structure.

---

#### Q18 — Compare & Contrast | Bloom's: Evaluate | Difficulty: Hard | Marks: 5

**Question:**
Compare **Linked-list Queue** vs **Circular Array Queue** in terms of: memory usage, capacity limits, enqueue/dequeue complexity, and when to use each.

**Guide answer:**

| Criterion | Linked-list Queue | Circular Array Queue |
|-----------|:----------------:|:-------------------:|
| Memory | Dynamic — allocates per node (data + pointer overhead) | Static — fixed `MAX_SIZE` array (may waste if underfilled) |
| Capacity | **Unlimited** (bounded only by system memory) | **Fixed** at `MAX_SIZE` — `isFull()` needed |
| Enqueue time | O(1) | O(1) |
| Dequeue time | O(1) | O(1) |
| Memory overhead per element | Higher (pointer per node) | Lower (just array cell) |
| Use when | Queue size is unpredictable or unbounded | Queue size has known upper bound; cache-friendly access needed |

**Key points to include for Full Marks:**
- Both are O(1) for enqueue and dequeue — performance is the same.
- Key difference is **dynamic vs fixed size**.
- Array queue is more cache-friendly (contiguous memory).
- Linked-list queue has pointer overhead but no capacity limit.

---

### 7. Essay / Long Answer

---

#### Q19 — Essay | Bloom's: Create | Difficulty: Hard | Marks: 10

**Question:**
**(a)** Implement the complete link-based Queue class (Node, constructor, destructor, enqueue, dequeue, isEmpty, length).

**(b)** Using your Queue, implement a function `void reverseQueue(Queue& q)` that reverses the queue **without using any auxiliary data structure except recursion**.

**(c)** Trace the function with queue contents: `[5, 6, 2]` (front=5, rear=2).

*(From 06-Queues.txt assignment: "Reverse a Queue without using any other data structure")*

**Guide answer:**

**(a)** Full Queue class:
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
    ~Queue() { while (!isEmpty()) dequeue(); }
    bool isEmpty() { return size == 0; }
    int length() { return size; }

    void enqueue(int data) {
        Node* n = new Node(data);
        if (isEmpty()) front = rear = n;
        else { rear->next = n; rear = n; }
        size++;
    }

    int dequeue() {
        if (isEmpty()) return -1;
        Node* temp = front;
        int val = temp->data;
        front = front->next;
        delete temp;
        size--;
        if (isEmpty()) rear = nullptr;
        return val;
    }
};
```

**(b)** Recursive reversal (no auxiliary structure):
```cpp
void reverseQueue(Queue& q) {
    if (q.isEmpty()) return;         // base case
    int frontVal = q.dequeue();      // remove front
    reverseQueue(q);                 // reverse the rest
    q.enqueue(frontVal);             // put front at the back
}
```

**(c)** Trace with `[5, 6, 2]`:

| Call | Action | Queue state | Held value |
|------|--------|-------------|------------|
| 1 | dequeue 5 | [6, 2] | 5 |
| 2 | dequeue 6 | [2] | 6 |
| 3 | dequeue 2 | [] | 2 |
| 3 (return) | enqueue 2 | [2] | — |
| 2 (return) | enqueue 6 | [2, 6] | — |
| 1 (return) | enqueue 5 | **[2, 6, 5]** | — |

Result: Queue reversed from `[5, 6, 2]` → `[2, 6, 5]` ✓

**Key points to include for Full Marks:**
- Recursion uses the **call stack** as implicit storage — no explicit auxiliary data structure.
- Base case: `if (q.isEmpty()) return`.
- The dequeued element is enqueued **after** the recursive call returns → moves it to the back.
- Full trace showing each call and return.

---

## Section 4 — Study Tips & Weak Areas

| Weak Area | Why Students Lose Marks | Fix |
|-----------|------------------------|-----|
| **Circular queue modulo** | Writing `rear = rear + 1` without `% MAX_SIZE` | Always: `rear = (rear + 1) % MAX_SIZE`. |
| **rear reset when empty** | Not setting `rear = nullptr` after last dequeue | Add: `if (isEmpty()) { rear = nullptr; front = nullptr; }` |
| **FIFO vs LIFO confusion** | Saying "Queue uses LIFO" or "Stack uses FIFO" | Queue = FIFO (line), Stack = LIFO (plates). |
| **Naïve vs Circular** | Not explaining *why* naïve is O(n) | Naïve: front fixed → shift all elements → O(n). Circular: both indices wrap → O(1). |
| **PrintReversed destroys queue** | Dequeuing permanently without restoring | Traverse internal linked list and push to stack. Never dequeue permanently. |
| **Palindrome checker logic** | Not understanding why queue+stack comparison works | Queue = forward order, Stack = reversed. If all pairs match → palindrome. |

---

## Section 5 — Coverage Gap Analysis

| Concept | Suggested Question |
|---------|-------------------|
| Queue `front()` — peek without removing | "Implement `int front()` that returns the front element without dequeuing." |
| Array queue `isFull` edge case | "Why can't we use `rear == front` to detect a full circular queue? What alternative is used?" |
| Queue using two stacks | "Implement a Queue using two Stacks. Show enqueue and dequeue operations." |
| Priority Queue introduction | Not in this lecture — would come from a Heap lecture (not yet uploaded). |
