# Linked Lists in Data Structures

## 1. Basic Structure of a Linked List

A linked list is a linear data structure made up of nodes connected through references or pointers.

Each node typically contains:

- **Data:** The value stored in the node.
    
- **Link/Pointer:** A reference to another node.
    

### Singly Linked List Structure

```
head
  |
  v
[10 | next] → [20 | next] → [30 | None]
```

- `head` points to the first node.
    
- The last node's `next` reference is `None`.
    
- Nodes are connected through references rather than stored as one contiguous block.
    

**Python note:** Python does not have a built-in linked-list collection like its built-in `list`. Linked lists can be implemented using objects and references.

---

## 2. Singly Linked List

A singly linked list stores data and a reference to the next node. Each node can move only forward through the list.

### 2.1 Creating Nodes in Python

```
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None


first = Node(10)
second = Node(20)
third = Node(30)

first.next = second
second.next = third

print(first.data)
print(first.next.data)
print(first.next.next.data)
```

Output:

```
10
20
30
```

Explanation:

- `first.data` accesses the first node's data.
    
- `first.next.data` accesses the second node's data.
    
- `first.next.next.data` accesses the third node's data.
    

### 2.2 Traversing a Singly Linked List

Traversal means visiting each node starting from `head` until the end of the list is reached.

```
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None


head = Node(10)
head.next = Node(20)
head.next.next = Node(30)

current = head

while current is not None:
    print(current.data)
    current = current.next
```

Output:

```
10
20
30
```

The condition `current is not None` stops traversal when the end of the list is reached.

**Exam trap:** Accessing `current.next` after `current` becomes `None` raises an `AttributeError`.

---

## 3. Singly Linked List: Insertion

Insertion means adding a new node to a linked list.

Common cases:

1. Insertion at the beginning.
    
2. Insertion at the end.
    
3. Insertion after a specified node.
    

### 3.1 Insertion at the Beginning

Before:

```
10 → 20 → 30 → None
```

Insert `5` at the beginning.

After:

```
5 → 10 → 20 → 30 → None
```

The new node points to the previous head, and then `head` is updated.

```
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None


head = Node(10)
head.next = Node(20)
head.next.next = Node(30)

new_node = Node(5)
new_node.next = head
head = new_node

current = head

while current is not None:
    print(current.data)
    current = current.next
```

Output:

```
5
10
20
30
```

**Time complexity: O(1)** because no traversal is required.

### 3.2 Insertion at the End

To insert at the end, traverse to the last node and connect its `next` reference to the new node.

```
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None


head = Node(10)
head.next = Node(20)

new_node = Node(30)

current = head

while current.next is not None:
    current = current.next

current.next = new_node

current = head

while current is not None:
    print(current.data)
    current = current.next
```

Output:

```
10
20
30
```

**Time complexity:**

- O(n) when only `head` is maintained.
    
- O(1) when a `tail` reference is maintained.
    

### 3.3 Insertion After a Specified Node

Suppose we want to insert `25` after the node containing `20`.

Before:

```
10 → 20 → 30 → None
```

After:

```
10 → 20 → 25 → 30 → None
```

```
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None


head = Node(10)
head.next = Node(20)
head.next.next = Node(30)

current = head.next  # Node containing 20

new_node = Node(25)
new_node.next = current.next
current.next = new_node

current = head

while current is not None:
    print(current.data)
    current = current.next
```

Output:

```
10
20
25
30
```

**Important:** First connect the new node to the remainder of the list. Then connect the current node to the new node.

- Insertion after a known node: O(1).
    
- Finding the target node by value: O(n).
    

---

## 4. Singly Linked List: Deletion

Deletion removes a node by changing the relevant references.

### 4.1 Deletion from the Beginning

Before:

```
10 → 20 → 30 → None
```

After deleting the first node:

```
20 → 30 → None
```

The head is moved to the second node.

```
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None


head = Node(10)
head.next = Node(20)
head.next.next = Node(30)

if head is not None:
    head = head.next

current = head

while current is not None:
    print(current.data)
    current = current.next
```

Output:

```
20
30
```

**Time complexity: O(1).**

### 4.2 Deletion from the End

To delete the final node in a singly linked list, find the second-last node and set its `next` reference to `None`.

```
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None


head = Node(10)
head.next = Node(20)
head.next.next = Node(30)

if head is not None:
    if head.next is None:
        head = None
    else:
        current = head

        while current.next.next is not None:
            current = current.next

        current.next = None

current = head

while current is not None:
    print(current.data)
    current = current.next
```

Output:

```
10
20
```

The special case is a list containing one node. Deleting its final node means setting `head` to `None`.

