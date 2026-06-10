# Doubly Linked List (DLL) - Exam Questions
**Generated from:** `04-Doubly-Linked-List.md`
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

---

## Section 2 — Tone Analysis

From **`23-spring.txt`** and **`25-spring`**, the exam style for these topics is:
- **True/False (Q1)**: Real-world application matching (e.g., "Queue is used to undo/redo" — False, that's a Stack).
- **Code completion (Q1.3 in 25-spring)**: A function with a missing line/lines — identify and fill. *Very likely to appear.*
- **Independent coding functions (Q2 in 25-spring)**: 3–5 marks each — write a standalone method from scratch (e.g., `PrintReversed()`, `NewDelete()`, `MoveNegEnd()`).
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

### 2. Fill-in-the-blank

---

#### Q8 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
In a doubly linked list, the first node's `prev` pointer is set to ________, and the last node's `next` pointer is set to ________.

**Guide answer:** **nullptr (NULL)** ; **nullptr (NULL)**

---

### 4. True / False + Justify

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

## Section 4 — Study Tips & Weak Areas

| Weak Area | Why Students Lose Marks | Fix |
|-----------|------------------------|-----|
| **Delete in doubly linked list** | Forgetting to update both `head` AND `tail`; not null-guarding `p->prev` and `p->next` | Always check: is p the head? is p the tail? Then stitch: `p->prev->next = p->next` AND `p->next->prev = p->prev`. |
| **Advance pointer before deletion** | Using `curr = L.Next(curr)` AFTER `L.Delete(curr)` — curr is freed memory | Always: `Position next = L.Next(curr); L.Delete(curr); curr = next;` |
| **avg() with int division** | `(10+20)/2 = 15` (correct) but `(10+25)/2 = 17` instead of 17.5 — truncation error | Always declare sum as `float`. |

---

## Section 5 — Coverage Gap Analysis

### Concepts in lectures not yet covered in this question bank:

| Concept | From Lecture | Suggested Question |
|---------|-------------|-------------------|
| `InsertAfter(x, p)` implementation | `04-Doubly-Linked-List.md` | "Implement `InsertAfter(x, p)` that inserts value x immediately after position p. Handle the case when p is the tail." |
| `Locate(x)` + `Retrieve(p)` usage pattern | `04-Doubly-Linked-List.md` | "Write a function that finds and deletes the first occurrence of value x from a doubly linked list." |
