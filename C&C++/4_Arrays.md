# C Programming: Arrays — Complete DSSSB TGT Computer Science Notes

Arrays are an important C programming topic for understanding output-based questions, index calculations, loops, searching, sorting, and memory layout.

We will cover all five areas step by step:

1. One-dimensional arrays (1D)
    
2. Two-dimensional arrays (2D)
    
3. Searching algorithms
    
4. Sorting algorithms
    
5. Array operations
    

## 1. What is an array?

An array is a collection of elements of the same data type stored in contiguous memory locations. Each element is accessed using an index.

For example:

```
int marks[5] = {70, 80, 65, 90, 75};
```

Conceptually, the array looks like this:

## 70

Index 0

## 80

Index 1

## 65

Index 2

## 90

Index 3

## 75

Index 4

Array name: `marks` · Number of elements: 5 · Valid indexes: 0–4

In C, array indexing starts from 0, not 1.

- `marks[0]` gives `70`.
    
- `marks[2]` gives `65`.
    
- `marks[4]` gives `75`.
    

Accessing `marks[5]` is out of bounds because the last valid index is `4`. C does not automatically check array bounds, so such access causes undefined behavior.

## 2. One-dimensional array (1D)

A 1D array stores elements in a single sequence.

### A. Declaration

Syntax:

```
data_type array_name[size];
```

Examples:

```
int numbers[5];
float prices[10];
char letters[4];
```

The declaration `int numbers[5];` reserves space for five `int` elements. Their values are not automatically initialized when this is an ordinary local array.

### B. Initialization

```

#include <stdio.h>

int main(void)
{
    int a[5] = {10, 20, 30, 40, 50};

    printf("%d\n", a[0]);
    printf("%d\n", a[3]);

    return 0;
}
```

Output

```
10
40
```

Other initialization forms:

```
int a[5] = {1, 2};       // Remaining elements become 0
int b[] = {10, 20, 30};  // Size inferred as 3
int c[5] = {0};          // All elements initialized to 0
```

### C. Traversing an array

Traversing means visiting each element, usually with a loop.

```

#include <stdio.h>

int main(void)
{
    int a[5] = {10, 20, 30, 40, 50};

    for (int i = 0; i < 5; i++)
    {
        printf("%d ", a[i]);
    }

    return 0;
}
```

Output

```
10 20 30 40 50
```

How it works:

|Iteration|`i`|Expression|Printed value|
|---|---|---|---|
|1|0|`a[0]`|10|
|2|1|`a[1]`|20|
|3|2|`a[2]`|30|
|4|3|`a[3]`|40|
|5|4|`a[4]`|50|

The condition `i < 5` prevents the loop from accessing index `5`.

### D. Taking input into an array

```

#include <stdio.h>

int main(void)
{
    int a[5];

    for (int i = 0; i < 5; i++)
    {
        scanf("%d", &a[i]);
    }

    for (int i = 0; i < 5; i++)
    {
        printf("%d ", a[i]);
    }

    return 0;
}
```

If the input is:

```
5 10 15 20 25
```

The output is:

```
5 10 15 20 25
```

Notice `&a[i]`: `scanf()` needs the address of each integer so it can store the entered value there.

### E. Sum and average of an array

```

#include <stdio.h>

int main(void)
{
    int a[5] = {10, 20, 30, 40, 50};
    int sum = 0;

    for (int i = 0; i < 5; i++)
    {
        sum += a[i];
    }

    double average = (double)sum / 5;

    printf("Sum = %d\n", sum);
    printf("Average = %.2f\n", average);

    return 0;
}
```

Output

```
Sum = 150
Average = 30.00
```

The cast `(double)sum` ensures floating-point division. Without it, `sum / 5` would use integer division because both operands would be integers.

## 3. Two-dimensional array (2D)

A 2D array organizes elements into rows and columns. It is commonly used to represent a matrix or table.

Example: a matrix with 2 rows and 3 columns.

