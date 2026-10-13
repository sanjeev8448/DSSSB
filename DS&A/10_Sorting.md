# Sorting Algorithms — DSSSB TGT Computer Science

## 1. Sorting Fundamentals

Sorting arranges data in a particular order.

**Example:**

Unsorted array:

```
[40, 10, 30, 20, 50]
```

Ascending order:

```
[10, 20, 30, 40, 50]
```

Descending order:

```
[50, 40, 30, 20, 10]
```

### Important Terminology

|Term|Meaning|
|---|---|
|Ascending order|Smallest to largest|
|Descending order|Largest to smallest|
|Stable sort|Preserves the relative order of elements with equal keys|
|In-place sort|Uses little additional memory, typically O(1) auxiliary space|
|Adaptive sort|Takes advantage of existing order in the input|
|Comparison sort|Sorts elements by comparing their keys|
|Divide and conquer|Divides a problem into smaller subproblems and combines their solutions|

**Example of stability:** Suppose two records have the same marks.

```
(Amit, 80), (Neha, 70), (Ravi, 80)
```

A stable sort by marks preserves the relative order of Amit and Ravi because both have 80 marks.

---

## 2. Bubble Sort

Bubble sort repeatedly compares adjacent elements and swaps them if they are in the wrong order.

After each complete pass, the largest unsorted element moves to its correct position at the end.

### 2.1 Dry Run

Sort the array:

```
[5, 1, 4, 2, 8]
```

**Pass 1**

|Comparison|Action|Array afterward|
|---|---|---|
|5 and 1|Swap|[1, 5, 4, 2, 8]|
|5 and 4|Swap|[1, 4, 5, 2, 8]|
|5 and 2|Swap|[1, 4, 2, 5, 8]|
|5 and 8|No swap|[1, 4, 2, 5, 8]|

The largest element, 8, is already at the end.

**Pass 2**

```
[1, 4, 2, 5, 8]
        ↓
[1, 2, 4, 5, 8]
```

The optimized algorithm stops when a complete pass makes no swaps.

### 2.2 Python Implementation

```
def bubble_sort(arr):
    n = len(arr)

    for i in range(n - 1):
        swapped = False

        for j in range(n - 1 - i):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True

        if not swapped:
            break

    return arr


print(bubble_sort([5, 1, 4, 2, 8]))
```

Output:

```
[1, 2, 4, 5, 8]
```

The `swapped` flag detects whether any swaps occurred during a pass. If none occurred, the array is already sorted.

### 2.3 Complexity

|Case|Time complexity|
|---|---|
|Best case, with early-stop optimization|Θ(n)|
|Average case|Θ(n²)|
|Worst case|Θ(n²)|
|Auxiliary space|O(1)|

**Properties:**

- Stable.
    
- In-place.
    
- Repeatedly swaps adjacent out-of-order elements.
    

**Exam traps:**

- The largest unsorted element reaches the end after each pass.
    
- Without early-stop optimization, the best case is also Θ(n²).
    
- Standard bubble sort is stable when equal elements are not swapped.
    

---

## 3. Selection Sort

Selection sort divides the array into sorted and unsorted portions. It repeatedly finds the minimum element in the unsorted portion and swaps it with the first unsorted element.

### 3.1 Dry Run

Sort:

```
[64, 25, 12, 22, 11]
```

**Pass 1:** Minimum is 11. Swap it with 64.

```
[11, 25, 12, 22, 64]
```

**Pass 2:** Minimum among `[25, 12, 22, 64]` is 12.

```
[11, 12, 25, 22, 64]
```

**Pass 3:** Minimum among `[25, 22, 64]` is 22.

```
[11, 12, 22, 25, 64]
```

**Pass 4:** The remaining unsorted portion is already in order.

Final array:

```
[11, 12, 22, 25, 64]
```

### 3.2 Python Implementation

```
def selection_sort(arr):
    n = len(arr)

    for i in range(n):
        min_index = i

        for j in range(i + 1, n):
            if arr[j] < arr[min_index]:
                min_index = j

        arr[i], arr[min_index] = arr[min_index], arr[i]

    return arr


print(selection_sort([64, 25, 12, 22, 11]))
```

Output:

```
[11, 12, 22, 25, 64]
```

### 3.3 Complexity

|Case|Time complexity|
|---|---|
|Best|Θ(n²)|
|Average|Θ(n²)|
|Worst|Θ(n²)|
|Auxiliary space|O(1)|

