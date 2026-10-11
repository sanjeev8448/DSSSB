## 1. Arithmetic operators

Arithmetic operators perform mathematical calculations.

|Operator|Name|Example|Result|
|---|---|---|---|
|`+`|Addition|`10 + 3`|`13`|
|`-`|Subtraction|`10 - 3`|`7`|
|`*`|Multiplication|`10 * 3`|`30`|
|`/`|Division|`10 / 3`|`3.333...`|
|`//`|Floor division|`10 // 3`|`3`|
|`%`|Modulus|`10 % 3`|`1`|
|`**`|Exponentiation|`2 ** 3`|`8`|

```
print(10 + 3)print(10 / 2)print(10 // 3)print(10 % 3)print(2 ** 3)
```

Output:

```
13
5.0
3
1
8
```

### Important exam traps

Trap 1: `/` versus `//`

```
print(7 / 2)print(7 // 2)
```

Output:

```
3.5
3
```

`/` performs ordinary division; `//` performs floor division.

Trap 2: Negative floor division

```
print(-7 // 2)print(-7 % 2)
```

Output:

```
-4
1
```

Python rounds floor division down toward negative infinity. For the same operands, the quotient and remainder satisfy:

\[ a = (a // b)\times b + (a \% b) \]

Here, \(-7=(-4)\times2+1\).

Trap 3: Exponentiation

```
print(2 ** 3 ** 2)print(-2 ** 2)print((-2) ** 2)
```

Output:

```
512
-4
4
```

Exponentiation is right-associative, so `2 ** 3 ** 2` means `2 ** (3 ** 2)`. Also, exponentiation binds more tightly than unary minus, so `-2 ** 2` means `-(2 ** 2)`.

## 2. Relational (comparison) operators

Comparison operators compare two values and return a Boolean result: `True` or `False`.

|Operator|Meaning|Example|Result|
|---|---|---|---|
|`==`|Equal to|`5 == 5`|`True`|
|`!=`|Not equal to|`5 != 3`|`True`|
|`>`|Greater than|`5 > 3`|`True`|
|`<`|Less than|`5 < 3`|`False`|
|`>=`|Greater than or equal to|`5 >= 5`|`True`|
|`<=`|Less than or equal to|`3 <= 5`|`True`|

```
x = 10y = 20print(x == y)print(x != y)print(x < y)print(x >= 10)
```

Output:

```
False
True
True
True
```

### Chained comparisons

Python supports comparisons such as `a < b < c`.

```
x = 5print(1 < x < 10)print(1 < x > 3)print(1 < 2 < 1)
```

Output:

```
True
True
False
```

`1 < x < 10` is equivalent in result to checking both `1 < x` and `x < 10`, with the middle expression evaluated only once.

Exam trap: `=` is assignment, while `==` is comparison.

## 3. Logical operators

Python has three logical operators: `and`, `or`, and `not`.

|Operator|Meaning|Basic rule|
|---|---|---|
|`and`|Logical AND|Both operands must be truthy|
|`or`|Logical OR|At least one operand must be truthy|
|`not`|Logical NOT|Reverses truth value|

### Truth table

|A|B|`A and B`|`A or B`|
|---|---|---|---|
|`True`|`True`|`True`|`True`|
|`True`|`False`|`False`|`True`|
|`False`|`True`|`False`|`True`|
|`False`|`False`|`False`|`False`|

```
a = Trueb = Falseprint(a and b)print(a or b)print(not a)
```

Output:

```
False
True
False
```

### Very important: `and` and `or` do not always return Booleans

In Python, these operators return one of their operands.

```
print(0 and 10)print(5 and 10)print(0 or 10)print(5 or 10)print(not 5)
```

Output:

```
0
10
10
5
False
```

Rules:

- `x and y`: returns `x` if `x` is falsy; otherwise returns `y`.
    
- `x or y`: returns `x` if `x` is truthy; otherwise returns `y`.
    
- `not x`: always returns a Boolean.
    

Common falsy values include `False`, `None`, numeric zero, and empty strings, lists, tuples, sets, and dictionaries.

### Short-circuit evaluation

```
print(False and (10 / 0))print(True or (10 / 0))
```

Output:

```
False
True
```

Python does not evaluate the second operand when the first operand already determines the result. Therefore, the division by zero never occurs in these examples.

## 4. Assignment operators

Assignment operators assign values to variables or update an existing variable.

|Operator|Example|Equivalent operation|
|---|---|---|
|`=`|`x = 5`|Assign `5` to `x`|
|`+=`|`x += 3`|`x = x + 3`|
|`-=`|`x -= 3`|`x = x - 3`|
|`*=`|`x *= 3`|`x = x * 3`|
|`/=`|`x /= 3`|`x = x / 3`|
|`//=`|`x //= 3`|`x = x // 3`|
|`%=`|`x %= 3`|`x = x % 3`|
|`**=`|`x **= 3`|`x = x ** 3`|
|`&=`, `\\|=`, `^=`|Bitwise updates|Apply the corresponding bitwise operation|
|`<<=`, `>>=`|Shift updates|Apply the corresponding shift|

Example:

```
x = 10x += 5print(x)x *= 2print(x)x //= 3print(x)x **= 2print(x)
```

Output:

```
15
30
10
100
```

### Assignment and mutable objects

Python's augmented assignment can behave differently for mutable and immutable objects.

```
x = [1, 2]y = xx += [3]print(x)print(y)
```

Output:

```
[1, 2, 3]
[1, 2, 3]
```

For a list, `+=` modifies the existing list in place in this example. Both names therefore show the change.

Compare with string concatenation:

```
x = "Hi"y = xx += "!"print(x)print(y)
```

Output:

```
Hi!
Hi
```

Strings are immutable, so `x += "!"` rebinds `x` to a new string rather than modifying the original string.

Exam trap: Python does not have `++` or `--` increment/decrement operators like C/C++. `x += 1` is the usual alternative.

## 5. Bitwise operators

Bitwise operators work on the binary representation of integers.

Consider:

- `a = 5` → binary `0101`
    
- `b = 3` → binary `0011`
    

|Operator|Name|Example|Result|
|---|---|---|---|
|`&`|Bitwise AND|`5 & 3`|`1`|
|`\\|`|Bitwise OR|`5 \\| 3`|`7`|
|`^`|Bitwise XOR|`5 ^ 3`|`6`|
|`~`|Bitwise NOT|`~5`|`-6`|
|`<<`|Left shift|`5 << 1`|`10`|
|`>>`|Right shift|`5 >> 1`|`2`|

### Binary explanation

```
a = 5b = 3print(a & b)print(a | b)print(a ^ b)print(~a)print(a << 1)print(a >> 1)
```

Output:

```
1
7
6
-6
10
2
```

For the three binary operators:

```
  0101   (5)
& 0011   (3)
-------
  0001   (1)
```

```
  0101
| 0011
------
  0111   (7)
```

```
  0101
^ 0011
------
  0110   (6)
```

XOR (`^`) produces `1` when the corresponding bits differ.

### Why does `~5` equal `-6`?

In Python, integers use arbitrary precision, and bitwise NOT follows the relationship:

\[ \sim x = -x - 1 \]

Therefore:

\[ \sim 5 = -5 - 1 = -6 \]

This is a frequently tested expression.

### Shift operators

For non-negative integers:

- `x << n` shifts bits left by `n` positions.
    
- `x >> n` shifts bits right by `n` positions.
    

For example, `5` is `0101` in four-bit notation.

```
5 << 1  → 1010  → 10
5 >> 1  → 0010  → 2
```

For non-negative integers, shifting left by one is equivalent to multiplying by two, and shifting right by one is equivalent to floor-dividing by two.

Important: Bitwise operators `&`, `|`, and `^` are different from logical operators `and` and `or`. The former operate on bits for integers; the latter perform truth-value-based evaluation and may return an operand.

## 6. Membership operators

Python provides two membership operators:

- `in`
    
- `not in`
    

They test whether a value is present in a collection or sequence.

```
numbers = [10, 20, 30]print(20 in numbers)print(40 in numbers)print(40 not in numbers)print("Py" in "Python")
```

Output:

```
True
False
True
True
```

### Membership in a dictionary

For a dictionary, membership checks keys, not values.

```
student = {"name": "Amit", "age": 25}print("name" in student)print("Amit" in student)print("Amit" in student.values())
```

Output:

```
True
False
True
```

Why?

- `"name" in student` checks whether `"name"` is a key.
    
- `"Amit" in student` does not search the dictionary's values.
    
- `"Amit" in student.values()` explicitly checks the values.
    

Exam trap: Membership tests on strings are substring checks, and membership tests on dictionaries are key checks by default.

## 7. Identity operators

Python has two identity operators:

- `is`
    
- `is not`
    

They check whether two expressions refer to the same object, not merely whether their values are equal.

```
a = [1, 2]b = [1, 2]c = aprint(a == b)print(a is b)print(a is c)print(a is not b)
```

Output:

```
True
False
True
True
```

Explanation:

- `a == b` is `True` because their contents are equal.
    
- `a is b` is `False` because the lists are distinct objects.
    
- `a is c` is `True` because both names refer to the same list.
    

### The safest way to check `None`

```
x = Noneprint(x is None)print(x is not None)
```

Output:

```
True
False
```

Prefer `is None` over `== None`.

Exam trap: Do not rely on integer caching or string interning to predict identity for arbitrary objects. Use `==` for value equality and `is` for identity.

## 8. Operator precedence

Operator precedence determines which operations are evaluated first when an expression contains multiple operators.

For example:

```
print(2 + 3 * 4)
```

Output:

```
14
```

Multiplication happens before addition, so the expression is evaluated as `2 + (3 * 4)`.

### 8.1 Python operator precedence table

Listed from higher precedence to lower precedence. This is a study-focused table of the main operators in your syllabus.

|Priority|Operators|Meaning|
|---|---|---|
|1|`()`|Parentheses for grouping|
|2|`**`|Exponentiation|
|3|`+x`, `-x`, `~x`|Unary plus, minus, bitwise NOT|
|4|`*`, `/`, `//`, `%`|Multiplication, division, floor division, modulus|
|5|`+`, `-`|Addition, subtraction|
|6|`<<`, `>>`|Bit shifts|
|7|`&`|Bitwise AND|
|8|`^`|Bitwise XOR|
|9|`\\|`|Bitwise OR|
|10|`<`, `<=`, `>`, `>=`, `==`, `!=`, `in`, `not in`, `is`, `is not`|Comparisons, membership, identity|
|11|`not`|Logical NOT|
|12|`and`|Logical AND|
|13|`or`|Logical OR|
|14|`=`, `+=`, `-=`, `*=`, `/=`, etc.|Assignment statements, not ordinary expression operators|

Python also has other operators, such as `@`, `:=`, conditional expressions, and subscription or attribute-access operations. They are omitted here to keep the table focused on your requested topics.

### 8.2 Precedence examples

Example 1: Multiplication before addition

```
print(10 + 2 * 3)
```

Output:

```
16
```

Example 2: Parentheses first

```
print((10 + 2) * 3)
```

Output:

```
36
```

Example 3: Arithmetic before comparison

```
print(2 + 3 > 4)
```

Output:

```
True
```

Example 4: `not` before `and`, and `and` before `or`

```
print(not True or True and False)
```

Output:

```
False
```

It is evaluated as:

```
(not True) or (True and False)# False or False# False
```

Example 5: Bitwise AND before bitwise OR

```
print(2 | 3 & 1)
```

Output:

```
3
```

First, `3 & 1` gives `1`. Then `2 | 1` gives `3`.

Example 6: Exponentiation and unary minus

```
print(-3 ** 2)print((-3) ** 2)
```

Output:

```
-9
9
```

Exponentiation takes precedence over unary minus.

### 8.3 Associativity: another exam trap

When operators have the same precedence, associativity often determines evaluation order.

- Most arithmetic binary operators associate from left to right.
    
- Exponentiation associates from right to left.
    

```
print(20 - 5 - 3)print(2 ** 3 ** 2)
```

Output:

```
12
512
```

Interpretation:

- `20 - 5 - 3` means `(20 - 5) - 3`.
    
- `2 ** 3 ** 2` means `2 ** (3 ** 2)`.
    

Comparisons can also be chained, as in `1 < x < 10`; do not treat every chain as an ordinary left-to-right sequence of independent comparisons.