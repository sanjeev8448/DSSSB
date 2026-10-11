## 1. Queue fundamentals

A queue has two important ends:

- Front: The end from which elements are removed.
    
- Rear: The end where new elements are inserted.
    

The two basic operations are:

- Enqueue: Insert an element at the rear.
    
- Dequeue: Remove an element from the front.
    

### Example: FIFO order

Front

## 10

## 20

## 30

Rear

Dequeue ←

← Enqueue

Dequeuing removes `10` first. Enqueuing `40` adds it after `30`.

For example:

```
Enqueue(10) → [10]
Enqueue(20) → [10, 20]
Enqueue(30) → [10, 20, 30]
Dequeue()   → removes 10
Queue       → [20, 30]
```

Exam keyword: FIFO = First In, First Out. A stack follows LIFO, while a standard queue follows FIFO.

## 2. Linear queue

A linear queue is the basic queue structure in which elements are added at the rear and removed from the front.

### Operations

|Operation|Purpose|
|---|---|
|Enqueue|Adds an element at the rear|
|Dequeue|Removes the front element|
|Peek/Front|Views the front element without removing it|
|Rear|Views the last element|
|Is empty|Checks whether the queue has elements|

### Python implementation

Python lists can implement a queue for learning purposes. Here, `append()` adds at the rear and `pop(0)` removes at the front.

```
queue = []# Enqueuequeue.append(10)queue.append(20)queue.append(30)print("Queue:", queue)# Peek at frontprint("Front:", queue[0])# Dequeueremoved = queue.pop(0)print("Removed:", removed)print("Queue:", queue)
```

Output:

```
Queue: [10, 20, 30]
Front: 10
Removed: 10
Queue: [20, 30]
```

This is easy to understand, but `pop(0)` takes \(O(n)\) time for a Python list because the remaining elements must shift.

For practical Python applications, `collections.deque` is generally a better queue implementation.

### Linear queue using a fixed-size array

Suppose a queue has capacity 5:

```
Index:  0    1    2    3    4
       [10] [20] [30] [  ] [  ]
        Front      Rear
```

After removing `10` and `20`, the first two positions are empty:

```
Index:  0    1    2    3    4
       [  ] [  ] [30] [  ] [  ]
                  Front/Rear
```

A simple fixed-array implementation may advance `front` without moving elements. However, if `rear` has already reached the last index, new elements cannot be inserted even though earlier slots have become empty.

This problem is called false overflow or wasted space in a simple linear-array queue. A circular queue addresses it by reusing freed positions.

## 3. Circular queue

A circular queue connects the end of the logical array back to its beginning. When positions at the front become free, those positions can be reused.

Instead of moving all elements, the queue uses wraparound indexing.

### Circular queue concept

### 40

Index 0

### 50

Index 1

### —

Index 2

### 20

Index 3

### 30

Index 4

Illustration of wraparound: the next rear position can return to index 0.

The key idea is that array indexes are calculated circularly. For capacity \(N\), the next index is:

\[ \text{next}=(\text{current}+1)\bmod N \]

### How does modulo help?

For a circular queue of capacity 5:

|Current index|Calculation|Next index|
|---|---|---|
|0|`(0 + 1) % 5`|1|
|1|`(1 + 1) % 5`|2|
|2|`(2 + 1) % 5`|3|
|3|`(3 + 1) % 5`|4|
|4|`(4 + 1) % 5`|0|

When the rear reaches index `4`, the next position wraps to index `0`.

### Python implementation of a circular queue

This implementation uses a fixed-size list and a `size` variable, allowing all positions to be used without confusing a full queue with an empty one.

```
class CircularQueue:    def __init__(self, capacity):        if capacity <= 0:            raise ValueError("Capacity must be positive")        self.data = [None] * capacity        self.capacity = capacity        self.front = 0        self.size = 0    def enqueue(self, value):        if self.size == self.capacity:            print("Queue overflow")            return        rear = (self.front + self.size) % self.capacity        self.data[rear] = value        self.size += 1    def dequeue(self):        if self.size == 0:            print("Queue underflow")            return None        value = self.data[self.front]        self.data[self.front] = None        self.front = (self.front + 1) % self.capacity        self.size -= 1        return value    def display(self):        return [            self.data[(self.front + i) % self.capacity]            for i in range(self.size)        ]
```

Output:

```
[10, 20, 30]
Removed: 10
[20, 30, 40]
```

Although the queue was initially full, after removing `10`, the freed location could be reused when `40` was inserted.

### Full versus empty conditions

In this size-tracking implementation:

- Empty: `size == 0`
    
- Full: `size == capacity`
    
- Next insertion index: `(front + size) % capacity`
    
- Next front index after deletion: `(front + 1) % capacity`
    

Some textbook implementations use only `front` and `rear`, leaving one slot unused to distinguish full and empty states. That is a different convention, so follow the condition specified in a question.

### Linear queue vs circular queue

|Feature|Linear array queue|Circular queue|
|---|---|---|
|Reuses freed slots at the beginning|Not automatically|Yes|
|Wraparound|No|Yes|
|False overflow possible in a simple fixed-array design|Yes|Avoided through wraparound|
|Enqueue/dequeue with suitable index tracking|\(O(1)\)|\(O(1)\)|
|Extra complexity|Lower|Slightly higher|

Exam trap: Circular queues still follow FIFO. The circular arrangement does not mean elements are removed in a circular or arbitrary order.

## 4. Priority queue

A priority queue removes elements according to their priority rather than simply their insertion order.

The element with the highest priority is served first. If two elements have the same priority, their relative ordering depends on the implementation.

A frequent convention is that a smaller numerical priority value means higher priority. Other systems use the opposite convention, so always check the question's definition.

### Example

Suppose patients are assigned priorities:

|Patient|Priority|
|---|---|
|Patient A|3|
|Patient B|1|
|Patient C|2|

If the smaller number represents higher priority, the removal order is:

```
Patient B → Patient C → Patient A
```

Even though Patient A arrived first, Patient B is removed first because its priority is higher.

### Python implementation using `heapq`

Python provides the `heapq` module for heap-based priority queues. Its standard heap is a min-heap, so the smallest value is removed first.

```
import heapqpq = []heapq.heappush(pq, (3, "Patient A"))heapq.heappush(pq, (1, "Patient B"))heapq.heappush(pq, (2, "Patient C"))while pq:    priority, patient = heapq.heappop(pq)    print(priority, patient)
```

Output:

```
1 Patient B
2 Patient C
3 Patient A
```

The tuples are compared starting with their first element, which is the priority. When priorities tie, the second element may also be compared.

Exam trap: `heapq` is a min-heap by default; the smallest heap element comes out first. If larger numeric values mean higher priority, the implementation must account for that convention.

### Priority queue complexities

For a typical binary-heap implementation:

|Operation|Time complexity|
|---|---|
|Read minimum-priority item (`pq[0]`)|\(O(1)\)|
|Insert an element|\(O(\log n)\)|
|Remove the minimum-priority element|\(O(\log n)\)|
|Build a heap from \(n\) elements using `heapify()`|\(O(n)\)|

Applications include task scheduling, event simulation, shortest-path algorithms such as Dijkstra's algorithm, and handling work according to urgency.

## 5. Deque — double-ended queue

A deque (pronounced deck) is a double-ended queue. Elements can be inserted and removed at both the front and rear.

Unlike a standard queue, which ordinarily inserts at the rear and removes from the front, a deque supports operations at both ends.

### Operations on a deque

#### Front

Insert / Remove

## 10 | 20 | 30

Deque elements

#### Rear

Insert / Remove

### Common deque operations

|Operation|Purpose|
|---|---|
|`append(x)`|Insert at the rear|
|`appendleft(x)`|Insert at the front|
|`pop()`|Remove from the rear|
|`popleft()`|Remove from the front|

Python provides `collections.deque`, which supports efficient insertion and removal at both ends.

```
from collections import dequedq = deque([10, 20, 30])dq.append(40)print(dq)dq.appendleft(5)print(dq)print("Front removed:", dq.popleft())print("Rear removed:", dq.pop())print(dq)
```

Output:

```
deque([10, 20, 30, 40])
deque([5, 10, 20, 30, 40])
Front removed: 5
Rear removed: 40
deque([10, 20, 30])
```

### Types of deque

Two restricted forms are worth knowing:

- Input-restricted deque: Insertion is allowed at only one end, but deletion is allowed at both ends.
    
- Output-restricted deque: Deletion is allowed at only one end, but insertion is allowed at both ends.
    

These names describe the allowed operations; the particular end used for the restricted operation may vary by convention or implementation.

### Queue vs deque

|Feature|Standard queue|Deque|
|---|---|---|
|Insertion|Rear|Front and rear|
|Deletion|Front|Front and rear|
|Ordering principle|FIFO|Depends on operations|
|Python implementation|`collections.deque`|`collections.deque`|
|Typical end operations|Enqueue and dequeue|`append`, `appendleft`, `pop`, `popleft`|

