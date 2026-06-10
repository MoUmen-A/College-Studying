# Queues - Exam Questions
**Generated from:** `06-Queues.txt`
**Calibrated against:** `23-spring.txt` · `25-spring`
**Course:** CCS2401 — Data Structures & Algorithms | Dr. Ahmed Said

---

## Section 1 — Topic Summary

### Queues
- **FIFO** — First In, First Out. Insertion at **rear** (enqueue); deletion from **front** (dequeue).
- Operations: `enqueue`, `dequeue`, `front`, `isEmpty`, `isFull`, `length`.
- **Linked-list implementation**: front and rear pointers. Enqueue adds to rear; dequeue removes from front.
  - Both enqueue and dequeue: **O(1)** time and space.
- **Array implementation** — Naïve: shift elements on dequeue → O(n) — **inefficient**.
- **Circular Array**: rear = (rear + 1) % MAX_SIZE; front = (front + 1) % MAX_SIZE. Avoids wasted space.
  - Use a `size` counter to distinguish full from empty.
- Real-world uses: print queues, CPU scheduling, bank counters, BFS traversal.

---

## Section 2 — Tone Analysis

From **`23-spring.txt`** and **`25-spring`**, the exam style for these topics is:
- **True/False (Q1)**: Real-world application matching (e.g., "Queue is used to undo/redo" — False, that's a Stack).
- **Independent coding functions (Q2 in 25-spring)**: 3–5 marks each — write a standalone method from scratch (e.g., `PrintReversed()`).
- **Link-based ADT Implementation (Q4.1 in 23-spring)**: "Implement the link-based ADT Queue" — full class, constructor, enqueue, dequeue.

---

## Section 3 — Question Bank

---

### 1. Multiple Choice (MCQ)

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

#### Q9 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
In a queue, elements are **inserted** at the ________ and **removed** from the ________.

**Guide answer:** **rear (back/end)** ; **front**

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

### 5. Application (Code / Scenario)

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

### 7. Essay / Long Answer

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
| **Circular queue modulo** | Writing `rear = rear + 1` instead of `rear = (rear + 1) % MAX_SIZE` | The `% MAX_SIZE` is mandatory — without it the index goes out of bounds. |
| **Queue's rear after empty** | Not resetting `rear = nullptr` (or -1) after dequeuing the last element | In dequeue: `if (isEmpty()) { rear = nullptr; front = nullptr; }` |

---

## Section 5 — Coverage Gap Analysis

### Concepts in lectures not yet covered in this question bank:

| Concept | From Lecture | Suggested Question |
|---------|-------------|-------------------|
| **Queue Reverse** (without extra data structure) | `06-Queues.txt` assignment | "Write a function to reverse a queue without using any other data structure. Hint: use recursion." |
