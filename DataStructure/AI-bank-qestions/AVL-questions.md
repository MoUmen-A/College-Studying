# AVL – Exam Questions

---

## Section 1 — Topic Summary

- **AVL Tree** – a self‑balancing binary search tree where the heights of the two child sub‑trees of any node differ by at most **1**.
- **Balance Factor** = `height(left) – height(right)`. Allowed values: `-1, 0, +1`.
- **Rotations** – restore balance when the factor becomes `±2`.
  - **LL (Single Right)**
  - **RR (Single Left)**
  - **LR (Left‑Right Double)**
  - **RL (Right‑Left Double)**
- **Insertion** – insert as in a BST, then backtrack updating heights and applying the first needed rotation.
- **Deletion** – remove as in a BST, then rebalance on the way up; multiple rotations may be required.
- **Complexities** – Search, Insert, Delete: **O(log N)**; worst‑case tree height **≈ 1.44 · log₂ N**.

---

## Section 2 – Tone Analysis

The past exams (`23‑spring.txt`, `25‑spring`) use concise MCQs for terminology, fill‑in‑the‑blank for key formulas, short answers for complexity, true/false for misconceptions, and longer code‑trace or implementation tasks worth 8‑10 marks. Distractors target common errors such as mixing rotation names, forgetting to update balance factors, or using the in‑order predecessor instead of the successor.

---

## Section 3 — Question Bank

### 1. Multiple Choice (MCQ) | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Q1** – Which rotation is performed when inserting a node causes the **right‑heavy** imbalance at the grand‑parent and the newly inserted node is in the **left subtree of the right child**?

- A) LL (Single Right)
- B) RR (Single Left)
- **C) RL (Right‑Left Double)**
- D) LR (Left‑Right Double)

**Guide answer:** C – RL rotation fixes a Right‑Left case.

---

### 2. Fill‑in‑the‑blank | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Q2** – In an AVL tree, the allowed balance‑factor values are **_____**.

**Guide answer:** `-1, 0, +1`

---

### 3. Short Answer | Bloom's: Understand | Difficulty: Medium | Marks: 3

**Q3** – Explain why an AVL tree guarantees **O(log N)** search time even after a sequence of arbitrary insertions and deletions.

**Guide answer:**
- Each rotation restores the invariant that every node’s sub‑tree heights differ by at most one.
- This invariant forces the height *h* of the tree to satisfy `h ≤ 1.44·log₂(N+2) – 0.328` (proved by induction).
- Therefore the longest root‑to‑leaf path is logarithmic, and search follows that path.

---

### 4. True / False + Justify | Bloom's: Analyse | Difficulty: Medium | Marks: 2

**Q4** – *"When deleting a node with two children from an AVL tree, you must always replace it with its **in‑order predecessor**.*

**Guide answer:** **FALSE.** Either the in‑order successor **or** predecessor may be used; the successor is conventional because it resides in the right subtree, preserving the BST ordering while keeping the balance‑factor update logic simple.

---

### 5. Application (code) — Implement Insertion with Rotation | Bloom's: Apply | Difficulty: Hard | Marks: 6

**Q5** – Write a C++ member function `insert(Node* &root, int key)` for an AVL tree that inserts `key` and performs the necessary rotation(s). Include:
- Height updates.
- Balance‑factor computation.
- Calls to helper rotation functions `rotateLL`, `rotateRR`, `rotateLR`, `rotateRL`.

