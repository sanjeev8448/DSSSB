# 1. Linear Search

Linear search, also called sequential search, examines elements one by one from the beginning until the target is found or the collection ends.

## 1.1 How linear search works

Suppose we have this array:

```
A = [10, 25, 30, 45, 50]
Target = 45
```

The search proceeds as follows:

### Interactive linear search

Target = 45

### 10

Index 0

### 25

Index 1

### 30

Index 2

### 45

Index 3

### 50

Index 4

Comparison 1: Check `{linearData[linearStep]}` against `45`.

Not a match. Move to the next element.

PreviousNext comparison

The comparisons are:

|Comparison|Element|Result|
|---|---|---|
|1|10|Not found|
|2|25|Not found|
|3|30|Not found|
|4|45|Found at index 3|

The algorithm stops as soon as it finds the target.

## 1.2 Python implementation

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

Output:

```
3
-1
```

Here, `-1` means the target was not found. It is a convention used by this implementation.

### Algorithm steps

1. Start at index `0`.
    
2. Compare the current element with the target.
    
3. If equal, return the index.
    
4. Otherwise, move to the next element.
    
5. If all elements are examined, return `-1`.
    

### Complexity of linear search

Let \(n\) be the number of elements.

|Case|Comparisons|Time complexity|
|---|---|---|
|Best case|1|\(\Theta(1)\)|
|Average case, successful search with target equally likely at any index|\((n+1)/2\)|\(\Theta(n)\)|
|Worst case|Up to \(n\)|\(\Theta(n)\)|
|Auxiliary space|Constant|\(\Theta(1)\)|

Why is the best case \(O(1)\)? If the target is the first element, only one comparison is needed.

Why is the worst case \(O(n)\)? If the target is last or absent, the algorithm may examine every element.

Exam trap: Linear search works on both sorted and unsorted collections.

# 2. Binary Search

Binary search finds a target by repeatedly dividing the search interval in half.

Requirement: The collection must be sorted in the order expected by the algorithm. The standard implementation below assumes ascending order.

## 2.1 How binary search works

Suppose:

```
A = [10, 20, 30, 40, 50, 60, 70]
Target = 60
```

Initially:

\[ low=0,\qquad high=6 \]

Calculate the middle index:

\[ mid=\left\lfloor\frac{low+high}{2}\right\rfloor \]

### Step 1

\[ mid=\left\lfloor\frac{0+6}{2}\right\rfloor=3 \]

The middle element is `40`.

Since \(60>40\), discard the left half, including index 3.

Update:

\[ low=mid+1=4 \]

### Step 2

Now `low = 4`, `high = 6`.

\[ mid=\left\lfloor\frac{4+6}{2}\right\rfloor=5 \]

The middle element is `60`. The target is found at index `5`.

### Interactive binary search

Sorted array · Target = 60

### 10

0

### 20

1

### 30

2

### 40

3

### 50

4

### 60

5

### 70

6

Middle value is 40. The target 60 is greater, so search the right half.

Current range: low = 0, high = 6, mid = 3

PreviousNext step

Notice that binary search does not check `10`, `20`, `30`, and `50` individually. It eliminates half of the remaining search interval with each comparison.

## 2.2 Python implementation

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

Output:

```
5
-1
```

### Understanding the conditions

|Condition|Meaning|Action|
|---|---|---|
|`arr[mid] == target`|Target found|Return `mid`|
|`arr[mid] < target`|Target may be on the right|Set `low = mid + 1`|
|`arr[mid] > target`|Target may be on the left|Set `high = mid - 1`|
|`low > high`|Search interval is empty|Return `-1`|

### Why use `low <= high`?

The current interval includes both `low` and `high`.

When `low == high`, one candidate element remains and must be checked. Once `low > high`, the interval is empty and the target cannot be found within it.

Exam trap: Using `while low < high` with this exact implementation can cause the last remaining element not to be checked.

## 2.3 Complexity of binary search

|Case|Time complexity|Explanation|
|---|---|---|
|Best case|\(\Theta(1)\)|Target is at the first midpoint|
|Average case|\(\Theta(\log n)\)|Search interval repeatedly halves|
|Worst case|\(\Theta(\log n)\)|Repeated halving continues until found or exhausted|
|Auxiliary space, iterative|\(\Theta(1)\)|Only a fixed number of variables|
|Auxiliary space, recursive|\(\Theta(\log n)\)|Recursive calls use stack frames|

