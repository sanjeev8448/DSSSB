# Python Lists — DSSSB TGT Computer Science

## Key Fact

A Python list is an ordered, mutable collection. It supports duplicate values, indexing, slicing, and elements of different data types.

## 1. List Creation

A list is created using square brackets `[]`, with elements separated by commas.

### Example

```
numbers = [10, 20, 30, 40]
names = ["Amit", "Ravi", "Neha"]
mixed = [10, "Python", 3.14, True]
empty = []

print(numbers)
print(names)
print(mixed)
print(empty)
print(type(numbers))
```

**Output:**

```
[10, 20, 30, 40]
['Amit', 'Ravi', 'Neha']
[10, 'Python', 3.14, True]
[]
<class 'list'>
```

### Different Ways to Create Lists

```
a = list((1, 2, 3))
b = list("CAT")
c = list(range(1, 5))
d = [0] * 4

print(a)
print(b)
print(c)
print(d)
```

**Output:**

```
[1, 2, 3]
['C', 'A', 'T']
[1, 2, 3, 4]
[0, 0, 0, 0]
```

Remember:

- `list()` can convert an iterable into a list.
    
- `list("CAT")` produces one element per character.
    
- `range(1, 5)` excludes `5`.
    
- `[0] * 4` creates a list containing four references to the immutable integer `0`.
    

### Nested Lists

A list can contain other lists.

```
matrix = [
    [1, 2, 3],
    [4, 5, 6]
]

print(matrix)
print(matrix[0])
print(matrix[1][2])
```

**Output:**

```
[[1, 2, 3], [4, 5, 6]]
[1, 2, 3]
6
```

**Exam trap:** `matrix[1][2]` means the element at row index `1`, column index `2`. Both indexes start at `0`.

---

## 2. List Indexing

Indexing accesses an individual element of a list.

Consider:

```
a = [10, 20, 30, 40, 50]
```

### List Index Map

|Element|Positive index|Negative index|
|---|---|---|
|`10`|`0`|`-5`|
|`20`|`1`|`-4`|
|`30`|`2`|`-3`|
|`40`|`3`|`-2`|
|`50`|`4`|`-1`|

The first index is positive `0`; the last index is negative `-1`.

### Example

```
a = [10, 20, 30, 40, 50]

print(a[0])
print(a[2])
print(a[-1])
print(a[-2])
```

**Output:**

```
10
30
50
40
```

### Updating an Element

Lists are mutable, so an element can be replaced by assigning a new value to its index.

```
a = [10, 20, 30]
a[1] = 99

print(a)
```

**Output:**

```
[10, 99, 30]
```

### Index Out of Range

```
a = [10, 20, 30]
print(a[3])
```

This raises an `IndexError`. The valid positive indexes are `0`, `1`, and `2`.

**Exam trap:** Accessing an element using an invalid index raises an error; slicing beyond the end usually does not.

---

## 3. List Slicing

Slicing extracts a portion of a list.

**Syntax:**

```
list[start:stop:step]
```

The `start` index is included, the `stop` index is excluded, and `step` specifies the interval.

For `a = [10, 20, 30, 40, 50, 60]`:

|Expression|Result|
|---|---|
|`a[1:4]`|`[20, 30, 40]`|
|`a[:3]`|`[10, 20, 30]`|
|`a[3:]`|`[40, 50, 60]`|
|`a[::2]`|`[10, 30, 50]`|
|`a[::-1]`|`[60, 50, 40, 30, 20, 10]`|
|`a[-4:-1]`|`[30, 40, 50]`|

### Example

```
a = [10, 20, 30, 40, 50, 60]

print(a[1:4])
print(a[:3])
print(a[::2])
print(a[::-1])
print(a[1:100])
```

**Output:**

```
[20, 30, 40]
[10, 20, 30]
[10, 30, 50]
[60, 50, 40, 30, 20, 10]
[20, 30, 40, 50, 60]
```

### Slicing vs Indexing

|Operation|Returns|Invalid boundary behaviour|
|---|---|---|
|`a[10]`|One element|Raises `IndexError` if the index is invalid|
|`a[1:10]`|A list|Clamps the slice boundary to the available range|

### Important: A Slice Creates a New List

```
a = [1, 2, 3]
b = a[:]

b.append(4)

print(a)
print(b)
print(a is b)
```

**Output:**

```
[1, 2, 3]
[1, 2, 3, 4]
False
```

