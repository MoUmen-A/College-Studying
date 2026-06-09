# CCS2401 — Data Structures & Algorithms
## 04 — Doubly Linked List
**Dr. Ahmed Said**

---

## So far…

| Structure | Strengths | Weaknesses |
|---|---|---|
| Array-based list | Easy access (get i-th element) | Requires knowing list size; insertion/deletion is harder |
| Singly linked list | Insertion/deletion is easy | Access is harder; cannot go back |

---

## Doubly Linked List

In a Doubly Linked List, each item points to **both** its predecessor and successor.

- `prev` points to the predecessor
- `next` points to the successor

> 📌 Extracted from image: Doubly linked list memory layout
>
> ```
> HEAD                                                  NULL
> NULL ←  [prev | data | next] ↔ [prev | data | next] ↔ [prev | data | next] →
> ```
>
> Concrete example with values:
> ```
> Head → [ / | 10 | ] ↔ [ | 20 | ] ↔ [ | 40 | ] ↔ [ | 55 | ] ↔ [ | 70 | / ]
>                ↑              ↑              ↑
>           Cur->prev          Cur         Cur->next
> ```
> (/ denotes NULL pointer)

### Use cases

- Playing video and sound files with **rewind** and instant **replay**
- Any linked data that requires fast forward and backward traversal

---

## Structure of Storage

### Node definition

```cpp
typedef int ElementType;

class Node {
public:
    ElementType data;
    Node* next;
    Node* prev;
};

typedef Node* Position;
```

---

### DoublyList class declaration

```cpp
class DoublyList {
private:
    Position head;    // points to the first node
    Position tail;    // points to the last node
    int counter;
public:
    void MakeNull();
    Position First();
    Position Next(Position p);
    Position Previous(Position p);
    Position End();
    void InsertAtEnd(ElementType x);
    void InsertAtStart(ElementType x);
    void Insert(ElementType x, Position p);
    void Delete(Position p);
    Position Locate(int x);
    ElementType Retrieve(Position p);
    void PrintList();
};
```

---

## Operations

### MakeNull, First, End

```cpp
void DoublyList::MakeNull()
{
    head = nullptr;
    tail = nullptr;
    counter = 0;
    // need to add code to free (delete) nodes memory allocation
}

Position DoublyList::First()
{
    return head;
}

Position DoublyList::End()
{
    return tail;
}
```

---

### Next & Previous

`NEXT(p)` and `PREVIOUS(p)` return the positions following and preceding position `p` on list `L`.

```cpp
Position DoublyList::Next(Position p) {
    if (p == nullptr) {
        return nullptr;
    }
    return p->next;
}

Position DoublyList::Previous(Position p) {
    if (p == nullptr) {
        return nullptr;
    }
    return p->prev;
}
```

---

### Insert

`INSERT(x, p)`: Insert `x` at position `p` in list `L`.

`p` may be:
- At the Start
- In the Middle
- At the End

#### Insert at Start

```cpp
void DoublyList::InsertAtStart(ElementType x) {
    Position newNode = new Node;
    newNode->data = x;
    newNode->next = head;
    newNode->prev = nullptr;
    if (head != nullptr) {
        head->prev = newNode;
    }
    head = newNode;
    if (tail == nullptr) {
        tail = head;
    }
    counter++;
}
```

#### Insert at End

```cpp
void DoublyList::InsertAtEnd(ElementType x) {
    Position newNode = new Node;
    newNode->data = x;
    newNode->next = nullptr;
    newNode->prev = tail;
    if (tail != nullptr) {
        tail->next = newNode;
    }
    tail = newNode;
    if (head == nullptr) {
        head = tail;
    }
    counter++;
}
```

#### Insert at Position (InsertAt)

`INSERT(x, p)`: Insert `x` at position `p`. If list `L` has no position `p`, use tail.

```cpp
void DoublyList::InsertAt(ElementType x, Position p = nullptr) {
    if (p == nullptr) {
        InsertAtEnd(x);
    }
    else if (p == head) {
        InsertAtStart(x);
    }
    else {
        Position newNode = new Node();
        newNode->data = x;
        newNode->prev = p->prev;
        newNode->next = p;
        if (p->prev != nullptr) {
            p->prev->next = newNode;
        }
        p->prev = newNode;
        counter++;
    }
}
```

#### InsertAfter

