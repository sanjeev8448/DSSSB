# DSSSB TGT Computer Science — Python Functions

A function is a reusable block of code designed to perform a particular task. Functions help reduce code repetition, improve readability, and make programs easier to test and maintain.

Your syllabus has seven areas: built-in functions, user-defined functions, arguments, positional arguments, default arguments, return values, and local/global scope.

For DSSSB, pay special attention to parameter vs argument, `print()` vs `return`, default argument rules, and local vs global variables.

## 1. Built-in functions

Built-in functions are provided by Python and can be used without defining them yourself or importing a module.

|Function|Purpose|Example|Result|
|---|---|---|---|
|`print()`|Displays output|`print("Hi")`|`Hi`|
|`len()`|Counts items|`len("Python")`|`6`|
|`type()`|Returns an object's type|`type(10)`|`int` type|
|`int()`|Converts to integer where valid|`int("25")`|`25`|
|`float()`|Converts to float where valid|`float("2.5")`|`2.5`|
|`str()`|Converts to string|`str(123)`|`"123"`|
|`abs()`|Absolute value|`abs(-8)`|`8`|
|`round()`|Rounds a number|`round(3.14159, 2)`|`3.14`|
|`sum()`|Adds items|`sum([1, 2, 3])`|`6`|
|`max()`|Finds maximum|`max(4, 8, 2)`|`8`|
|`min()`|Finds minimum|`min(4, 8, 2)`|`2`|
|`range()`|Produces a range of integers|`list(range(4))`|`[0, 1, 2, 3]`|

Example:

```
numbers = [10, 20, 30]print(len(numbers))print(sum(numbers))print(max(numbers))print(min(numbers))print(type(numbers))
```

Output:

```
3
60
30
10
<class 'list'>
```

Exam traps:

- `print()` displays a value; it does not return that displayed value.
    
- `len()` returns the number of elements, not their sum.
    
- `range(5)` generates values from `0` through `4`.
    
- `input()` returns a string by default, even when the user enters digits.
    

For example:

```
x = input("Enter a number: ")print(type(x))
```

If the user enters `25`, the type printed is:

```
<class 'str'>
```

To perform arithmetic, convert it when appropriate: `x = int(input())`.

## 2. User-defined functions

A user-defined function is created by the programmer using the `def` keyword.

### Syntax

```
def function_name(parameters):    statements    return value
```

The `return` statement is optional. If no value is explicitly returned, the function returns `None`.

### Example 1: Function without parameters

```
def greet():    print("Hello, Python!")greet()greet()
```

Output:

```
Hello, Python!
Hello, Python!
```

The function is defined once and called twice.

### Example 2: Function with parameters

```
def greet(name):    print("Hello,", name)greet("Amit")greet("Ravi")
```

Output:

```
Hello, Amit
Hello, Ravi
```

Here, `name` is the parameter, while `"Amit"` and `"Ravi"` are arguments passed during the calls.

### Example 3: Function performing a calculation

```
def add(a, b):    result = a + b    return resultanswer = add(10, 20)print(answer)
```

Output:

```
30
```

Execution flow:

1. Python defines the function `add`.
    
2. `add(10, 20)` calls the function.
    
3. `a` receives `10` and `b` receives `20`.
    
4. The function calculates `30`.
    
5. `return` sends the result back to the caller.
    
6. The returned value is assigned to `answer`.
    

Important: Defining a function does not execute its body. The body runs when the function is called.

## 3. Parameters and arguments

These two terms are related but have different meanings.

- Parameter: A variable written in the function definition.
    
- Argument: A value or expression supplied when calling the function.
    

```
def multiply(a, b):    return a * bresult = multiply(4, 5)print(result)
```

Output:

```
20
```

In this example:

|Element|Meaning|
|---|---|
|`a`, `b`|Parameters|
|`4`, `5`|Arguments|
|`multiply(4, 5)`|Function call|
|`a * b`|Expression being evaluated|
|`return`|Sends the result back|

