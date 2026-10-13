
## Topic: Binary Trees, Tree Traversals, BST and Heaps

# 1. Binary Tree

A **binary tree** is a tree in which each node has at most two children:

- Left child
    
- Right child
    

A node does not need to have both children.

### Example

```
             50
           /    \
         30      70
        /  \    /  \
       20  40  60  80
```

### Important terminology

|Term|Meaning|Example|
|---|---|---|
|Root|Topmost node|50|
|Parent|A node that has a child|30 is the parent of 20|
|Child|A node directly below its parent|40 is a child of 30|
|Leaf|Node with no children|20, 40, 60, 80|
|Edge|Connection between two nodes|50 to 30|
|Subtree|A node and its descendants|Subtree rooted at 30|
|Depth|Number of edges from the root to a node|Depth of 20 is 2|
|Height|Longest downward path, measured in edges|Height of this tree is 2|

**Exam trap:** A binary tree permits at most two children per node, not exactly two.

## 1.1 Creating a binary tree in Python

Each node can be represented by a class containing three fields: data, left child, and right child.

```
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None


root = Node(50)

root.left = Node(30)
root.right = Node(70)

root.left.left = Node(20)
root.left.right = Node(40)

root.right.left = Node(60)
root.right.right = Node(80)

print(root.data)
print(root.left.data)
print(root.right.data)
```

Output:

```
50
30
70
```

The `root` variable refers to node 50. Its `left` and `right` attributes refer to the roots of its two subtrees.

## 1.2 Important binary tree properties

- Each node has at most two children.
    
- Maximum number of nodes at level L, when the root is at level 0: `2^L`
    
- Maximum number of nodes in a binary tree of height h, measured in edges: `2^(h+1) - 1`
    
- A binary tree with n nodes has `n - 1` edges, provided `n >= 1`.
    

Example: A perfect binary tree of height 2 has a maximum of:

`2^(2+1) - 1 = 7 nodes`

The example tree containing 50, 30, 70, 20, 40, 60 and 80 has seven nodes.

# 2. Tree Traversal

**Traversal** means visiting every node of a tree in a particular order.

The three depth-first traversals covered here are:

1. Preorder
    
2. Inorder
    
3. Postorder
    

Use this tree for all three examples:

```
             50
           /    \
         30      70
        /  \    /  \
       20  40  60  80
```

## 2.1 Preorder Traversal

**Rule:** Root → Left → Right

**Mnemonic:** NLR — Node, Left, Right.

Steps:

1. Visit 50.
    
2. Traverse the left subtree: 30, 20, 40.
    
3. Traverse the right subtree: 70, 60, 80.
    

Output:

```
50 30 20 40 70 60 80
```

Python implementation:

```
def preorder(root):
    if root is None:
        return

    print(root.data, end=" ")
    preorder(root.left)
    preorder(root.right)
```

Uses:

- Copying a tree
    
- Producing a prefix representation of an expression tree
    

## 2.2 Inorder Traversal

**Rule:** Left → Root → Right

**Mnemonic:** LNR — Left, Node, Right.

Steps:

1. Traverse the left subtree: 20, 30, 40.
    
2. Visit the root: 50.
    
3. Traverse the right subtree: 60, 70, 80.
    

Output:

```
20 30 40 50 60 70 80
```

Python implementation:

```
def inorder(root):
    if root is None:
        return

    inorder(root.left)
    print(root.data, end=" ")
    inorder(root.right)
```

**Important exam fact:** Inorder traversal of a BST with distinct keys produces the keys in ascending order.

For a general binary tree, inorder traversal does not necessarily produce sorted output.

## 2.3 Postorder Traversal

**Rule:** Left → Right → Root

**Mnemonic:** LRN — Left, Right, Node.

Steps:

1. Traverse the left subtree: 20, 40, 30.
    
2. Traverse the right subtree: 60, 80, 70.
    
3. Visit the root: 50.
    

Output:

```
20 40 30 60 80 70 50
```

Python implementation:

```
def postorder(root):
    if root is None:
        return

    postorder(root.left)
    postorder(root.right)
    print(root.data, end=" ")
```

Uses:

- Deleting or freeing a tree from the leaves upward
    
- Evaluating expression trees
    

## 2.4 Comparison of tree traversals

|Traversal|Order|Mnemonic|Output|
|---|---|---|---|
|Preorder|Root → Left → Right|NLR|50 30 20 40 70 60 80|
|Inorder|Left → Root → Right|LNR|20 30 40 50 60 70 80|
|Postorder|Left → Right → Root|LRN|20 40 30 60 80 70 50|

