## 1. Basic structure of a linked list

A node typically contains two things:

- Data: the value stored in the node.
    
- Link/pointer: a reference to another node.
    

For a singly linked list:

### Singly linked list

## 10

Data

next →

## 20

Data

next →

## 30

Data

None

Head points to the first node. The last node's `next` reference is `None`.

A linked list is usually accessed using a reference called `head`, which points to the first node.

Important: Python does not have a built-in linked-list collection like its built-in `list`. We implement linked lists using objects and references.

## 2. Singly linked list

A singly linked list stores data and a reference to the next node. Each node can move only forward through the list.

Structure:

```
head
  |
  v
[10 | next] → [20 | next] → [30 | None]
```

### 2.1 Creating a node in Python

```
class Node:    def __init__(self, data):        self.data = data        self.next = Nonefirst = Node(10)second = Node(20)third = Node(30)first.next = secondsecond.next = thirdprint(first.data)print(first.next.data)print(first.next.next.data)
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
    

The nodes are connected using references rather than stored as one contiguous block.

### 2.2 Traversing a singly linked list

Traversal means visiting each node starting at `head` until the last node is reached.

```
class Node:    def __init__(self, data):        self.data = data        self.next = Nonehead = Node(10)head.next = Node(20)head.next.next = Node(30)current = headwhile current is not None:    print(current.data)    current = current.next
```

Output:

```
10
20
30
```

The condition `current is not None` is important. It stops traversal when the end of the list is reached.

Exam trap: Accessing `current.next` after `current` becomes `None` raises an `AttributeError`.

## 3. Singly linked list: insertion

Insertion means adding a new node to the linked list. Common cases are insertion at the beginning, at the end, or after a specified node.

### 3.1 Insertion at the beginning

Suppose the list is:

```
10 → 20 → 30 → None
```

Insert `5` at the beginning:

```
5 → 10 → 20 → 30 → None
```

The new node points to the previous head, and then `head` is updated to point to the new node.

```
class Node:    def __init__(self, data):        self.data = data        self.next = Nonehead = Node(10)head.next = Node(20)head.next.next = Node(30)new_node = Node(5)new_node.next = headhead = new_nodecurrent = headwhile current is not None:    print(current.data)    current = current.next
```

Output:

```
5
10
20
30
```

Complexity: \(O(1)\), because no traversal is required.

### 3.2 Insertion at the end

To insert at the end, traverse to the last node and connect its `next` reference to the new node.

```
class Node:    def __init__(self, data):        self.data = data        self.next = Nonehead = Node(10)head.next = Node(20)new_node = Node(30)current = headwhile current.next is not None:    current = current.nextcurrent.next = new_nodecurrent = headwhile current is not None:    print(current.data)    current = current.next
```

Output:

```
10
20
30
```

Complexity: \(O(n)\) when only `head` is maintained, because traversal is needed. If a `tail` reference is maintained, insertion at the end can be \(O(1)\).

### 3.3 Insertion after a specified node

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
class Node:    def __init__(self, data):        self.data = data        self.next = Nonehead = Node(10)head.next = Node(20)head.next.next = Node(30)current = head.next  # Node containing 20new_node = Node(25)new_node.next = current.nextcurrent.next = new_nodecurrent = headwhile current is not None:    print(current.data)    current = current.next
```

Output:

```
10
20
25
30
```

The order of the two reference assignments is important: connect the new node to the remainder of the list first, then connect the current node to the new node.

Complexity: \(O(1)\) if the target node is already known. Finding the target by value usually takes \(O(n)\).

## 4. Singly linked list: deletion

Deletion removes a node from the list by changing the relevant references.

