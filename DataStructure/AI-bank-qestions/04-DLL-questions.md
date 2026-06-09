# Question Bank — Doubly Linked List
**Source lecture:** [`04-Doubly-Linked-List.md`](file:///d:/Gam3a/Exam-Creation/DataStructure/Lec/04-Doubly-Linked-List.md)
**Calibrated against:** [`23-spring.txt`](file:///d:/Gam3a/Exam-Creation/DataStructure/PrevExams/23-spring.txt) · [`25-spring`](file:///d:/Gam3a/Exam-Creation/DataStructure/PrevExams/25-spring)
**Course:** CCS2401 — Data Structures & Algorithms | Dr. Ahmed Said

---

## Section 1 — Topic Summary

- Each node has three fields: `data`, `next` (points to successor), `prev` (points to predecessor).
- `head->prev = nullptr` (first node). `tail->next = nullptr` (last node).
- **Advantage over singly linked list**: bidirectional traversal — can go both forward and backward (e.g., media player rewind/replay).
- **Disadvantage vs singly linked list**: extra `prev` pointer = more memory per node.
- **Key operations**: `InsertAtStart`, `InsertAtEnd`, `InsertAt(x, p)`, `InsertAfter(x, p)`, `Delete(p)`, `Locate(x)`, `Retrieve(p)`, `PrintList`.
- **InsertAtStart**: `newNode->next = head`; `head->prev = newNode`; `head = newNode`. Handle empty list: `tail = head`.
- **InsertAtEnd**: `newNode->prev = tail`; `tail->next = newNode`; `tail = newNode`. Handle empty list: `head = tail`.
- **Delete(p)**: update head/tail if needed → `p->prev->next = p->next` → `p->next->prev = p->prev` → `delete p; counter--`.
- **Application functions**: `Sum()` (traverse and accumulate), `Reverse()` (insert each at front of new list), `Split()` (separate by value or index into two lists).

---

## Section 2 — Tone Analysis

From past exams, Doubly Linked List questions appear as:
- **Code-completion** (25-spring Q1.3): a function with a missing line — identify and fill correctly.
- **Independent coding functions** (25-spring Q2.4): write `NewDelete` that deletes nodes above average — requires `avg()` helper and safe pointer advancement before deletion.
- **Link-based ADT implementation** (23-spring Q2.1): implement a full list-based ADT from a given struct/class declaration.
- Expected mark range per function: **3–6 marks**.

---

## Section 3 — Question Bank

### 1. Multiple Choice (MCQ)

---

#### Q1 — MCQ | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**
What is the **main advantage** of a Doubly Linked List over a Singly Linked List?

- A) It uses less memory per node.
- B) It allows **bidirectional** traversal (forward and backward).
- C) It supports random access in O(1).
- D) Insertion at the end is faster.

**Guide answer:**
**B** — Each node has both `next` and `prev` pointers enabling backward traversal (e.g., rewind in media players). Singly linked lists only support forward traversal.

**Key points to include for Full Marks:**
- Name both pointers: `next` (successor) and `prev` (predecessor).
- Real-world example: video/audio file rewind and replay.

**Common mistakes to avoid:**
A is **wrong** — doubly linked list uses **more** memory (extra `prev` pointer). C is wrong — linked lists never support O(1) random access.

---

#### Q2 — MCQ | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
In the `InsertAtEnd` operation for a doubly linked list, which of the following correctly describes the pointer updates for the **new node**?

- A) `newNode->next = nullptr` ; `newNode->prev = head`
- B) `newNode->next = nullptr` ; `newNode->prev = tail`
- C) `newNode->next = tail` ; `newNode->prev = nullptr`
- D) `newNode->next = head` ; `newNode->prev = tail`

**Guide answer:**
**B** — The new node is placed at the end: its `next` is `nullptr` (nothing after it) and its `prev` links back to the current tail.

**Key points to include for Full Marks:**
- After setting the new node's pointers, also update: `tail->next = newNode` and `tail = newNode`.
- Handle empty list: if `head == nullptr`, set `head = tail = newNode`.

---

#### Q3 — MCQ | Bloom's: Analyse | Difficulty: Medium | Marks: 2

**Question:**
After calling `Delete(p)` on a **middle node** in a doubly linked list, which of the following pointer updates is **missing** from this code?