### Time and space complexity

- Time complexity for each traversal: `O(n)`, because every node is visited once.
    
- Auxiliary space for recursive traversal: `O(h)`, where h is the tree height, due to the function-call stack.
    

## 2.5 Traversal practice

Consider this tree:

```
        A
       / \
      B   C
     / \
    D   E
```

Correct outputs:

|Traversal|Output|
|---|---|
|Preorder|A B D E C|
|Inorder|D B E A C|
|Postorder|D E B C A|

# 3. Binary Search Tree (BST)

A **Binary Search Tree (BST)** is a binary tree that follows an ordering rule.

For a BST with distinct keys:

- Values smaller than a node go into its left subtree.
    
- Values greater than a node go into its right subtree.
    
- Both subtrees must also follow the BST rule.
    

Example:

```
             50
           /    \
         30      70
        /  \    /  \
       20  40  60  80
```

This is a BST because:

- 30 < 50 and 70 > 50.
    
- 20 < 30 < 50.
    
- 40 > 30 but 40 < 50.
    
- 60 > 50 but 60 < 70.
    
- 80 > 70 > 50.
    

## 3.1 BST vs general binary tree

|Feature|Binary Tree|BST|
|---|---|---|
|Maximum children per node|Two|Two|
|Ordering rule|No required key ordering|Left keys are smaller and right keys are larger, for distinct keys|
|Search|Can require O(n)|O(log n) average when reasonably balanced|
|Inorder traversal|Not necessarily sorted|Sorted order for distinct keys|
|Every BST is a binary tree?|—|Yes|
|Every binary tree is a BST?|No|No|

**Exam trap:** A BST is a special type of binary tree, not a completely different tree structure.

# 4. BST Insertion

Insertion adds a new value while preserving the BST ordering property.

For the following example, assume duplicate values are ignored.

Starting BST:

```
        50
       /  \
      30   70
```

Insert 40:

1. Compare 40 with 50. Since 40 < 50, go left.
    
2. Compare 40 with 30. Since 40 > 30, go right.
    
3. The right position beneath 30 is empty, so insert 40 there.
    

Result:

```
        50
       /  \
      30   70
        \
         40
```

## 4.1 Python implementation of BST insertion

```
class Node:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None


def insert(root, key):
    if root is None:
        return Node(key)

    if key < root.key:
        root.left = insert(root.left, key)
    elif key > root.key:
        root.right = insert(root.right, key)

    # Duplicate keys are ignored.
    return root


def inorder(root):
    if root is not None:
        inorder(root.left)
        print(root.key, end=" ")
        inorder(root.right)


root = None

for value in [50, 30, 70, 20, 40, 60, 80]:
    root = insert(root, value)

inorder(root)
```

Output:

```
20 30 40 50 60 70 80
```

## 4.2 BST insertion complexity

|BST shape|Time complexity|
|---|---|
|Balanced tree|O(log n)|
|Average case under suitable random-insertion assumptions|Expected O(log n)|
|Skewed tree|O(n)|

A BST can become skewed if values are inserted in sorted order.

For example, inserting `10, 20, 30, 40` produces a structure resembling a linked list rather than a balanced tree.

**Exam trap:** Ordinary BST insertion is not guaranteed to be O(log n). Its cost depends on tree height.

# 5. BST Deletion

Deletion is more complicated than insertion because the BST property must be preserved.

There are three main cases.

## Case 1: Deleting a leaf node

A leaf has no children.

Before deleting 20:

```
        50
       /  \
      30   70
     /
    20
```

After deletion:

```
        50
       /  \
      30   70
```

Because 20 has no children, its parent's reference to it is set to `None`.

## Case 2: Deleting a node with one child

Suppose we delete 30:

```
        50
       /  \
      30   70
        \
         40
```

After deletion:

```
        50
       /  \
      40   70
```

The node's parent is linked directly to its only child.

## Case 3: Deleting a node with two children

This is the most important case.

Suppose we delete 50:

```
             50
           /    \
         30      70
        /  \    /  \
       20  40  60  80
```

We can replace 50 with its **inorder successor**, the smallest key in its right subtree.

The smallest key in the right subtree is 60.

After replacing 50 with 60 and removing the original 60 node:

```
             60
           /    \
         30      70
        /  \       \
       20  40       80
```

