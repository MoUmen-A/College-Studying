# CCS2401 — Data Structures & Algorithms
## 08 — Binary Search Trees (BST)
**Dr. Ahmed Said**

---

## Binary Search Tree (BST)

- An important application of binary trees is their use in searching.
- A Binary Search Tree (BST) is a binary tree that:
  - Stores data in an ordered fashion.
  - Provides fast access operations to:
    - Insert data in new nodes
    - Remove old data and delete their nodes
    - Search for data in existing nodes
- The average running time of most operations is `O(log N)`.

---

## BST Property

For every node X in a BST:

- The values of all nodes in its **left subtree** are **(< )** smaller than the item in X.
- The values of all nodes in its **right subtree** are **(≥)** larger than the item in X.

> 📌 Extracted from image: BST structure diagram
> Root node contains `Data`. Left subtree contains values `< Data`. Right subtree contains values `≥ Data`.

---

## Binary Search Tree Example

Construct a BST from: `1, 3, 4, 6, 7, 8, 10, 13, 14`

> 📌 Extracted from image: BST example diagram
>
> ```
>            8
>          /   \
>         3     10
>        / \      \
>       1   6      14
>          / \    /
>         4   7  13
> ```

---

## Which is a BST?

> 📌 Extracted from image: Two trees side by side
>
> **(1) NOT a valid BST** — node `7` is in the right subtree of `4` (which is in the left subtree of `6`), but `7 > 6`, which violates the BST property. Marked with a red ✗.
>
> ```
>         6
>        / \
>       2   8
>      / \
>     1   4
>        / \
>       3   7✗
> ```
>
> **(2) Valid BST** — all nodes satisfy the BST property. Marked with a green arrow.
>
> ```
>         6
>        / \
>       2   8
>      / \
>     1   4
>        /
>       3
> ```

---

## BST Operations

- **Search(value)**: returns `true` if "value" exists in the tree.
- **Insert(value)**: adds a value to the tree.
- **Remove(value)**: deletes a node from the tree.
- **Traverse** (display): displays all nodes in the tree.
  - InOrder
  - PreOrder
  - PostOrder

---

## Insertion in BST

A BST sorts data as it is entered into the tree by moving data greater than the root toward the right and data less than the root to the left.

To insert data into a BST:

1. If tree is empty → insert data as root node
2. If inserted data < root data → insert new node in left subtree
3. If inserted data ≥ root data → insert new node in right subtree
4. Repeat steps 1–3 for each subtree recursively

---

## Example: Insertion (step-by-step)

Starting tree after inserting: `60, 41, 74, 16, 65`

> 📌 Extracted from image: Insertion trace
>
> ```
>              60
>            /    \
>           41     74
>          /      /
>         16     65
>           \   /  \
>           53  63  70
>          / \   \
>         46  55  64
>        /
>       42
> ```

### Inserting 48 — trace:

| Step | Node visited | Decision |
|------|-------------|----------|
| 1 | 60 | 48 < 60 → go left |
| 2 | 41 | 48 > 41 → go right (has right child) |
| 3 | 53 | 48 < 53 → go left (has left child) |
| 4 | 46 | 48 > 46 → go right (no right child) |
| 5 | — | Insert 48 as right child of 46 ✓ |

Result after inserting 48:

> 📌 Extracted from image: Final tree with 48 inserted
>
> ```
>              60
>            /    \
>           41     74
>          / \    /  \
>         16  53  65
>        /   / \  / \
>       25  46 55 63 70
>          / \    \
>         42  48   64
> ```

---

## Assignment 1

Construct a Binary Search Tree by inserting the following values in order:

`100, 200, 90, 150, 125, 88, 99, 210`

---

## Search in BST

To search for data in a BST:

- Compare data with the root node data:
  - If **equal** → found
  - If **less than** → recursively search left subtree
  - If **greater than** → recursively search right subtree
  - If **subtree is empty** → data not found

### Example: Search for 55

> 📌 Extracted from image: Search trace for value 55
>
> | Step | Node visited | Decision |
> |------|-------------|----------|
> | 1 | 60 | 55 < 60 → go left |
> | 2 | 41 | 55 > 41 → go right |
> | 3 | 53 | 55 > 53 → go right |
> | 4 | 55 | 55 == 55 → **Found ✓** |

