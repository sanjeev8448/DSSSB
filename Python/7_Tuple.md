# PYTHON TUPLES — DSSSB TGT COMPUTER SCIENCE

## 1. Tuple Creation

Tuples are ordered collections of elements. They are commonly created using parentheses `()` with elements separated by commas.

### Example: Creating tuples

```
t1 = (10, 20, 30)
t2 = ("Python", "Java", "C")
t3 = (10, "Hello", 3.14, True)
t4 = ()

print(t1)
print(t2)
print(t3)
print(t4)
print(type(t1))
print(type(t4))
```

**Output:**

```
(10, 20, 30)
('Python', 'Java', 'C')
(10, 'Hello', 3.14, True)
()
<class 'tuple'>
<class 'tuple'>
```

### A. Tuple without parentheses

Parentheses are often optional. The comma is what makes the comma-separated values a tuple.

```
a = 10, 20, 30

print(a)
print(type(a))
```

**Output:**

```
(10, 20, 30)
<class 'tuple'>
```

### B. Single-element tuple — very important

```
a = (5)
b = (5,)
c = 5,

print(type(a))
print(type(b))
print(type(c))
```

**Output:**

```
<class 'int'>
<class 'tuple'>
<class 'tuple'>
```

**Remember:**

- `(5)` is an integer.
    
- `(5,)` is a tuple.
    
- `5,` is also a tuple.
    

**Exam trap:** The comma, not the parentheses alone, creates a single-element tuple.

### C. Creating a tuple using `tuple()`

```
a = tuple([1, 2, 3])
b = tuple("CAT")
c = tuple(range(1, 5))

print(a)
print(b)
print(c)
```

**Output:**

```
(1, 2, 3)
('C', 'A', 'T')
(1, 2, 3, 4)
```

The `tuple()` constructor converts an iterable into a tuple.

---

## 2. Tuple Indexing

Indexing accesses an individual element by its position. Like lists and strings, tuples use zero-based indexing.

Consider:

```
t = (10, 20, 30, 40, 50)
```

### Tuple index map

|Element|Positive index|Negative index|
|---|---|---|
|`10`|`0`|`-5`|
|`20`|`1`|`-4`|
|`30`|`2`|`-3`|
|`40`|`3`|`-2`|
|`50`|`4`|`-1`|

Positive indexing starts at `0`, while negative indexing starts at `-1` from the end.

### Example

```
t = (10, 20, 30, 40, 50)

print(t[0])
print(t[2])
print(t[-1])
print(t[-2])
```

**Output:**

```
10
30
50
40
```

### Nested tuple indexing

A tuple can contain another tuple.

```
t = (10, 20, (30, 40, 50))

print(t[0])
print(t[2])
print(t[2][1])
```

**Output:**

```
10
(30, 40, 50)
40
```

Here, `t[2][1]` accesses the second element of the nested tuple.

**Exam trap:** Accessing an invalid index, such as `t[5]` for a five-element tuple, raises an `IndexError`.

---

## 3. Tuple Slicing

Slicing extracts a portion of a tuple.

**Syntax:**

```
tuple[start:stop:step]
```

- `start`: Index where slicing begins; included.
    
- `stop`: Index where slicing ends; excluded.
    
- `step`: Interval between selected elements.
    

Consider:

```
t = (10, 20, 30, 40, 50, 60)
```

### Common slicing expressions

|Expression|Result|
|---|---|
|`t[1:4]`|`(20, 30, 40)`|
|`t[:3]`|`(10, 20, 30)`|
|`t[3:]`|`(40, 50, 60)`|
|`t[::2]`|`(10, 30, 50)`|
|`t[::-1]`|`(60, 50, 40, 30, 20, 10)`|
|`t[-4:-1]`|`(30, 40, 50)`|

### Example

```
t = (10, 20, 30, 40, 50, 60)

print(t[1:4])
print(t[:3])
print(t[::2])
print(t[::-1])
print(t[1:100])
```

**Output:**

```
(20, 30, 40)
(10, 20, 30)
(10, 30, 50)
(60, 50, 40, 30, 20, 10)
(20, 30, 40, 50, 60)
```

### Slicing vs. indexing