```cpp
void DoublyList::InsertAfter(ElementType x, Position p) {
    if (p == nullptr) {
        InsertAtEnd(x);
    }
    else {
        Position newNode = new Node();
        newNode->data = x;
        newNode->next = p->next;
        newNode->prev = p;
        if (p->next != nullptr) {
            p->next->prev = newNode;
        }
        p->next = newNode;
        if (p == tail) {
            tail = newNode;
        }
        counter++;
    }
}
```

---

### Delete

`DELETE(p)`: Delete the element at position `p` of list `L`.

`p` may be:
- The Head
- In the Middle
- The Tail

```cpp
void DoublyList::Delete(Position p) {
    if (p == nullptr) {
        // No element to delete
        return;
    }
    if (p == tail) {
        tail = p->prev;
    }
    if (p == head) {
        head = p->next;
    }
    Position temp = p;
    if (p->prev != nullptr) {
        p->prev->next = p->next;
    }
    if (p->next != nullptr) {
        p->next->prev = p->prev;
    }
    delete temp;
    counter--;
}
```

---

### Locate(x)

```cpp
Position DoublyList::Locate(ElementType x) {
    Position p = head;
    while (p != nullptr) {
        if (p->data == x)
            return p;
        p = p->next;
    }
    return nullptr;
}
```

---

### Retrieve(p)

```cpp
ElementType DoublyList::Retrieve(Position p)
{
    if (p == nullptr) {
        return NULL;
    }
    return p->data;
}
```

---

### PrintList

```cpp
void DoublyList::PrintList()
{
    Position p = head;
    while (p != nullptr) {
        std::cout << p->data << " -> ";
        p = p->next;
    }
}
```

---

## Testing the Implementation

```cpp
int main() {
    DoublyList list;
    list.InsertAtStart(1);
    list.InsertAtStart(2);
    list.InsertAtStart(3);
    list.InsertAtStart(4);
    list.InsertAt(10, list.End());
    list.InsertAt(-30, list.First());
    list.InsertAt(-10, list.First());
    list.InsertAt(20, list.End());

    Position n10 = list.Locate(10);
    list.Delete(n10);

    Position n20 = list.Locate(20);
    list.Delete(n20);

    list.PrintList();
    return 0;
}
```

**Expected output:**

```
-10 -> -30 -> 4 -> 3 -> 2 -> 1
```

---

## Applications

### 1. Sum

Calculates the summation of all values in the list.

```cpp
ElementType Sum(DoublyList L)
{
    Position curr = L.First();
    ElementType s = 0;
    while (curr != NULL)
    {
        ElementType x = L.Retrieve(curr);
        s = s + x;
        curr = L.Next(curr);
    }
    return s;
}
```

---

### 2. Reverse

Returns a new list with elements in reverse order.

> 📌 Extracted from image: Reverse example output
>
> ```
> List is: -200 -90 4 3 2 10 100 400 1 534
> List is: 534 1 400 100 10 2 3 4 -90 -200
> ```

```cpp
List Reverse(List l1)
{
    List l2;
    Position pos = l1.First();
    while (pos != NULL)
    {
        int x = l1.Retrieve(pos);
        l2.InsertAt(x, l2.First());
        pos = l1.Next(pos);
    }
    return l2;
}
```

---

### 3. Split

Splits the list into two lists: one for odd numbers and one for even numbers.

> 📌 Extracted from image: Split example output
>
> ```
> all: List is: -200 -90 4 3 2 1 4 3 2 10 100 400 1 534
> Even: List is: 3 1 3 1
> Odd:  List is: -200 -90 4 2 4 2 10 100 400 534
> ```

```cpp
void Split(DoublyList L, DoublyList& lOdd, DoublyList& lEven)
{
    Position curr = L.First();
    while (curr != NULL)
    {
        int x = L.Retrieve(curr);
        if (x % 2 == 0)
            lEven.InsertAt(x);
        else
            lOdd.InsertAt(x);
        curr = L.Next(curr);
    }
}
```

---

## Assignment

Using ADT Operations, implement the following:

1. `List Merge(List L1, List L2)`
2. Swap two adjacent nodes by adjusting their positions using:
   - a. Singly linked list
   - b. Doubly linked list

---

## Bonus Assignments

1. The code did not provide a way to clean up memory allocated when `MakeNull` is called. Resolve this issue.
2. Modify the Linked List implementation to store items **sorted in ascending order**:
   - Singly linked list
   - Doubly linked list