`a[:]` creates a shallow copy of the list. The outer list is new, but nested mutable objects inside a shallow copy may still be shared.

---

## 4. `append()`

`append()` adds one object to the end of a list.

**Syntax:**

```
list.append(element)
```

### Example

```
a = [10, 20, 30]

a.append(40)
print(a)

a.append([50, 60])
print(a)
```

**Output:**

```
[10, 20, 30, 40]
[10, 20, 30, 40, [50, 60]]
```

Notice that `[50, 60]` becomes one nested element, not two separate elements.

The `append()` method modifies the existing list and returns `None`.

```
a = [1, 2]
result = a.append(3)

print(a)
print(result)
```

**Output:**

```
[1, 2, 3]
None
```

**Exam trap:** `append()` changes the list; it does not return the updated list.

---

## 5. `extend()`

`extend()` adds each element from an iterable to the end of the existing list.

**Syntax:**

```
list.extend(iterable)
```

### Example

```
a = [10, 20]

a.extend([30, 40])
print(a)

a.extend("XY")
print(a)
```

**Output:**

```
[10, 20, 30, 40]
[10, 20, 30, 40, 'X', 'Y']
```

When extending with a string, Python iterates through its characters.

### `append()` vs `extend()` — Extremely Important

```
a = [1, 2]
a.append([3, 4])
print(a)

b = [1, 2]
b.extend([3, 4])
print(b)
```

**Output:**

```
[1, 2, [3, 4]]
[1, 2, 3, 4]
```

|Feature|`append(x)`|`extend(iterable)`|
|---|---|---|
|Adds|One object|Each element of the iterable|
|Changes original list?|Yes|Yes|
|Return value|`None`|`None`|
|Example with `[3, 4]`|Adds one nested list|Adds `3` and `4` separately|

**Remember for MCQs:** `append()` = one item; `extend()` = multiple items from an iterable.

---

## 6. `insert()`

`insert()` inserts an element at a specified index.

**Syntax:**

```
list.insert(index, element)
```

### Example

```
a = [10, 20, 40]

a.insert(2, 30)
print(a)

a.insert(0, 5)
print(a)
```

**Output:**

```
[10, 20, 30, 40]
[5, 10, 20, 30, 40]
```

- `insert(2, 30)` inserts `30` before the element currently at index `2`.
    
- `insert(0, 5)` inserts `5` at the beginning.
    

### Inserting at an Index Outside the List

Python adjusts an out-of-range insertion position rather than raising an `IndexError`.

```
a = [10, 20, 30]

a.insert(100, 40)
print(a)

a.insert(-100, 5)
print(a)
```

**Output:**

```
[10, 20, 30, 40]
[5, 10, 20, 30, 40]
```

A very large positive index inserts at the end; a very negative index inserts at the beginning.

**Exam trap:** `insert()` modifies the original list and returns `None`.

---

## 7. `remove()`

`remove(value)` removes the first occurrence of a specified value.

```
a = [10, 20, 30, 20, 40]

a.remove(20)
print(a)
```

**Output:**

```
[10, 30, 20, 40]
```

Only the first `20` is removed.

### What if the Value Is Absent?

```
a = [10, 20, 30]
a.remove(99)
```

This raises a `ValueError` because `99` is not in the list.

### `remove()` vs `pop()`

This distinction is frequently useful for output-based questions.

|Feature|`remove(x)`|`pop(i)`|
|---|---|---|
|Removes by|Value|Index|
|Return value|`None`|Removed element|
|Default target|First matching value|Last element if no index is supplied|
|If target is missing/invalid|`ValueError` if value is absent|`IndexError` if index is invalid|

### Example

```
a = [10, 20, 30, 20]

a.remove(20)
print(a)

removed = a.pop(1)
print(removed)
print(a)
```

**Output:**

```
[10, 30, 20]
30
[10, 20]
```

---

## 8. `pop()`

`pop()` removes an element from a list and returns the removed element.

**Syntax:**

```
list.pop(index)
```

The index is optional. If omitted, the last element is removed.

### Example

```
a = [10, 20, 30, 40]

x = a.pop()
print(x)
print(a)

y = a.pop(1)
print(y)
print(a)
```

**Output:**

```
40
[10, 20, 30]
20
[10, 30]
```

### Important Cases

```
a = [10, 20, 30]

print(a.pop(0))
print(a.pop(-1))
print(a)
```

**Output:**