```cpp
p->prev->next = p->next;
delete p;
```

- A) `p->next = nullptr`
- B) `p->next->prev = p->prev`
- C) `head = p->next`
- D) `tail = p->prev`

**Guide answer:**
**B** — Deleting a middle node requires stitching both directions. `p->prev->next = p->next` fixes the forward chain, but `p->next->prev = p->prev` is missing to fix the **backward chain**. Without it, the successor node's `prev` still points to the deleted (freed) memory.

**Key points to include for Full Marks:**
- Both directions must be updated: `p->prev->next` AND `p->next->prev`.
- Also null-guard each: check `p->prev != nullptr` and `p->next != nullptr` before accessing.

---

### 2. Fill-in-the-blank

---

#### Q4 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
In a doubly linked list, the first node's `prev` pointer is set to ________, and the last node's `next` pointer is set to ________.

**Guide answer:** **`nullptr`** ; **`nullptr`**

---

#### Q5 — Fill-in-the-blank | Bloom's: Understand | Difficulty: Easy | Marks: 2

**Question:**
Complete the pointer update steps for `InsertAtStart(x)` on a non-empty doubly linked list:

```
1. newNode->next = ________
2. newNode->prev = ________
3. head->prev    = ________
4. head          = ________
```

**Guide answer:**
1. `head`
2. `nullptr`
3. `newNode`
4. `newNode`

**Key points to include for Full Marks:**
- All 4 steps must be in the correct order — step 3 must happen **before** step 4, otherwise `head` is already updated and `head->prev` would point to the new node itself.

---

#### Q6 — Fill-in-the-blank | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
In the `Delete(p)` function, before deleting `p` we must save the next node: `Position nextNode = L.Next(curr)`. This is done **before** the deletion because after `delete p`, the pointer `curr` points to ________ memory, making `L.Next(curr)` ________.

**Guide answer:** **freed (invalid/dangling)** ; **undefined behavior (invalid/unsafe)**

---

### 3. Short Answer

---

#### Q7 — Short Answer | Bloom's: Understand | Difficulty: Easy | Marks: 3

**Question:**
Compare **Singly Linked List** vs **Doubly Linked List** vs **Array-based List** across three criteria: traversal direction, insertion/deletion ease, and random access speed.

**Guide answer:**

| Criterion | Array-based List | Singly Linked List | Doubly Linked List |
|-----------|:---------------:|:-----------------:|:-----------------:|
| Traversal direction | Forward (by index) | Forward only | **Both directions** |
| Insertion/Deletion | Hard — O(n) shifting | Easy — O(1) at known node | Easy — O(1) at known node |
| Random access (i-th) | **O(1)** — direct index | O(n) — must traverse | O(n) — must traverse |

**Key points to include for Full Marks:**
- All 3 structures × 3 criteria = 9 cells addressed.
- Bidirectional traversal is the unique advantage of doubly linked list.
- Array's advantage is O(1) random access; disadvantage is fixed size and O(n) insertion.

---

#### Q8 — Short Answer | Bloom's: Analyse | Difficulty: Medium | Marks: 4

**Question:**
Explain all the steps required to **delete the head node** from a doubly linked list. What goes wrong if you only update `head = head->next` without doing anything else?

**Guide answer:**

**Complete steps:**
1. Save the old head: `Position temp = head`.
2. Advance head: `head = head->next`.
3. If new head is not null: `head->prev = nullptr` — remove dangling backward pointer.
4. If list is now empty (head == nullptr): also set `tail = nullptr`.
5. `delete temp` — free the memory of the old head.
6. `counter--`.

**What goes wrong if only `head = head->next`:**
- The new head's `prev` pointer still points to the deleted (freed) node — a **dangling pointer**.
- If the list had only one node, `tail` still points to the freed node — also **dangling**.
- The old node's memory is never freed → **memory leak**.

**Key points to include for Full Marks:**
- All 6 steps.
- Explicitly name: dangling pointer on `head->prev` and `tail`, and memory leak.

---

### 4. True / False + Justify

---

#### Q9 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 2

**Question:**
*"A Doubly Linked List uses more memory per node than a Singly Linked List."*
True or False? Justify.

**Guide answer:**
**TRUE.**
Every node in a doubly linked list stores two pointers: `next` AND `prev`. A singly linked list node stores only `next`. The extra `prev` pointer adds the size of one pointer (typically 4 or 8 bytes depending on architecture) per node. This is the trade-off for gaining bidirectional traversal.

