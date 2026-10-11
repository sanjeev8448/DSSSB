# 1. Sorting fundamentals

Consider this unsorted array:

```
[40, 10, 30, 20, 50]
```

After sorting in ascending order:

```
[10, 20, 30, 40, 50]
```

Sorting in descending order produces:

```
[50, 40, 30, 20, 10]
```

## Important terminology

|Term|Meaning|
|---|---|
|Ascending order|Smallest to largest|
|Descending order|Largest to smallest|
|Stable sort|Preserves the relative order of equal-key elements|
|In-place sort|Uses little additional memory, typically \(O(1)\) auxiliary space|
|Adaptive sort|Can take advantage of existing order in the input|
|Comparison sort|Orders elements by comparing keys|
|Divide and conquer|Breaks a problem into smaller subproblems, solves them, then combines the results|

Example of stability: Suppose two records have the same marks:

```
(Amit, 80), (Neha, 70), (Ravi, 80)
```

A stable ascending sort by marks puts the two records with `80` in their original relative order: Amit appears before Ravi.

# 2. Bubble sort

Bubble sort repeatedly compares adjacent elements and swaps them when they are in the wrong order.

After a complete pass through the array, the largest unsorted element has moved to its correct position at the end.

## 2.1 Dry run

Sort the array:

```
[5, 1, 4, 2, 8]
```

### Pass 1

|Comparison|Action|Array afterward|
|---|---|---|
|5 and 1|Swap|`[1, 5, 4, 2, 8]`|
|5 and 4|Swap|`[1, 4, 5, 2, 8]`|
|5 and 2|Swap|`[1, 4, 2, 5, 8]`|
|5 and 8|No swap|`[1, 4, 2, 5, 8]`|

The largest element, `8`, is already at the end.

### Pass 2

```
[1, 4, 2, 5, 8]
     ↓
[1, 2, 4, 5, 8]
```

The remaining passes verify the order. With an optimization that stops when no swaps occur, the algorithm terminates once the array is sorted.

## 2.2 Python implementation

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

The `swapped` flag detects whether a pass made any swaps. If no swap occurs, the array is already sorted.

## 2.3 Complexity

|Case|Time complexity|
|---|---|
|Best case, with swap optimization|\(\Theta(n)\)|
|Average case|\(\Theta(n^2)\)|
|Worst case|\(\Theta(n^2)\)|
|Auxiliary space|\(O(1)\)|

Bubble sort is stable when equal elements are not swapped, as in the implementation above. It is also in-place.

Exam traps:

- In each full pass, the largest unsorted value reaches the end.
    
- The unoptimized version has \(\Theta(n^2)\) best-case time too; the linear best case depends on the early-stop optimization.
    
- Standard bubble sort is stable.
    

# 3. Selection sort

Selection sort divides the array into a sorted portion and an unsorted portion. It repeatedly finds the smallest element in the unsorted portion and swaps it with the first unsorted element.

## 3.1 Dry run

Sort:

```
[64, 25, 12, 22, 11]
```

Pass 1: The minimum is `11`. Swap it with `64`.

```
[11, 25, 12, 22, 64]
```

Pass 2: The minimum among `[25, 12, 22, 64]` is `12`. Swap it with `25`.

```
[11, 12, 25, 22, 64]
```

Pass 3: The minimum among `[25, 22, 64]` is `22`.

```
[11, 12, 22, 25, 64]
```

Pass 4: The remaining unsorted portion is already in order.

Final array:

```
[11, 12, 22, 25, 64]
```

## 3.2 Python implementation

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

## 3.3 Complexity

|Case|Time complexity|
|---|---|
|Best|\(\Theta(n^2)\)|
|Average|\(\Theta(n^2)\)|
|Worst|\(\Theta(n^2)\)|
|Auxiliary space|\(O(1)\)|