The BST property is preserved.

An inorder predecessor — the largest key in the left subtree — can also be used.

## 5.1 Python implementation of BST deletion

```
class Node:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None


def insert(root, key):
    if root is None:
        return Node(key)

    if key < root.key:
        root.left = insert(root.left, key)
    elif key > root.key:
        root.right = insert(root.right, key)

    return root


def min_node(root):
    current = root

    while current.left is not None:
        current = current.left

    return current


def delete_node(root, key):
    if root is None:
        return None

    if key < root.key:
        root.left = delete_node(root.left, key)

    elif key > root.key:
        root.right = delete_node(root.right, key)

    else:
        # Case 1 and case 2: No left child.
        if root.left is None:
            return root.right

        # Case 2: No right child.
        if root.right is None:
            return root.left

        # Case 3: Two children.
        successor = min_node(root.right)
        root.key = successor.key
        root.right = delete_node(root.right, successor.key)

    return root


def inorder(root):
    if root is not None:
        inorder(root.left)
        print(root.key, end=" ")
        inorder(root.right)


root = None

for value in [50, 30, 70, 20, 40, 60, 80]:
    root = insert(root, value)

root = delete_node(root, 50)
inorder(root)
```

Output:

```
20 30 40 60 70 80
```

**Exam trap:** When deleting a BST node with two children, use a replacement strategy such as the inorder successor or predecessor.

### BST deletion complexity

- Balanced BST: `O(log n)`
    
- Skewed BST: `O(n)`
    
- The cost depends on tree height, just as it does for insertion and searching.
    

# 6. Heap

A **heap** is a specialized tree-based data structure that satisfies two properties.

1. **Shape property:** A binary heap is a complete binary tree. Every level is full except possibly the last, which is filled from left to right.
    
2. **Heap-order property:** Parent and child values satisfy the min-heap or max-heap rule.
    

Heaps are commonly used to implement priority queues.

## 6.1 Min-heap

In a min-heap, each parent is less than or equal to its children. Therefore, the minimum value is at the root.

Example:

```
             10
           /    \
         20      15
        /  \
       40  50
```

The root, 10, is the minimum.

A heap does not require every element in the left subtree to be smaller than every element in the right subtree. That is different from a BST.

## 6.2 Max-heap

In a max-heap, each parent is greater than or equal to its children. Therefore, the maximum value is at the root.

```
             50
           /    \
         30      40
        /  \
       10  20
```

The root, 50, is the maximum.

### Min-heap vs max-heap

|Feature|Min-heap|Max-heap|
|---|---|---|
|Root contains|Minimum|Maximum|
|Parent-child rule|Parent ≤ children|Parent ≥ children|
|Typical use|Retrieve smallest item quickly|Retrieve largest item quickly|
|Heap shape|Complete binary tree|Complete binary tree|

**Exam trap:** A heap is not necessarily a BST. A heap maintains local ordering between parents and children, not global ordering across entire subtrees.

## 6.3 Array representation of a binary heap

A binary heap is commonly stored in an array.

Example:

```
Heap: [10, 20, 15, 40, 50]
```

Corresponding tree:

```
             10                 Index 0
           /    \
         20      15              Index 1, 2
        /  \
       40  50                    Index 3, 4
```

For an element at index `i` in a zero-indexed array:

- Left child: `2*i + 1`
    
- Right child: `2*i + 2`
    
- Parent: `(i - 1) // 2`, when `i > 0`
    

Examples:

- For `i = 1`, the children are at indexes 3 and 4.
    
- For `i = 4`, the parent is at index 1.
    

**Important:** These formulas assume zero-based indexing. One-based indexing uses different formulas.

## 6.4 Heap insertion

When inserting into a binary heap:

1. Place the new element in the next available position to preserve the complete-tree shape.
    
2. Compare it with its parent.
    
3. If the heap property is violated, swap it with the parent.
    
4. Continue until the property is restored or the root is reached.
    

This process is called **sift-up** or **bubble-up**.

### Min-heap example

Insert 5 into:

```
             10
           /    \
         20      15
        /  \
       40  50
```

First, put 5 in the next available position:

```
             10
           /    \
         20      15
        /  \    /
       40  50  5
```

Compare 5 with 15 and swap:

```
             10
           /    \
         20      5
        /  \    /
       40  50  15
```

Compare 5 with 10 and swap again:

```
              5
            /   \
          20     10
         /  \   /
        40  50 15
```

The min-heap property is restored.

