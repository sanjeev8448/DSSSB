## 1. String indexing

Indexing is used to access an individual character in a string.

Consider:

```
s = "PYTHON"
```

### Positive and negative indexing

![[Pasted image 20261011163504.png]]

- Positive indexing starts at `0`.
    
- Negative indexing starts at `-1` from the end.
    

```
s = "PYTHON"print(s[0])print(s[2])print(s[-1])print(s[-3])
```

Output:

```
P
T
N
H
```

### Index out of range

```
s = "PYTHON"print(s[6])
```

This raises an `IndexError` because valid positive indexes are `0` through `5`.

Exam trap: `s[-1]` accesses the last character, but `s[len(s)]` is out of range.

## 2. String slicing

Slicing extracts a portion of a string.

Syntax:

```
string[start:stop:step]
```

- `start`: index where extraction begins; included.
    
- `stop`: index where extraction ends; excluded.
    
- `step`: interval between selected characters; defaults to `1`.
    

For `s = "PYTHON"`:

|Expression|Result|Explanation|
|---|---|---|
|`s[0:3]`|`"PYT"`|Indexes 0, 1, 2|
|`s[1:4]`|`"YTH"`|Indexes 1, 2, 3|
|`s[:3]`|`"PYT"`|Starts from the beginning|
|`s[3:]`|`"HON"`|Goes to the end|
|`s[::2]`|`"PTO"`|Every second character|
|`s[::-1]`|`"NOHTYP"`|Reverses the string|
|`s[-4:-1]`|`"THO"`|Negative indexes|

```
s = "PYTHON"print(s[1:4])print(s[:3])print(s[3:])print(s[::2])print(s[::-1])
```

Output:

```
YTH
PYT
HON
PTO
NOHTYP
```

### Important slicing traps

Trap 1: The stop index is excluded.

```
print("COMPUTER"[1:5])
```

Output:

```
OMPU
```

Trap 2: Slicing out of range does not normally raise `IndexError`.

```
s = "CAT"print(s[0:100])print(s[100:200])
```

Output:

```
CAT
```

The second result is an empty string.

Trap 3: Negative step reverses traversal.

```
print("ABCDE"[::-1])print("ABCDE"[4:1:-1])
```

Output:

```
EDCBA
EDC
```

In the second expression, traversal begins at index `4` and stops before index `1`.

## 3. String concatenation

Concatenation means joining strings using the `+` operator.

```
first = "Hello"second = "Python"print(first + " " + second)print("A" * 3)
```

Output:

```
Hello Python
AAA
```

The `*` operator repeats a string when multiplied by an integer.

### Common trap: String and integer

```
print("Age: " + 25)
```

This raises a `TypeError` because a string cannot be concatenated directly with an integer using `+`.

Correct version:

```
print("Age: " + str(25))
```

Output:

```
Age: 25
```

Alternatively, use an f-string:

```
age = 25print(f"Age: {age}")
```

## 4. `len()`

The built-in `len()` function returns the number of characters in a string.

```
s = "Python"print(len(s))print(len(""))print(len("Hello World"))
```

Output:

```
6
0
11
```

Spaces count as characters. For ordinary Python strings, `len()` counts Unicode code points, not necessarily user-perceived characters.

Exam trap: The last index is `len(s) - 1`, not `len(s)`.

## 5. `strip()`

`strip()` removes leading and trailing whitespace by default. It does not remove whitespace from the middle.

```
s = "   Hello Python   "print(s.strip())print(s.lstrip())print(s.rstrip())
```

Output:

```
Hello Python
Hello Python   
   Hello Python
```

|Method|What it removes|
|---|---|
|`strip()`|Both ends|
|`lstrip()`|Left/start|
|`rstrip()`|Right/end|

### Removing specific characters

```
s = "***Python***"print(s.strip("*"))
```

Output:

```
Python
```

Important: `strip(chars)` treats `chars` as a set of characters to remove from either end, not as one exact substring.

```
print("xyPythonxy".strip("xy"))
```

Output:

```
Python
```

The characters `x` and `y` are removed from both ends as long as they occur there.

Exam trap: Strings are immutable. `strip()` returns a new string; it does not change the original string in place.

## 6. `upper()`

`upper()` returns a new string with lowercase letters converted to uppercase.

```
s = "Hello Python"print(s.upper())print(s)
```

Output:

```
HELLO PYTHON
Hello Python
```

The original `s` remains unchanged.

## 7. `lower()`

`lower()` returns a new string with uppercase letters converted to lowercase.

```
s = "HELLO Python"print(s.lower())print(s)
```

Output:

```
hello python
HELLO Python
```

### Comparing strings without case differences

```
a = "Python"b = "PYTHON"print(a == b)print(a.lower() == b.lower())
```

Output:

```
False
True
```

`lower()` is useful for case-insensitive comparisons involving ordinary English text. For more complete Unicode case-insensitive matching, Python also provides `casefold()`.

