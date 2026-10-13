# Queue in Data Structures

## 1. Queue Fundamentals

A queue is a linear data structure that follows the **FIFO (First In, First Out)** principle.

A queue has two important ends:

- **Front:** The end from which elements are removed.
    
- **Rear:** The end where new elements are inserted.
    

The two basic operations are:

- **Enqueue:** Insert an element at the rear.
    
- **Dequeue:** Remove an element from the front.
    

### Example: FIFO Order

```
Front                         Rear
  ↓                             ↓
[10]  →  [20]  →  [30]
```

Dequeuing removes `10` first. Enqueuing `40` adds it after `30`.

```
Enqueue(10) → [10]
Enqueue(20) → [10, 20]
Enqueue(30) → [10, 20, 30]
Dequeue()   → removes 10
Queue       → [20, 30]
```

**Exam keyword:** FIFO = First In, First Out.

A stack follows LIFO, while a standard queue follows FIFO.

---

## 2. Linear Queue

A linear queue is the basic queue structure in which elements are added at the rear and removed from the front.

### Basic Operations

|Operation|Purpose|
|---|---|
|Enqueue|Adds an element at the rear|
|Dequeue|Removes the front element|
|Peek/Front|Views the front element without removing it|
|Rear|Views the last element|
|Is empty|Checks whether the queue contains elements|

### Python Implementation

Python lists can implement a queue for learning purposes. Here, `append()` adds at the rear and `pop(0)` removes from the front.

```
queue = []

# Enqueue
queue.append(10)
queue.append(20)
queue.append(30)

print("Queue:", queue)

# Peek at front
print("Front:", queue[0])

# Dequeue
removed = queue.pop(0)

print("Removed:", removed)
print("Queue:", queue)
```

Output:

```
Queue: [10, 20, 30]
Front: 10
Removed: 10
Queue: [20, 30]
```

This implementation is easy to understand, but `pop(0)` takes O(n) time for a Python list because the remaining elements must shift.

For practical Python applications, `collections.deque` is generally a better choice.

### Linear Queue Using a Fixed-Size Array

Suppose a queue has capacity 5:

```
Index:   0    1    2    3    4
        [10] [20] [30] [  ] [  ]
         ↑         ↑
       Front      Rear
```

After removing `10` and `20`, the first two positions become empty:

```
Index:   0    1    2    3    4
        [  ] [  ] [30] [  ] [  ]
                   ↑
               Front/Rear
```

A simple fixed-array implementation may advance `front` without moving elements. However, if `rear` has already reached the last index, new elements cannot be inserted even when earlier slots are empty.

This problem is called **false overflow** or wasted space in a simple linear-array queue.

A circular queue addresses this problem by reusing freed positions.

---

## 3. Circular Queue

A circular queue connects the end of the logical array back to its beginning. When positions at the front become free, those positions can be reused.

Instead of moving all elements, the queue uses wraparound indexing.

### Circular Queue Concept

For a circular queue with capacity N, the next index is:

**Next index = (Current index + 1) % N**

Here, `%` is the modulo operator.

### Example: Capacity 5

|Current Index|Calculation|Next Index|
|---|---|---|
|0|`(0 + 1) % 5`|1|
|1|`(1 + 1) % 5`|2|
|2|`(2 + 1) % 5`|3|
|3|`(3 + 1) % 5`|4|
|4|`(4 + 1) % 5`|0|

When the rear reaches index `4`, the next position wraps around to index `0`.

### Python Implementation of a Circular Queue

This implementation uses a fixed-size list and a `size` variable, allowing all positions to be used without confusing a full queue with an empty one.

```
class CircularQueue:
    def __init__(self, capacity):
        if capacity <= 0:
            raise ValueError("Capacity must be positive")

        self.data = [None] * capacity
        self.capacity = capacity
        self.front = 0
        self.size = 0

    def enqueue(self, value):
        if self.size == self.capacity:
            print("Queue overflow")
            return

        rear = (self.front + self.size) % self.capacity
        self.data[rear] = value
        self.size += 1

    def dequeue(self):
        if self.size == 0:
            print("Queue underflow")
            return None

        value = self.data[self.front]
        self.data[self.front] = None

        self.front = (self.front + 1) % self.capacity
        self.size -= 1

        return value

    def display(self):
        return [
            self.data[(self.front + i) % self.capacity]
            for i in range(self.size)
        ]


q = CircularQueue(3)

q.enqueue(10)
q.enqueue(20)
q.enqueue(30)

print(q.display())

print("Removed:", q.dequeue())

q.enqueue(40)

print(q.display())
```