Selection sort performs approximately n(n − 1) / 2 comparisons, even when the array is already sorted. This implementation performs at most n − 1 swaps.

**Properties and exam traps:**

- Selects the minimum from the unsorted portion.
    
- Generally performs fewer swaps than bubble sort.
    
- In-place.
    
- Unstable in general because a swap can change the relative order of equal-key elements.
    
- Has quadratic time complexity in all three cases.
    

---

## 4. Insertion Sort

Insertion sort builds a sorted portion from left to right. Each new element is inserted into its correct position within the already-sorted portion.

Think of arranging playing cards in your hand: take the next card and insert it into the correct position.

### 4.1 Dry Run

Sort:

```
[5, 2, 4, 6, 1, 3]
```

Initially, `[5]` is considered sorted.

|Step|Element being inserted|Array afterward|
|---|---|---|
|1|2|[2, 5, 4, 6, 1, 3]|
|2|4|[2, 4, 5, 6, 1, 3]|
|3|6|[2, 4, 5, 6, 1, 3]|
|4|1|[1, 2, 4, 5, 6, 3]|
|5|3|[1, 2, 3, 4, 5, 6]|

After every step, the portion to the left of the current position remains sorted.

### 4.2 Python Implementation

```
def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1

        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1

        arr[j + 1] = key

    return arr


print(insertion_sort([5, 2, 4, 6, 1, 3]))
```

Output:

```
[1, 2, 3, 4, 5, 6]
```

The condition `arr[j] > key` is important for stability. Equal elements are not shifted past one another.

### 4.3 Complexity

|Case|Time complexity|
|---|---|
|Best case, already sorted|Θ(n)|
|Average case|Θ(n²)|
|Worst case, reverse sorted|Θ(n²)|
|Auxiliary space|O(1)|

**Properties:**

- Stable.
    
- In-place.
    
- Adaptive.
    
- Particularly effective on small or nearly sorted arrays.
    

**Exam traps:**

- Best case is linear because each element needs only one comparison with its predecessor.
    
- Worst case occurs when the elements are in reverse order.
    
- Insertion sort shifts elements to make room; it does not repeatedly select the minimum.
    

---

## 5. Merge Sort

Merge sort uses the **divide-and-conquer** technique.

Its process:

1. Divide the array into smaller halves.
    
2. Recursively sort each half.
    
3. Merge the sorted halves into one sorted array.
    

### 5.1 Dry Run

Sort:

```
[38, 27, 43, 3]
```

**Divide:**

```
             [38, 27, 43, 3]
               /           \
          [38, 27]        [43, 3]
           /    \          /   \
         [38]  [27]      [43]  [3]
```

**Merge sorted parts:**

```
[38] + [27]  → [27, 38]
[43] + [3]   → [3, 43]
```

Merge the two sorted halves:

```
[27, 38] + [3, 43]
          ↓
[3, 27, 38, 43]
```

### 5.2 Python Implementation

```
def merge_sort(arr):
    if len(arr) <= 1:
        return arr

    mid = len(arr) // 2

    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

    return merge(left, right)


def merge(left, right):
    result = []
    i = j = 0

    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    result.extend(left[i:])
    result.extend(right[j:])

    return result


print(merge_sort([38, 27, 43, 3]))
```

Output:

```
[3, 27, 38, 43]
```

The comparison `left[i] <= right[j]` ensures that equal-key elements from the left half are selected first, preserving their relative order.

### 5.3 Complexity

|Case|Time complexity|
|---|---|
|Best|Θ(n log n)|
|Average|Θ(n log n)|
|Worst|Θ(n log n)|
|Auxiliary space for standard array implementation|O(n)|

**Properties:**

- Stable when ties are merged consistently.
    
- Uses divide and conquer.
    
- Requires additional storage in the standard array implementation.
    
- Returns a new list rather than sorting the original list in place.
    

**Exam traps:**

- Merge sort consistently achieves Θ(n log n) time.
    
- The merge step combines already-sorted parts; it does not simply concatenate them.
    
- It is useful when predictable worst-case performance and stability are required.
    

---

## 6. Quick Sort

Quick sort is another divide-and-conquer algorithm. It selects a **pivot** and partitions the array so that smaller elements go to one side and larger elements go to the other. It then recursively sorts the partitions.

### 6.1 Dry Run

Consider:

```
[7, 2, 9, 4, 3]
```