**Time complexity: O(n)** when only `head` is maintained.

### 4.3 Deletion by Value

Suppose we want to remove the first node containing `20`.

Before:

```
10 → 20 → 30 → None
```

After:

```
10 → 30 → None
```

```
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None


head = Node(10)
head.next = Node(20)
head.next.next = Node(30)

target = 20

if head is not None and head.data == target:
    head = head.next
else:
    current = head

    while current is not None and current.next is not None:
        if current.next.data == target:
            current.next = current.next.next
            break

        current = current.next

current = head

while current is not None:
    print(current.data)
    current = current.next
```

Output:

```
10
30
```

This implementation handles deleting the head or a later node. It leaves the list unchanged if the target is absent.

**Time complexity: O(n)** in the worst case because the target may need to be searched for.

---

## 5. Doubly Linked List

A doubly linked list stores three fields in each node:

1. Data.
    
2. Reference to the previous node (`prev`).
    
3. Reference to the next node (`next`).
    

### Structure

```
None ← [10] ⇄ [20] ⇄ [30] → None
```

Each node links to both its previous and next neighbours.

- The first node's `prev` is `None`.
    
- The last node's `next` is `None`.
    

### 5.1 Creating and Traversing a Doubly Linked List

```
class Node:
    def __init__(self, data):
        self.data = data
        self.prev = None
        self.next = None


first = Node(10)
second = Node(20)
third = Node(30)

first.next = second
second.prev = first

second.next = third
third.prev = second

# Forward traversal
current = first

while current is not None:
    print(current.data)
    current = current.next

# Backward traversal
current = third

while current is not None:
    print(current.data)
    current = current.prev
```

Output:

```
10
20
30
30
20
10
```

A doubly linked list supports traversal in both directions.

### 5.2 Insertion into a Doubly Linked List

To insert a node between nodes `10` and `30`, the new node must be connected in both directions.

Before:

```
10 ⇄ 30
```

After inserting `20`:

```
10 ⇄ 20 ⇄ 30
```

```
class Node:
    def __init__(self, data):
        self.data = data
        self.prev = None
        self.next = None


first = Node(10)
third = Node(30)

first.next = third
third.prev = first

new_node = Node(20)

new_node.prev = first
new_node.next = third

first.next = new_node
third.prev = new_node

current = first

while current is not None:
    print(current.data)
    current = current.next
```

Output:

```
10
20
30
```

### 5.3 Deletion from a Doubly Linked List

To remove the middle node (`20`) from:

```
10 ⇄ 20 ⇄ 30
```

Reconnect the surrounding nodes:

```
10 ⇄ 30
```

If the node to delete is already known, its neighbours can be connected by adjusting the `prev` and `next` references. Special handling is needed when deleting the head or tail.

**Time complexity:**

- Deleting a known node: O(1), when the required references are available.
    
- Searching for a node by value: O(n).
    

### Singly vs Doubly Linked List

|Feature|Singly Linked List|Doubly Linked List|
|---|---|---|
|Links per node|`next`|`prev` and `next`|
|Traversal|Forward only|Forward and backward|
|Memory per node|Lower|Higher|
|Deleting a known node|Often requires predecessor|Neighbours can be reconnected directly|
|Implementation|Simpler|More reference updates|

**Exam trap:** A doubly linked list uses extra memory for the `prev` reference, but it enables backward traversal.

---

## 6. Circular Linked List

In a circular linked list, the final node points back to the first node instead of pointing to `None`.

There are singly circular and doubly circular linked lists. In the common singly circular version, each node has a `next` reference.

### Structure

```
head
 |
 v
[10] → [20] → [30]
 ^              |
 |______________|
```

The link from node `30` returns to node `10`. A non-empty circular list has no `None` link at its end.

### 6.1 Creating and Traversing a Circular Linked List

```
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None


first = Node(10)
second = Node(20)
third = Node(30)

first.next = second
second.next = third
third.next = first

current = first

if current is not None:
    start = current

    while True:
        print(current.data)
        current = current.next

        if current is start:
            break
```

Output:

```
10
20
30
```

Traversal stops when it reaches the starting node again.

**Exam trap:** Using `while current is not None` for this non-empty circular list causes an infinite loop because the links never reach `None`.

### 6.2 Insertion at the Beginning of a Circular Linked List

With a maintained `head` and `tail`:

Before:

```
head → 10 → 20 → 30 → head
```

After inserting `5`:

```
head → 5 → 10 → 20 → 30 → head
```

Example:

```
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None


head = Node(10)
second = Node(20)
tail = Node(30)

head.next = second
second.next = tail
tail.next = head

new_node = Node(5)
new_node.next = head

tail.next = new_node
head = new_node

current = head

while True:
    print(current.data)
    current = current.next

    if current is head:
        break
```

