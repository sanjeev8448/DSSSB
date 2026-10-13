# PANDAS SERIES — DSSSB TGT COMPUTER SCIENCE

A **Pandas Series** is a one-dimensional labeled data structure that can store integers, strings, floating-point numbers, Boolean values, and other data types. Each value is associated with an index label.

**Important exam areas:**

- Creating a Series from arrays, lists, dictionaries, and scalars
    
- Indexing and selection
    
- Slicing with `loc` and `iloc`
    
- `head()` and `tail()`
    
- Arithmetic operations and index alignment
    
- Mathematical methods and missing values
    

## 1. Importing Pandas and NumPy

```
import pandas as pd
import numpy as np
```

- `pd` is the conventional alias for Pandas.
    
- `np` is the conventional alias for NumPy.
    

## 2. Creating a Series

### A. From a NumPy array

```
import pandas as pd
import numpy as np

arr = np.array([10, 20, 30, 40])
s = pd.Series(arr)

print(s)
```

Output:

```
0    10
1    20
2    30
3    40
dtype: int64
```

Pandas assigns default index labels starting from `0`.

### B. From a Python list

```
s = pd.Series([5, 15, 25, 35])
print(s)
```

Output:

```
0     5
1    15
2    25
3    35
dtype: int64
```

### C. Using a custom index

```
s = pd.Series(
    np.array([80, 90, 70]),
    index=["A", "B", "C"]
)

print(s)
```

Output:

```
A    80
B    90
C    70
dtype: int64
```

**Exam points:**

- The array or list supplies the values.
    
- The `index` parameter supplies the labels.
    
- The number of index labels must match the number of values when constructing a Series from an array or list.
    

### D. From a dictionary

Dictionary keys become index labels, and dictionary values become Series values.

```
data = {
    "Amit": 85,
    "Riya": 92,
    "Neha": 78
}

s = pd.Series(data)
print(s)
```

Output:

```
Amit    85
Riya    92
Neha    78
dtype: int64
```

Selecting a value using a dictionary key:

```
print(s["Riya"])
```

Output:

```
92
```

#### Specifying a different index

```
s = pd.Series(data, index=["Neha", "Amit"])
print(s)
```

Output:

```
Neha    78
Amit    85
dtype: int64
```

Only the requested keys are selected, in the specified order.

**Important exam trap: Missing dictionary keys**

If the requested index contains a key that does not exist in the dictionary, Pandas assigns `NaN`.

```
s = pd.Series(
    {"A": 10, "B": 20},
    index=["A", "C"]
)

print(s)
```

Output:

```
A    10.0
C     NaN
dtype: float64
```

`NaN` represents a missing value. The integer values may be converted to floating-point values to accommodate the missing value.

### E. From a scalar

A scalar is a single value, such as `10`, `5.5`, or `"Hello"`.

Without an explicit index:

```
s = pd.Series(100)
print(s)
```

Output:

```
0    100
dtype: int64
```

With a custom index:

```
s = pd.Series(7, index=["A", "B", "C"])
print(s)
```

Output:

```
A    7
B    7
C    7
dtype: int64
```

The scalar value is repeated for every supplied index label.

|Creation method|How values are obtained|
|---|---|
|Array or list|Values come from the array or list|
|Dictionary|Keys become labels; values become data|
|Scalar with an index|Scalar is repeated for the supplied labels|

## 3. Indexing in a Series

Indexing means accessing an element using its label or position.

```
s = pd.Series(
    [10, 20, 30, 40],
    index=["a", "b", "c", "d"]
)
```

The Series contains these label-value pairs:

|Index label|Value|
|---|---|
|`a`|10|
|`b`|20|
|`c`|30|
|`d`|40|

### A. Label-based indexing

```
print(s["b"])
print(s.loc["c"])
```

Output:

```
20
30
```

- `s["b"]` accesses the value associated with label `b`.
    
- `.loc[]` explicitly selects using index labels.
    

### B. Position-based indexing

```
print(s.iloc[0])
print(s.iloc[2])
```

Output:

```
10
30
```

`iloc` uses zero-based integer positions:

- Position `0` → first element
    
- Position `2` → third element
    

### C. Negative positions

```
print(s.iloc[-1])
```

Output:

```
40
```

Position `-1` selects the last element.

