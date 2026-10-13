# Arrays in Data Structures
## 1. Array Fundamentals

Consider the following array:

`A = [10, 20, 30, 40, 50]`

|Element|Index|
|---|---|
|10|0|
|20|1|
|30|2|
|40|3|
|50|4|

The first element is at index 0, and the last element is at index 4.

### Important Properties

- Arrays are linear data structures.
    
- Elements are accessed using indexes.
    
- Accessing an element by index generally takes O(1) time.
    
- In a conventional fixed-size array, capacity is determined at creation.
    
- Inserting or deleting elements in the middle usually requires shifting elements.
    

**Python note:** Python's built-in `list` is a dynamic, array-like sequence, not a strict fixed-size, homogeneous array. Python lists will be used here to demonstrate operations, while conventional array terminology is used for algorithm and complexity questions.

---

## 2. Array Traversal

Traversal means visiting each element of an array to display, count, search, or process its elements.

Consider:

```
A = [10, 20, 30, 40, 50]
```

### Example 1: Traversal Using a `for` Loop

```
A = [10, 20, 30, 40, 50]

for element in A:
    print(element)
```

Output:

```
10
20
30
40
50
```

### Example 2: Traversal Using Indexes

```
A = [10, 20, 30, 40, 50]

for i in range(len(A)):
    print("Index:", i, "Value:", A[i])
```

Output:

```
Index: 0 Value: 10
Index: 1 Value: 20
Index: 2 Value: 30
Index: 3 Value: 40
Index: 4 Value: 50
```

### Example 3: Calculate the Sum

```
A = [10, 20, 30, 40, 50]

total = 0

for element in A:
    total += element

print(total)
```

Output:

```
150
```

### Traversal Algorithm

```
Algorithm TRAVERSE(A, n):
    for i = 0 to n - 1:
        display A[i]
```

For an array containing n elements:

- Time complexity: O(n)
    
- Extra space: O(1), excluding output storage.
    

**Exam trap:** Traversing an array of 100 elements requires 100 visits. Its time complexity is O(n), not O(1).

---

## 3. Searching

Searching means determining whether a particular element exists in an array and, if it does, finding its index.

The two important searching algorithms are:

1. Linear Search
    
2. Binary Search
    

### 3.1 Linear Search

Linear search checks elements one by one, starting from the beginning, until the target is found or the array ends.

Example: Search for `30` in `[10, 20, 30, 40, 50]`.

### Python Implementation

```
def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i

    return -1


A = [10, 20, 30, 40, 50]

print(linear_search(A, 30))
print(linear_search(A, 99))
```

Output:

```
2
-1
```

Here, `-1` means the target was not found. It is a convention used by this implementation, not an actual array index.

### Complexity of Linear Search

|Case|Time Complexity|Explanation|
|---|---|---|
|Best|O(1)|Target is the first element|
|Average|O(n)|A substantial portion may be examined|
|Worst|O(n)|Target is last or absent|
|Extra space|O(1)|No additional structure proportional to input size|

### 3.2 Binary Search

Binary search repeatedly halves the search range to locate the target.

**Critical requirement:** The array must be sorted for ordinary binary search to work correctly.

Example: Search for `40` in `[10, 20, 30, 40, 50, 60, 70]`.

1. The middle element is `40`.
    
2. The target matches the middle element.
    
3. Return index `3`.
    

### Python Implementation

```
def binary_search(arr, target):
    low = 0
    high = len(arr) - 1

    while low <= high:
        mid = (low + high) // 2

        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1

    return -1


A = [10, 20, 30, 40, 50, 60, 70]

print(binary_search(A, 40))
print(binary_search(A, 25))
```

Output:

```
3
-1
```

### Binary Search Walkthrough

Search for `60` in the sorted array:

`A = [10, 20, 30, 40, 50, 60, 70]`

|Step|Low|High|Mid|Middle Value|Action|
|---|---|---|---|---|---|
|1|0|6|3|40|Search right half|
|2|4|6|5|60|Target found|

The target is found at index 5.

### Complexity of Binary Search

- Best case: O(1)
    
- Average case: O(log n)
    
- Worst case: O(log n)
    
- Extra space for iterative implementation: O(1)
    

### Linear Search vs Binary Search

|Feature|Linear Search|Binary Search|
|---|---|---|
|Requires sorted array?|No|Yes, for the standard algorithm|
|Search method|Checks elements one by one|Repeatedly halves the search range|
|Worst-case time|O(n)|O(log n)|
|Best-case time|O(1)|O(1)|
|Typical use|Small or unsorted data|Sorted data|

**DSSSB exam trap:** Binary search is not automatically suitable for an unsorted array. Sorting the data first also has a cost, which must be considered when comparing complete operations.

---

## 4. Array Insertion

Insertion means adding a new element at a specified position in an array.

Suppose:

`A = [10, 20, 30, 40, 50]`

Insert `25` at index 2.

Before insertion:

`[10, 20, 30, 40, 50]`

After insertion:

`[10, 20, 25, 30, 40, 50]`

In a conventional array, the elements from index 2 onward must move one position to the right.

### Python Implementation Using `insert()`

