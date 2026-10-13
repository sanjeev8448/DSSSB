# Python Programming: Data Types and Mutability

## 1. Overview of Python Data Types

Python is dynamically typed: you do not need to declare a variable's type explicitly. The type is determined by the object assigned to it.

### Example

```
a = 10
b = 3.14
c = 2 + 3j
d = True
e = "Python"
f = [1, 2, 3]
g = (1, 2, 3)
h = {1, 2, 3}
i = {"name": "Amit", "age": 25}
j = None

print(type(a))
print(type(b))
print(type(c))
print(type(d))
print(type(e))
print(type(f))
print(type(g))
print(type(h))
print(type(i))
print(type(j))
```

### Output

```
<class 'int'>
<class 'float'>
<class 'complex'>
<class 'bool'>
<class 'str'>
<class 'list'>
<class 'tuple'>
<class 'set'>
<class 'dict'>
<class 'NoneType'>
```

### Data Types and Mutability

|Data type|Example|Mutable?|
|---|---|---|
|`int`|`10`|No|
|`float`|`3.14`|No|
|`complex`|`2+3j`|No|
|`bool`|`True`|No|
|`str`|`"Hello"`|No|
|`list`|`[1, 2, 3]`|Yes|
|`tuple`|`(1, 2, 3)`|No|
|`set`|`{1, 2, 3}`|Yes|
|`dict`|`{"a": 1}`|Yes|
|`NoneType`|`None`|No|

---

## 2. Integer — `int`

An integer represents a whole number, positive, negative or zero, without a fractional part.

```
a = 10
b = -25
c = 0

print(type(a))
print(10 + 5)
print(10 // 3)
print(10 % 3)
```

Output:

```
<class 'int'>
15
3
1
```

### Important Points

- Python integers can grow beyond the fixed-width integer limits of common C integer types, subject to available memory.
    
- `//` performs floor division.
    
- `%` returns the remainder according to Python's modulo rules.
    

### Exam Trap: Negative Floor Division

```
print(7 // 2)
print(-7 // 2)
```

Output:

```
3
-4
```

Python rounds floor division down toward negative infinity, not toward zero.

---

## 3. Floating-Point — `float`

A `float` represents a floating-point number, commonly used for fractional values.

```
x = 3.14
y = 5.0
z = 1.5e2

print(type(x))
print(type(y))
print(z)
print(10 / 2)
```

Output:

```
<class 'float'>
<class 'float'>
150.0
5.0
```

Notice that `5.0` is a float even though its numerical value is a whole number. In Python, `/` returns a float for ordinary numeric division.

### Floating-Point Precision

Some decimal fractions cannot be represented exactly in binary floating-point.

```
print(0.1 + 0.2)
print(0.1 + 0.2 == 0.3)
```

Typical output:

```
0.30000000000000004
False
```

This is a precision issue, not a Python arithmetic bug.

**Exam trap:** `type(5)` is `int`, whereas `type(5.0)` is `float`.

---

## 4. Complex — `complex`

A complex number has a real part and an imaginary part. Python uses `j` to represent the imaginary unit.

Formula:

(z = a + bj)

Here, (a) is the real part and (b) is the imaginary coefficient.

```
z = 2 + 3j

print(z)
print(z.real)
print(z.imag)
print(type(z))
print((2 + 3j) + (1 + 2j))
```

Output:

```
(2+3j)
2.0
3.0
<class 'complex'>
(3+5j)
```

### Key Points

- Use `j`, not `i`, in Python complex literals.
    
- `.real` and `.imag` return floating-point values for ordinary complex numbers.
    
- Complex numbers are immutable.
    
- Complex numbers cannot be directly ordered using `<` or `>`.
    

For example:

```
print(2 + 3j < 4 + 5j)
```

This raises a `TypeError`.

---

## 5. Boolean — `bool`

The Boolean type represents two truth values:

- `True`
    
- `False`
    

The names are case-sensitive. `true` and `false` are not Python Boolean literals.

```
a = 10 > 5
b = 10 == 5

print(a)
print(b)
print(type(a))
print(int(True))
print(int(False))
```