---

## Tree Traversal — In-order (Recall)

In-order traversal of a BST visits nodes in **sorted (ascending) order**.

> 📌 Extracted from image: In-order traversal numbered diagram
>
> ```
>              63
>            /    \
>           41     74
>          / \    /  \
>         16  53  65  (end)
>        /   / \ /  \
>       25  46 55 64  70
> ```
> Traversal order (numbered 1→11): 16, 25, 41, 46, 53, 55, 63, 64, 65, 70, 74

- **Inorder predecessor** of a node = node visited immediately before it
  - Inorder predecessor of `63` is `55`
- **Inorder successor** of a node = node visited immediately after it
  - Inorder successor of `63` is `64`

---

## Removing a Node from BST

Removing a node is more complex than insertion or search, and can destroy ordering if done naively.

Three cases:

1. Deleting a **leaf node**
2. Deleting a node with **one child**
3. Deleting a node with **two children**

---

### Case 1: Deleting a Leaf Node (simplest)

- Simply remove the node pointer from the parent.
- Rest of the tree is NOT affected.

> 📌 Extracted from image: Delete leaf node 16
>
> ```
> Before:              After:
>      31                  31
>     /  \               /  \
>    3   95              3   95
>     \  /  \             \  /  \
>     12 78              12  78
>    / \   \            /     \
>   7  [16] 81         7      81
> ```

---

### Case 2: Deleting a Node with One Child

- Bypass the deleted node: set the parent's pointer to the deleted node's child.

> 📌 Extracted from image: Delete node 95 (one child)
>
> ```
> Before:         After:
>      31              31
>     /  \           /   \
>    3  [95]  →     3    78
>        /               \
>       78               81
>        \
>        81
> ```
> Node 31's right pointer is updated to point to node 78 (left child of 95).

---

### Case 3: Deleting a Node with Two Children

Simply moving a child up breaks BST ordering. Two correct solutions exist:

> 📌 Extracted from image: Wrong approaches for deleting root 31
>
> Both replacing root with left child (3) or right child (95) directly produce invalid BSTs — labelled **WRONG!**

---

#### Solution 1 — Use Inorder Predecessor

1. Locate the **inorder predecessor** (go to left subtree, then as far right as possible)
2. Copy its data into the current node
3. Delete the inorder predecessor node
4. Parent of inorder predecessor now points to its **left subtree**

> 📌 Extracted from image: Delete root 31 using inorder predecessor
>
> ```
> Inorder predecessor of 31 = 16
>
> Step 1: Copy 16 into root     Step 2: Delete original 16 node
>      31 → 16                        16
>     /   \                          /   \
>    3    95                         3    95
>   / \   / \                       / \   / \
>  12  78               →          12  78
> / \   \                          /     \
>7  16  81                        7(14)  81
>    /
>   14
> ```

---

#### Solution 2 — Use Inorder Successor

1. Locate the **inorder successor** (go to right child, then as far left as possible)
2. Copy its data into the current node
3. Delete the inorder successor node
4. Parent of inorder successor now points to its **right subtree**

> 📌 Extracted from image: Delete root 31 using inorder successor
>
> ```
> Inorder successor of 31 = 78
>
> Step 1: Copy 78 into root     Step 2: Delete original 78 node
>      31 → 78                        78
>     /   \                          /   \
>    3    95                         3    95
>        /  \              →              \
>       78   (end)                        81
>        \
>        81
> ```

---

## BST Implementation (C++)

### Binary Tree Node Structure

> 📌 Extracted from image: Node memory layout diagram
>
> Each node contains: `data`, `left` pointer, `right` pointer.
> Leaf nodes have both pointers set to `NULL`.

```cpp
class Node {
public:
    int data;
    Node* left;
    Node* right;
    Node(int value);
};
```

---

### BST Class Declaration (`bst.h`)

