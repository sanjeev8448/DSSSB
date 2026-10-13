# Searching Algorithms: Linear Search and Binary Search

## 1. Linear Search

Linear search, also called **sequential search**, examines elements one by one from the beginning until the target is found or the collection ends.

### 1.1 How Linear Search Works

Suppose we have the following array:

```
A = [10, 25, 30, 45, 50]
Target = 45
```

The search proceeds sequentially:

|Comparison|Element|Index|Result|
|---|---|---|---|
|1|10|0|Not found|
|2|25|1|Not found|
|3|30|2|Not found|
|4|45|3|Found|

The algorithm stops as soon as the target is found. Therefore, `45` is found at index `3` after four comparisons.

### 1.2 Python Implementation

```
def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i

    return -1


arr = [10, 25, 30, 45, 50]

print(linear_search(arr, 45))
print(linear_search(arr, 99))
```

**Output:**

```
3
-1
```

Here, `-1` means the target was not found. It is the convention used by this implementation.

### 1.3 Algorithm Steps

1. Start at index `0`.
    
2. Compare the current element with the target.
    
3. If they are equal, return the index.
    
4. Otherwise, move to the next element.
    
5. If all elements have been examined, return `-1`.
    

### 1.4 Complexity of Linear Search

Let `n` be the number of elements.

|Case|Number of comparisons|Time complexity|
|---|---|---|
|Best case|1|Θ(1)|
|Average case, successful search|Approximately (n + 1) / 2|Θ(n)|
|Worst case|Up to n|Θ(n)|
|Auxiliary space|Constant|Θ(1)|

**Why is the best case O(1)?**

If the target is the first element, only one comparison is required.

**Why is the worst case O(n)?**

If the target is the last element or is absent, the algorithm may examine every element.

**Exam trap:** Linear search works on both sorted and unsorted collections.

---

## 2. Binary Search

Binary search finds a target by repeatedly dividing the search interval in half.

**Requirement:** The collection must be sorted in the order expected by the algorithm. The standard implementation below assumes ascending order.

### 2.1 How Binary Search Works

Consider this sorted array:

```
A = [10, 20, 30, 40, 50, 60, 70]
Target = 60
```

Initially:

```
low = 0
high = 6
```

Calculate the middle index:

```
mid = (low + high) // 2
```

#### Step 1

```
mid = (0 + 6) // 2
mid = 3
```

The middle element is `40`.

Since `60 > 40`, discard the left half, including index `3`.

Update:

```
low = mid + 1
low = 4
```

#### Step 2

Now:

```
low = 4
high = 6
```

Calculate the middle index again:

```
mid = (4 + 6) // 2
mid = 5
```

The middle element is `60`. The target is found at index `5`.

**Key concept:** Binary search eliminates approximately half of the remaining search interval with each comparison. It does not check every element individually.

### 2.2 Python Implementation

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


arr = [10, 20, 30, 40, 50, 60, 70]