Output:

```
True
False
<class 'bool'>
1
0
```

In Python, `bool` is a subclass of `int`.

Therefore:

```
print(True + True)
print(False + 10)
```

Output:

```
2
10
```

**Exam trap:** `True` and `False` are Boolean values, but they can participate in numeric operations because of their relationship with integers.

---

## 6. String — `str`

A string is an immutable sequence of Unicode characters. Strings can be written using single quotes, double quotes or triple quotes.

```
s1 = 'Hello'
s2 = "Python"
s3 = """This is
a multiline string"""

print(s1)
print(s2)
print(s3)
print(s1[0])
print(s1[-1])
print(s1[1:4])
```

Output:

```
Hello
Python
This is
a multiline string
H
o
ell
```

### A. String Indexing and Slicing

For `s = "PYTHON"`:

|Expression|Result|Meaning|
|---|---|---|
|`s[0]`|`'P'`|First character|
|`s[-1]`|`'N'`|Last character|
|`s[1:4]`|`'YTH'`|Index 1 through 3|
|`s[:3]`|`'PYT'`|First three characters|
|`s[::-1]`|`'NOHTYP'`|Reversed string|

### B. Strings Are Immutable

```
s = "Python"
s[0] = "J"
```

This raises a `TypeError` because individual string characters cannot be changed in place.

Instead, create a new string:

```
s = "Python"
s = "J" + s[1:]
print(s)
```

Output:

```
Jython
```

### C. Useful String Methods

```
s = "  Hello Python  "

print(s.strip())
print(s.lower())
print(s.upper())
print("hello".replace("h", "H"))
print("a,b,c".split(","))
print("-".join(["a", "b", "c"]))
```

Output:

```
Hello Python
  hello python  
  HELLO PYTHON  
Hello
['a', 'b', 'c']
a-b-c
```

### Exam Traps

- `strip()` removes leading and trailing whitespace; it does not remove whitespace from the middle.
    
- `split()` produces a list.
    
- `join()` combines strings from an iterable.
    
- `s[1:4]` excludes index `4`.
    
- Methods such as `upper()` return a new string; they do not modify the original string.
    

---

## 7. List — `list`

A list is an ordered, mutable collection. It allows duplicate values and can contain different data types.

```
items = [10, 20, 30, 20, "Python"]

print(items)
print(items[0])
print(items[-1])

items[1] = 99
items.append(40)

print(items)
```

Output:

```
[10, 20, 30, 20, 'Python']
10
Python
[10, 99, 30, 20, 'Python', 40]
```

### Common List Methods

|Method|Purpose|Example|
|---|---|---|
|`append(x)`|Adds one item at the end|`a.append(5)`|
|`extend(iterable)`|Adds items from an iterable|`a.extend([5, 6])`|
|`insert(i, x)`|Inserts at an index|`a.insert(1, 5)`|
|`remove(x)`|Removes the first matching value|`a.remove(5)`|
|`pop(i)`|Removes and returns an item|`a.pop()`|
|`sort()`|Sorts the list in place|`a.sort()`|
|`reverse()`|Reverses the list in place|`a.reverse()`|
|`clear()`|Removes all items|`a.clear()`|

### A. `append()` vs `extend()`

```
a = [1, 2]
a.append([3, 4])
print(a)

b = [1, 2]
b.extend([3, 4])
print(b)
```

Output:

```
[1, 2, [3, 4]]
[1, 2, 3, 4]
```

`append()` adds its argument as one item. `extend()` adds the elements from the iterable individually.

### B. Aliasing and Mutability

```
a = [1, 2]
b = a

a.append(3)

print(a)
print(b)
```

Output:

```
[1, 2, 3]
[1, 2, 3]
```

Both names refer to the same list object.

### C. Important Exam Trap: `sort()`

`a.sort()` sorts the list in place and returns `None`.

```
a = [3, 1, 2]
result = a.sort()

print(a)
print(result)
```

Output:

```
[1, 2, 3]
None
```

---

## 8. Tuple — `tuple`