## 10

[0][0]

## 20

[0][1]

## 30

[0][2]

## 40

[1][0]

## 50

[1][1]

## 60

[1][2]

2 rows × 3 columns

### A. Declaration and initialization

Syntax:

```
data_type array_name[rows][columns];
```

Example:

```
int matrix[2][3] = {
    {10, 20, 30},
    {40, 50, 60}
};
```

Access individual elements using two indexes:

- `matrix[0][0]` → `10`
    
- `matrix[0][2]` → `30`
    
- `matrix[1][0]` → `40`
    
- `matrix[1][2]` → `60`
    

The first index is the row, and the second index is the column. Both indexes start at zero.

### B. Printing a 2D array using nested loops

```

#include <stdio.h>

int main(void)
{
    int a[2][3] = {
        {10, 20, 30},
        {40, 50, 60}
    };

    for (int i = 0; i < 2; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            printf("%d ", a[i][j]);
        }
        printf("\n");
    }

    return 0;
}
```

Output

```
10 20 30
40 50 60
```

Understand the nested loops:

- The outer loop (`i`) selects the row.
    
- The inner loop (`j`) visits every column in that row.
    
- Once all columns are printed, `printf("\n")` moves to the next line.
    

### C. Row-wise and column-wise traversal

Consider:

```
int a[2][3] = {{1, 2, 3}, {4, 5, 6}};
```

Row-wise order: `1 2 3 4 5 6`

Column-wise order: `1 4 2 5 3 6`

C stores a normal 2D array in row-major order: all elements of the first row are followed by all elements of the second row, and so on.

### D. Sum of all elements

```

#include <stdio.h>

int main(void)
{
    int a[2][3] = {{1, 2, 3}, {4, 5, 6}};
    int sum = 0;

    for (int i = 0; i < 2; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            sum += a[i][j];
        }
    }

    printf("Sum = %d\n", sum);
    return 0;
}
```

Output

```
Sum = 21
```

### E. Matrix addition

Two matrices can be added element by element if they have the same dimensions.

```

#include <stdio.h>

int main(void)
{
    int a[2][2] = {{1, 2}, {3, 4}};
    int b[2][2] = {{5, 6}, {7, 8}};
    int c[2][2];

    for (int i = 0; i < 2; i++)
    {
        for (int j = 0; j < 2; j++)
        {
            c[i][j] = a[i][j] + b[i][j];
        }
    }

    for (int i = 0; i < 2; i++)
    {
        for (int j = 0; j < 2; j++)
        {
            printf("%d ", c[i][j]);
        }
        printf("\n");
    }

    return 0;
}
```

Output

```
6 8
10 12
```

### F. Memory address calculation — exam concept

For a 2D array, C uses row-major storage. If the array has \(C\) columns, the linear element offset of `a[i][j]`, measured in elements from the beginning of the array, is:

Offset in elements: (i*C+j)