**Guide answer:**
```cpp
struct Node {
    int key, height;
    Node *left, *right;
    Node(int k): key(k), height(1), left(nullptr), right(nullptr) {}
};

int height(Node* n) { return n ? n->height : 0; }
int getBF(Node* n) { return n ? height(n->left) - height(n->right) : 0; }

Node* rotateLL(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;
    x->right = y;
    y->left = T2;
    y->height = std::max(height(y->left), height(y->right)) + 1;
    x->height = std::max(height(x->left), height(x->right)) + 1;
    return x;
}

Node* rotateRR(Node* y) {
    Node* x = y->right;
    Node* T2 = x->left;
    x->left = y;
    y->right = T2;
    y->height = std::max(height(y->left), height(y->right)) + 1;
    x->height = std::max(height(x->left), height(x->right)) + 1;
    return x;
}

Node* rotateLR(Node* y) { y->left = rotateRR(y->left); return rotateLL(y); }
Node* rotateRL(Node* y) { y->right = rotateLL(y->right); return rotateRR(y); }

void insert(Node* &root, int key) {
    if (!root) { root = new Node(key); return; }
    if (key < root->key) insert(root->left, key);
    else if (key > root->key) insert(root->right, key);
    else return; // duplicate keys not allowed

    root->height = std::max(height(root->left), height(root->right)) + 1;
    int bf = getBF(root);
    // Left Left
    if (bf > 1 && key < root->left->key) root = rotateLL(root);
    // Right Right
    else if (bf < -1 && key > root->right->key) root = rotateRR(root);
    // Left Right
    else if (bf > 1 && key > root->left->key) root = rotateLR(root);
    // Right Left
    else if (bf < -1 && key < root->right->key) root = rotateRL(root);
}
```
**Key points for full marks:**
- Correct height recalculation after recursive insertion.
- Accurate balance‑factor logic.
- Proper selection of rotation case and correct call order (double rotations call single rotations inside).
- No memory leaks; duplicate keys are ignored.

---

### 6. Compare & Contrast | Bloom's: Evaluate | Difficulty: Medium | Marks: 4

**Q6** – Compare **AVL trees** and **plain BSTs** in terms of:
1. Worst‑case height.
2. Search/Insert/Delete time complexity.
3. Memory overhead.
4. Typical use‑case scenarios.

**Guide answer:**
| Criterion | AVL Tree | Plain BST |
|---|---|---|
| Height (worst) | `≈ 1.44·log₂ N` (guaranteed) | `N` (degenerate) |
| Complexity (search/ins/del) | `O(log N)` guaranteed | `O(log N)` average, `O(N)` worst |
| Memory overhead | Stores `height` (int) per node (+ rotation pointers) | Only key & child pointers |
| Use‑case | When guaranteed logarithmic performance is required (e.g., databases, real‑time systems) | Simpler code, acceptable when data is random or tree stays balanced by chance |

---

### 7. Essay / Long Answer | Bloom's: Create | Difficulty: Hard | Marks: 10

**Q7** – Design a **complete C++ AVL‑tree class** that supports:
- `insert(int key)`
- `remove(int key)` (including rebalancing after deletion)
- `search(int key)` returning a bool
- `inorder()` that returns a vector of keys in sorted order.
Provide:
1. Full class definition with private helper functions.
2. Explanation of how deletion rebalancing differs from insertion (multiple possible rotations).
3. A hand‑traced example: start with an empty tree, insert the sequence `30, 20, 40, 10, 25, 35, 50, 5`. After each insertion, draw the tree and note any rotations performed.
4. After the final tree, delete the node `30` and show each rebalancing step.