Output:

```
5
10
20
30
```

With a maintained tail reference, insertion at the beginning takes O(1).

### 6.3 Deletion from a Circular Linked List

To delete the head from a circular singly linked list containing more than one node:

1. Find the tail if it is not already maintained.
    
2. Set the tail's `next` to the second node.
    
3. Update `head` to that second node.
    

The last node must continue pointing to the new head.

For a one-node circular list, deletion makes the list empty. If both `head` and `tail` are maintained, set both to `None`.

### Types of Linked Lists: Comparison

|Feature|Singly|Doubly|Circular Singly|
|---|---|---|---|
|Links per node|One (`next`)|Two (`prev`, `next`)|One (`next`)|
|Last node points to|`None`|`None`|Head|
|Backward traversal|No|Yes|No|
|Natural stopping condition|`None`|`None`|Return to starting node|
|Extra reference memory|Low|Higher|Low|
|Common application|Simple chains|Navigation in both directions|Round-robin scheduling|

---

## 7. Time Complexity of Linked-List Operations

This table is especially important for DSSSB MCQs.

|Operation|Singly Linked List|Doubly Linked List|Circular Singly Linked List|
|---|---|---|---|
|Access by index|O(n)|O(n)|O(n)|
|Traverse all nodes|O(n)|O(n)|O(n)|
|Search by value|O(n)|O(n)|O(n)|
|Insert at beginning|O(1)|O(1)|O(1) with suitable references|
|Insert after known node|O(1)|O(1)|O(1)|
|Delete head|O(1)|O(1)|O(1) with suitable references|
|Delete known node|May require finding predecessor|O(1) when node is known|Generally requires predecessor|
|Insert at end|O(n) with only head; O(1) with tail|O(n) with only head; O(1) with tail|O(1) with tail|
|Delete end|O(n)|O(1) with tail reference|O(n)|

These complexities assume standard implementations. Maintaining a tail reference and knowing the target node can change the cost of an operation.

---

## 8. Array vs Linked List

|Feature|Array-Like List|Linked List|
|---|---|---|
|Access by index|O(1)|O(n)|
|Insert at beginning|O(n) for Python list|O(1) with head|
|Delete at beginning|O(n) for Python list|O(1) with head|
|Memory layout|Dynamic array-like storage in Python|Separate node objects connected by references|
|Extra links|No per-element `next` references|One or more references per node|
|Binary search|Efficient on sorted arrays with random access|Not efficient in the standard linked-list form|
|Sequential traversal|Efficient|Efficient|

### Advantages of Linked Lists

- Insertion and deletion at known positions can be efficient.
    
- They can grow and shrink without shifting all subsequent elements.
    
- Doubly linked lists support movement in both directions.
    

### Disadvantages of Linked Lists

- Indexed access requires traversal.
    
- Nodes require extra memory for references.
    
- Implementations must carefully handle empty lists, head and tail changes, and circular links.
    

---

## 9. Common DSSSB Exam Traps

1. **Singly linked list:** The last node's `next` is `None`; traversal normally stops when `current` becomes `None`.
    
2. **Doubly linked list:** Each node maintains both `prev` and `next`. Forgetting to update one reference can break forward or backward traversal.
    
3. **Circular linked list:** The last node points back to the head, so a standard `while current is not None` traversal does not terminate.
    
4. **Insertion complexity:** Inserting after a node that is already known is O(1). Searching for that node first can make the complete operation O(n).
    
5. **Deleting the last node:** A singly linked list generally must find the previous node, even if it maintains a tail reference. A doubly linked list with a tail can remove the last node in O(1).
    

---

## Final Revision Sheet

|Topic|Key Takeaway|
|---|---|
|Singly linked list|Each node has data and `next`|
|Doubly linked list|Each node has data, `prev`, and `next`|
|Circular linked list|Last node points to the head|
|Traversal|O(n)|
|Search by value|O(n)|
|Access by index|O(n)|
|Insert at beginning|O(1)|
|Delete at beginning|O(1)|
|Insert at end|O(n) with only head; O(1) with tail|
|Delete at end|O(n) for singly linked list; O(1) for doubly linked list with tail|
|Array advantage|Fast indexed access|
|Linked-list advantage|Efficient insertion and deletion at known positions|

### Quick Memory Tricks

- **Singly:** One link, forward only.
    
- **Doubly:** Two links, forward and backward.
    
- **Circular:** Last node connects to the first.
    
- **Array:** Fast index access.
    
- **Linked list:** Nodes connected by references.