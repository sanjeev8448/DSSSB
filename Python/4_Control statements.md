## 1. `if` statement

The `if` statement executes a block of code when a condition evaluates to `True`.

Syntax:

```
if condition:    statement
```

Example:

```
age = 20if age >= 18:    print("Eligible to vote")
```

Output:

```
Eligible to vote
```

### Important: Indentation

Python uses indentation to define code blocks. The conventional indentation is four spaces.

```
x = 10if x > 5:    print("Greater than 5")    print("Inside if")print("Outside if")
```

Output:

```
Greater than 5
Inside if
Outside if
```

The last `print()` is outside the `if` block because it is not indented.

Exam trap: Forgetting the colon after `if` causes a `SyntaxError`.

## 2. `elif` statement

`elif` means else if. It checks another condition when the preceding `if` or `elif` condition was false.

Syntax:

```
if condition1:    statement1elif condition2:    statement2elif condition3:    statement3
```

Example:

```
marks = 75if marks >= 90:    print("Grade A")elif marks >= 70:    print("Grade B")elif marks >= 50:    print("Grade C")else:    print("Fail")
```

Output:

```
Grade B
```

Python checks conditions from top to bottom and executes the first matching branch. The remaining branches are skipped.

Exam trap: If `marks = 95`, only `Grade A` is printed, not all grades whose conditions are true.

## 3. `else` statement

The `else` block executes when none of the preceding conditions in the corresponding `if`/`elif` chain is true.

```
number = 4if number > 10:    print("Greater than 10")else:    print("10 or less")
```

Output:

```
10 or less
```

### Nested `if` statements

An `if` statement can appear inside another `if` statement.

```
x = 15if x > 0:    if x % 2 == 0:        print("Positive even")    else:        print("Positive odd")else:    print("Non-positive")
```

Output:

```
Positive odd
```

Exam trap: An `else` belongs to the nearest unmatched `if` at the same indentation level.

### Quick comparison

|Statement|Purpose|
|---|---|
|`if`|Tests the first condition|
|`elif`|Tests another condition if previous conditions failed|
|`else`|Handles the remaining case|
|Nested `if`|Tests a condition inside another conditional block|

## 4. `for` loop

A `for` loop iterates over the items of an iterable, such as a list, tuple, string, set, dictionary, or range.

Syntax:

```
for variable in iterable:    statement
```

### Example 1: Iterating through a list

```
numbers = [10, 20, 30]for n in numbers:    print(n)
```

Output:

```
10
20
30
```

The loop assigns each item to `n`, one at a time.

### Example 2: Using `range()`

`range()` is frequently tested in programming MCQs.

```
for i in range(5):    print(i)
```

Output:

```
0
1
2
3
4
```

`range(5)` starts at `0` and stops before `5`.

The three common forms are:

|Expression|Values generated|
|---|---|
|`range(5)`|`0, 1, 2, 3, 4`|
|`range(2, 6)`|`2, 3, 4, 5`|
|`range(2, 10, 2)`|`2, 4, 6, 8`|
|`range(5, 0, -1)`|`5, 4, 3, 2, 1`|
|`range(0)`|No values|

### Example 3: Sum using a `for` loop

```
total = 0for i in range(1, 6):    total += iprint(total)
```

Output:

```
15
```

Calculation: \(1+2+3+4+5=15\).

### Example 4: Iterating over a string

```
for ch in "CAT":    print(ch)
```

Output:

```
C
A
T
```

### Example 5: Nested `for` loop

```
for i in range(2):    for j in range(3):        print(i, j)
```

Output:

```
0 0
0 1
0 2
1 0
1 1
1 2
```

The inner loop completes all three iterations for each iteration of the outer loop.

Exam traps:

- `range()` excludes its stop value.
    
- `range(1, 6)` produces five values, not six.
    
- `range(5, 0, -1)` counts downward and excludes `0`.
    
- A `for` loop can iterate over strings and collections, not just numbers.
    

## 5. `while` loop

A `while` loop repeats a block as long as its condition is true.

Syntax:

```
while condition:    statement
```

### Example 1: Basic `while` loop

```
i = 1while i <= 5:    print(i)    i += 1
```