|Feature|Indexing|Slicing|
|---|---|---|
|Example|`t[2]`|`t[1:4]`|
|Returns|One element|A tuple|
|Invalid position|Raises `IndexError`|Out-of-range boundaries are generally allowed|
|Original tuple|Unchanged|Unchanged|

**Exam trap:** Even when a slice contains just one element, the result is still a tuple.

```
t = (10, 20, 30)

print(t[1])
print(t[1:2])
```

**Output:**

```
20
(20,)
```

---

## 4. Tuple Operations

Tuple operations include concatenation, repetition, membership testing, comparisons, built-in functions, and methods such as `count()` and `index()`.

### 4.1 Concatenation using `+`

The `+` operator joins two tuples and produces a new tuple.

```
a = (1, 2, 3)
b = (4, 5)
c = a + b

print(c)
print(a)
print(b)
```

**Output:**

```
(1, 2, 3, 4, 5)
(1, 2, 3)
(4, 5)
```

The original tuples remain unchanged.

**Exam trap:** Tuple concatenation requires compatible operands. The expression `(1, 2) + [3, 4]` raises a `TypeError` because a tuple cannot be concatenated directly with a list.

### 4.2 Repetition using `*`

The `*` operator repeats the tuple's elements.

```
t = (1, 2)

print(t * 3)
print(t * 0)
```

**Output:**

```
(1, 2, 1, 2, 1, 2)
()
```

Repeating a tuple zero times produces an empty tuple.

### 4.3 Membership operators: `in` and `not in`

```
t = (10, 20, 30, 40)

print(20 in t)
print(50 in t)
print(50 not in t)
```

**Output:**

```
True
False
True
```

- `in` checks whether an element exists in the tuple.
    
- `not in` checks whether an element does not exist.
    

### 4.4 `len()`, `min()`, `max()` and `sum()`

These built-in functions operate on tuples when their elements support the relevant operation.

```
t = (10, 20, 30, 40)

print(len(t))
print(min(t))
print(max(t))
print(sum(t))
```

**Output:**

```
4
10
40
100
```

|Function|Purpose|
|---|---|
|`len(t)`|Returns the number of elements|
|`min(t)`|Returns the smallest element|
|`max(t)`|Returns the largest element|
|`sum(t)`|Adds numeric elements|

**Exam trap:** `len()` counts elements; it does not calculate their numerical total.

### 4.5 The `count()` method

`count(x)` returns the number of times a value appears.

```
t = (10, 20, 10, 30, 10)

print(t.count(10))
print(t.count(20))
print(t.count(99))
```

**Output:**

```
3
1
0
```

If the value is absent, `count()` returns `0`.

### 4.6 The `index()` method

`index(x)` returns the index of the first occurrence of a value.

```
t = (10, 20, 30, 20, 40)

print(t.index(20))
print(t.index(40))
```

**Output:**

```
1
4
```

If the value is absent, `index()` raises a `ValueError`.

|Method|Purpose|If value is absent|
|---|---|---|
|`count(x)`|Counts occurrences|Returns `0`|
|`index(x)`|Finds the first matching index|Raises `ValueError`|

### 4.7 Tuple comparisons

Tuples are compared lexicographically. Python compares elements from left to right and stops at the first unequal pair.

```
print((1, 2, 3) == (1, 2, 3))
print((1, 2, 3) < (1, 3, 0))
print((5, 1) < (5, 2))
```

**Output:**

```
True
True
True
```

For `(1, 2, 3) < (1, 3, 0)`, the first elements are equal, but `2 < 3`, so the first tuple is smaller.

---

## 5. Immutable Nature of Tuples

**Immutability** means that the elements of a tuple cannot be reassigned after the tuple is created.

Unlike lists, tuples do not support changing an element by assigning a new value at an index.

### Example 1: Attempting to modify a tuple

```
t = (10, 20, 30)
t[1] = 99
print(t)
```

This raises a `TypeError` because tuples do not support item assignment.

### Example 2: Reassignment of the variable is allowed

```
t = (10, 20, 30)
t = (40, 50, 60)

print(t)
```

**Output:**

```
(40, 50, 60)
```

Why does this work? The original tuple was not modified. The name `t` was rebound to a different tuple.

