# 1. Binary tree

A binary tree is a tree in which each node has at most two children:

- Left child
    
- Right child
    

A node does not have to contain both children.

Consider this binary tree:

```
             50             ← Root
           /    \
         30      70
        /  \    /  \
       20  40  60  80
```

Important terminology:

|Term|Meaning|Example|
|---|---|---|
|Root|Topmost node|`50`|
|Parent|A node that has a child|`30` is parent of `20`|
|Child|A node directly below its parent|`40` is a child of `30`|
|Leaf|Node with no children|`20`, `40`, `60`, `80`|
|Edge|Connection between two nodes|`50` to `30`|
|Subtree|A node and its descendants|Subtree rooted at `30`|
|Depth|Number of edges from root to a node|Depth of `20` is `2`|
|Height|Longest downward path, measured in edges|Height of this tree is `2`|

Exam trap: A binary tree allows at most two children per node, not exactly two.

## 1.1 Creating a binary tree in Python

We can represent each node using a class with three fields: data, left child, and right child.

```
class Node:    def __init__(self, data):        self.data = data        self.left = None        self.right = Noneroot = Node(50)root.left = Node(30)root.right = Node(70)root.left.left = Node(20)root.left.right = Node(40)root.right.left = Node(60)root.right.right = Node(80)print(root.data)print(root.left.data)print(root.right.data)
```

Output:

```
50
30
70
```

The `root` variable refers to node `50`. Its `left` and `right` attributes refer to the roots of its two subtrees.

### Important binary tree properties

For a binary tree:

- Each node has at most two children.
    
- The maximum number of nodes at level \(L\), when the root is at level \(0\), is \(2^L\).
    
- The maximum number of nodes in a binary tree of height \(h\), measured in edges, is \(2^{h+1}-1\).
    
- A binary tree with \(n\) nodes has \(n-1\) edges, provided \(n\geq1\).
    

For example, a perfect binary tree of height \(2\) has a maximum of:

\[ 2^{2+1}-1=7 \text{ nodes} \]

The example tree containing `50`, `30`, `70`, `20`, `40`, `60`, and `80` has seven nodes.

# 2. Tree traversal

Traversal means visiting every node of a tree in a particular order.

The three depth-first traversals in your syllabus are:

1. Preorder
    
2. Inorder
    
3. Postorder
    

All three use the same tree, but they visit the root and subtrees in different orders.

Use this tree for all three examples:

```
             50
           /    \
         30      70
        /  \    /  \
       20  40  60  80
```

## 2.1 Preorder traversal

Rule: Root → Left → Right

Remember: NLR — Node, Left, Right.

Steps for the example tree:

1. Visit `50`.
    
2. Traverse the left subtree: `30`, `20`, `40`.
    
3. Traverse the right subtree: `70`, `60`, `80`.
    

Result:

```
50 30 20 40 70 60 80
```

Python implementation:

```
def preorder(root):    if root is None:        return    print(root.data, end=" ")    preorder(root.left)    preorder(root.right)
```

Calling `preorder(root)` prints:

```
50 30 20 40 70 60 80
```

Uses: Preorder traversal is useful when processing a node before its children, such as copying a tree or producing a prefix representation of an expression tree.

## 2.2 Inorder traversal

Rule: Left → Root → Right

Remember: LNR — Left, Node, Right.

For our tree:

1. Traverse the left subtree: `20`, `30`, `40`.
    
2. Visit root: `50`.
    
3. Traverse the right subtree: `60`, `70`, `80`.
    

Result:

```
20 30 40 50 60 70 80
```

Python implementation:

```
def inorder(root):    if root is None:        return    inorder(root.left)    print(root.data, end=" ")    inorder(root.right)
```

Calling `inorder(root)` prints:

```
20 30 40 50 60 70 80
```

Highly important exam fact: Inorder traversal of a BST with distinct keys produces the keys in ascending order.

For a general binary tree, inorder traversal does not necessarily produce sorted output.

## 2.3 Postorder traversal

Rule: Left → Right → Root

Remember: LRN — Left, Right, Node.

For our tree:

1. Traverse the left subtree: `20`, `40`, `30`.
    
2. Traverse the right subtree: `60`, `80`, `70`.
    
3. Visit root: `50`.
    

Result:

```
20 40 30 60 80 70 50
```

Python implementation:

```
def postorder(root):    if root is None:        return    postorder(root.left)    postorder(root.right)    print(root.data, end=" ")
```

Calling `postorder(root)` prints:

```
20 40 30 60 80 70 50
```

Uses: Postorder traversal is useful for deleting or freeing a tree from the leaves upward and for evaluating expression trees.

## 2.4 Compare all three traversals

This is one of the most important tables to memorize.

|Traversal|Order|Mnemonic|Output for our tree|
|---|---|---|---|
|Preorder|Root → Left → Right|NLR|`50 30 20 40 70 60 80`|
|Inorder|Left → Root → Right|LNR|`20 30 40 50 60 70 80`|
|Postorder|Left → Right → Root|LRN|`20 40 30 60 80 70 50`|

The functions take \(O(n)\) time because every node is visited exactly once.

For a recursive implementation, auxiliary space is \(O(h)\), where \(h\) is the height of the tree, due to the function-call stack.

### Quick traversal practice

Consider this smaller tree:

```
        A
       / \
      B   C
     / \
    D   E
```

### Identify the traversal output

Choose the correct output for each traversal.

Preorder

A B D E C

D B E A C

D E B C A

Inorder

A B D E C

D B E A C

D B E A C

Postorder

A B D E C

D B E C A

D E B C A

# 3. Binary Search Tree (BST)

A Binary Search Tree (BST) is a binary tree that follows an ordering rule.

For a BST with distinct keys:

- Values smaller than a node go into its left subtree.
    
- Values greater than a node go into its right subtree.
    
- Both subtrees must themselves obey the BST rule.
    

Consider:

```
             50
           /    \
         30      70
        /  \    /  \
       20  40  60  80
```

This is a BST because:

- `30 < 50` and `70 > 50`.
    
- `20 < 30 < 50`.
    
- `40 > 30` but `40 < 50`.
    
- `60 > 50` but `60 < 70`.
    
- `80 > 70 > 50`.
    

### BST vs general binary tree

|Feature|Binary tree|BST|
|---|---|---|
|Maximum children per node|Two|Two|
|Ordering rule|No required key ordering|Left keys are smaller and right keys are larger, for distinct keys|
|Search|Can require \(O(n)\)|Average \(O(\log n)\) when reasonably balanced|
|Inorder traversal|Not necessarily sorted|Sorted order for distinct keys|
|Every BST is a binary tree?|—|Yes|
|Every binary tree is a BST?|No|No|

Exam trap: A BST is a special type of binary tree, not a completely different tree structure.

## 4. BST insertion

Insertion adds a new value while preserving the BST ordering property.

For this example, assume duplicate values are ignored.

Starting BST:

```
        50
       /  \
      30   70
```

Insert `40`:

1. Compare `40` with `50`. Since `40 < 50`, go left.
    
2. Compare `40` with `30`. Since `40 > 30`, go right.
    
3. The right position beneath `30` is empty, so insert `40` there.
    

Result:

```
        50
       /  \
      30   70
        \
         40
```

### Python implementation

```
class Node:    def __init__(self, key):        self.key = key        self.left = None        self.right = Nonedef insert(root, key):    if root is None:        return Node(key)    if key < root.key:        root.left = insert(root.left, key)    elif key > root.key:        root.right = insert(root.right, key)    # Duplicate keys are ignored.    return rootdef inorder(root):    if root is not None:        inorder(root.left)        print(root.key, end=" ")        inorder(root.right)root = Nonefor value in [50, 30, 70, 20, 40, 60, 80]:    root = insert(root, value)inorder(root)
```

Output:

```
20 30 40 50 60 70 80
```

### Complexity of insertion

|BST shape|Time complexity|
|---|---|
|Balanced tree|\(O(\log n)\)|
|Average case for common random insertion orders|Expected \(O(\log n)\), under suitable assumptions|
|Skewed tree|\(O(n)\)|

A BST can become skewed if values are inserted in sorted order.

For example, inserting `10, 20, 30, 40` produces a structure resembling a linked list rather than a balanced tree.

Exam trap: Ordinary BST insertion is not guaranteed to be \(O(\log n)\). That bound depends on tree height; a skewed BST can take \(O(n)\).

# 5. BST deletion