Selection sort makes approximately \(n(n-1)/2\) comparisons regardless of whether the array starts sorted. It performs at most \(n-1\) swaps in this implementation.

Exam traps:

- Selection sort selects the minimum from the unsorted portion.
    
- It generally performs fewer swaps than bubble sort.
    
- Standard selection sort is not stable in general, because swapping a minimum element can change the relative order of equal-key elements.
    
- It is in-place and has quadratic time complexity in all three cases.
    

# 4. Insertion sort

Insertion sort builds a sorted portion from left to right. Each new element is inserted into its correct position within the already-sorted portion.

Think of arranging playing cards in your hand: take the next card and insert it into the correct place among the cards already arranged.

## 4.1 Dry run

Sort:

```
[5, 2, 4, 6, 1, 3]
```

Initially, `[5]` is considered sorted.

|Step|Element being inserted|Array afterward|
|---|---|---|
|1|2|`[2, 5, 4, 6, 1, 3]`|
|2|4|`[2, 4, 5, 6, 1, 3]`|
|3|6|`[2, 4, 5, 6, 1, 3]`|
|4|1|`[1, 2, 4, 5, 6, 3]`|
|5|3|`[1, 2, 3, 4, 5, 6]`|

After every step, the portion to the left of the current position remains sorted.

## 4.2 Python implementation

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

The condition `arr[j] > key` is important for stability: equal elements are not shifted past one another.

## 4.3 Complexity

|Case|Time complexity|
|---|---|
|Best case, already sorted|\(\Theta(n)\)|
|Average case|\(\Theta(n^2)\)|
|Worst case, reverse sorted|\(\Theta(n^2)\)|
|Auxiliary space|\(O(1)\)|

Insertion sort is stable, in-place, and adaptive. It works particularly well on small arrays or data that is already nearly sorted.

Exam traps:

- The best case is linear because each element needs only one comparison with its predecessor.
    
- The worst case occurs when elements are in reverse order.
    
- Insertion sort shifts elements to make room; it does not repeatedly select the minimum or simply swap adjacent elements as bubble sort does.
    

# 5. Merge sort

Merge sort uses the divide-and-conquer technique.

Its process is:

1. Divide the array into smaller halves.
    
2. Recursively sort each half.
    
3. Merge the sorted halves into one sorted array.
    

## 5.1 Dry run

Sort:

```
[38, 27, 43, 3]
```

Divide:

```
           [38, 27, 43, 3]
             /          \
        [38, 27]       [43, 3]
         /    \         /   \
       [38]  [27]     [43]  [3]
```

Merge sorted parts:

```
[38] + [27] → [27, 38]
[43] + [3]  → [3, 43]
```

Merge the two sorted halves:

```
[27, 38] + [3, 43]
          ↓
[3, 27, 38, 43]
```

### Merge sort: divide and merge

### [38, 27, 43, 3]

[38, 27]

[43, 3]

[27, 38]

[3, 43]

### [3, 27, 38, 43]

## 5.2 Python implementation

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

The implementation uses `<=` when comparing elements. This ensures that when equal keys appear in both sorted halves, the element from the left half is selected first, preserving their relative order.

## 5.3 Complexity

|Case|Time complexity|
|---|---|
|Best|\(\Theta(n\log n)\)|
|Average|\(\Theta(n\log n)\)|
|Worst|\(\Theta(n\log n)\)|
|Auxiliary space, standard array implementation|\(O(n)\)|

Merge sort is stable when implemented with the stable merge rule shown above. The displayed Python implementation also returns new lists instead of sorting the original list in place.

Exam traps:

- Merge sort consistently achieves \(\Theta(n\log n)\) time.
    
- Its extra space for a standard array implementation is \(O(n)\).
    
- It is a divide-and-conquer algorithm.
    
- The merge step combines already-sorted arrays; it does not simply concatenate them.
    

# 6. Quick sort