**Complexity:** `O(log n)`, because the element can move upward by at most the height of the heap.

## 6.5 Removing the root

In a min-heap, removing the root removes the minimum element.

Procedure:

1. Save the root value.
    
2. Move the last element to the root.
    
3. Remove the last position.
    
4. Sift the replacement downward, swapping it with the smaller child when necessary.
    

For a heap of n elements, this takes `O(log n)` time.

A heap is designed to retrieve its minimum or maximum efficiently, not to search for an arbitrary value.

## 6.6 Heap implementation in Python using `heapq`

Python's `heapq` module implements a min-heap.

```
import heapq

numbers = [40, 10, 30, 20, 50]

heapq.heapify(numbers)

print("Heap:", numbers)
print("Minimum:", numbers[0])

heapq.heappush(numbers, 5)

print("After insertion:", numbers)

smallest = heapq.heappop(numbers)

print("Removed:", smallest)
print("Remaining heap:", numbers)
```

Key observations:

- The minimum is 10 immediately after `heapify()`.
    
- After inserting 5, the minimum becomes 5.
    
- `heappop()` removes and returns 5.
    
- The list's internal order is not necessarily sorted.
    

### Heap complexity table

|Operation|Typical time complexity|
|---|---|
|Get minimum in a min-heap|O(1)|
|Insert using `heappush()`|O(log n)|
|Remove minimum using `heappop()`|O(log n)|
|Build a heap using `heapify()`|O(n)|
|Search for an arbitrary value|O(n)|

**Exam trap:** `heapify()` builds a heap in `O(n)` time. Inserting n elements individually with `heappush()` has an `O(n log n)` worst-case upper bound.

# 7. BST vs Heap — Important Comparison

Both are tree-based data structures, but they serve different purposes.

|Feature|Binary Search Tree (BST)|Binary Heap|
|---|---|---|
|Main property|Left keys are smaller; right keys are larger, for distinct keys|Parent-child ordering is maintained|
|Root|Not necessarily minimum or maximum|Minimum in a min-heap; maximum in a max-heap|
|Shape|Can be balanced or skewed|Complete binary tree|
|Search for arbitrary key|O(log n) average in a reasonably balanced BST; O(n) worst case|O(n) worst case|
|Insert|Depends on tree height|O(log n)|
|Remove minimum/maximum|Depends on tree structure|O(log n) for root removal|
|Inorder traversal|Sorted order for distinct keys|Not necessarily sorted|
|Common use|Searching and ordered data|Priority queues|

# 8. Binary Tree Types — Extra Revision

These terms can appear in conceptual MCQs.

## 8.1 Full binary tree

Every node has either zero or two children.

```
    A
   / \
  B   C
```

## 8.2 Complete binary tree

All levels except possibly the last are full, and the last level is filled from left to right.

```
    A
   / \
  B   C
 /
D
```

## 8.3 Perfect binary tree

Every internal node has two children, and every leaf is at the same depth.

```
        A
       / \
      B   C
     / \ / \
    D  E F  G
```

A heap must be a complete binary tree, but a complete binary tree is not necessarily a heap. It must also satisfy the heap-order property.

# 9. Final Revision Sheet

|Topic|Key point|
|---|---|
|Binary tree|At most two children per node|
|Preorder|Root → Left → Right|
|Inorder|Left → Root → Right|
|Postorder|Left → Right → Root|
|BST|Ordered binary tree|
|BST insertion|Follow comparisons until an empty position|
|BST deletion|Leaf, one-child, and two-child cases|
|Inorder successor|Smallest key in the right subtree|
|Inorder predecessor|Largest key in the left subtree|
|Min-heap|Parent ≤ children|
|Max-heap|Parent ≥ children|
|Binary heap shape|Complete binary tree|
|Heap insertion/removal|O(log n)|
|Heap minimum/maximum at root|O(1) to inspect|
|Heap construction with `heapify()`|O(n)|

## Highest-priority exam concepts

1. Memorize the three traversal orders and practise tracing them.
    
2. Practise BST insertion and all three deletion cases.
    
3. Distinguish BST ordering from heap ordering.
    
4. Learn the heap array index formulas:
    
    - Left child: `2*i + 1`
        
    - Right child: `2*i + 2`
        
    - Parent: `(i - 1) // 2`, for `i > 0`
        
5. Memorize heap operation complexities, especially `heapify()` = `O(n)`.
    
6. Understand the differences between full, complete and perfect binary trees.