Choose the last element, `3`, as the pivot.

After partitioning, one valid result is:

```
[2, 3, 9, 4, 7]
```

The pivot `3` is now at its final sorted position. The left side `[2]` is sorted, but the right side `[9, 4, 7]` still needs sorting.

After sorting the right partition:

```
[2, 3, 4, 7, 9]
```

The exact intermediate order depends on the partition algorithm and pivot-selection rule.

### 6.2 Python Implementation: Lomuto Partition

```
def partition(arr, low, high):
    pivot = arr[high]
    i = low - 1

    for j in range(low, high):
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]

    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1


def quick_sort(arr, low=0, high=None):
    if high is None:
        high = len(arr) - 1

    if low < high:
        pivot_index = partition(arr, low, high)

        quick_sort(arr, low, pivot_index - 1)
        quick_sort(arr, pivot_index + 1, high)

    return arr


print(quick_sort([7, 2, 9, 4, 3]))
```

Output:

```
[2, 3, 4, 7, 9]
```

This implementation modifies the original list in place and uses the last element as the pivot.

### 6.3 Complexity

|Case|Time complexity|
|---|---|
|Best|Θ(n log n)|
|Average, under common assumptions|Θ(n log n)|
|Worst|Θ(n²)|
|Recursive call stack|Typically O(log n) average; O(n) worst|

### Why Can Quick Sort Become Quadratic?

Suppose the input is already sorted and the algorithm always chooses the final element as the pivot. The partitions can become highly unbalanced, with sizes `n − 1` and `0`.

The recurrence is approximately:

```
T(n) = T(n − 1) + Θ(n)
```

Therefore, the worst-case time complexity becomes:

```
Θ(n²)
```

Choosing a pivot that tends to produce balanced partitions reduces the chance of the worst case but does not eliminate the theoretical worst-case bound for this implementation.

**Properties and exam traps:**

- Often fast in practice.
    
- Worst-case time is O(n²).
    
- Pivot selection and partition strategy affect performance.
    
- Standard in-place quick sort is not stable in general.
    
- The displayed recursive implementation can use O(n) call-stack space in the worst case.
    

---

## 7. Heap Sort

Heap sort uses a binary heap, a complete binary tree satisfying the heap-order property.

For ascending order, a common approach is to build a **max-heap**, where the largest element is at the root.

### 7.1 Main Steps

1. Build a max-heap from the array.
    
2. Swap the root (maximum) with the final element of the current heap.
    
3. Reduce the heap size by one.
    
4. Restore the heap property by sifting the root downward.
    
5. Repeat until the array is sorted.
    

### 7.2 Dry Run

Sort:

```
[4, 10, 3, 5, 1]
```

**Step 1: Build a max-heap**

One valid max-heap representation is:

```
[10, 5, 3, 4, 1]
```

Tree representation:

```
        10
       /  \
      5    3
     / \
    4   1
```

**Step 2: Move the maximum to the end**

Swap `10` and `1`, then restore the heap property in the reduced heap:

```
[5, 4, 3, 1, 10]
```

**Step 3: Repeat**

Continue moving the maximum remaining element to the end:

```
[4, 1, 3, 5, 10]
[3, 1, 4, 5, 10]
[1, 3, 4, 5, 10]
```

Final sorted array:

```
[1, 3, 4, 5, 10]
```

These are illustrative intermediate states; exact states depend on the heap-building procedure and the sequence of sift-down operations.

### 7.3 Python Implementation

```
def heapify(arr, n, i):
    largest = i
    left = 2 * i + 1
    right = 2 * i + 2

    if left < n and arr[left] > arr[largest]:
        largest = left

    if right < n and arr[right] > arr[largest]:
        largest = right

    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify(arr, n, largest)


def heap_sort(arr):
    n = len(arr)

    # Build a max-heap
    for i in range(n // 2 - 1, -1, -1):
        heapify(arr, n, i)

    # Move maximum elements to the end
    for end in range(n - 1, 0, -1):
        arr[0], arr[end] = arr[end], arr[0]
        heapify(arr, end, 0)

    return arr


print(heap_sort([4, 10, 3, 5, 1]))
```

Output:

```
[1, 3, 4, 5, 10]
```

### 7.4 Understanding Child Indexes

For a zero-indexed array representation of a binary heap, a node at index `i` has:

```
Left child  = 2 * i + 1
Right child = 2 * i + 2
```