Quick sort is another divide-and-conquer sorting algorithm. It selects a pivot and partitions the array so that smaller elements go to one side and larger elements go to the other, then recursively sorts the partitions.

## 6.1 Dry run

Consider:

```
[7, 2, 9, 4, 3]
```

Choose the last element, `3`, as the pivot.

After partitioning, one valid partition result is:

```
[2, 3, 9, 4, 7]
```

The pivot `3` is now at its final sorted position. The left side `[2]` is sorted, and the right side `[9, 4, 7]` still needs sorting.

Sorting that right partition produces:

```
[2, 3, 4, 7, 9]
```

The exact intermediate order depends on the partition algorithm and pivot-selection rule.

## 6.2 Python implementation: Lomuto partition

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

This implementation modifies the original list in place. It uses the last element as the pivot.

## 6.3 Complexity

|Case|Time complexity|
|---|---|
|Best|\(\Theta(n\log n)\)|
|Average, under common assumptions|\(\Theta(n\log n)\)|
|Worst|\(\Theta(n^2)\)|
|Auxiliary space, recursive call stack|Typically \(O(\log n)\) average; \(O(n)\) worst|

### Why can quick sort become quadratic?

Suppose the input is already sorted and the algorithm always selects the final element as the pivot. The partitions can become highly unbalanced, of sizes `n-1` and `0`.

The recurrence is approximately:

\[ T(n)=T(n-1)+\Theta(n) \]

Therefore, the worst-case time becomes:

\[ \boxed{\Theta(n^2)} \]

Choosing a pivot that tends to create balanced partitions reduces the chance of the worst case, but does not eliminate the theoretical worst-case bound for this implementation.

Exam traps:

- Quick sort is usually fast in practice, but its worst-case time is \(O(n^2)\).
    
- The pivot-selection and partition strategy affect performance.
    
- Standard in-place quick sort is not stable in general.
    
- The displayed implementation can use \(O(n)\) call-stack space in the worst case.
    

# 7. Heap sort

Heap sort uses a binary heap, a complete binary tree satisfying the heap-order property.

For ascending order, a common approach is to build a max-heap, where the largest element is at the root.

The main steps are:

1. Build a max-heap from the array.
    
2. Swap the root (maximum) with the final element of the current heap.
    
3. Reduce the heap size by one.
    
4. Restore the heap property by sifting the root downward.
    
5. Repeat until the array is sorted.
    

## 7.1 Dry run

Sort:

```
[4, 10, 3, 5, 1]
```

Step 1: Build a max-heap

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

Step 2: Move the maximum to the end

Swap `10` and `1`, then restore the heap property in the reduced heap:

```
[5, 4, 3, 1, 10]
```

Step 3: Repeat

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

These are illustrative intermediate states; the exact states depend on the heap-building procedure and the sequence of sift-down operations.

## 7.2 Python implementation

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

### Understanding the child indexes

For a zero-indexed array representation of a binary heap, the node at index \(i\) has:

\[ \text{Left child}=2i+1 \]

\[ \text{Right child}=2i+2 \]

The implementation's `heapify()` operation ensures that the parent is at least as large as its children, restoring the max-heap property.

## 7.3 Complexity

|Case|Time complexity|
|---|---|
|Best|\(\Theta(n\log n)\)|
|Average|\(\Theta(n\log n)\)|
|Worst|\(\Theta(n\log n)\)|
|Auxiliary space for this recursive implementation|\(O(\log n)\) worst-case call stack|

The sorting algorithm is in-place, but this particular recursive `heapify()` implementation uses additional call-stack memory. An iterative heapify implementation can achieve \(O(1)\) auxiliary space.

Exam traps:

- Building the heap using bottom-up heap construction takes \(O(n)\), not \(O(n\log n)\).
    
- Repeatedly extracting the maximum takes \(O(n\log n)\) overall.
    
- Heap sort is not stable in its standard form.
    
- A max-heap is typically used for ascending heap sort; a min-heap is commonly used for descending heap sort, with the corresponding extraction arrangement.
    