**Key points to include for Full Marks:**
- State TRUE and name both pointers.
- Acknowledge it as a trade-off: more memory cost in exchange for backward traversal capability.

---

#### Q10 — True/False | Bloom's: Analyse | Difficulty: Medium | Marks: 3

**Question:**
*"When deleting a middle node p from a doubly linked list, updating only `p->prev->next = p->next` is sufficient to maintain a valid list."*
True or False? Justify.

**Guide answer:**
**FALSE.**
Updating only `p->prev->next = p->next` fixes the **forward direction** of the list (traversing from head to tail), but the **backward direction** remains broken. Specifically, `p->next->prev` still points to the deleted node `p`. If the list is traversed backward (from tail to head), it will reach freed memory, causing **undefined behavior**.

The complete fix requires both:
```cpp
p->prev->next = p->next;   // fix forward chain
p->next->prev = p->prev;   // fix backward chain
```

**Key points to include for Full Marks:**
- State FALSE and identify which direction is fixed and which is broken.
- State the consequence: backward traversal hits freed memory.
- Show the correct two-line fix.

---

#### Q11 — True/False | Bloom's: Analyse | Difficulty: Hard | Marks: 3

**Question:**
*"The `Reverse(L)` function that builds a new list by inserting each element at the start of a new list correctly reverses the original list."*
True or False? Trace with list: `10 → 20 → 40`.

**Guide answer:**
**TRUE.**
Starting with `10 → 20 → 40`:
- Insert 10 at front of L2 → L2: `10`
- Insert 20 at front of L2 → L2: `20 → 10`
- Insert 40 at front of L2 → L2: `40 → 20 → 10`

L2 is the exact reverse of L. The original list L is not modified.

```cpp
List Reverse(List l1) {
    List l2;
    Position pos = l1.First();
    while (pos != NULL) {
        int x = l1.Retrieve(pos);
        l2.InsertAt(x, l2.First()); // insert at start each time
        pos = l1.Next(pos);
    }
    return l2;
}
```

**Key points to include for Full Marks:**
- State TRUE and show the trace step by step.
- Confirm original list is unchanged (function takes by value, not reference).

---

### 5. Application (Code / Scenario)

---

#### Q12 — Application | Bloom's: Apply | Difficulty: Easy | Marks: 4

**Question:**
Using the `DoublyList` ADT from the lecture, implement `ElementType Sum(DoublyList L)` that returns the sum of all values in the list.

```cpp
// Use these ADT functions only:
// L.First()      → returns head position
// L.Next(p)      → returns next position after p
// L.Retrieve(p)  → returns data at position p
```

**Guide answer:**

```cpp
ElementType Sum(DoublyList L) {
    Position curr = L.First();   // start at head
    ElementType s = 0;
    while (curr != nullptr) {
        s += L.Retrieve(curr);   // accumulate data
        curr = L.Next(curr);     // advance forward
    }
    return s;
}
```

**Trace** — List: `10 → 20 → 40 → 55 → 70`:
| Step | curr->data | s |
|------|-----------|---|
| 1 | 10 | 10 |
| 2 | 20 | 30 |
| 3 | 40 | 70 |
| 4 | 55 | 125 |
| 5 | 70 | **195** |

**Key points to include for Full Marks:**
- Use `L.First()`, `L.Retrieve(curr)`, `L.Next(curr)` — ADT interface, not `curr->data` directly.
- Initialize `s = 0`.
- Loop condition: `curr != nullptr`.

**Common mistakes to avoid:**
Accessing `curr->data` directly bypasses the ADT and breaks encapsulation. Always use `L.Retrieve(curr)`.

---

#### Q13 — Application | Bloom's: Apply | Difficulty: Medium | Marks: 6

**Question:**
Implement the **`InsertAtEnd`** and **`Delete(p)`** member functions for the `DoublyList` class. `Delete` must handle all cases: head node, tail node, and middle node.

```cpp
class DoublyList {
private:
    Position head, tail;
    int counter;
public:
    void InsertAtEnd(ElementType x);
    void Delete(Position p);
};
```

**Guide answer:**