Deletion is more complicated than insertion because removing a node must preserve the BST property.

There are three main deletion cases.

## Case 1: Deleting a leaf node

A leaf has no children.

Before deleting `20`:

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

Because `20` has no children, its parent's reference to it is set to `None`.

## Case 2: Deleting a node with one child

Suppose we delete `30`:

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

The node's parent is linked directly to its only child. The subtree containing `40` remains connected.

## Case 3: Deleting a node with two children

This is the most important case.

Suppose we delete `50`:

```
             50
           /    \
         30      70
        /  \    /  \
       20  40  60  80
```

We can replace `50` with its inorder successor, the smallest key in its right subtree.

The smallest key in the right subtree is `60`.

After replacing `50` with `60` and removing the original `60` node:

```
             60
           /    \
         30      70
        /  \       \
       20  40       80
```

The BST property is preserved.

An inorder predecessor — the largest key in the left subtree — can also be used instead.

## 5.1 Python implementation of BST deletion

```
class Node:    def __init__(self, key):        self.key = key        self.left = None        self.right = Nonedef insert(root, key):    if root is None:        return Node(key)    if key < root.key:        root.left = insert(root.left, key)    elif key > root.key:        root.right = insert(root.right, key)    return rootdef min_node(root):    current = root    while current.left is not None:        current = current.left    return currentdef delete_node(root, key):    if root is None:        return None    if key < root.key:        root.left = delete_node(root.left, key)    elif key > root.key:        root.right = delete_node(root.right, key)    else:        # Case 1: No left child        if root.left is None:            return root.right
```

Output:

```
20 30 40 60 70 80
```

Exam trap: When deleting a BST node with two children, simply removing it would leave its subtrees disconnected. Use a replacement strategy, such as the inorder successor or predecessor.

### BST deletion complexity

- Balanced BST: \(O(\log n)\).
    
- Skewed BST: \(O(n)\).
    
- The cost depends on the tree height, just as it does for insertion and searching.
    

# 6. Heap

A heap is a specialized tree-based data structure that satisfies two properties:

1. Shape property: A binary heap is a complete binary tree. Every level is full except possibly the last, and the last level is filled from left to right.
    
2. Heap-order property: Parent and child values satisfy the min-heap or max-heap rule.
    

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

The root `10` is the minimum.

Notice that the heap does not require every element in the left subtree to be smaller than every element in the right subtree, unlike a BST.

## 6.2 Max-heap

In a max-heap, each parent is greater than or equal to its children. Therefore, the maximum value is at the root.

```
             50
           /    \
         30      40
        /  \
       10  20
```

The root `50` is the maximum.

### Min-heap vs max-heap

|Feature|Min-heap|Max-heap|
|---|---|---|
|Root contains|Minimum|Maximum|
|Parent-child rule|Parent ≤ children|Parent ≥ children|
|Typical use|Retrieve smallest item quickly|Retrieve largest item quickly|
|Heap shape|Complete binary tree|Complete binary tree|

Exam trap: A heap is not necessarily a BST. In a min-heap, values are ordered locally between parents and children, not globally across entire left and right subtrees.

## 6.3 Array representation of a binary heap

A binary heap is commonly stored in an array rather than using explicit node objects.

For a zero-indexed array representation:

```
Heap: [10, 20, 15, 40, 50]
```

Corresponding tree:

```
             10                 Index 0
           /    \
         20      15             Index 1, 2
        /  \
       40  50                   Index 3, 4
```

For an element at index \(i\):

\[ \text{Left child}=2i+1 \]

\[ \text{Right child}=2i+2 \]

\[ \text{Parent}=\left\lfloor\frac{i-1}{2}\right\rfloor \]

The parent formula is used only when \(i>0\).

Example: For `i = 1`, the children are at indexes `3` and `4`. For `i = 4`, its parent is at index `1`.

Important: These formulas assume zero-based indexing. A one-based heap representation uses different formulas.

## 6.4 Heap insertion

When inserting into a binary heap:

1. Place the new element in the next available position to preserve the complete-tree shape.
    
2. Compare it with its parent.
    
3. If the heap property is violated, swap it with the parent.
    
4. Continue until the property is restored or the root is reached.
    

This is called sift-up, or bubble-up.

### Min-heap example