```cpp
class Node {
public:
    int data;
    Node* left;
    Node* right;
    Node(int value);
};

class BinarySearchTree {
    Node* root;
    Node* insert(Node* node, int data);
    Node* remove(Node* node, int data);
    Node* findInOrderSuccessor(Node* node);
    bool search(Node* node, int data);
    void inorder(Node* node);
    void preorder(Node* node);
    void postorder(Node* node);
public:
    BinarySearchTree();
    void Insert(int data);
    void Remove(int data);
    bool Search(int data);
    void Traverse(string order);
};
```

---

### BST Insert (`bst.cpp`)

```cpp
Node::Node(int value) {
    data = value;
    left = right = nullptr;
}

BinarySearchTree::BinarySearchTree() {
    root = nullptr;
}

Node* BinarySearchTree::insert(Node* node, int data) {
    if (node == nullptr)
        return new Node(data);
    if (data < node->data)
        node->left = insert(node->left, data);
    else
        node->right = insert(node->right, data);
    return node;
}

void BinarySearchTree::Insert(int data) {
    root = insert(root, data);
}
```

---

### BST Remove (`bst.cpp`)

```cpp
void BinarySearchTree::Remove(int data) {
    root = remove(root, data);
}

Node* BinarySearchTree::remove(Node* node, int data) {
    if (node == nullptr)
        return node;
    if (data < node->data)
        node->left = remove(node->left, data);
    else if (data > node->data)
        node->right = remove(node->right, data);
    else {
        if (node->left == nullptr) {
            Node* temp = node->right;
            delete node;
            return temp;
        } else if (node->right == nullptr) {
            Node* temp = node->left;
            delete node;
            return temp;
        }
        // Node with two children: get inorder successor
        Node* temp = findInOrderSuccessor(node->right);
        node->data = temp->data;
        node->right = remove(node->right, temp->data);
    }
    return node;
}
```

---

### BST findInOrderSuccessor (`bst.cpp`)

> 📌 Extracted from image: findInOrderSuccessor example
>
> Deleting node 6 (two children). Inorder successor is 7 (leftmost node in right subtree).
>
> ```
> Before:        After:
>      6              7
>     / \            / \
>    5   7          5   (end)
>   /   /          /
>  2   (end)      2
> / \            / \
>1   3          1   3
>     \              \
>      4              4
> ```

```cpp
Node* BinarySearchTree::findInOrderSuccessor(Node* node) {
    Node* current = node;
    while (current && current->left != nullptr)
        current = current->left;
    return current;
}
```

---

### BST Search (`bst.cpp`)

```cpp
bool BinarySearchTree::Search(int data) {
    return search(root, data);
}

bool BinarySearchTree::search(Node* node, int data) {
    if (node == nullptr)
        return false;
    if (data < node->data)
        return search(node->left, data);
    else if (data > node->data)
        return search(node->right, data);
    else
        return true;
}
```

---

### BST Traverse (`bst.cpp`)

```cpp
void BinarySearchTree::Traverse(string order) {
    if (order == "inorder") {
        inorder(root);
    } else if (order == "preorder") {
        preorder(root);
    } else if (order == "postorder") {
        postorder(root);
    } else {
        cout << "Invalid traversal order." << endl;
    }
    cout << endl;
}

void BinarySearchTree::inorder(Node* node) {
    if (node != nullptr) {
        inorder(node->left);
        cout << node->data << " ";
        inorder(node->right);
    }
}

void BinarySearchTree::preorder(Node* node) {
    if (node != nullptr) {
        cout << node->data << " ";
        preorder(node->left);
        preorder(node->right);
    }
}

void BinarySearchTree::postorder(Node* node) {
    if (node != nullptr) {
        postorder(node->left);
        postorder(node->right);
        cout << node->data << " ";
    }
}
```

---

## Assignment 2

**i.** Write the `main` function that uses the BST implementation to:

1. Insert the following values in order: `40, 20, 66, 1, 32, 51, 78`
2. Traverse the tree using:
   1. In-order
   2. Pre-order
   3. Post-order
3. Remove value `66`
4. Traverse the tree again using In-order

**ii.** Write a function to display the tree of numbers using `/` and `\`.

**iii.** Display the tree after each task.