The `heapify()` operation ensures that the parent is at least as large as its children, restoring the max-heap property.

### 7.5 Complexity

|Case|Time complexity|
|---|---|
|Best|Θ(n log n)|
|Average|Θ(n log n)|
|Worst|Θ(n log n)|
|Auxiliary space in this recursive implementation|O(log n) worst-case call stack|

The sorting algorithm is in-place, but this recursive `heapify()` implementation uses additional call-stack memory. An iterative heapify implementation can achieve O(1) auxiliary space.

**Exam traps:**

- Bottom-up heap construction takes O(n), not O(n log n).
    
- Repeatedly extracting the maximum takes O(n log n) overall.
    
- Heap sort is not stable in its standard form.
    
- A max-heap is typically used for ascending heap sort.
    

---

## 8. Comparison of All Six Sorting Algorithms

This table is particularly important for DSSSB.

|Algorithm|Best time|Average time|Worst time|Auxiliary space|Stable?|
|---|---|---|---|---|---|
|Bubble sort, optimized|O(n)|O(n²)|O(n²)|O(1)|Yes|
|Selection sort|O(n²)|O(n²)|O(n²)|O(1)|No, generally|
|Insertion sort|O(n)|O(n²)|O(n²)|O(1)|Yes|
|Merge sort|O(n log n)|O(n log n)|O(n log n)|O(n) for arrays|Yes, with stable merge|
|Quick sort|O(n log n) expected/average|O(n log n) expected/average|O(n²)|O(log n) average; O(n) worst for recursive stack|No, generally|
|Heap sort|O(n log n)|O(n log n)|O(n log n)|O(1) with iterative in-place operations|No, generally|

These are standard complexities for the implementations discussed. Quick sort's average behavior assumes reasonably balanced partitions or suitable pivot selection.

### 8.1 Stability: Common MCQ Topic

A sorting algorithm is stable if equal-key items retain their original relative order.

|Algorithm|Standard stability|
|---|---|
|Bubble sort|Stable|
|Selection sort|Unstable in general|
|Insertion sort|Stable|
|Merge sort|Stable with consistent tie handling|
|Quick sort|Unstable in general|
|Heap sort|Unstable in general|

**Memory trick:** Among these six standard implementations, remember **Bubble, Insertion, Merge** as the stable algorithms.

### 8.2 In-Place vs Extra Memory

|Algorithm|Typical memory property|
|---|---|
|Bubble sort|In-place|
|Selection sort|In-place|
|Insertion sort|In-place|
|Merge sort|Needs auxiliary storage for conventional array sorting|
|Quick sort|In-place partitioning, but recursion needs stack memory|
|Heap sort|In-place with iterative heap operations|

### 8.3 Which Algorithm Should You Choose?

|Situation|Good candidate|
|---|---|
|Very small or nearly sorted data|Insertion sort|
|Simple example of adjacent swaps|Bubble sort|
|Minimize swaps in a basic comparison sort|Selection sort|
|Guaranteed O(n log n) time and stability|Merge sort|
|Often fast in practice with in-place partitioning|Quick sort|
|Guaranteed O(n log n) time with in-place sorting|Heap sort|

These are general trade-offs, not universal performance guarantees for every implementation or hardware environment.

---

## 9. Final Revision Sheet

|Algorithm|Main idea|Time complexity summary|Stable?|
|---|---|---|---|
|Bubble sort|Swap adjacent out-of-order elements|O(n) best with optimization; O(n²) worst|Yes|
|Selection sort|Select minimum and place it|O(n²) in all cases|No, generally|
|Insertion sort|Insert next element into sorted prefix|O(n) best; O(n²) worst|Yes|
|Merge sort|Divide, sort, merge|O(n log n) in all cases|Yes, with stable merge|
|Quick sort|Partition around pivot|O(n log n) average; O(n²) worst|No, generally|
|Heap sort|Build heap, repeatedly extract root|O(n log n) in all cases|No, generally|

### Highest-Priority DSSSB Topics

1. Memorize best-, average-, and worst-case complexities.
    
2. Learn which algorithms are stable and unstable.
    
3. Understand the difference between merge sort and quick sort.
    
4. Remember why heap construction is O(n), while complete heap sort is O(n log n).
    
5. Practise tracing array changes after every pass or partition.
    
6. Understand the effect of an already-sorted or reverse-sorted input on bubble, insertion, and quick sort.