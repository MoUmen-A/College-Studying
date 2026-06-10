
# 25‑Spring Exam Answers

## Question 1 — MCQ [10 Points]

### 1a — In‑order successor in BST deletion
**Correct answer:** "In‑order successor is always either a leaf node or a node with an empty **left** child."  
*(The in‑order successor = leftmost node in the right subtree; by definition, it has no left child.)*

### 1b — Common property of Inorder, Preorder, Postorder
**Correct answer:** "Left subtree is always visited before right subtree."  
*(All three traversals visit left before right; they differ only in when the root is visited.)*

### 1c — Stack state after: push(2), push(4), pop(), push(6), push(8)
- push 2 → [2]
- push 4 → [2, 4]
- pop() removes 4 → [2]
- push 6 → [2, 6]
- push 8 → [2, 6, 8]

**Answer: [2, 6, 8]** *(bottom to top)*

### 1d — False statement
**False:** "A labeled rooted binary tree can be uniquely constructed given its **postorder and preorder** traversal results."  
*(You need **inorder + preorder** OR **inorder + postorder** to uniquely reconstruct a tree. Preorder + postorder alone is insufficient when nodes have only one child.)*

### 1e — Postfix expression for (A+B)*(C-D)
**Answer: `AB+CD-*`**

### 1f — Worst‑case time complexity for reversing a singly linked list
**Answer: O(n)**  
*(Every node must be visited exactly once to reverse the pointers.)*

---

## Question 1.2 — Tree Construction from Traversals

**Given:**
- Preorder: `C F H G B E A D J I` (Root -> Left -> Right)
- Inorder:  `H F B G C A J D I E` (Left -> Root -> Right)

**Construction process:**
1. Preorder[0] = **C** → root of the tree.
2. Find C in Inorder → index 4.
   - Left subtree inorder: `H F B G`
   - Right subtree inorder: `A J D I E`
3. Left subtree (nodes: H, F, B, G):
   - Preorder for left: `F H G B` → Root is **F**.
   - Find F in `H F B G`: Left is `H`, Right is `B G`.
   - Node **H**: left child of F.
   - Right of F (nodes: B, G):
     - Preorder for these is `G B` → Root is **G**.
     - Find G in `B G`: Left is `B`, Right is empty.
     - Node **B**: left child of G.
4. Right subtree (nodes: A, J, D, I, E):
   - Preorder for right: `E A D J I` → Root is **E**.
   - Find E in `A J D I E`: Left is `A J D I`, Right is empty.
   - Left of E (nodes: A, J, D, I):
     - Preorder is `A D J I` → Root is **A**.
     - Find A in `A J D I`: Left is empty, Right is `J D I`.
   - Right of A (nodes: J, D, I):
     - Preorder is `D J I` → Root is **D**.
     - Find D in `J D I`: Left is `J`, Right is `I`.
     - Node **J**: left child of D.
     - Node **I**: right child of D.

**Resulting tree:**
```
           C
          / \
         F   E
        / \   \
       H   G   A
          /     \
         B       D
                / \
               J   I
```

*(Verify: Preorder of this tree = C F H G B E A D J I — matches. Inorder = H F B G C A J D I E — matches. ✓)*

---

## Question 1.3 — Code Completion (Move Last to Front)

**Missing lines:**
```cpp
q->link = nullptr;   // disconnect last node from second‑last
p->link = head;       // point last node to old head
head    = p;          // update head to last node
```

**Complete function:**
```cpp
node* mystery(node* head) {
    node *p, *q;
    if (head == NULL || head->link == NULL)
        return head;
    q = NULL;
    p = head;
    while (p->link != NULL) {
        q = p;
        p = p->link;
    }
    // p = last node, q = second‑last node
    q->link = NULL;  // ← missing line 1: detach last
    p->link = head;   // ← missing line 2: last points to old head
    head    = p;       // ← missing line 3: update head
    return head;
}
```

---

## Question 2 — Independent Coding Functions [10 Points]

