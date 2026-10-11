## 1. Array fundamentals

Consider this array:

### Array: `A = [10, 20, 30, 40, 50]`

## 10

Index 0

## 20

Index 1

## 30

Index 2

## 40

Index 3

## 50

Index 4

The first element is at index 0; the last element is at index 4.

Important properties:

- Arrays are linear data structures.
    
- Elements are accessed by index.
    
- Accessing an element by index generally takes \(O(1)\) time.
    
- In a conventional fixed-size array, capacity is determined at creation.
    
- Inserting or deleting elements in the middle usually requires shifting elements.
    

Python note: Python's built-in `list` is a dynamic array-like sequence, not a strict fixed-size, homogeneous array. We will use Python lists to demonstrate the operations and use conventional array terminology for algorithm and complexity questions.

## 2. Traversal

Traversal means visiting each element of an array, usually to display, count, search, or process its elements.

Suppose:

```
A = [10, 20, 30, 40, 50]
```

### Example 1: Traversal using a `for` loop

```
A = [10, 20, 30, 40, 50]for element in A:    print(element)
```

Output:

```
10
20
30
40
50
```

### Example 2: Traversal using indexes

```
A = [10, 20, 30, 40, 50]for i in range(len(A)):    print("Index:", i, "Value:", A[i])
```

Output:

```
Index: 0 Value: 10
Index: 1 Value: 20
Index: 2 Value: 30
Index: 3 Value: 40
Index: 4 Value: 50
```

### Example 3: Traversal to calculate the sum

```
A = [10, 20, 30, 40, 50]total = 0for element in A:    total += elementprint(total)
```

Output:

```
150
```

### Traversal algorithm

```
Algorithm TRAVERSE(A, n):    for i = 0 to n - 1:        display A[i]
```

For an array of \(n\) elements, each element is visited once.

- Time complexity: \(O(n)\)
    
- Extra space: \(O(1)\), excluding output storage.
    

Exam trap: Traversing an array of 100 elements requires 100 visits, so the time complexity is linear, \(O(n)\), not \(O(1)\).

## 3. Searching

Searching means finding whether a particular element exists in an array and, if it does, locating its index.

The two most important searching algorithms are:

1. Linear search
    
2. Binary search
    

### 3.1 Linear search

Linear search checks elements one by one, from the beginning, until the target is found or the array ends.

Example: Search for `30` in `[10, 20, 30, 40, 50]`.

### Linear search walkthrough

## 10

Index 0

## 20

Index 1

## 30

Index 2

## 40

Index 3

## 50

Index 4

Target: 30

Compare with `{searchValues[searchStep]}`: Not a match.

PreviousNext comparison

Python implementation:

```
def linear_search(arr, target):    for i in range(len(arr)):        if arr[i] == target:            return i    return -1A = [10, 20, 30, 40, 50]print(linear_search(A, 30))print(linear_search(A, 99))
```

Output:

```
2
-1
```

Here, `-1` means the target was not found. It is a convention used by this implementation, not an actual array index.

Complexity of linear search

|Case|Time complexity|Explanation|
|---|---|---|
|Best|\(O(1)\)|Target is the first element|
|Average|\(O(n)\)|A substantial portion may be examined|
|Worst|\(O(n)\)|Target is last or absent|
|Extra space|\(O(1)\)|No additional structure proportional to input size|

### 3.2 Binary search

Binary search repeatedly halves the search range to locate the target.

Critical requirement: The array must be sorted for ordinary binary search to work correctly.

Example: Search for `40` in `[10, 20, 30, 40, 50, 60, 70]`.

1. Middle element is `40`.
    
2. Target matches the middle element.
    
3. Return its index, `3`.
    

Python implementation:

```
def binary_search(arr, target):    low = 0    high = len(arr) - 1    while low <= high:        mid = (low + high) // 2        if arr[mid] == target:            return mid        elif arr[mid] < target:            low = mid + 1        else:            high = mid - 1    return -1A = [10, 20, 30, 40, 50, 60, 70]print(binary_search(A, 40))print(binary_search(A, 25))
```

Output:

```
3
-1
```

### Binary search walkthrough

Search for `60` in the sorted array:

|Step|Low|High|Mid|Middle value|Action|
|---|---|---|---|---|---|
|1|0|6|3|40|Search right half|
|2|4|6|5|60|Target found|

The target is found at index `5`.

Complexity of binary search

- Best case: \(O(1)\)
    
- Average and worst case: \(O(\log n)\)
    
- Iterative implementation's extra space: \(O(1)\)
    

### Linear vs binary search

|Feature|Linear search|Binary search|
|---|---|---|
|Requires sorted array?|No|Yes, for the standard algorithm|
|Search method|Checks one by one|Halves the range repeatedly|
|Worst-case time|\(O(n)\)|\(O(\log n)\)|
|Best case|\(O(1)\)|\(O(1)\)|
|Typical use|Small or unsorted data|Sorted data|

DSSSB exam trap: Binary search is not automatically suitable for an unsorted array. Sorting the data first has a cost too, so consider that when comparing whole operations.

## 4. Insertion

Insertion means adding a new element at a specified position in an array.

Suppose:

```
A = [10, 20, 30, 40, 50]
```

Insert `25` at index `2`.

The elements from index `2` onward must move one position to the right in a conventional array.

### Before insertion

## 10

0

## 20

1

## 30

2

## 40

3

## 50