A tuple is an ordered, immutable collection. It allows duplicate elements and can hold different data types.

```
t = (10, 20, 30, 20)

print(t[0])
print(t[-1])
print(t.count(20))
print(t.index(30))
```

Output:

```
10
20
2
2
```

### A. Creating a Tuple with One Element

This is a common MCQ trap.

```
a = (5)
b = (5,)

print(type(a))
print(type(b))
```

Output:

```
<class 'int'>
<class 'tuple'>
```

The comma creates the one-element tuple, not the parentheses alone.

### B. Tuple Immutability

```
t = (10, 20, 30)
t[0] = 99
```

This raises a `TypeError`.

However, a tuple can contain a mutable object. The tuple's references cannot be reassigned, but the contained mutable object can still be modified.

```
t = ([1, 2], 3)
t[0].append(99)

print(t)
```

Output:

```
([1, 2, 99], 3)
```

The tuple remains immutable, while its contained list changes.

---

## 9. Set — `set`

A set is a mutable collection of unique, hashable elements. Sets do not provide indexing or slicing.

```
s = {1, 2, 2, 3, 3, 3}

print(s)
print(len(s))

s.add(4)
s.discard(2)

print(s)
```

The initial set contains three unique values. The exact printed order of set elements is not guaranteed.

### A. Set Operations

```
a = {1, 2, 3}
b = {3, 4, 5}

print(a | b)
print(a & b)
print(a - b)
print(a ^ b)
```

Output, with element order possibly varying:

```
{1, 2, 3, 4, 5}
{3}
{1, 2}
{1, 2, 4, 5}
```

|Operator|Operation|Meaning|
|---|---|---|
|`\|`|Union|Elements in either set|
|`&`|Intersection|Elements in both sets|
|`-`|Difference|Elements in the first but not the second|
|`^`|Symmetric difference|Elements in either set, but not both|

### B. Empty Set Trap

```
a = {}
b = set()

print(type(a))
print(type(b))
```

Output:

```
<class 'dict'>
<class 'set'>
```

Important points:

- `{}` creates an empty dictionary.
    
- `set()` creates an empty set.
    
- Set elements must be hashable. Lists and dictionaries cannot be set elements.
    
- Sets are not indexed; `s[0]` raises a `TypeError`.
    

---

## 10. Dictionary — `dict`

A dictionary stores information as key-value pairs. It is mutable and preserves insertion order in modern Python.

```
student = {
    "name": "Amit",
    "age": 25,
    "marks": 85
}

print(student["name"])
print(student["marks"])

student["age"] = 26
student["city"] = "Delhi"

print(student)
```

Output:

```
Amit
85
{'name': 'Amit', 'age': 26, 'marks': 85, 'city': 'Delhi'}
```

### Dictionary Rules

- Keys must be unique and hashable.
    
- Values can be of different types and can be duplicated.
    
- Assigning an existing key updates its value.
    
- Accessing a missing key using `d[key]` raises a `KeyError`.
    
- `d.get(key)` returns `None` by default when the key is missing, unless a different default is supplied.
    

```
d = {"a": 10, "b": 20}

print(d["a"])
print(d.get("c"))
print(d.get("c", 0))

d["a"] = 99
print(d)
```

Output:

```
10
None
0
{'a': 99, 'b': 20}
```

### Dictionary Methods

|Method|Purpose|
|---|---|
|`keys()`|Returns a view of the keys|
|`values()`|Returns a view of the values|
|`items()`|Returns a view of key-value pairs|
|`get(key)`|Retrieves a value safely if a key is absent|
|`pop(key)`|Removes a key and returns its value|
|`update()`|Adds or updates entries|
|`clear()`|Removes all entries|

**Exam trap:** In `for x in d`, Python iterates over the dictionary's keys by default, not its values.

---

## 11. `None` and `NoneType`

`None` represents the absence of a value. Its type is `NoneType`.

```
x = None

print(x)
print(type(x))
print(x is None)
```

Output:

```
None
<class 'NoneType'>
True
```

### Important Rules

- `None` is not the same as `0`, `False` or an empty string.
    