Actual address: (B+(i*C+j)* W
Where:
- (B) = base address of the array
- (C) = number of columns
- (W) = size of each element in bytes

Total elements: rows × columns

C uses row-major storage.

Valid indexes for a[3][4]: rows 0–2, columns 0–3.

So it is the tenth element when counting from one, or offset 9 when counting from zero.

Common exam traps

- `a[2][3]` has 2 rows and 3 columns only when these numbers are the declared dimensions; valid indexes are rows `0–1`, columns `0–2`.
    
- `int a[3][4]` has 12 elements, not 7.
    
- `a[i][j]` is not the same element as `a[j][i]`.
    
- A 2D array's elements are stored in row-major order in C.
    

## 4. Searching algorithms

Searching means finding whether a target value exists in an array and, if it does, locating its index.

The two fundamental algorithms are:

- Linear search
    
- Binary search
    

### A. Linear search

Linear search checks elements one by one until it finds the target or reaches the end.

It works on both sorted and unsorted arrays.

Example: find `30` in `{10, 20, 30, 40, 50}`.

Search trace for target = 30

## 10

Index 0

Check 10 — not found

## 20

Index 1

Check 20 — not found

## 30

Index 2

Check 30 — found!

```

#include <stdio.h>

int main(void)
{
    int a[] = {10, 20, 30, 40, 50};
    int n = 5;
    int target = 30;
    int found = -1;

    for (int i = 0; i < n; i++)
    {
        if (a[i] == target)
        {
            found = i;
            break;
        }
    }

    if (found != -1)
        printf("Found at index %d\n", found);
    else
        printf("Not found\n");

    return 0;
}
```

Output

```
Found at index 2
```

The variable `found` starts at `-1`, meaning no matching index has been recorded. Once a match occurs, the index is saved and `break` ends the loop.

Time complexity:

- Best case: \(O(1)\) — the first element matches.
    
- Average case: \(O(n)\) — typically several elements must be checked.
    
- Worst case: \(O(n)\) — the target is last or absent.
    

Here, \(n\) is the number of elements.

### B. Binary search

Binary search repeatedly halves the search interval. The array must be sorted for the standard binary search algorithm to work correctly.

Example: search for `40` in `{10, 20, 30, 40, 50, 60, 70}`.

1. Middle value is `40`.
    
2. The target matches immediately, so the search ends.
    

A different target illustrates the narrowing process: searching for `60` first compares against `40`, then discards the left half and searches the right half.

```

#include <stdio.h>

int main(void)
{
    int a[] = {10, 20, 30, 40, 50, 60, 70};
    int n = 7;
    int target = 60;
    int low = 0, high = n - 1;
    int found = -1;

    while (low <= high)
    {
        int mid = low + (high - low) / 2;

        if (a[mid] == target)
        {
            found = mid;
            break;
        }
        else if (a[mid] < target)
        {
            low = mid + 1;
        }
        else
        {
            high = mid - 1;
        }
    }

    printf("Index = %d\n", found);
    return 0;
}
```

Output

```
Index = 5
```

Why `low = mid + 1`? If the middle value is smaller than the target, the target—if present—must be to the right.

Why `high = mid - 1`? If the middle value is larger than the target, the target must be to the left.

Using `low + (high - low) / 2` avoids a potential integer overflow in the common expression `(low + high) / 2`.

Time complexity:

- Best case: \(O(1)\)
    
- Worst case: \(O(\log n)\)
    

### Linear vs binary search

|Feature|Linear search|Binary search|
|---|---|---|
|Requires sorted array?|No|Yes|
|Method|Check one by one|Halve search interval|
|Worst-case time|\(O(n)\)|\(O(\log n)\)|
|Best suited for|Small or unsorted arrays|Sorted arrays with many elements|

DSSSB tip: If a question asks which search is faster for a large sorted array, binary search is usually the expected answer.

## 5. Sorting algorithms

Sorting means arranging array elements in a particular order, usually ascending or descending.

For DSSSB, focus on the working steps, output, and time complexity of these common algorithms:

1. Bubble sort
    
2. Selection sort
    
3. Insertion sort
    

### A. Bubble sort

Bubble sort repeatedly compares adjacent elements and swaps them if they are in the wrong order.

Example: sort `{5, 3, 8, 1}` in ascending order.

Pass 1

## 5

## 3

## 8

## 1

Compare 5 and 3 → swap: 3, 5, 8, 1

Compare 5 and 8 → no swap

Compare 8 and 1 → swap: 3, 5, 1, 8

Pass 2

## 3

## 5

## 1

## 8

After further adjacent comparisons, the array becomes 3, 1, 5, 8.

Continue passes until the array is sorted: 1, 3, 5, 8.

```

#include <stdio.h>

int main(void)
{
    int a[] = {5, 3, 8, 1};
    int n = 4;

    for (int i = 0; i < n - 1; i++)
    {
        for (int j = 0; j < n - 1 - i; j++)
        {
            if (a[j] > a[j + 1])
            {
                int temp = a[j];
                a[j] = a[j + 1];
                a[j + 1] = temp;
            }
        }
    }

    for (int i = 0; i < n; i++)
        printf("%d ", a[i]);

    return 0;
}
```

Output

```
1 3 5 8
```

Why does the inner loop use `n - 1 - i`? After each pass, the largest remaining element reaches its correct position at the end, so that portion no longer needs comparison.

Complexity:

- Average and worst case: \(O(n^2)\)
    
- Best case: \(O(n)\) for an optimized version that stops when a pass makes no swaps; the basic version above still performs \(O(n^2)\) comparisons.
    
- Standard bubble sort is stable when equal elements are not swapped.
    

### B. Selection sort

Selection sort finds the smallest element in the unsorted portion and swaps it into the next correct position.

Example: `{29, 10, 14, 37, 13}`

- Pass 1: smallest is `10`; swap with `29` → `{10, 29, 14, 37, 13}`
    
- Pass 2: smallest in the remaining part is `13`; swap with `29` → `{10, 13, 14, 37, 29}`
    
- Pass 3: smallest is `14`; it is already in place.
    
- Pass 4: smallest remaining is `29`; swap with `37`.
    

Final array: `{10, 13, 14, 29, 37}`.

```

#include <stdio.h>

int main(void)
{
    int a[] = {29, 10, 14, 37, 13};
    int n = 5;

    for (int i = 0; i < n - 1; i++)
    {
        int minIndex = i;

        for (int j = i + 1; j < n; j++)
        {
            if (a[j] < a[minIndex])
                minIndex = j;
        }

        int temp = a[i];
        a[i] = a[minIndex];
        a[minIndex] = temp;
    }

    for (int i = 0; i < n; i++)
        printf("%d ", a[i]);

    return 0;
}
```

Output

```
10 13 14 29 37
```

Complexity: Best, average, and worst cases are all \(O(n^2)\) for the standard algorithm. Selection sort generally makes fewer swaps than bubble sort, but its standard implementation is not stable.

### C. Insertion sort

Insertion sort builds a sorted section from left to right. Each new element is inserted into its correct position among the previously processed elements.

Think of arranging playing cards in your hand.

Example: `{5, 3, 4, 1}`

- Start with `5` as the sorted portion.
    
- Insert `3` before `5` → `{3, 5, 4, 1}`.
    
- Insert `4` between `3` and `5` → `{3, 4, 5, 1}`.
    
- Insert `1` at the beginning → `{1, 3, 4, 5}`.
    

```

#include <stdio.h>

int main(void)
{
    int a[] = {5, 3, 4, 1};
    int n = 4;

    for (int i = 1; i < n; i++)
    {
        int key = a[i];
        int j = i - 1;

        while (j >= 0 && a[j] > key)
        {
            a[j + 1] = a[j];
            j--;
        }

        a[j + 1] = key;
    }

    for (int i = 0; i < n; i++)
        printf("%d ", a[i]);

    return 0;
}
```

Output

```
1 3 4 5
```

Important detail: `key` stores the element being inserted. The `while` loop shifts larger elements to the right, and `a[j + 1] = key` places the element into the resulting gap.

Complexity:

- Best case: \(O(n)\), when already sorted.
    
- Average and worst case: \(O(n^2)\).
    
- Insertion sort is stable when implemented as above because it shifts only elements strictly greater than `key`.
    

### Sorting algorithms: revision table

|Algorithm|Main idea|Best case|Average/worst case|
|---|---|---|---|
|Bubble sort|Swap adjacent out-of-order elements|\(O(n)\)*|\(O(n^2)\)|
|Selection sort|Select minimum and place it next|\(O(n^2)\)|\(O(n^2)\)|
|Insertion sort|Insert each element into sorted portion|\(O(n)\)|\(O(n^2)\)|

*Bubble sort's \(O(n)\) best case requires the early-stop optimization; the code above is not optimized.

## 6. Array operations

Common array operations include traversal, insertion, deletion, updating, searching, and merging.

### A. Traversal

Traversal means visiting each element.

```
for (int i = 0; i < n; i++)
    printf("%d ", a[i]);
```

Time complexity: \(O(n)\).

### B. Insertion

Inserting into the middle of an array usually requires shifting elements to the right. The array must have enough allocated capacity for the new element.

Suppose the array is `{10, 20, 40, 50}` and you want to insert `30` at index `2`.

Before insertion

10

20

40

50

Shift 50 and 40 one position to the right.

After insertion at index 2

10

20

30

40

50

```

#include <stdio.h>

int main(void)
{
    int a[10] = {10, 20, 40, 50};
    int n = 4;
    int position = 2;
    int value = 30;

    // Check that capacity and position are valid
    if (n < 10 && position >= 0 && position <= n)
    {
        for (int i = n; i > position; i--)
            a[i] = a[i - 1];

        a[position] = value;
        n++;
    }

    for (int i = 0; i < n; i++)
        printf("%d ", a[i]);

    return 0;
}
```

Output

```
10 20 30 40 50
```

For insertion at index `position`, shift elements from right to left, starting at `n - 1` and moving toward `position`. The new value is then placed at `a[position]`.

Time complexity: \(O(n)\) in the worst case, because elements may need to be shifted.

### C. Deletion

Deletion removes an element at a specified index. The elements to its right are shifted left to fill the gap.

Example: delete the element at index `1` from `{10, 20, 30, 40, 50}`.

```

#include <stdio.h>

int main(void)
{
    int a[5] = {10, 20, 30, 40, 50};
    int n = 5;
    int position = 1;

    if (position >= 0 && position < n)
    {
        for (int i = position; i < n - 1; i++)
            a[i] = a[i + 1];

        n--;
    }

    for (int i = 0; i < n; i++)
        printf("%d ", a[i]);

    return 0;
}
```

Output

```
10 30 40 50
```

The logical array size becomes `4`. The old value may still physically remain in the final array slot, but it is no longer part of the logical array.

Time complexity: \(O(n)\) in the worst case.

### D. Updating an element

Updating means replacing an existing element's value.

```
int a[] = {10, 20, 30, 40};
a[2] = 99;
```

The array becomes `{10, 20, 99, 40}`.

Time complexity: \(O(1)\) for direct access by index.

### E. Merging two arrays

Merging means combining the elements of two arrays into one array. This example appends the second array to the first; it does not sort the result.

```

#include <stdio.h>

int main(void)
{
    int a[] = {1, 2, 3};
    int b[] = {4, 5};
    int c[5];

    for (int i = 0; i < 3; i++)
        c[i] = a[i];

    for (int i = 0; i < 2; i++)
        c[3 + i] = b[i];

    for (int i = 0; i < 5; i++)
        printf("%d ", c[i]);

    return 0;
}
```

Output

```
1 2 3 4 5
```

For arrays of lengths \(m\) and \(n\), simple concatenation takes \(O(m+n)\) time and requires an output array of at least \(m+n\) elements.

## 7. Array operation complexity chart

| Operation                 | Typical time complexity               |
| ------------------------- | ------------------------------------- |
| Access element by index   | \(O(1)\)                              |
| Update element by index   | \(O(1)\)                              |
| Traverse all elements     | \(O(n)\)                              |
| Linear search             | \(O(n)\) worst case                   |
| Binary search             | \(O(log n)\) worst case, sorted array |
| Insert at arbitrary index | \(O(n)\) worst case                   |
| Delete at arbitrary index | \(O(n)\) worst case                   |
| Bubble sort               | \(O(n^2)\) average/worst              |
| Selection sort            | \(O(n^2)\)                            |
| Insertion sort            | \(O(n^2)\) average/worst              |