### 2.1 — Cousin Nodes in BST

```cpp
// Helper: finds the depth and parent of a node with given value
struct NodeInfo {
    int depth;
    Node* parent;
};

NodeInfo findInfo(Node* root, int val, Node* par, int depth) {
    if (!root) return {-1, nullptr};
    if (root->data == val) return {depth, par};
    NodeInfo left = findInfo(root->left, val, root, depth + 1);
    if (left.depth != -1) return left;
    return findInfo(root->right, val, root, depth + 1);
}

bool cousin(Node* t1, int a, int b) {
    NodeInfo infoA = findInfo(t1, a, nullptr, 0);
    NodeInfo infoB = findInfo(t1, b, nullptr, 0);
    // Cousins: same depth, different parents
    return (infoA.depth == infoB.depth && infoA.parent != infoB.parent);
}
```

**Verification with example tree (root=5):**
- Node 3: depth=2, parent=2
- Node 9: depth=2, parent=12
- Same depth ✓, different parents ✓ → **cousins** ✓

**Key points for full marks:**
- Must check **both** same depth AND different parents.
- Use a helper that passes the parent and depth through recursion.

---

### 2.2 — MoveNegEnd (Stack)

```cpp
void MoveNegEnd(Stack& S) {
    // Use a temporary queue to preserve original order
    Queue tempQ;
    // Step 1: Move all positives to queue, collect negatives
    Stack negStack, tempStack;

    // Unload S into tempStack (to reverse and preserve order)
    while (!S.isEmpty()) {
        tempStack.push(S.pop());
    }
    // Now tempStack is in correct order (top = original bottom)
    Queue pos, neg;
    while (!tempStack.isEmpty()) {
        int x = tempStack.pop();
        if (x < 0) neg.enqueue(x);
        else        pos.enqueue(x);
    }
    // Rebuild S: positives first, then negatives
    // Push in reverse so original order is maintained on top
    Stack result;
    // push negatives first (they'll be at bottom)
    while (!neg.isEmpty()) result.push(neg.dequeue());
    // push positives (they'll be on top)
    while (!pos.isEmpty()) result.push(pos.dequeue());
    // Transfer to S (in correct order)
    while (!result.isEmpty()) S.push(result.pop());
}
```

**Example trace:**
- Original (top→bottom): 5, -3, 9, 7, -4, 10, 7, -3, 10, -4
- After: Positives: 5, 9, 7, 10, 7 then Negatives: -3, -4, -3, -4

---

### 2.3 — QueueList::PrintReversed()

```cpp
void queueList::PrintReversed() {
    Stack aux;                  // auxiliary stack
    Node* cur = front;
    // Step 1: push all elements onto stack
    while (cur != nullptr) {
        aux.push(cur->data);
        cur = cur->next;
    }
    // Step 2: pop and print (LIFO = reversed)
    while (!aux.isEmpty()) {
        cout << aux.pop() << " ";
    }
    cout << endl;
    // Queue is unchanged (we only read, never modified it)
}
```

**Example:** Queue = 5, 6, 2, 7, 3 (front to rear) → Output: `3 7 2 6 5`

**Key points for full marks:**
- Use an **auxiliary stack** — do NOT modify the queue.
- Traverse queue from front to rear pushing each element.
- Pop from stack gives reversed order.
- Confirm queue content is unchanged after the function.

---

### 2.4 — Doubly Linked List Average Deletion

```cpp
// Step 1: compute average
float avg(List L) {
    Position curr = L.First();
    float sum = 0;
    int   count = 0;
    while (curr != nullptr) {
        sum += L.Retrieve(curr);
        count++;
        curr = L.Next(curr);
    }
    if (count == 0) return 0;   // avoid division by zero
    return sum / count;
}

// Step 2: delete all nodes > average
void NewDelete(List& L) {
    float average = avg(L);
    Position curr = L.First();
    while (curr != nullptr) {
        Position nextNode = L.Next(curr); // MUST save next BEFORE deleting
        if (L.Retrieve(curr) > average) {
            L.Delete(curr);
        }
        curr = nextNode;
    }
}
```