- Use `is None` to check whether a value is `None`.
    
- A function with no explicit `return` statement returns `None`.
    

```
def greet():
    print("Hello")

result = greet()
print(result)
```

Output:

```
Hello
None
```

`print()` itself also returns `None`.

---

## 12. Mutable vs Immutable — Most Important Topic

### 12.1 What Is Mutability?

- **Mutable:** An object can be changed after it is created.
    
- **Immutable:** An object cannot be changed after it is created. An operation that appears to change it instead produces another object or value.
    

For DSSSB, memorize this table.

|Data type|Mutable or immutable?|Can elements be changed in place?|
|---|---|---|
|`int`|Immutable|No|
|`float`|Immutable|No|
|`complex`|Immutable|No|
|`bool`|Immutable|No|
|`str`|Immutable|No|
|`list`|Mutable|Yes|
|`tuple`|Immutable|No reassignment of tuple elements|
|`set`|Mutable|Yes|
|`dict`|Mutable|Yes|
|`NoneType`|Immutable|No|

### 12.2 Example: Immutable Integer

```
x = 10
y = x

x = 20

print(x)
print(y)
```

Output:

```
20
10
```

Initially, `x` and `y` refer to the integer object representing `10`. The assignment `x = 20` rebinds `x`; it does not change the integer object `10`.

### 12.3 Example: Mutable List

```
x = [10, 20]
y = x

x.append(30)

print(x)
print(y)
```

Output:

```
[10, 20, 30]
[10, 20, 30]
```

Both names refer to the same list. The `append()` method modifies that list, so both names reflect the change.

### 12.4 Reassignment vs Modification

These two operations are not the same.

#### Reassignment

```
x = [1, 2]
y = x

x = [3, 4]

print(x)
print(y)
```

Output:

```
[3, 4]
[1, 2]
```

The name `x` is rebound to a new list. `y` still refers to the original list.

#### Modification

```
x = [1, 2]
y = x

x.append(3)

print(x)
print(y)
```

Output:

```
[1, 2, 3]
[1, 2, 3]
```

The original list is modified, so both names show the updated list.

### 12.5 The `id()` Function

`id()` returns an object's identity during its lifetime. It can help illustrate whether two names refer to the same object.

```
a = [1, 2]
b = a

print(a is b)

b = [1, 2]

print(a == b)
print(a is b)
```

Output:

```
True
True
False
```

Remember:

- `==` checks whether values are equal.
    
- `is` checks whether two references point to the same object.
    
- Equal values do not necessarily mean identical objects.
    

Do not rely on `id()` values themselves being a particular number.

### 12.6 Common Exam Traps

**Trap 1: Strings are immutable**

`s.upper()` returns an uppercase string; it does not modify `s` in place.

**Trap 2: Tuples can contain mutable objects**

A tuple containing a list can have that list modified, even though the tuple's elements cannot be reassigned.

**Trap 3: Dictionary keys and set elements**

They must be hashable. A list cannot be used as a dictionary key or a set element, but a tuple of hashable elements can.

**Trap 4:** `**bool**` **is a subclass of** `**int**`

`isinstance(True, int)` returns `True`.

**Trap 5: Empty braces**

`{}` creates a dictionary, not a set. Use `set()` for an empty set.

---

## Quick Revision Sheet

|Question|Answer|
|---|---|
|Which type stores whole numbers?|`int`|
|Which type stores decimal numbers?|`float`|
|Which type uses `j`?|`complex`|
|Is `bool` a subclass of `int`?|Yes|
|Is a string mutable?|No|
|Is a list mutable?|Yes|
|Is a tuple mutable?|No|
|Does a set allow duplicates?|No|
|Does a dictionary store key-value pairs?|Yes|
|What is the type of `None`?|`NoneType`|
|What checks object identity?|`is`|
|What checks value equality?|`==`|

### DSSSB Study Priority

Make sure you can trace outputs involving list aliasing, tuple immutability, set duplicates, dictionary access, Boolean arithmetic, and `is` versus `==`. These concepts combine naturally into exam-style MCQs.