### Types of arguments

For your syllabus, focus on positional and default arguments. Python also supports keyword arguments, which are useful for understanding function calls.

## 4. Positional arguments

Positional arguments are assigned to parameters according to their positions in the function call.

```
def student(name, age):    print(name)    print(age)student("Amit", 22)
```

Output:

```
Amit
22
```

The first argument `"Amit"` is assigned to `name`, and the second argument `22` is assigned to `age`.

### Reversing the argument order

```
def subtract(a, b):    return a - bprint(subtract(10, 3))print(subtract(3, 10))
```

Output:

```
7
-7
```

The result changes because positional arguments are assigned according to their order.

### Too many or too few positional arguments

```
def add(a, b):    return a + bprint(add(5, 10))
```

Output:

```
15
```

But `add(5)` raises a `TypeError` because one required argument is missing, while `add(5, 10, 15)` raises a `TypeError` because too many positional arguments were supplied.

### Positional vs keyword arguments

```
def introduce(name, age):    print(name, age)introduce("Amit", 22)introduce(age=22, name="Amit")
```

Output:

```
Amit 22
Amit 22
```

The first call uses positional arguments. The second uses keyword arguments, so order is not important when the parameter names are specified correctly.

Exam trap: A positional argument cannot normally follow a keyword argument in a function call.

For example, `introduce(name="Amit", 22)` causes a `SyntaxError`. Use `introduce("Amit", 22)` or `introduce(name="Amit", age=22)` instead.

## 5. Default arguments

A default argument is a parameter that has a predefined value in the function definition. The default is used when the caller does not supply that argument.

### Example 1: One default parameter

```
def greet(name="Guest"):    print("Hello,", name)greet()greet("Amit")
```

Output:

```
Hello, Guest
Hello, Amit
```

- `greet()` uses the default value `"Guest"`.
    
- `greet("Amit")` uses the supplied argument instead.
    

### Example 2: Multiple default parameters

```
def calculate(a, b=10):    return a + bprint(calculate(5))print(calculate(5, 20))
```

Output:

```
15
25
```

In `calculate(5)`, `b` defaults to `10`. In `calculate(5, 20)`, the supplied value `20` replaces the default for that call.

### Rule: Non-default parameters must come before default parameters

Valid:

```
def example(a, b=10):    return a + bprint(example(5))
```

Output:

```
15
```

Invalid:

```
def example(a=10, b):    return a + b
```

This causes a `SyntaxError` because a required parameter follows a default parameter.

### Default arguments are evaluated once

This is a common advanced Python trap.

```
def add_item(item, items=[]):    items.append(item)    return itemsprint(add_item(1))print(add_item(2))
```

Output:

```
[1]
[1, 2]
```

The same default list is reused across calls. It is not recreated each time.

A safer version uses `None`:

```
def add_item(item, items=None):    if items is None:        items = []    items.append(item)    return itemsprint(add_item(1))print(add_item(2))
```

Output:

```
[1]
[2]
```

DSSSB priority: Remember the default-parameter ordering rule, what happens when an argument is omitted, and the behavior of mutable default values.

## 6. Return statement

The `return` statement ends a function call and sends a result back to the caller. It can return a value, an object, or `None`.

### `print()` vs `return`

This distinction is very important.

```
def show_sum(a, b):    print(a + b)def get_sum(a, b):    return a + bx = show_sum(2, 3)y = get_sum(2, 3)print("x =", x)print("y =", y)
```

Output:

```
5
x = None
y = 5
```

Why?

- `show_sum()` displays `5`, but has no explicit return statement. Therefore, `x` becomes `None`.
    
- `get_sum()` returns `5`, so `y` becomes `5`.
    

|Feature|`print()`|`return`|
|---|---|---|
|Main purpose|Display output|Send a value back|
|Ends the function immediately?|No|Yes|
|Can its result be assigned to a variable?|Assignment receives `None`|Returned value is assigned|
|Can it support further calculations directly?|Not through its displayed output|Yes|