**Exam trap:** An immutable object cannot be changed in place, but a variable referring to that object can be assigned a different object.

### Example 3: A tuple containing a list

This is a subtle and frequently misunderstood concept.

```
t = ([10, 20], 30)
t[0].append(99)

print(t)
```

**Output:**

```
([10, 20, 99], 30)
```

The tuple contains a reference to a list. The list can be modified even though the tuple itself is immutable.

However, the following operation is not allowed:

```
t[0] = [1, 2, 3]
```

It attempts to replace a tuple element, so it raises a `TypeError`.

### Example 4: Tuple aliasing

```
a = (10, 20)
b = a

print(a is b)
print(a == b)
```

**Output:**

```
True
True
```

Both names refer to the same tuple object in this example.

- `==` checks value equality.
    
- `is` checks object identity.
    

---

## 6. Tuple vs. List

|Feature|Tuple|List|
|---|---|---|
|Syntax|`(1, 2, 3)`|`[1, 2, 3]`|
|Ordered|Yes|Yes|
|Allows duplicates|Yes|Yes|
|Supports indexing|Yes|Yes|
|Supports slicing|Yes|Yes|
|Elements can be reassigned|No|Yes|
|Can grow or shrink in place|No|Yes|
|Has `append()` method|No|Yes|
|Has `count()` and `index()`|Yes|Yes|

### Can tuples be dictionary keys?

Tuples can be dictionary keys when all their elements are hashable. Lists cannot be dictionary keys because lists are mutable and unhashable.

**Valid example:**

```
d = {
    (1, 2): "valid key"
}

print(d[(1, 2)])
```

**Output:**

```
valid key
```

**Invalid example:**

```
d = {([1, 2], 3): "value"}
```

This raises a `TypeError` because the tuple contains an unhashable list.

---

## 7. Tuple Packing and Unpacking

Tuple packing and unpacking are useful concepts for output-tracing questions.

### 7.1 Packing

Assigning multiple comma-separated values creates a tuple.

```
student = "Amit", 25, 85

print(student)
print(type(student))
```

**Output:**

```
('Amit', 25, 85)
<class 'tuple'>
```

### 7.2 Unpacking

The elements of a tuple can be assigned to multiple variables in one statement.

```
student = ("Amit", 25, 85)

name, age, marks = student

print(name)
print(age)
print(marks)
```

**Output:**

```
Amit
25
85
```

The number of variables must match the number of unpacked elements unless extended unpacking using `*` is used.

### 7.3 Extended unpacking using `*`

```
a, *b = (10, 20, 30, 40)

print(a)
print(b)
```

**Output:**

```
10
[20, 30, 40]
```

Notice that `b` is a **list**, not a tuple.

---

## 8. Final Revision Sheet

|Topic|Must remember|
|---|---|
|Creation|`(1, 2, 3)`|
|Single-element tuple|`(5,)`|
|Indexing|`t[0]`, `t[-1]`|
|Slicing|`t[1:3]` excludes index `3`|
|Concatenation|`t1 + t2`|
|Repetition|`t * 3`|
|Membership|`in`, `not in`|
|Methods|`count()`, `index()`|
|Immutability|Cannot reassign individual tuple elements|
|Packing/unpacking|`a, b = (10, 20)`|
|Dictionary keys|All tuple elements must be hashable|

## Highest-Priority DSSSB Exam Traps

1. `**(5)**` **vs.** `**(5,)**`**:** The former is an integer; the latter is a tuple.
    
2. **Slicing boundaries:** The start index is included, but the stop index is excluded.
    
3. `**count()**` **vs.** `**index()**`**:** `count()` returns `0` for a missing value; `index()` raises `ValueError`.
    
4. **Immutability:** Tuple elements cannot be reassigned, but mutable objects inside a tuple, such as lists, can still be modified.
    
5. **Packing and unpacking:** Multiple comma-separated values form a tuple; `*` extended unpacking collects remaining values into a list.
    
6. **Dictionary keys:** A tuple is a valid dictionary key only when all its elements are hashable.
    
7. **Indexing vs. slicing:** An invalid index raises `IndexError`, while out-of-range slice boundaries are generally allowed.
    
8. **Tuple concatenation:** A tuple cannot be directly concatenated with a list using `+`.