**Trace — List: 10 → 20 → 40 → 55 → 70**
- avg = (10+20+40+55+70)/5 = 195/5 = **39.0**
- 10 ≤ 39 → keep | 20 ≤ 39 → keep | 40 > 39 → **delete** | 55 > 39 → **delete** | 70 > 39 → **delete**
- Result: `10 → 20` ✓

**Key points for full marks:**
- Declare `sum` as `float` to avoid integer division truncation.
- Save `nextNode = L.Next(curr)` **before** calling `L.Delete(curr)`.
- Pass `L` by **reference** (`List& L`) so deletion persists in the caller.

---

## Question 3 — AVL Tree (10 Marks)

### Insertions: 15, 20, 10, 8, 12, 17, 25, 19, 30, 16

**1) Insert 15, 20, 10**
No rotations needed.
```
      15
     /  \
   10    20
```

**2) Insert 8**
Imbalance at 15. BF(15) = +2 (left-heavy). Inserted in left subtree of left child → **LL (Single Right) Rotation**.
```
      15 (+2)                  10 (0)
     /  \                     /  \
   10    20     ---LL--->    8   15 (0)
   /                              \
  8                                20
```

**3) Insert 12, 17, 25**
No rotations needed.
```
         10
       /    \
      8      15
            /  \
          12    20
               /  \
             17    25
```

**4) Insert 19**
Inserted as right child of 17. Imbalance at 20. BF(20) = -2 (right-heavy). Inserted in left subtree of right child → **RL (Double) Rotation**.
```
         10
       /    \
      8      15
            /  \
          12    20 (-2)
               /  \
             17    25
               \
               19

---RL Rotation at 20--->
Step 1: LL at 17                 Step 2: RR at 20
        20                                19 (0)
       /  \                              /  \
     19    25         --->             17    20 (0)
     /                                         \
   17                                           25
```
Tree after 19:
```
         10
       /    \
      8      15
            /  \
          12    19
               /  \
             17    20
                     \
                      25
```

**5) Insert 30**
Inserted as right child of 25. Tree remains balanced.
```
         10
       /    \
      8      15
            /  \
          12    19
               /  \
             17    20
                     \
                      25
                       \
                        30
```

**6) Insert 16**
Inserted as left child of 17. Imbalance at 19. BF(19) = +2 (left-heavy). Node 16 is in right subtree of left child (17) → **LR Double Rotation at 19**.
```
         10
       /    \
      8      15
            /  \
          12    19 (+2)
               /  \
             17    20
            /        \
          16          25
                       \
                        30
```
LR at 19 (Step 1: RR at 17, Step 2: LL at 19):
```
---LR at 19--->
           17
         /    \
       10      20
      /  \    /  \
     8   15  19   25
        /  \        \
      12    16       30
```
**Final AVL Tree after all Insertions:**
```
           17
         /    \
       10      20
      /  \    /  \
     8   15  19   25
        /  \        \
      12    16       30
```

### Deletions: 20, 15, 8

**Starting Tree for Deletions:**
```
           17
         /    \
       10      20
      /  \    /  \
     8   15  19   25
        /  \        \
      12    16       30
```

**1) Delete 20**
20 has two children. In-order successor is 25.
Copy 25 to 20, delete 25. 30 moves up to 25's old spot.
```
           17
         /    \
       10      25
      /  \    /  \
     8   15  19   30
        /  \        
      12    16       
```
Check BFs:
25: left 19 (ht 1), right 30 (ht 1) -> 0.
17: left 10 (ht 3), right 25 (ht 2) -> +1.
Balanced. **No rotations needed (Type: N)**.