### A function without `return`

```
def greet():    print("Hello")result = greet()print(result)
```

Output:

```
Hello
None
```

Python implicitly returns `None` when a function reaches its end without a `return` statement.

### `return` ends the function immediately

```
def test():    print("A")    return 10    print("B")result = test()print(result)
```

Output:

```
A
10
```

`"B"` is never printed because execution stops at `return`.

### Returning multiple values

```
def calculate(a, b):    return a + b, a * bx, y = calculate(4, 3)print(x)print(y)
```

Output:

```
7
12
```

Python packages the two returned values into a tuple, which is then unpacked into `x` and `y`.

Exam trap: A function can contain multiple `return` statements, but only the one reached during a particular call will execute.

## 7. Local and global scope

Scope determines where a variable can be accessed.

For the DSSSB syllabus, understand local variables, global variables, shadowing, and the `global` keyword.

### 7.1 Local variable

A variable created inside a function is usually local to that function.

```
def greet():    message = "Hello"    print(message)greet()
```

Output:

```
Hello
```

The variable `message` is local to `greet()`. Trying to access it outside the function using `print(message)` would raise a `NameError` if there were no other binding for that name.

### 7.2 Global variable

A variable defined at the module level can be accessed by functions in that module.

```
message = "Hello"def greet():    print(message)greet()print(message)
```

Output:

```
Hello
Hello
```

The function can read the global variable because it does not define a local variable with the same name.

### 7.3 Local variable with the same name as a global variable

A local variable can have the same name as a global variable. The local name shadows the global name within the function.

```
x = 100def test():    x = 50    print(x)test()print(x)
```

Output:

```
50
100
```

Inside the function, `x` refers to the local variable. Outside the function, `x` still refers to the global variable.

### 7.4 The `global` keyword

Use `global` inside a function when you intend to reassign a name at the module level.

```
x = 10def change():    global x    x = 20change()print(x)
```

Output:

```
20
```

Without `global`, an assignment such as `x = 20` inside the function normally creates a local variable instead of rebinding the global name.

### 7.5 A common scope trap

```
x = 10def test():    print(x)    x = 20test()
```

This raises an `UnboundLocalError`.

Why? Because the assignment makes `x` local to `test()`. Python then tries to read that local `x` before it has been assigned a value.

### Local vs global summary

|Feature|Local variable|Global variable|
|---|---|---|
|Typical definition|Inside a function|At module level|
|Ordinary accessibility|Within its function|Throughout the module, subject to scope rules|
|Lifetime|Typically associated with function execution, although objects may live longer|Typically lasts while the module/global binding exists|
|Reassignment inside a function|Usually local assignment|Requires `global` to rebind the module-level name|
|Same-name behavior|Can shadow a global name|Remains unchanged when shadowed by a local variable|

Python also has enclosing-function scope and the `nonlocal` keyword, but for your current syllabus, prioritize the local/global distinction.

## Final revision sheet

|Topic|Key point|
|---|---|
|Built-in functions|Examples: `len()`, `sum()`, `type()`, `max()`|
|User-defined functions|Created using `def`|
|Parameters|Names defined in a function's signature|
|Arguments|Values supplied during a call|
|Positional arguments|Assigned according to order|
|Default arguments|Used when the caller omits the corresponding argument|
|`return`|Ends the current function call and returns a value|
|`print()`|Displays output; its own return value is `None`|
|Local scope|Names assigned locally inside a function are generally local to it|
|Global scope|Module-level bindings can be read inside functions|
|`global`|Allows rebinding a module-level name inside a function|
|Mutable default trap|A default list or dictionary is reused across calls|

Study priority: Practise output-tracing questions on `print()` versus `return`, positional and default arguments, mutable default parameters, and local/global scope. These concepts test the actual behavior of functions rather than just their syntax.