# 8. Compare all six sorting algorithms

This summary table is especially important for your DSSSB exam.

|Algorithm|Best time|Average time|Worst time|Auxiliary space|Stable?|
|---|---|---|---|---|---|
|Bubble sort, optimized|\(O(n)\)|\(O(n^2)\)|\(O(n^2)\)|\(O(1)\)|Yes|
|Selection sort|\(O(n^2)\)|\(O(n^2)\)|\(O(n^2)\)|\(O(1)\)|No, generally|
|Insertion sort|\(O(n)\)|\(O(n^2)\)|\(O(n^2)\)|\(O(1)\)|Yes|
|Merge sort|\(O(n\log n)\)|\(O(n\log n)\)|\(O(n\log n)\)|\(O(n)\) for arrays|Yes, with stable merge|
|Quick sort|\(O(n\log n)\)|\(O(n\log n)\)|\(O(n^2)\)|\(O(\log n)\) average; \(O(n)\) worst for recursive stack|No, generally|
|Heap sort|\(O(n\log n)\)|\(O(n\log n)\)|\(O(n\log n)\)|\(O(1)\) for iterative in-place implementation|No, generally|

These are the standard complexities for the common implementations studied above. Quick sort's expected/average behavior assumes reasonably balanced partitions or suitable pivot selection; the exact space use depends on its implementation.

### 8.1 Stability: a common MCQ topic

A sorting algorithm is stable if equal-key items keep their original relative order.

|Algorithm|Standard stability|
|---|---|
|Bubble sort|Stable|
|Selection sort|Unstable in general|
|Insertion sort|Stable|
|Merge sort|Stable when ties are merged consistently|
|Quick sort|Unstable in general|
|Heap sort|Unstable in general|

Easy memory trick: Among these six standard implementations, remember Bubble, Insertion, Merge as the stable algorithms.

### 8.2 In-place vs extra memory

|Algorithm|Typical memory property|
|---|---|
|Bubble sort|In-place|
|Selection sort|In-place|
|Insertion sort|In-place|
|Merge sort|Needs auxiliary storage for conventional array sorting|
|Quick sort|Typically in-place partitioning, but recursion needs stack memory|
|Heap sort|In-place with iterative heap operations|

### 8.3 Which algorithm should you choose?

|Situation|Good candidate|
|---|---|
|Very small or nearly sorted data|Insertion sort|
|Simple teaching example of adjacent swaps|Bubble sort|
|Minimize the number of swaps in a basic comparison sort|Selection sort|
|Guaranteed \(O(n\log n)\) time and stability|Merge sort|
|Often fast in practice with in-place partitioning|Quick sort|
|Guaranteed \(O(n\log n)\) time with in-place sorting|Heap sort|

These are general algorithmic trade-offs, not universal performance guarantees for every implementation or hardware environment.

## 10. Final revision sheet

|Algorithm|Main idea|Best to worst time|Stable?|
|---|---|---|---|
|Bubble|Swap adjacent out-of-order elements|\(O(n)\) to \(O(n^2)\), optimized|Yes|
|Selection|Select minimum and place it|\(O(n^2)\) in all cases|No, generally|
|Insertion|Insert next element in the sorted prefix|\(O(n)\) to \(O(n^2)\)|Yes|
|Merge|Divide, sort, merge|\(O(n\log n)\) in all cases|Yes, with stable merge|
|Quick|Partition around pivot|\(O(n\log n)\) average; \(O(n^2)\) worst|No, generally|
|Heap|Build heap, extract root repeatedly|\(O(n\log n)\) in all cases|No, generally|

Highest-priority topics for DSSSB: Memorize the six algorithms' best/average/worst complexities, the stable versus unstable distinction, the difference between merge sort and quick sort, and why heap construction is \(O(n)\) while complete heap sort is \(O(n\log n)\).