**Exam trap:** A Series may have integer index labels that differ from its positions. Use `.loc[label]` for labels and `.iloc[position]` for positions to avoid ambiguity.

## 4. Selecting Series Elements

### A. Select one element

```
print(s["a"])
```

Output:

```
10
```

### B. Select multiple labels

```
print(s.loc[["a", "c"]])
```

Output:

```
a    10
c    30
dtype: int64
```

The inner list specifies multiple labels.

### C. Select multiple positions

```
print(s.iloc[[0, 2]])
```

Output:

```
a    10
c    30
dtype: int64
```

### D. Boolean selection

```
print(s[s > 20])
```

Output:

```
c    30
d    40
dtype: int64
```

Only values greater than `20` are selected.

### E. Selection using multiple conditions

```
print(s[(s >= 20) & (s <= 30)])
```

Output:

```
b    20
c    30
dtype: int64
```

For element-wise conditions in Pandas:

- `&` means AND.
    
- `|` means OR.
    
- Put each condition inside parentheses.
    

Example using OR:

```
print(s[(s < 20) | (s > 30)])
```

Output:

```
a    10
d    40
dtype: int64
```

## 5. Slicing a Series

Slicing selects a range of elements.

```
s = pd.Series(
    [10, 20, 30, 40, 50],
    index=["a", "b", "c", "d", "e"]
)
```

### A. Position-based slicing with `iloc`

```
print(s.iloc[1:4])
```

Output:

```
b    20
c    30
d    40
dtype: int64
```

The starting position is included, but the stopping position is excluded.

Therefore, `iloc[1:4]` selects positions `1`, `2`, and `3`.

Other examples:

```
s.iloc[:3]     # First three elements
s.iloc[2:]     # From the third element to the end
s.iloc[::2]    # Every second element
s.iloc[::-1]   # Reverse order
```

### B. Label-based slicing with `loc`

```
print(s.loc["b":"d"])
```

Output:

```
b    20
c    30
d    40
dtype: int64
```

With `.loc`, both the start and end labels are included when they exist in the index.

|Expression|Result|
|---|---|
|`s.iloc[1:4]`|Positions 1, 2, 3|
|`s.loc["b":"d"]`|Labels b, c, d|
|`s.iloc[:2]`|First two elements|
|`s.iloc[-2:]`|Last two elements|

### C. Slicing with a default index

```
s = pd.Series([11, 22, 33, 44, 55])
print(s.iloc[1:4])
```

Result: `22, 33, 44`.

**Exam tip:** Prefer `.iloc` for position-based slicing and `.loc` for label-based slicing.

## 6. The `head()` Method

`head()` returns the first five elements by default.

```
s = pd.Series([10, 20, 30, 40, 50, 60, 70])
print(s.head())
```

Output:

```
0    10
1    20
2    30
3    40
4    50
dtype: int64
```

Specifying the number of elements:

```
print(s.head(3))
```

Output:

```
0    10
1    20
2    30
dtype: int64
```

Other examples:

```
s.head(1)  # First element
s.head(4)  # First four elements
s.head(0)  # Empty Series
```

`head(n)` returns up to the first `n` elements. If `n` exceeds the Series length, all available elements are returned.

## 7. The `tail()` Method

`tail()` returns the last five elements by default.

```
s = pd.Series([10, 20, 30, 40, 50, 60, 70])
print(s.tail())
```

Output:

```
2    30
3    40
4    50
5    60
6    70
dtype: int64
```

Specifying the number of elements:

```
print(s.tail(3))
```

Output:

```
4    50
5    60
6    70
dtype: int64
```

Other examples:

```
s.tail(1)  # Last element
s.tail(4)  # Last four elements
s.tail(0)  # Empty Series
```

### `head()` vs. `tail()`

|Feature|`head(n)`|`tail(n)`|
|---|---|---|
|Purpose|First `n` elements|Last `n` elements|
|Default|5 elements|5 elements|
|Example|`s.head(2)`|`s.tail(2)`|
|Order|Original order|Original order among selected elements|

For `[10, 20, 30, 40, 50]`:

- `s.head(2)` → `[10, 20]`
    
- `s.tail(2)` → `[40, 50]`
    

## 8. Mathematical Operations on a Series