Output:

```
1
2
3
4
5
```

The variable `i` increases each time until the condition becomes false.

### Example 2: When the condition is initially false

```
i = 10while i < 5:    print(i)print("Finished")
```

Output:

```
Finished
```

The body executes zero times because the condition is false from the beginning.

### Example 3: Infinite loop trap

```
i = 1while i <= 5:    print(i)
```

This loop does not terminate normally because `i` is never updated. It keeps printing `1` unless interrupted.

### `for` vs `while`

|Feature|`for`|`while`|
|---|---|---|
|Typical use|Iterate over an iterable|Repeat while a condition is true|
|Iteration count|Often determined by iterable|Depends on condition and updates|
|Automatic iteration|Advances through iterable|Programmer usually updates state|
|Risk of accidental infinite loop|Possible|Common if condition never becomes false|

## 6. `break` statement

`break` immediately terminates the nearest enclosing loop. Execution continues after that loop.

```
for i in range(1, 6):    if i == 3:        break    print(i)print("Loop ended")
```

Output:

```
1
2
Loop ended
```

When `i` becomes `3`, `break` ends the loop before `print(i)` executes.

### `break` in nested loops

```
for i in range(3):    for j in range(3):        if j == 1:            break        print(i, j)
```

Output:

```
0 0
1 0
2 0
```

Exam trap: `break` terminates only the innermost loop that contains it, not every nested loop.

## 7. `continue` statement

`continue` skips the remaining statements in the current iteration and proceeds to the next iteration of the nearest enclosing loop.

```
for i in range(1, 6):    if i == 3:        continue    print(i)
```

Output:

```
1
2
4
5
```

When `i == 3`, the `print()` statement is skipped, but the loop continues.

### `break` vs `continue`

`break` — stop the loop

The loop ends immediately.

`continue` — skip this iteration

The loop proceeds with its next iteration.

### `continue` in a `while` loop: a common trap

```
i = 0while i < 5:    i += 1    if i == 3:        continue    print(i)
```

Output:

```
1
2
4
5
```

Notice that `i` is incremented before `continue`. If the increment were placed after `continue`, the loop could get stuck when `i == 3`.

## 8. `pass` statement

`pass` is a null statement. It performs no action when executed and is used as a placeholder where Python syntax requires a statement.

### Example 1: Empty `if` block

```
x = 10if x > 5:    passprint("Program continues")
```

Output:

```
Program continues
```

Without `pass`, leaving the block empty would cause an `IndentationError` or syntax-related failure.

### Example 2: Placeholder for future code

```
def calculate():    passcalculate()print("Completed")
```

Output:

```
Completed
```

The function does nothing and implicitly returns `None`.

### `pass` vs `break` vs `continue`

|Statement|Effect|
|---|---|
|`pass`|Does nothing; execution proceeds normally|
|`break`|Terminates the nearest enclosing loop|
|`continue`|Skips the remainder of the current loop iteration|

Exam trap: `pass` does not skip a loop iteration and does not terminate the loop.

## 9. Bonus: `for`/`while` loop `else`

Python allows an `else` clause with a loop. This is worth understanding for output-based questions.

The loop's `else` block runs when the loop finishes normally, including when a `while` condition becomes false. It does not run if the loop exits through `break`.

```
for i in range(3):    print(i)else:    print("Completed")
```

Output:

```
0
1
2
Completed
```

Now compare:

```
for i in range(3):    if i == 1:        break    print(i)else:    print("Completed")
```

Output:

```
0
```

The `else` block does not execute because the loop ended through `break`

## Final revision sheet

| Topic       | Remember this                                     |
| ----------- | ------------------------------------------------- |
| `if`        | Executes when the condition is true               |
| `elif`      | Checks another condition if earlier branches fail |
| `else`      | Handles the remaining case                        |
| `for`       | Iterates over an iterable                         |
| `while`     | Repeats while a condition is true                 |
| `break`     | Exits the nearest enclosing loop                  |
| `continue`  | Skips to the next iteration                       |
| `pass`      | Does nothing                                      |
| `range(n)`  | Generates integers from `0` to `n-1`              |
| Loop `else` | Runs after normal completion, not after `break`   |