**2) Delete 15**
15 has two children. In-order successor is 16.
Copy 16 to 15, delete 16.
```
           17
         /    \
       10      25
      /  \    /  \
     8   16  19   30
        /           
      12           
```
Check BFs:
16: left 12 (ht 1), right empty -> +1.
10: left 8 (ht 1), right 16 (ht 2) -> -1.
17: left 10 (ht 3), right 25 (ht 2) -> +1.
Balanced. **No rotations needed (Type: N)**.

**3) Delete 8**
8 is a leaf. Remove directly.
```
           17
         /    \
       10      25
         \    /  \
         16  19   30
        /           
      12           
```
Check BFs:
10: left empty (ht 0), right 16 (ht 2) -> -2! **Imbalance at 10.**
10 is right-heavy (-2). Right child (16) has BF=+1 (left-heavy).
Signs differ -> **RL (Right-Left) Double Rotation at 10**.

RL Rotation at 10:
Step 1: LL (Right Rotation) at 16. Pivot is 12.
```
      10                           10
        \                            \
         16        ---LL--->          12
        /                              \
      12                                16
```
Step 2: RR (Left Rotation) at 10. Pivot is 12.
```
         17                              17
       /    \                          /    \
     10      25        ---RR--->     12      25
       \    /  \                    /  \    /  \
       12  19   30                10   16  19   30
         \
         16
```
**Final AVL Tree after Deletions:**
```
           17
         /    \
       12      25
      /  \    /  \
    10   16  19   30
```

---

## Question 4 — Graphs [10 Points]

### 4.1 Graph Traversals

**Adjacency list:**
```
50: [20, 65, 80]
20: [10, 50, 40]
10: [20]
40: [20]
65: [50, 70]
70: [65]
80: [50, 90]
90: [80]
```

**DFS from 50** (visit neighbours in increasing numerical order):

| Step | Visited | Stack |
|------|---------|-------|
| Start | 50 | [50] |
| Visit 50 → neighbours 20,65,80; push in reverse: 80,65,20 | 50 | [80,65,20] |
| Pop 20 → visit | 50,20 | [80,65,10,50,40]→unvisited: 10,40 |
| Pop 10 → visit | 50,20,10 | [80,65,40] |
| Pop 40 → visit | 50,20,10,40 | [80,65] |
| Pop 65 → visit | 50,20,10,40,65 | [80,70] |
| Pop 70 → visit | 50,20,10,40,65,70 | [80] |
| Pop 80 → visit | 50,20,10,40,65,70,80 | [90] |
| Pop 90 → visit | 50,20,10,40,65,70,80,90 | [] |

**DFS order: 50 → 20 → 10 → 40 → 65 → 70 → 80 → 90**

**BFS from 50** (visit neighbours in increasing numerical order):

| Step | Visited | Queue |
|------|---------|-------|
| Start | 50 | [50] |
| Dequeue 50 → enqueue 20,65,80 | 50 | [20,65,80] |
| Dequeue 20 → enqueue unvisited: 10,40 | 50,20 | [65,80,10,40] |
| Dequeue 65 → enqueue unvisited: 70 | 50,20,65 | [80,10,40,70] |
| Dequeue 80 → enqueue unvisited: 90 | 50,20,65,80 | [10,40,70,90] |
| Dequeue 10 → no new | 50,20,65,80,10 | [40,70,90] |
| Dequeue 40 → no new | 50,20,65,80,10,40 | [70,90] |
| Dequeue 70 → no new | 50,20,65,80,10,40,70 | [90] |
| Dequeue 90 → no new | 50,20,65,80,10,40,70,90 | [] |

**BFS order: 50 → 20 → 65 → 80 → 10 → 40 → 70 → 90**

### 4.2 Dijkstra's Shortest Path
*(Exact answer depends on the graph image which was not fully extractable from the exam file. Apply Dijkstra's manually: initialize all distances to ∞ except source = 0; greedily pick the minimum‑distance unvisited vertex; update neighbours. Cross out old values when updated.)*

---

*All answers are calibrated to full‑mark expectations per `DSA-instruction.md`.*