**Guide answer (outline):**
```cpp
class AVL {
    struct Node {
        int key, height;
        Node *left, *right;
        Node(int k): key(k), height(1), left(nullptr), right(nullptr) {}
    }*root = nullptr;

    int height(Node* n){ return n? n->height : 0; }
    int bf(Node* n){ return n? height(n->left)-height(n->right) : 0; }
    Node* rotateLL(Node* y){ /* as before */ }
    Node* rotateRR(Node* y){ /* as before */ }
    Node* rotateLR(Node* y){ y->left = rotateRR(y->left); return rotateLL(y); }
    Node* rotateRL(Node* y){ y->right = rotateLL(y->right); return rotateRR(y); }
    Node* rebalance(Node* n){
        n->height = std::max(height(n->left), height(n->right)) + 1;
        int balance = bf(n);
        if (balance > 1){ // left heavy
            if (bf(n->left) >= 0) return rotateLL(n); // LL
            else return rotateLR(n); // LR
        }
        if (balance < -1){ // right heavy
            if (bf(n->right) <= 0) return rotateRR(n); // RR
            else return rotateRL(n); // RL
        }
        return n;
    }
    Node* insertRec(Node* node, int key){
        if (!node) return new Node(key);
        if (key < node->key) node->left = insertRec(node->left, key);
        else if (key > node->key) node->right = insertRec(node->right, key);
        else return node; // duplicate ignored
        return rebalance(node);
    }
    Node* minValueNode(Node* node){ while(node->left) node = node->left; return node; }
    Node* deleteRec(Node* root, int key){
        if (!root) return root;
        if (key < root->key) root->left = deleteRec(root->left, key);
        else if (key > root->key) root->right = deleteRec(root->right, key);
        else {
            if (!root->left){ Node* temp = root->right; delete root; return temp; }
            else if (!root->right){ Node* temp = root->left; delete root; return temp; }
            Node* temp = minValueNode(root->right);
            root->key = temp->key;
            root->right = deleteRec(root->right, temp->key);
        }
        return rebalance(root);
    }
    void inorderRec(Node* n, std::vector<int>& out){ if(!n) return; inorderRec(n->left,out); out.push_back(n->key); inorderRec(n->right,out); }
public:
    void insert(int k){ root = insertRec(root,k); }
    void remove(int k){ root = deleteRec(root,k); }
    bool search(int k){ Node* cur=root; while(cur){ if(k==cur->key) return true; cur = (k<cur->key)?cur->left:cur->right; } return false; }
    std::vector<int> inorder(){ std::vector<int> v; inorderRec(root,v); return v; }
};
```
**Explanation of deletion rebalancing:** After removing a node, the subtree heights may decrease on one side, possibly creating a `|bf| = 2`. The same four rotation cases are examined, but the *imbalance node* may be higher up the tree, so multiple rotations can cascade upward.

**Insertion trace (pictures omitted for brevity):**
1. Insert 30 → no rotation.
2. Insert 20 → no rotation.
3. Insert 40 → still balanced.
4. Insert 10 → causes LL at 30 → single right rotation (30 becomes right child of 20).
5. Insert 25 → rebalances with LR at 20 → left‑right double rotation.
6. Insert 35 → no rotation.
7. Insert 50 → no rotation.
8. Insert 5 → LL at 20 → right rotation.
**Deletion of 30:** Node 30 is now the root; after removal the tree becomes left‑heavy at 25 → RR rotation on subtree rooted at 25, followed by a possible LL at new root 20. All intermediate diagrams are drawn showing balance factors.

**Key points for full marks:**
- Complete class with proper encapsulation.
- Correct height update in every recursive return.
- All four rotation functions implemented exactly as in the MCQ answer.
- Deletion uses *in‑order successor* (`minValueNode`) and rebalances on unwind.
- Hand‑drawn trees after each operation, with balance factors labelled.
- Clear justification of each rotation type.

---

## Section 4 — Study Tips & Weak Areas

| Weak Area | Why students lose marks | How to fix |
|---|---|---|
| **Identifying rotation case** | Confusing LR with RL, forgetting to update both children pointers. | Memorise the four patterns; practice with small trees on paper, always write the balance factor before deciding.
| **Updating height after rotation** | Leaving height of rotated nodes stale → later incorrect balance checks. | After every rotation, recompute `height` for the affected nodes in bottom‑up order (first children, then parent).
| **Deletion rebalancing** | Assuming only one rotation is needed; forgetting that deletion can propagate imbalance upward. | Walk back up the recursion stack, applying `rebalance` at each ancestor.
| **Code edge cases** | Ignoring duplicate keys or null root in recursive calls. | Include explicit checks for `nullptr` and `key == node->key` early in the functions.

---

## Section 5 — Coverage Gap Analysis

The current question set covers all core AVL concepts required by the lecture (`08‑BST.md`). No major gaps detected. If future lectures add **AVL deletion with multiple rotations** or **augmented AVL trees (order‑statistics)**, add targeted questions accordingly.