```cpp
void DoublyList::InsertAtEnd(ElementType x) {
    Position newNode = new Node;
    newNode->data = x;
    newNode->next = nullptr;
    newNode->prev = tail;           // link back to current tail

    if (tail != nullptr)
        tail->next = newNode;       // current tail points forward

    tail = newNode;                 // update tail

    if (head == nullptr)
        head = tail;                // empty list: head = tail = new node

    counter++;
}

void DoublyList::Delete(Position p) {
    if (p == nullptr) return;       // nothing to delete

    if (p == tail)  tail = p->prev; // update tail if deleting last node
    if (p == head)  head = p->next; // update head if deleting first node

    if (p->prev != nullptr)
        p->prev->next = p->next;    // stitch forward chain

    if (p->next != nullptr)
        p->next->prev = p->prev;    // stitch backward chain

    delete p;
    counter--;
}
```

**Key points to include for Full Marks:**
- `InsertAtEnd`: set `newNode->prev = tail` AND `tail->next = newNode`. Handle empty list.
- `Delete`: check `p == head` AND `p == tail` **separately** (not else-if) — a single-node list is both head and tail simultaneously.
- Null-guard both `p->prev` and `p->next` before dereferencing.
- Call `delete p` and decrement `counter`.

**Common mistakes to avoid:**
Using `else if` for head/tail checks causes the tail to not be updated when deleting a single-node list.

---

#### Q14 — Application | Bloom's: Analyse | Difficulty: Hard | Marks: 7

**Question:**
Using ADT Doubly Linked List, implement:

**(a)** `float avg(DoublyList L)` — returns the average of all values.
**(b)** `void NewDelete(DoublyList& L)` — deletes all nodes with values **greater than the average**.

*(Taken directly from 25-spring Q2.4)*

**Guide answer:**

```cpp
float avg(DoublyList L) {
    Position curr = L.First();
    float sum = 0;      // float to avoid integer division
    int count = 0;
    while (curr != nullptr) {
        sum += L.Retrieve(curr);
        count++;
        curr = L.Next(curr);
    }
    if (count == 0) return 0;   // avoid division by zero
    return sum / count;
}

void NewDelete(DoublyList& L) {
    float average = avg(L);
    Position curr = L.First();
    while (curr != nullptr) {
        Position nextNode = L.Next(curr); // MUST save next BEFORE deleting
        if (L.Retrieve(curr) > average) {
            L.Delete(curr);               // removes the node safely
        }
        curr = nextNode;                  // advance using saved pointer
    }
}
```

**Trace** — List: `10 → 20 → 40 → 55 → 70`
- avg = (10+20+40+55+70)/5 = **39.0**
- 10 ≤ 39 → keep | 20 ≤ 39 → keep | 40 > 39 → **delete** | 55 > 39 → **delete** | 70 > 39 → **delete**
- Result: `10 → 20` ✓

**Key points to include for Full Marks:**
- `avg()`: use `float sum` (not `int`) to avoid truncation.
- `avg()`: handle empty list — `if (count == 0) return 0`.
- `NewDelete()`: save `nextNode = L.Next(curr)` **before** `L.Delete(curr)` — after deletion, `curr` is freed memory.
- Pass `L` by **reference** (`DoublyList& L`) so the caller's list is modified.

**Common mistakes to avoid:**
- Not saving `nextNode` before deletion → accessing freed memory → **undefined behavior** (most commonly penalized).
- Integer division: `int sum / int count` truncates decimals — average would be wrong.

---

### 6. Compare & Contrast

---

#### Q15 — Compare & Contrast | Bloom's: Evaluate | Difficulty: Medium | Marks: 5

**Question:**
You are designing a music player that needs to:
- Play songs forward through a playlist.
- Skip backward to the previous song instantly.
- Insert a song at any position.

Which list structure — **Array-based**, **Singly Linked**, or **Doubly Linked** — would you choose, and why? Compare all three.

**Guide answer:**

**Best choice: Doubly Linked List.**

| Criterion | Array-based | Singly Linked | **Doubly Linked** |
|-----------|:-----------:|:-------------:|:-----------------:|
| Forward traversal | ✓ O(1) index | ✓ O(n) traverse | ✓ O(n) traverse |
| **Backward traversal** | ✓ (by decrementing index) | ✗ impossible without full re-traverse | ✓ **O(1) via `prev`** |
| Insert at position | ✗ O(n) shift | ✗ O(n) find position | ✓ O(1) at known position |
| Memory per element | Minimal | 1 extra pointer | 2 extra pointers |
| Dynamic size | ✗ fixed | ✓ | ✓ |