print(binary_search(arr, 60))
print(binary_search(arr, 25))
```

**Output:**

```
5
-1
```

### 2.3 Understanding the Conditions

|Condition|Meaning|Action|
|---|---|---|
|`arr[mid] == target`|Target found|Return `mid`|
|`arr[mid] < target`|Target may be on the right|Set `low = mid + 1`|
|`arr[mid] > target`|Target may be on the left|Set `high = mid - 1`|
|`low > high`|Search interval is empty|Return `-1`|

### 2.4 Why Use `while low <= high`?

The current search interval includes both `low` and `high`.

- When `low == high`, one candidate element remains and must be checked.
    
- When `low > high`, the interval is empty, so the target cannot be found within it.
    

**Exam trap:** Using `while low < high` with this exact implementation can leave the last remaining element unchecked.

### 2.5 Complexity of Binary Search

|Case|Time complexity|Explanation|
|---|---|---|
|Best case|Θ(1)|Target is at the first midpoint|
|Average case|Θ(log n)|Search interval repeatedly halves|
|Worst case|Θ(log n)|Repeated halving continues until the target is found or the interval is exhausted|
|Iterative auxiliary space|Θ(1)|Only a fixed number of variables are used|
|Recursive auxiliary space|Θ(log n)|Recursive calls use stack frames|

These complexities describe the search itself, assuming the data is already sorted and efficient random access is available. If sorting is required first, its cost must also be included when analyzing the complete task.

---

## 3. Linear Search vs Binary Search

This comparison is an important exam topic.

|Feature|Linear Search|Binary Search|
|---|---|---|
|Method|Checks items one by one|Repeatedly halves the search interval|
|Requires sorted data?|No|Yes, for the standard algorithm|
|Best-case time|O(1)|O(1)|
|Average-case time|O(n)|O(log n)|
|Worst-case time|O(n)|O(log n)|
|Iterative auxiliary space|O(1)|O(1)|
|Suitable for|Small or unsorted collections|Large, sorted, random-access collections|

Here, `n` is the number of elements.

### 3.1 Comparing the Number of Checks

Suppose `n = 1,024`.

- Linear search may require up to **1,024 comparisons**.
    
- Binary search requires at most approximately **11 midpoint checks** to find a target or establish that it is absent.
    

Why approximately 11?

```
log₂(1024) = 10
```

Because each comparison approximately halves the remaining interval, the number of comparisons grows logarithmically. The exact number depends on the target and the search interval.

### 3.2 When Should You Use Each Algorithm?

**Choose linear search when:**

- The data is unsorted.
    
- The collection is small.
    
- A single sequential scan is sufficient.
    

**Choose binary search when:**

- The data is sorted.
    
- Efficient indexed access is available.
    
- The collection is large enough for logarithmic search to be beneficial.
    

**Exam trap:** Binary search on an unsorted list does not reliably return the correct result because its left/right decisions depend on sorted order.

---

## 4. Common Output-Based Exam Traps

### Trap 1: Binary Search Midpoint

```
low = 2
high = 8

mid = (low + high) // 2
print(mid)
```

**Output:**

```
5
```

Python's `//` operator performs floor division.

### Trap 2: Target Absent in Binary Search

```
arr = [10, 20, 30, 40, 50]

print(binary_search(arr, 35))
```

**Output:**

```
-1
```

The search interval eventually becomes empty, meaning `low > high`.

### Trap 3: Duplicate Values

Suppose:

```
arr = [10, 20, 20, 20, 30]
```

The standard binary search implementation can return a matching index for `20`, but it does not guarantee that the first occurrence is returned.

If the question asks for the first occurrence, the algorithm must continue searching toward the left after finding a match.

### Trap 4: Data Structure Matters

Binary search is efficient on arrays and Python lists because they support constant-time indexing.

A standard linked list does not provide constant-time access to its middle element. Therefore, the usual binary-search time complexity does not directly apply to a linked list.

---

## 5. Bonus: Finding the First Occurrence with Binary Search

When duplicate elements exist, standard binary search may return any matching index encountered.

To find the **first occurrence**, record the match and continue searching to its left.

### Python Implementation

```
def first_occurrence(arr, target):
    low = 0
    high = len(arr) - 1
    result = -1

    while low <= high:
        mid = (low + high) // 2

        if arr[mid] == target:
            result = mid
            high = mid - 1
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1

    return result


arr = [10, 20, 20, 20, 30]

print(first_occurrence(arr, 20))
print(first_occurrence(arr, 25))
```

**Output:**

```
1
-1
```

The worst-case time complexity remains **O(log n)** because each iteration reduces the search interval by approximately half.

This is an extension of the standard algorithm and helps distinguish between finding any occurrence and finding the first occurrence.

---

## 6. Final Revision Sheet

|Topic|Must Remember|
|---|---|
|Linear search|Checks elements sequentially|
|Binary search|Repeatedly halves the search interval|
|Linear search prerequisite|No sorted-data requirement|
|Binary search prerequisite|Sorted sequence|
|Linear best case|Θ(1)|
|Linear average and worst cases|Θ(n)|
|Binary best case|Θ(1)|
|Binary average and worst cases|Θ(log n)|
|Binary-search midpoint|`(low + high) // 2`|
|Empty search interval|`low > high`|
|Not-found convention in these examples|Return `-1`|
|Iterative auxiliary space|Θ(1) for both algorithms|

### Highest-Priority Exam Concepts

1. Trace the midpoint calculation correctly.
    
2. Update `low` and `high` correctly.
    
3. Compare best-, average-, and worst-case complexities.
    
4. Remember that binary search requires sorted data.
    
5. Understand the difference between finding any duplicate occurrence and finding the first occurrence.
    

**Next topic: Sorting algorithms** — bubble sort, selection sort, insertion sort, merge sort, and quick sort, including algorithms, dry runs, Python implementations, complexity tables, and exam-style MCQs.