### 4.1 Deletion from the beginning

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
class Node:    def __init__(self, data):        self.data = data        self.next = Nonehead = Node(10)head.next = Node(20)head.next.next = Node(30)if head is not None:    head = head.nextcurrent = headwhile current is not None:    print(current.data)    current = current.next
```

Output:

```
20
30
```

Complexity: \(O(1)\).

### 4.2 Deletion from the end

To delete the final node in a singly linked list, find the second-last node and set its `next` reference to `None`.

```
class Node:    def __init__(self, data):        self.data = data        self.next = Nonehead = Node(10)head.next = Node(20)head.next.next = Node(30)if head is not None:    if head.next is None:        head = None    else:        current = head        while current.next.next is not None:            current = current.next        current.next = Nonecurrent = headwhile current is not None:    print(current.data)    current = current.next
```

Output:

```
10
20
```

The special case is a list containing one node. Deleting its final node means setting `head` to `None`.

Complexity: \(O(n)\) for a singly linked list when only `head` is maintained.

### 4.3 Deletion by value

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
class Node:    def __init__(self, data):        self.data = data        self.next = Nonehead = Node(10)head.next = Node(20)head.next.next = Node(30)target = 20if head is not None and head.data == target:    head = head.nextelse:    current = head    while current is not None and current.next is not None:        if current.next.data == target:            current.next = current.next.next            break        current = current.nextcurrent = headwhile current is not None:    print(current.data)    current = current.next
```

Output:

```
10
30
```

This implementation handles deleting the head or a later node, and leaves the list unchanged if the target is absent.

Complexity: \(O(n)\) in the worst case because the target may need to be searched for.

## 5. Doubly linked list

A doubly linked list stores three fields in each node:

1. Data
    
2. Reference to the previous node (`prev`)
    
3. Reference to the next node (`next`)
    

Structure:

### Doubly linked list

None

## 10

Node

## 20

Node

## 30

Node

None

Each node links to both its previous and next neighbours. The first node's `prev` and last node's `next` are `None`.

### 5.1 Creating and traversing a doubly linked list

```
class Node:    def __init__(self, data):        self.data = data        self.prev = None        self.next = Nonefirst = Node(10)second = Node(20)third = Node(30)first.next = secondsecond.prev = firstsecond.next = thirdthird.prev = second# Forward traversalcurrent = firstwhile current is not None:    print(current.data)    current = current.next# Backward traversalcurrent = thirdwhile current is not None:    print(current.data)    current = current.prev
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

### 5.2 Insertion into a doubly linked list

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
class Node:    def __init__(self, data):        self.data = data        self.prev = None        self.next = Nonefirst = Node(10)third = Node(30)first.next = thirdthird.prev = firstnew_node = Node(20)new_node.prev = firstnew_node.next = thirdfirst.next = new_nodethird.prev = new_nodecurrent = firstwhile current is not None:    print(current.data)    current = current.next
```

Output:

```
10
20
30
```

### 5.3 Deletion from a doubly linked list

To remove the middle node (`20`) from `10 ⇄ 20 ⇄ 30`, link the surrounding nodes directly:

```
10 ⇄ 30
```

If the node to delete is already known, its neighbours can be connected by adjusting the `prev` and `next` references. Special handling is needed when deleting the head or tail.

Complexity: Deletion is \(O(1)\) when the node is already known and the required head/tail references are maintained. Searching for a node by value still takes \(O(n)\).

### Singly vs doubly linked list

|Feature|Singly linked list|Doubly linked list|
|---|---|---|
|Links per node|`next`|`prev` and `next`|
|Traversal|Forward only|Forward and backward|
|Memory per node|Lower|Higher|
|Delete known node|Often requires predecessor|Can reconnect neighbours directly|
|Implementation|Simpler|More reference updates|

Exam trap: A doubly linked list uses extra memory for the `prev` reference, but it makes backward traversal possible.

## 6. Circular linked list

In a circular linked list, the final node points back to the first node instead of pointing to `None`.

There are singly circular and doubly circular linked lists. In the common singly circular version, each node has a `next` reference.

### Singly circular linked list

## 10

## 20

## 30

The link from node 30 returns to node 10. There is no `None` link at the end in a non-empty circular list.

### 6.1 Creating and traversing a circular linked list

```
class Node:    def __init__(self, data):        self.data = data        self.next = Nonefirst = Node(10)second = Node(20)third = Node(30)first.next = secondsecond.next = thirdthird.next = firstcurrent = firstif current is not None:    start = current    while True:        print(current.data)        current = current.next        if current is start:            break
```

Output:

```
10
20
30
```

Notice that the traversal stops when it reaches the starting node again.

Exam trap: Using `while current is not None` for this non-empty circular list causes an infinite loop because the links never reach `None`.

### 6.2 Insertion into a circular linked list

A simple insertion at the beginning can be performed by redirecting the last node's link to the new node and making the new node point to the previous head.

For a list with a maintained `head` and `tail`:

```
Before: head → 10 → 20 → 30 → head
After:  head → 5 → 10 → 20 → 30 → head
```