Insert `5` into:

```
             10
           /    \
         20      15
        /  \
       40  50
```

First put `5` in the next available position:

```
             10
           /    \
         20      15
        /  \    /
       40  50  5
```

Now sift `5` upward:

```
             10              Compare 5 with 15
           /    \
         20      5            Swap
        /  \    /
       40  50  15
```

Compare `5` with `10`, then swap again:

```
              5
           /     \
         20       10
        /  \     /
       40  50   15
```

The min-heap property is restored.

Complexity: \(O(\log n)\), because the element can move up at most the height of the heap.

## 6.5 Removing the root

In a min-heap, removing the root removes the minimum element.

The typical procedure is:

1. Save the root value.
    
2. Move the last element to the root.
    
3. Remove the last position.
    
4. Sift the replacement downward by swapping it with the smaller child when necessary.
    

For a heap of \(n\) elements, this takes \(O(\log n)\) time.

The key difference from a BST is that a heap is designed to efficiently retrieve its minimum or maximum element, not to search for an arbitrary value.

## 6.6 Heap implementation in Python using `heapq`

Python's `heapq` module implements a min-heap.

```
import heapqnumbers = [40, 10, 30, 20, 50]heapq.heapify(numbers)print("Heap:", numbers)print("Minimum:", numbers[0])heapq.heappush(numbers, 5)print("After insertion:", numbers)smallest = heapq.heappop(numbers)print("Removed:", smallest)print("Remaining heap:", numbers)
```

The exact internal arrangement depends on heap operations, but the output values will show:

- The minimum is `10` immediately after `heapify()`.
    
- The inserted `5` becomes the minimum.
    
- `heappop()` removes and returns `5`.
    

The list's internal order is not necessarily sorted. A heap only guarantees its heap-order property.

### Heap complexity table

|Operation|Typical time complexity|
|---|---|
|Get minimum in min-heap|\(O(1)\)|
|Insert using `heappush()`|\(O(\log n)\)|
|Remove minimum using `heappop()`|\(O(\log n)\)|
|Build a heap using `heapify()`|\(O(n)\)|
|Search for an arbitrary value|\(O(n)\)|

Exam trap: `heapify()` builds a heap in \(O(n)\) time; inserting \(n\) elements individually using `heappush()` takes \(O(n\log n)\) in the worst-case bound.

# 7. BST vs heap — important comparison

Both are tree-based data structures, but they serve different purposes.

|Feature|Binary search tree (BST)|Binary heap|
|---|---|---|
|Main property|Left subtree keys are smaller; right subtree keys are larger, for distinct keys|Parent-child ordering is maintained|
|Root|Not necessarily minimum or maximum|Minimum in min-heap; maximum in max-heap|
|Shape|Can be balanced or skewed|Complete binary tree|
|Search for arbitrary key|\(O(\log n)\) average in a reasonably balanced BST; \(O(n)\) worst case|\(O(n)\) worst case|
|Insert|Depends on tree height|\(O(\log n)\)|
|Remove minimum/maximum|Depends on tree structure|\(O(\log n)\) for root removal|
|Inorder traversal|Sorted order for distinct keys|Not necessarily sorted|
|Common use|Searching and ordered data|Priority queues|

## 8. Binary tree types — extra revision

These terms can appear in conceptual MCQs.

Full binary tree

Every node has either zero or two children.

A 
/ \
B C

Complete binary tree

All levels except possibly the last are full, and the last level is filled from left to right.

A 
/ \
B C 
/ D

Perfect binary tree

Every internal node has two children, and every leaf is at the same depth.

A 
/ \
B C 
/ \ / \
D E F G

A heap must be a complete binary tree, but a complete binary tree is not necessarily a heap; it must also satisfy the heap-order property.

## Final revision sheet

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
|Min-heap|Parent ≤ children|
|Max-heap|Parent ≥ children|
|Binary heap shape|Complete binary tree|
|Heap insertion/removal|\(O(\log n)\)|
|Heap minimum/maximum at root|\(O(1)\) to inspect|
|Heap construction with `heapify()`|\(O(n)\)|

Highest-priority exam concepts: Memorize the three traversal orders, practise tracing BST insertion and deletion, distinguish BST ordering from heap ordering, and learn the array index formulas for heap children and parents.