Pandas supports arithmetic operations on every element. Operations between two Series align values by their index labels.

### A. Scalar arithmetic

```
s = pd.Series([10, 20, 30])

print(s + 5)
print(s - 5)
print(s * 2)
print(s / 10)
```

Output:

```
0    15
1    25
2    35
dtype: int64

0     5
1    15
2    25
dtype: int64

0    20
1    40
2    60
dtype: int64

0    1.0
1    2.0
2    3.0
dtype: float64
```

A scalar operation is applied to every element. Division commonly produces floating-point values.

### B. Operations between two Series

```
s1 = pd.Series([10, 20, 30])
s2 = pd.Series([1, 2, 3])

print(s1 + s2)
```

Output:

```
0    11
1    22
2    33
dtype: int64
```

With matching default indexes, corresponding elements are added.

### C. Operations align by index labels

This is a particularly important exam concept.

```
s1 = pd.Series([10, 20], index=["a", "b"])
s2 = pd.Series([1, 2], index=["b", "a"])

print(s1 + s2)
```

Output:

```
a    12
b    21
dtype: int64
```

Explanation:

- Label `a`: `10 + 2 = 12`
    
- Label `b`: `20 + 1 = 21`
    

Pandas aligns by index labels, not simply by the order in which values appear.

### D. Arithmetic with unmatched indexes

```
s1 = pd.Series([10, 20], index=["a", "b"])
s2 = pd.Series([1, 2], index=["b", "c"])

print(s1 + s2)
```

Output:

```
a     NaN
b    21.0
c     NaN
dtype: float64
```

Only label `b` occurs in both Series, so those values can be added. Labels `a` and `c` have no matching value in the other Series, producing `NaN`.

**Exam trap:** Pandas does not automatically add values by position when the index labels differ. It aligns the labels and produces missing values where an alignment partner is absent.

## 9. Mathematical Methods

Pandas provides built-in methods for calculations.

```
s = pd.Series([10, 20, 30, 40])

print(s.sum())
print(s.mean())
print(s.median())
print(s.max())
print(s.min())
print(s.count())
```

Output:

```
100
25.0
25.0
40
10
4
```

|Method|Purpose|
|---|---|
|`sum()`|Sum of values|
|`mean()`|Arithmetic mean|
|`median()`|Middle value after sorting|
|`max()`|Maximum value|
|`min()`|Minimum value|
|`count()`|Number of non-missing values|
|`std()`|Standard deviation|
|`var()`|Variance|
|`abs()`|Absolute value of each element|
|`round(n)`|Round values to `n` decimal places|

### `size` vs. `count()`

- `size` counts all elements, including missing values.
    
- `count()` counts only non-missing values.
    

```
s = pd.Series([10, 20, None])

print(s.size)   # 3
print(s.count())  # 2
print(s.sum())  # 30.0
```

Pandas skips missing values in many statistical calculations by default.

## 10. Quick Revision Sheet

|Concept|Remember|
|---|---|
|Create a Series|`pd.Series(data)`|
|Array/list|Values come from the array or list|
|Dictionary|Keys become index labels|
|Scalar with index|Scalar repeats for each label|
|Label-based indexing|`loc`|
|Position-based indexing|`iloc`|
|Positional slicing|Stop position is excluded|
|Label slicing|End label is included when present|
|First elements|`head()` — first five by default|
|Last elements|`tail()` — last five by default|
|Scalar arithmetic|Applied element-wise|
|Series arithmetic|Aligns by index labels|
|Missing value|`NaN`|
|Total elements|`size`|
|Non-missing elements|`count()`|

## 11. Important Exam Traps

1. A Series is **one-dimensional** and has index labels.
    
2. Dictionary keys become index labels; dictionary values become data.
    
3. A scalar supplied with multiple index labels is repeated.
    
4. `.loc` selects by label; `.iloc` selects by integer position.
    
5. `.iloc[1:4]` includes positions 1, 2, and 3—not 4.
    
6. `.loc["b":"d"]` includes the end label `d` when present.
    
7. `head()` and `tail()` return five elements by default.
    
8. Series arithmetic aligns values by labels, not merely by position.
    
9. Missing values may cause integer data to be represented as floating-point data.
    
10. `size` includes missing entries, whereas `count()` excludes them.