## 8. `replace()`

`replace()` returns a new string in which occurrences of a specified substring are replaced.

Syntax:

```
string.replace(old, new, count)
```

The optional `count` limits the number of replacements.

```
s = "banana"print(s.replace("a", "o"))print(s.replace("a", "o", 2))print(s.replace("na", "XY"))print(s)
```

Output:

```
bonono
bonana
baXYXY
banana
```

Explanation:

- `replace("a", "o")` replaces all occurrences.
    
- `replace("a", "o", 2)` replaces only the first two occurrences.
    
- `replace("na", "XY")` replaces each non-overlapping occurrence of `"na"`.
    
- The original string remains `"banana"`.
    

Exam trap: `replace()` does not modify the original string because strings are immutable.

## 9. `split()`

`split()` divides a string into a list of substrings.

### Example 1: Split on whitespace

```
s = "Python is easy"print(s.split())print(type(s.split()))
```

Output:

```
['Python', 'is', 'easy']
<class 'list'>
```

When no separator is provided, consecutive whitespace is treated as a separator, and leading/trailing whitespace is ignored.

### Example 2: Split using a separator

```
s = "red,green,blue"print(s.split(","))print(s.split(",", 1))
```

Output:

```
['red', 'green', 'blue']
['red', 'green,blue']
```

The optional second argument, `maxsplit`, limits the number of splits.

### Example 3: Empty strings in the result

```
print("a,,b,".split(","))print("  a   b  ".split())print("  a   b  ".split(" "))
```

Output:

```
['a', '', 'b', '']
['a', 'b']
['', '', 'a', '', '', 'b', '', '']
```

Very important exam distinction:

- `split()` with no argument groups whitespace and ignores leading/trailing whitespace.
    
- `split(" ")` splits at each literal space, so empty strings can appear in the result.
    

## 10. `find()`

`find()` returns the index of the first occurrence of a substring. If the substring is not found, it returns `-1`.

```
s = "hello world"print(s.find("o"))print(s.find("world"))print(s.find("Python"))print(s.find("o", 5))
```

Output:

```
4
6
-1
7
```

The optional arguments can specify a start and stop position for the search.

### `find()` vs `index()`

|Method|If substring is found|If not found|
|---|---|---|
|`find()`|Returns its index|Returns `-1`|
|`index()`|Returns its index|Raises `ValueError`|

Example:

```
s = "Python"print(s.find("z"))print(s.index("y"))
```

Output:

```
-1
1
```

Exam trap: `find()` returns an index, not `True` or `False`. Also, index `0` is a valid result, so avoid checking the result with `if s.find("x"):` when you need to distinguish “found” from “not found.”

## 11. `ord()`

`ord()` is a built-in function that returns the Unicode code point of a single-character string.

```
print(ord("A"))print(ord("a"))print(ord("0"))print(ord("₹"))
```

Output:

```
65
97
48
8377
```

Important points:

- `ord("A")` is `65`.
    
- `ord("a")` is `97`.
    
- `ord("0")` is `48`.
    
- Uppercase and lowercase letters have different code points.
    
- The argument must be a string containing exactly one Unicode character.
    

For example, `ord("AB")` raises a `TypeError`.

## 12. `chr()`

`chr()` is the reverse of `ord()` for valid Unicode code points: it returns a string containing the character corresponding to an integer code point.

```
print(chr(65))print(chr(97))print(chr(48))print(chr(8377))
```

Output:

```
A
a
0
₹
```

The integer must be in the valid Unicode code-point range, from `0` through `0x10FFFF`. An integer outside that range raises a `ValueError`.

### `ord()` vs `chr()`

|Function|Input|Output|
|---|---|---|
|`ord("A")`|One-character string|`65`|
|`chr(65)`|Integer code point|`"A"`|

Remember:

\[ \operatorname{chr}(\operatorname{ord}("A")) = "A" \]

### Character arithmetic trap

Python does not allow direct addition of a character and an integer.

```
print("A" + 1)
```

This raises a `TypeError`.

To get the next code point, use:

```
print(chr(ord("A") + 1))
```

Output:

```
B
```

## Final revision sheet

| Function or operation | Key fact                        |
| --------------------- | ------------------------------- |
| `s[i]`                | Accesses one character          |
| `s[start:stop]`       | Stop index is excluded          |
| `s[::-1]`             | Reverses a string               |
| `s1 + s2`             | Concatenates strings            |
| `len(s)`              | Returns string length           |
| `s.strip()`           | Removes whitespace at both ends |
| `s.upper()`           | Returns uppercase string        |
| `s.lower()`           | Returns lowercase string        |
| `s.replace(old, new)` | Replaces occurrences            |
| `s.split()`           | Returns a list                  |
| `s.find(sub)`         | Returns index or `-1`           |
| `ord(ch)`             | Character to Unicode code point |
| `chr(n)`              | Unicode code point to character |