A deque can also be used to implement a standard FIFO queue or a stack.

### Deque complexities

For Python's `collections.deque`, insertion and removal at either end are typically \(O(1)\).

However, indexed access near the middle is \(O(n)\) in the worst case, so a deque is not a replacement for an array when frequent arbitrary indexed access is required.

## 6. Applications of queues

Queues are useful wherever tasks should be processed in arrival order or according to scheduling rules.

![Premium Print Marketing: Flyers, Business Cards, Brochures & Booklets
– Cutting Edge Signs & Graphics](https://images.openai.com/static-rsc-4/Ch2aBx0ObyNvyN16teQf2zE-b06w4B78co9ov2s7RikDBc__ziaHS8CSL8fXssOuXlzdcmvpH4EqRwhzaHDiwKjF0B3CloPX5c8IF5ZpxPbE_k1kbufzCZlG6Yn-7BeCy5KtAOpzR5bkvcXxDcgXvai_lOFYjijZvbxpphUX42U?purpose=inline)

Printer queue

Documents are typically processed in the order they are submitted.

![How Operating Systems Manage Memory and Processes: The Backbone of Modern Computing | by Jaimil Shah | Medium](https://images.openai.com/static-rsc-4/iuWj50GD1b3O3wplQ1sDC5vn8qnpr_niYoicqnzRIRPX6bESkxeWSG1liTw_wsUfWaiSZAol4i8uECutzDes8biEFMUMAd6EbP3wb9BlZX0rso3mcj0XKZsRMlP6pTwcWmiNBeQ3HMeDbNPQMvM1QVG60HaElHj6zICEwe2R4AM?purpose=inline)

CPU and task scheduling

Queues can hold processes or ready tasks. Priority queues can select tasks according to priority.

![different color cable connected to the router in different ports in the background wall of the room](https://images.openai.com/static-rsc-4/Mdap_jBW24GG2Q4cfeJiTkor67CBEvc1eJk1XaJ66Jx8uBNLqRuny76S3Bu_fQ_oAF5DP1ox5OHdfBUsiGJpKWnW-7zWgrAycaXrh_HeBFbYlxiZ9NfOIPN3KUO44dkesPPNvPpS2uNAfff1QigF1Tt37CylcORn8U_8ZX9r6MdgNV1pBNl-QvMJRdYG1URq?purpose=inline)

Networking

Routers and communication systems use queues to buffer packets while they wait to be transmitted.

![Introduction to Algorithms: Shortest Paths I -  ppt download](https://images.openai.com/static-rsc-4/yNycE7DN9UHEzJ_PdHyBpqxTOog9XKtdCHXtAh-pOXWi18imkTV8tqDLWkOvk-jNxhymCzezdu4hdPKjz-JU1ZSUPv-0IN5sVB9NxKklKpURf0sgRk-xsBbTve83FAQuiIIgL_iUrd953pDPjZtia81hy-Sj76UOofZC5SAbUps?purpose=inline)

Breadth-first search (BFS)

BFS uses a FIFO queue to explore nodes level by level in a graph.

## 7. Comparison of all four queue types

|Feature|Linear queue|Circular queue|Priority queue|Deque|
|---|---|---|---|---|
|Removal rule|FIFO|FIFO|Based on priority|Either end|
|Insertion position|Rear|Rear, with wraparound|According to implementation|Front or rear|
|Reuses freed array slots|Not automatically in a simple linear array|Yes|Implementation-dependent|Depends on implementation|
|Typical implementation|Array or linked list|Circular array|Binary heap|Double-ended queue|
|Main purpose|Standard waiting line|Efficient fixed-array queue|Priority-based processing|Flexible operations at both ends|
## Final revision sheet

|Topic|Must remember|
|---|---|
|Linear queue|FIFO; insert at rear and remove from front|
|Circular queue|Uses modulo arithmetic to wrap around|
|False overflow|Can occur in a simple fixed-array linear queue|
|Priority queue|Removal depends on priority|
|Python `heapq`|Min-heap; smallest item first|
|Deque|Insert and remove at both ends|
|`append()`|Add at right/rear|
|`appendleft()`|Add at left/front|
|`pop()`|Remove from right/rear|
|`popleft()`|Remove from left/front|
|BFS|Uses a FIFO queue|
|Circular queue complexity|Enqueue and dequeue are \(O(1)\) with proper tracking|

Highest-priority exam concepts: FIFO vs LIFO, false overflow, circular-queue modulo formulas, priority-queue ordering, and the difference between `pop()` and `popleft()` in a deque.