**Justification**: The key requirement is instant **skip backward**, which needs O(1) backward traversal. Only the doubly linked list's `prev` pointer achieves this. The extra memory cost is acceptable for a music player.

**Key points to include for Full Marks:**
- All 3 structures compared.
- Backward traversal highlighted as the deciding factor.
- Acknowledge memory trade-off.

---

### 7. Essay / Long Answer

---

#### Q16 — Essay | Bloom's: Create | Difficulty: Hard | Marks: 10

**Question:**
Implement the following two functions using the `DoublyList` ADT:

**(a)** `void Split(DoublyList L, DoublyList& lOdd, DoublyList& lEven)` — splits the list by **index** (0-indexed): even-indexed elements → `lEven`; odd-indexed elements → `lOdd`.

**(b)** `DoublyList Merge(DoublyList L1, DoublyList L2)` — merges two lists by alternating elements: L1[0], L2[0], L1[1], L2[1], … Append remaining elements if one list is longer.

**(c)** Write a `main` function that creates list `10 → 20 → 30 → 40 → 50`, splits it, prints lEven and lOdd, merges them back, and prints the merged result.

**Guide answer:**

```cpp
// (a) Split by index
void Split(DoublyList L, DoublyList& lOdd, DoublyList& lEven) {
    Position curr = L.First();
    int index = 0;
    while (curr != nullptr) {
        int x = L.Retrieve(curr);
        if (index % 2 == 0)
            lEven.InsertAtEnd(x);   // indices 0, 2, 4 → even
        else
            lOdd.InsertAtEnd(x);    // indices 1, 3   → odd
        index++;
        curr = L.Next(curr);
    }
}

// (b) Merge alternating
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

// (c) Main
int main() {
    DoublyList L, lEven, lOdd;
    L.InsertAtEnd(10); L.InsertAtEnd(20); L.InsertAtEnd(30);
    L.InsertAtEnd(40); L.InsertAtEnd(50);

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
- Split by **index** (not value): use `index % 2`, increment index each step.
- Merge: use `while (p1 != nullptr || p2 != nullptr)` — `||` not `&&` — to handle unequal-length lists.
- `lOdd` and `lEven` passed by **reference** — changes persist in caller.
- ADT interface throughout: `InsertAtEnd`, `Retrieve`, `Next`, `First`.

---

## Section 4 — Study Tips & Weak Areas

| Weak Area | Why Students Lose Marks | Fix |
|-----------|------------------------|-----|
| **Advance pointer before Delete** | Calling `L.Next(curr)` after `L.Delete(curr)` → freed memory | Always: `Position next = L.Next(curr); L.Delete(curr); curr = next;` |
| **head/tail both-check in Delete** | Using `else if` → single-node list leaves `tail` dangling | Use two **separate** `if` statements for head and tail |
| **Empty list in InsertAtEnd** | Not setting `head = tail` when list was empty | After `tail = newNode`, add: `if (head == nullptr) head = tail;` |
| **float vs int in avg()** | Integer division truncates: 39/2 = 19, not 19.5 | Declare `float sum = 0;` |
| **Null-guard in Delete** | `p->prev->next = ...` crashes if `p` is the head | Always check `if (p->prev != nullptr)` before dereferencing |
| **Split by value vs index** | Splitting by `x % 2` (value) instead of `index % 2` (position) | Maintain a separate `int index = 0;` counter |

---

## Section 5 — Coverage Gap Analysis

| Concept | Suggested Question |
|---------|-------------------|
| `InsertAfter(x, p)` when p is tail | "Implement `InsertAfter(x, p)`. Handle the case where p is the tail node." |
| `Locate(x)` + `Retrieve(p)` usage | "Write a function that finds and deletes the **first** occurrence of value x from the list." |
| Memory cleanup in `MakeNull()` | "The `MakeNull()` implementation does not free node memory. Rewrite it to properly delete all nodes." |
| Sorted insertion | "Implement `InsertSorted(x)` that inserts x maintaining ascending order." |
| Swap adjacent nodes | "Swap two adjacent nodes in a doubly linked list by adjusting pointers only (not swapping data)." |