Output:

```
[10, 20, 30]
Removed: 10
[20, 30, 40]
```

Although the queue was initially full, after removing `10`, the freed location could be reused when `40` was inserted.

### Full and Empty Conditions

In this size-tracking implementation:

- Empty: `size == 0`
    
- Full: `size == capacity`
    
- Next insertion index: `(front + size) % capacity`
    
- Next front index after deletion: `(front + 1) % capacity`
    

Some textbook implementations use only `front` and `rear`, leaving one slot unused to distinguish full and empty states. Always follow the convention specified in an exam question.

### Linear Queue vs Circular Queue

|Feature|Linear Array Queue|Circular Queue|
|---|---|---|
|Reuses freed slots at the beginning|Not automatically|Yes|
|Wraparound|No|Yes|
|False overflow in a simple fixed-array design|Possible|Avoided through wraparound|
|Enqueue/dequeue with suitable index tracking|O(1)|O(1)|
|Implementation complexity|Lower|Slightly higher|

**Exam trap:** Circular queues still follow FIFO. The circular arrangement does not mean elements are removed in an arbitrary order.

---

## 4. Priority Queue

A priority queue removes elements according to their priority rather than simply their insertion order.

The element with the highest priority is served first. If two elements have the same priority, their relative ordering depends on the implementation.

A common convention is that a smaller numerical value means higher priority. Other systems use the opposite convention, so always check the question's definition.

### Example

Suppose patients are assigned priorities:

|Patient|Priority|
|---|---|
|Patient A|3|
|Patient B|1|
|Patient C|2|

If a smaller number represents higher priority, the removal order is:

```
Patient B → Patient C → Patient A
```

Patient A arrived first, but Patient B is removed first because it has the highest priority.

### Python Implementation Using `heapq`

Python provides the `heapq` module for heap-based priority queues. Its standard heap is a min-heap, so the smallest value is removed first.

```
import heapq

pq = []

heapq.heappush(pq, (3, "Patient A"))
heapq.heappush(pq, (1, "Patient B"))
heapq.heappush(pq, (2, "Patient C"))

while pq:
    priority, patient = heapq.heappop(pq)
    print(priority, patient)
```

Output:

```
1 Patient B
2 Patient C
3 Patient A
```

The tuples are compared starting with their first element, which is the priority. If priorities tie, the second element may also be compared.

**Exam trap:** `heapq` is a min-heap by default. The smallest heap element comes out first. If larger numeric values mean higher priority, the implementation must account for that convention.

### Priority Queue Complexities

For a typical binary-heap implementation:

|Operation|Time Complexity|
|---|---|
|Read minimum-priority item (`pq[0]`)|O(1)|
|Insert an element|O(log n)|
|Remove the minimum-priority element|O(log n)|
|Build a heap using `heapify()`|O(n)|

Applications include task scheduling, event simulation, shortest-path algorithms such as Dijkstra's algorithm, and processing work according to urgency.

---

## 5. Deque — Double-Ended Queue

A deque, pronounced "deck", is a double-ended queue. Elements can be inserted and removed at both the front and rear.

Unlike a standard queue, which ordinarily inserts at the rear and removes from the front, a deque supports operations at both ends.

### Common Deque Operations

|Operation|Purpose|
|---|---|
|`append(x)`|Insert at the rear|
|`appendleft(x)`|Insert at the front|
|`pop()`|Remove from the rear|
|`popleft()`|Remove from the front|

### Python Implementation

Python provides `collections.deque`, which supports efficient insertion and removal at both ends.

```
from collections import deque

dq = deque([10, 20, 30])

dq.append(40)
print(dq)

dq.appendleft(5)
print(dq)

print("Front removed:", dq.popleft())
print("Rear removed:", dq.pop())

print(dq)
```

Output:

```
deque([10, 20, 30, 40])
deque([5, 10, 20, 30, 40])
Front removed: 5
Rear removed: 40
deque([10, 20, 30])
```

### Types of Deque

Two restricted forms are important:

- **Input-restricted deque:** Insertion is allowed at only one end, but deletion is allowed at both ends.
    
- **Output-restricted deque:** Deletion is allowed at only one end, but insertion is allowed at both ends.
    

These names describe the allowed operations. The particular end used for the restricted operation may vary by convention or implementation.

### Queue vs Deque

|Feature|Standard Queue|Deque|
|---|---|---|
|Insertion|Rear|Front and rear|
|Deletion|Front|Front and rear|
|Ordering principle|FIFO|Depends on operations|
|Python implementation|`collections.deque`|`collections.deque`|
|Typical operations|Enqueue and dequeue|`append`, `appendleft`, `pop`, `popleft`|

A deque can also be used to implement a standard FIFO queue or a stack.

### Deque Complexity

For Python's `collections.deque`, insertion and removal at either end are typically O(1).

However, indexed access near the middle is O(n) in the worst case. Therefore, a deque is not a replacement for an array when frequent arbitrary indexed access is required.

---

## 6. Applications of Queues

Queues are useful wherever tasks should be processed in arrival order or according to scheduling rules.

### 6.1 Printer Queue

Documents are typically processed in the order they are submitted.

### 6.2 CPU and Task Scheduling

Queues can hold processes or ready tasks. Priority queues can select tasks according to priority.

### 6.3 Networking

Routers and communication systems use queues to buffer packets while they wait to be transmitted.

### 6.4 Breadth-First Search (BFS)

BFS uses a FIFO queue to explore nodes level by level in a graph.

**Exam trap:** BFS uses a queue, whereas depth-first search (DFS) can use a stack.

---

## 7. Comparison of All Four Queue Types

|Feature|Linear Queue|Circular Queue|Priority Queue|Deque|
|---|---|---|---|---|
|Removal rule|FIFO|FIFO|Based on priority|Either end|
|Insertion position|Rear|Rear, with wraparound|According to implementation|Front or rear|
|Reuses freed array slots|Not automatically in a simple linear array|Yes|Implementation-dependent|Depends on implementation|
|Typical implementation|Array or linked list|Circular array|Binary heap|Double-ended queue|
|Main purpose|Standard waiting line|Efficient fixed-array queue|Priority-based processing|Flexible operations at both ends|

---

## 8. Common DSSSB Exam Traps

1. **FIFO:** First In, First Out.
    
2. **Enqueue:** Insert at the rear.
    
3. **Dequeue:** Remove from the front.
    
4. **False overflow:** Can occur in a simple fixed-array linear queue when the rear reaches the last index despite free slots at the beginning.
    
5. **Circular queue:** Uses modulo arithmetic to wrap around.
    
6. **Priority queue:** Removal depends on priority, not necessarily arrival order.
    
7. **Python** `**heapq**`**:** Min-heap; the smallest item comes out first.
    
8. **Deque:** Supports insertion and removal at both ends.
    
9. `**append()**`**:** Add at the right/rear.
    
10. `**appendleft()**`**:** Add at the left/front.
    
11. `**pop()**`**:** Remove from the right/rear.
    
12. `**popleft()**`**:** Remove from the left/front.
    
13. **BFS:** Uses a FIFO queue.
    
14. **Circular queue complexity:** Enqueue and dequeue are O(1) with proper index tracking.
    

---

## Final Revision Sheet

|Topic|Must Remember|
|---|---|
|Linear queue|FIFO; insert at rear and remove from front|
|Circular queue|Uses modulo arithmetic to wrap around|
|False overflow|Possible in a simple fixed-array linear queue|
|Priority queue|Removal depends on priority|
|Python `heapq`|Min-heap; smallest item first|
|Deque|Insert and remove at both ends|
|`append()`|Add at right/rear|
|`appendleft()`|Add at left/front|
|`pop()`|Remove from right/rear|
|`popleft()`|Remove from left/front|
|BFS|Uses a FIFO queue|
|Circular queue complexity|Enqueue and dequeue are O(1) with proper tracking|

**Highest-priority exam concepts:** FIFO vs LIFO, false overflow, circular-queue modulo formulas, priority-queue ordering, and the difference between `pop()` and `popleft()` in a deque.

**Next Data Structures topic:** Trees — terminology, binary trees, binary search trees, tree traversals, and heaps.