```
10
30
[20]
```

- `pop(0)` removes the first element.
    
- `pop(-1)` removes the last element.
    
- `pop()` on an empty list raises `IndexError`.
    

**Exam trap:** `remove(20)` searches for the value `20`; `pop(20)` attempts to remove the element at index `20`.

---

## 9. `sort()`

`sort()` sorts a list in place, meaning the existing list is modified.

By default, it sorts in ascending order.

```
a = [40, 10, 30, 20]

a.sort()
print(a)

a.sort(reverse=True)
print(a)
```

**Output:**

```
[10, 20, 30, 40]
[40, 30, 20, 10]
```

### Sorting Strings

```
names = ["Ravi", "Amit", "Neha"]

names.sort()
print(names)
```

**Output:**

```
['Amit', 'Neha', 'Ravi']
```

Strings are compared lexicographically, using their Unicode values.

### `sort()` vs `sorted()`

This is an important exam distinction.

```
a = [30, 10, 20]

result = a.sort()
print(a)
print(result)

b = [30, 10, 20]
new_list = sorted(b)

print(b)
print(new_list)
```

**Output:**

```
[10, 20, 30]
None
[30, 10, 20]
[10, 20, 30]
```

|Feature|`list.sort()`|`sorted()`|
|---|---|---|
|Changes original list?|Yes|No|
|Returns a new sorted list?|No; returns `None`|Yes|
|Works with|Lists|Any iterable whose elements can be sorted together|

### `sort()` with a Key

You can provide a key function to decide how elements are compared.

```
words = ["banana", "kiwi", "apple", "fig"]

words.sort(key=len)
print(words)
```

**Output:**

```
['fig', 'kiwi', 'apple', 'banana']
```

The words are sorted by length. Python's sort is stable, so items with equal keys preserve their relative order.

**Exam trap:** Sorting a list containing incompatible values, such as integers and strings, can raise a `TypeError` in Python 3.

---

## 10. `reverse()`

`reverse()` reverses the order of elements in the original list. It does not sort the list.

```
a = [10, 30, 20, 40]

a.reverse()
print(a)
```

**Output:**

```
[40, 20, 30, 10]
```

The order is reversed exactly; the values are not arranged numerically.

### `reverse()` vs `sort(reverse=True)`

```
a = [30, 10, 20]

a.reverse()
print(a)

b = [30, 10, 20]
b.sort(reverse=True)
print(b)
```

**Output:**

```
[20, 10, 30]
[30, 20, 10]
```

|Method|Meaning|
|---|---|
|`a.reverse()`|Reverses current element order|
|`a.sort()`|Sorts in ascending order|
|`a.sort(reverse=True)`|Sorts in descending order|
|`sorted(a, reverse=True)`|Returns a new list in descending order|

Like `sort()`, the `reverse()` method modifies the existing list and returns `None`.

---

## 11. Quick Revision Table — All List Methods

|Method|Action|Return value|Common error/trap|
|---|---|---|---|
|`append(x)`|Add one item at end|`None`|A list argument becomes one nested element|
|`extend(it)`|Add iterable's elements|`None`|Strings are extended character by character|
|`insert(i, x)`|Insert at index|`None`|Inserts before the specified index|
|`remove(x)`|Remove first matching value|`None`|`ValueError` if value is absent|
|`pop(i)`|Remove and return item|Removed item|`IndexError` for invalid index|
|`sort()`|Sort in place|`None`|Does not return the sorted list|
|`reverse()`|Reverse in place|`None`|Does not sort the values|
|`sorted(a)`|Return sorted iterable as a list|New list|Does not modify the original list|

## Common List Mistakes

### 1. Assigning the Result of `append()`

```
a = [1, 2]
a = a.append(5)
print(a)
```

Output:

```
None
```

`a` becomes `None` because `append()` returns `None`.

### 2. Confusing Value and Index

- `remove(2)` removes the value `2`.
    
- `pop(2)` removes the item at index `2`.
    

### 3. Assuming `reverse()` Sorts

Reversing `[3, 1, 2]` produces `[2, 1, 3]`, not `[1, 2, 3]`.

### 4. Mutable Aliasing

After `b = a`, modifying a list through `b` also affects `a` because both names reference the same list.

```
a = [1, 2, 3]
b = a

b.append(4)

print(a)
print(b)
```

**Output:**

```
[1, 2, 3, 4]
[1, 2, 3, 4]
```