4

Insert 25 at index 2.

### After insertion

## 10

0

## 20

1

## 25

2

## 30

3

## 40

4

## 50

5

### Python implementation using `insert()`

```
A = [10, 20, 30, 40, 50]A.insert(2, 25)print(A)
```

Output:

```
[10, 20, 25, 30, 40, 50]
```

Python's `list.insert(index, value)` handles the shifting automatically.

### How insertion works internally

In a conventional array with available capacity, the basic algorithm is:

```
Algorithm INSERT(A, n, capacity, pos, value):    if n == capacity:        report overflow    for i = n - 1 down to pos:        A[i + 1] = A[i]    A[pos] = value    n = n + 1
```

The loop moves elements from right to left so that values are not overwritten before they are copied.

### Insertion at different positions

|Position|Elements shifted|Typical time|
|---|---|---|
|Beginning|Nearly all elements|\(O(n)\)|
|Middle|Elements after the position|\(O(n)\)|
|End|No existing elements need to shift|\(O(1)\) if capacity is available|

For Python lists, `append()` is typically amortized \(O(1)\); inserting at the beginning or in the middle is \(O(n)\) because elements must shift.

Exam trap: Insertion into a full fixed-size array is impossible without additional capacity. Python lists can grow dynamically, so this fixed-capacity limitation does not apply in the same way.

## 5. Deletion

Deletion means removing an element from an array.

Suppose:

```
A = [10, 20, 30, 40, 50]
```

Delete the element at index `2`, which is `30`.

In a conventional array, elements to its right shift one position to the left.

### Before deletion

## 10

0

## 20

1

## 30

2

## 40

3

## 50

4

Delete the element at index 2.

### After deletion

## 10

0

## 20

1

## 40

2

## 50

3

### Python implementation using `pop()`

```
A = [10, 20, 30, 40, 50]removed = A.pop(2)print("Deleted:", removed)print("Array:", A)
```

Output:

```
Deleted: 30
Array: [10, 20, 40, 50]
```

### Deletion algorithm

```
Algorithm DELETE(A, n, pos):    if n == 0:        report underflow    for i = pos to n - 2:        A[i] = A[i + 1]    n = n - 1
```

After deleting an element, the remaining elements shift from left to right to fill the empty position.

### Deletion at different positions

|Position|Elements shifted|Typical time|
|---|---|---|
|Beginning|Nearly all remaining elements|\(O(n)\)|
|Middle|Elements after the deleted element|\(O(n)\)|
|End|No existing elements need to shift|\(O(1)\)|

In Python, `pop()` with no index removes the last element. `pop(i)` removes and returns the element at index `i`.

Exam trap: Deletion from the end is typically \(O(1)\), but deletion from the start of an array-like list is \(O(n)\).

## 6. Time complexity of array operations

This comparison is especially useful for DSSSB complexity-based MCQs.

|Operation|Best case|Average case|Worst case|
|---|---|---|---|
|Access by index|\(O(1)\)|\(O(1)\)|\(O(1)\)|
|Traversal|\(O(n)\)|\(O(n)\)|\(O(n)\)|
|Linear search|\(O(1)\)|\(O(n)\)|\(O(n)\)|
|Binary search on sorted data|\(O(1)\)|\(O(\log n)\)|\(O(\log n)\)|
|Insert at beginning|\(O(n)\)|\(O(n)\)|\(O(n)\)|
|Insert in middle|Depends on position|\(O(n)\)|\(O(n)\)|
|Delete at beginning|\(O(n)\)|\(O(n)\)|\(O(n)\)|
|Delete in middle|Depends on position|\(O(n)\)|\(O(n)\)|
|Insert at end|\(O(1)\) when capacity exists|Usually \(O(1)\) amortized for Python lists|Can be \(O(n)\) when resizing is needed|

The table describes common array operations. The exact insertion and deletion complexity depends on the position and whether capacity changes are involved.

### Why does insertion in the middle take \(O(n)\)?

If an array contains \(n\) elements and a new element is inserted at index `0`, all \(n\) existing elements may need to shift right. The amount of work grows linearly with array size.

### Why is index access \(O(1)\)?

An array's indexed access can locate an element directly from its base address and index, rather than checking every preceding element.

This is one of the principal advantages of arrays.

## 7. Common exam traps

1. Binary search requires sorted data

Standard binary search cannot reliably find an element in arbitrary unsorted data.

2. Indexing and traversal have different complexities

Accessing `A[3]` is \(O(1)\); processing every element is \(O(n)\).

3. Insertion and deletion may require shifting

Inserting or deleting near the beginning can require moving many elements.

4. Indexing starts at zero in Python

For an array-like sequence of length \(n\), valid indexes are `0` through `n-1`.

5. Overflow depends on the array model

A fixed-size array may be full and unable to accept an insertion. Python lists can grow dynamically, although growth can require resizing.

## Final revision sheet

|Topic|Key takeaway|
|---|---|
|Traversal|Visits elements; \(O(n)\)|
|Linear search|Works on sorted or unsorted data; worst case \(O(n)\)|
|Binary search|Standard version needs sorted data; worst case \(O(\log n)\)|
|Insertion|May shift elements to the right|
|Deletion|May shift elements to the left|
|Indexed access|\(O(1)\) for a conventional array|
|Fixed-size array|Cannot grow beyond capacity without extra storage|
|Python list|Dynamic, array-like sequence|