```
A = [10, 20, 30, 40, 50]

A.insert(2, 25)

print(A)
```

Output:

```
[10, 20, 25, 30, 40, 50]
```

Python's `list.insert(index, value)` handles the shifting automatically.

### Insertion Algorithm

```
Algorithm INSERT(A, n, capacity, pos, value):

    if n == capacity:
        report overflow

    for i = n - 1 down to pos:
        A[i + 1] = A[i]

    A[pos] = value
    n = n + 1
```

The loop moves elements from right to left so that values are not overwritten before being copied.

### Insertion at Different Positions

|Position|Elements Shifted|Typical Time|
|---|---|---|
|Beginning|Nearly all elements|O(n)|
|Middle|Elements after the insertion position|O(n)|
|End|No existing elements need to shift|O(1), if capacity is available|

For Python lists, `append()` is typically amortized O(1). Inserting at the beginning or in the middle takes O(n) because elements must shift.

**Exam trap:** Insertion into a full fixed-size array is impossible without additional capacity. Python lists can grow dynamically, so this limitation does not apply in the same way.

---

## 5. Array Deletion

Deletion means removing an element from an array.

Suppose:

`A = [10, 20, 30, 40, 50]`

Delete the element at index 2, which is `30`.

Before deletion:

`[10, 20, 30, 40, 50]`

After deletion:

`[10, 20, 40, 50]`

In a conventional array, elements to the right of the deleted element shift one position to the left.

### Python Implementation Using `pop()`

```
A = [10, 20, 30, 40, 50]

removed = A.pop(2)

print("Deleted:", removed)
print("Array:", A)
```

Output:

```
Deleted: 30
Array: [10, 20, 40, 50]
```

### Deletion Algorithm

```
Algorithm DELETE(A, n, pos):

    if n == 0:
        report underflow

    for i = pos to n - 2:
        A[i] = A[i + 1]

    n = n - 1
```

After deletion, the remaining elements shift to the left to fill the empty position.

### Deletion at Different Positions

|Position|Elements Shifted|Typical Time|
|---|---|---|
|Beginning|Nearly all remaining elements|O(n)|
|Middle|Elements after the deleted element|O(n)|
|End|No existing elements need to shift|O(1)|

In Python:

- `pop()` removes and returns the last element.
    
- `pop(i)` removes and returns the element at index `i`.
    

**Exam trap:** Deletion from the end is typically O(1), but deletion from the beginning of an array-like list is O(n).

---

## 6. Time Complexity of Array Operations

This comparison is especially useful for DSSSB complexity-based MCQs.

|Operation|Best Case|Average Case|Worst Case|
|---|---|---|---|
|Access by index|O(1)|O(1)|O(1)|
|Traversal|O(n)|O(n)|O(n)|
|Linear search|O(1)|O(n)|O(n)|
|Binary search on sorted data|O(1)|O(log n)|O(log n)|
|Insert at beginning|O(n)|O(n)|O(n)|
|Insert in middle|Depends on position|O(n)|O(n)|
|Delete at beginning|O(n)|O(n)|O(n)|
|Delete in middle|Depends on position|O(n)|O(n)|
|Insert at end|O(1), if capacity exists|Usually amortized O(1) for Python lists|Can be O(n) if resizing is needed|

The exact insertion and deletion complexity depends on the position and whether capacity changes are involved.

### Why Does Insertion in the Middle Take O(n)?

If an array contains n elements and a new element is inserted at index 0, all n existing elements may need to shift right.

The amount of work grows linearly with the array size. Therefore, the time complexity is O(n).

### Why Is Index Access O(1)?

An array can locate an element directly using its base address and index, rather than checking every preceding element.

This is one of the principal advantages of arrays.

---

## 7. Common DSSSB Exam Traps

1. **Binary search requires sorted data.** Standard binary search cannot reliably find an element in arbitrary unsorted data.
    
2. **Indexing and traversal have different complexities.**
    
    - Accessing `A[3]`: O(1).
        
    - Processing every element: O(n).
        
3. **Insertion and deletion may require shifting.** Operations near the beginning can require moving many elements.
    
4. **Python indexing starts at zero.** For a sequence of length n, valid indexes are `0` through `n - 1`.
    
5. **Overflow depends on the array model.** A fixed-size array may be full and unable to accept an insertion. Python lists can grow dynamically, although growth may require resizing.
    

---

## 8. Final Revision Sheet

|Topic|Key Takeaway|
|---|---|
|Traversal|Visits all elements; O(n)|
|Linear search|Works on sorted or unsorted data; worst case O(n)|
|Binary search|Standard version requires sorted data; worst case O(log n)|
|Insertion|May shift elements to the right|
|Deletion|May shift elements to the left|
|Indexed access|O(1) for a conventional array|
|Fixed-size array|Cannot grow beyond capacity without additional storage|
|Python list|Dynamic, array-like sequence|

### Quick Memory Tricks

- **Access:** Direct access by index → O(1).
    
- **Traversal:** Visit every element → O(n).
    
- **Linear search:** Check one by one → O(n) worst case.
    
- **Binary search:** Halve the range → O(log n) worst case.
    
- **Insertion:** Shift elements right.
    
- **Deletion:** Shift elements left.