Example implementation:

```
class Node:    def __init__(self, data):        self.data = data        self.next = Nonehead = Node(10)second = Node(20)tail = Node(30)head.next = secondsecond.next = tailtail.next = headnew_node = Node(5)new_node.next = headtail.next = new_nodehead = new_nodecurrent = headwhile True:    print(current.data)    current = current.next    if current is head:        break
```

Output:

```
5
10
20
30
```

With a maintained tail reference, insertion at the beginning can be \(O(1)\).

### 6.3 Deletion from a circular linked list

To delete the head from a circular singly linked list with more than one node:

1. Find the tail if it is not already maintained.
    
2. Set the tail's `next` to the second node.
    
3. Update `head` to that second node.
    

The last node must continue pointing to the new head. For a one-node circular list, deletion makes the list empty, so both `head` and `tail` become `None` in an implementation that maintains both references.

### Types of linked lists — comparison

|Feature|Singly|Doubly|Circular singly|
|---|---|---|---|
|Links per node|One (`next`)|Two (`prev`, `next`)|One (`next`)|
|Last node points to|`None`|`None`|Head|
|Backward traversal|No|Yes|No, in the singly circular version|
|Natural stopping condition|`None`|`None`|Return to starting node|
|Extra reference memory|Low|Higher|Low|
|Common applications|Simple chains|Navigation in both directions|Round-robin scheduling|

## 7. Time complexity of linked-list operations

This table is especially important for DSSSB MCQs.

|Operation|Singly linked list|Doubly linked list|Circular singly linked list|
|---|---|---|---|
|Access by index|\(O(n)\)|\(O(n)\)|\(O(n)\)|
|Traverse all nodes|\(O(n)\)|\(O(n)\)|\(O(n)\)|
|Search by value|\(O(n)\)|\(O(n)\)|\(O(n)\)|
|Insert at beginning|\(O(1)\)|\(O(1)\)|\(O(1)\) with suitable head/tail references|
|Insert after known node|\(O(1)\)|\(O(1)\)|\(O(1)\)|
|Delete head|\(O(1)\)|\(O(1)\)|\(O(1)\) with suitable references|
|Delete known node|May require finding predecessor|\(O(1)\) when the node is known|Singly circular deletion generally requires predecessor|
|Insert at end|\(O(n)\) with only head; \(O(1)\) with tail|\(O(n)\) with only head; \(O(1)\) with tail|\(O(1)\) with tail|
|Delete end|\(O(n)\)|\(O(1)\) with a tail reference|\(O(n)\) for singly circular lists|

These complexities assume standard linked-list implementations. Maintaining a tail reference and knowing the target node can change the cost of an operation.

## 8. Array vs linked list

|Feature|Array-like list|Linked list|
|---|---|---|
|Access by index|\(O(1)\)|\(O(n)\)|
|Insert at beginning|\(O(n)\) for Python list|\(O(1)\) with head|
|Delete at beginning|\(O(n)\) for Python list|\(O(1)\) with head|
|Memory layout|Dynamic array-like storage in Python|Separate node objects linked through references|
|Extra links|No per-element `next` references|One or more references per node|
|Binary search|Efficient on sorted arrays with random access|Not efficient in the standard linked-list form|
|Sequential traversal|Efficient|Efficient|

### Advantages of linked lists

- Insertion and deletion at known positions can be efficient.
    
- They can grow and shrink without shifting all subsequent elements.
    
- Doubly linked lists support movement in both directions.
    

### Disadvantages of linked lists

- Indexed access requires traversal.
    
- Nodes need extra memory for references.
    
- Implementations require careful handling of empty lists, head/tail changes, and circular links.
    

## 9. Common exam traps

1. Singly linked list

The last node's `next` is `None`; traversal normally stops when `current` becomes `None`.

2. Doubly linked list

Each node maintains both `prev` and `next`. Forgetting to update one reference can break backward or forward traversal.

3. Circular linked list

The last node points back to the head, so a standard `while current is not None` traversal does not terminate.

4. Insertion complexity

Inserting after a node that is already known is \(O(1)\). Searching for that node first can make the whole operation \(O(n)\).

5. Deleting the last node

A singly linked list generally must find the previous node, even if it maintains a tail reference. A doubly linked list with a tail can remove the last node in \(O(1)\).