Important: These complexities describe the search itself, assuming the data is already sorted and random access is available. If sorting must be performed first, its cost must be included when analyzing the entire task.

# 3. Linear Search vs Binary Search

This comparison is one of the most important parts of the topic.

|Feature|Linear search|Binary search|
|---|---|---|
|Method|Checks items one by one|Repeatedly halves the search interval|
|Requires sorted data?|No|Yes, for the standard algorithm|
|Best-case time|\(O(1)\)|\(O(1)\)|
|Average-case time|\(O(n)\)|\(O(\log n)\)|
|Worst-case time|\(O(n)\)|\(O(\log n)\)|
|Iterative auxiliary space|\(O(1)\)|\(O(1)\)|
|Good choice for|Small or unsorted collections|Large, sorted, random-access collections|

Here, \(n\) is the number of elements. For the iterative implementations shown above, auxiliary space is constant for both algorithms.

### Comparing the number of checks

For \(n=1,024\):

- Linear search may require up to \(1,024\) comparisons.
    
- Binary search requires at most about \(11\) midpoint checks to reduce the range to a single candidate or an empty interval.
    

Why approximately 11?

\[ \log_2(1024)=10 \]

The number of comparisons depends on whether the target is found early and on the exact search interval, but it grows logarithmically for binary search.

### When should you use each algorithm?

Choose linear search when the data is unsorted, the collection is small, or a one-pass scan is sufficient.

Choose binary search when the data is sorted and efficient indexed access is available.

Exam trap: Binary search on an unsorted list does not reliably return the correct result because the algorithm's left/right decision relies on sorted order.

# 4. Common output-based exam traps

### Trap 1: Binary search midpoint

```
low = 2high = 8mid = (low + high) // 2print(mid)
```

Output:

```
5
```

Python's `//` performs floor division.

### Trap 2: Target absent in binary search

```
arr = [10, 20, 30, 40, 50]print(binary_search(arr, 35))
```

Output:

```
-1
```

The interval eventually becomes empty, meaning `low > high`.

### Trap 3: Duplicate values

Suppose:

```
arr = [10, 20, 20, 20, 30]
```

The binary search implementation shown earlier returns a matching index for `20`, but it does not guarantee that the first occurrence is returned.

If the question asks for the first occurrence, the algorithm needs to continue searching toward the left after finding a match.

### Trap 4: Data structure matters

Binary search is efficient on arrays and Python lists because they support constant-time indexing. A standard linked list does not provide constant-time access to the middle element, so the usual binary-search complexity does not directly apply.

# 5. Bonus: Finding the first occurrence with binary search

When duplicate elements are present, the standard binary search may return any matching index encountered. To find the first occurrence, record the match and continue searching to its left.

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

Output:

```
1
-1
```

The same \(O(\log n)\) worst-case time complexity is maintained because each iteration halves the search interval.

This is an extension of the standard syllabus algorithm and is useful for understanding the difference between finding an occurrence and finding the first occurrence.

## Final revision sheet

|Topic|Must remember|
|---|---|
|Linear search|Checks elements sequentially|
|Binary search|Repeatedly halves the search interval|
|Linear search prerequisite|No sorted data requirement|
|Binary search prerequisite|Sorted sequence|
|Linear best case|\(\Theta(1)\)|
|Linear average/worst|\(\Theta(n)\), under the usual assumptions|
|Binary best case|\(\Theta(1)\)|
|Binary average/worst|\(\Theta(\log n)\)|
|Binary-search midpoint|`(low + high) // 2`|
|Search interval empty|`low > high`|
|Not-found convention in these examples|Return `-1`|
|Iterative auxiliary space|\(\Theta(1)\) for both shown algorithms|

Highest-priority exam concepts: Trace the midpoint calculation, update `low` and `high` correctly, compare best and worst cases, and remember the sorted-data requirement for binary search. These are the main foundations for searching-algorithm MCQs.Next topic in your Data Structures syllabus is Sorting: bubble sort, selection sort, insertion sort, merge sort, and quick sort—with algorithms, dry runs, and complexity comparisons.