## 1. Python features

Python is a high-level, general-purpose programming language known for readable syntax and a large ecosystem of libraries.

### Important features

|Feature|Explanation|
|---|---|
|High-level|Hides many low-level hardware details|
|Readable syntax|Uses relatively simple, English-like statements|
|Interpreted execution|Commonly runs through a Python interpreter, which compiles source to bytecode and executes it|
|Dynamically typed|Variable names can refer to objects of different types at different times|
|Strongly typed|Incompatible types are not automatically combined in many operations|
|Object-oriented|Supports classes, objects, inheritance, and polymorphism|
|Multi-paradigm|Supports procedural, object-oriented, and functional programming styles|
|Portable|Python programs can run on different platforms with a compatible interpreter and dependencies|
|Large standard library|Includes modules for files, dates, math, networking, and more|
|Automatic memory management|Uses automatic memory management, including reference counting and garbage collection in CPython|

### Example: dynamic typing

Output

The name `x` first refers to an integer object, then to a string object.

### Example: strongly typed behavior

This raises a `TypeError` because Python does not automatically add a string and an integer.

Exam trap: Dynamically typed does not mean that Python has no types. Objects have types; variable names are not permanently declared with one type.

## 2. Python interpreter

An interpreter is software that processes and executes a program. In standard Python implementations, the process involves more than simply reading each source line directly.

In CPython, the usual flow is:

Python source code (`.py`)

Compilation to bytecode

Python virtual machine executes bytecode

Bytecode may be cached in `.pyc` files, such as in `__pycache__`, but this is an implementation detail and does not happen in exactly the same way for every execution.

### Example

Save this code in `hello.py`:

Run it in a terminal:

Output:

Exam trap: Python is often called interpreted, but CPython typically compiles source code into bytecode before execution. It is not accurate to say Python never compiles code.

## 3. Interactive mode

Interactive mode lets you type Python statements into a prompt and see results immediately.

Start Python by running:

You may see a prompt like `>>>`.

Example session:

Interactive mode is useful for:

- Testing small expressions.
    
- Checking the result of a function.
    
- Learning syntax.
    
- Debugging short pieces of code.
    

A statement such as `10 + 20` displays its result automatically in the interactive interpreter.

## 4. Script mode

In script mode, Python code is saved in a file, typically with the `.py` extension, and executed as a program.

Example file, `sum.py`:

Run it:

Output:

### Interactive mode vs script mode

|Interactive mode|Script mode|
|---|---|
|Enter commands at a prompt|Save commands in a file|
|Results can appear immediately|Output appears when the script executes printing or other output operations|
|Convenient for experimentation|Convenient for complete programs|
|Often uses `>>>`|Runs a `.py` file, for example|

Exam tip: A `.py` file is not automatically a script merely because it exists; script mode refers to executing the file as a program.

## 5. Indentation

Indentation means spaces or tabs at the beginning of a line. In Python, indentation defines code blocks.

Unlike C or C++, Python normally uses indentation instead of braces `{}` to group statements.

### Example

Output

The two indented statements belong to the `if` block. The final `print()` is outside the block.

### Incorrect indentation

This causes an `IndentationError` because the body of the `if` statement is not indented.

### Important rules

- Use consistent indentation.
    
- Four spaces per indentation level is the standard Python style.
    
- Do not mix tabs and spaces inconsistently.
    
- A colon (`:`) usually introduces a compound statement's suite, such as `if`, `for`, `while`, `def`, and `class`.
    

Exam trap: Incorrect indentation can cause a syntax-related error even when the words and operators appear correct.

## 6. Tokens

A token is a basic unit recognized by Python's lexical analysis.

For example:

This statement contains tokens such as:

- `total` — identifier
    
- `=` — operator
    
- `price` — identifier
    
- `+` — operator
    
- `10` — numeric literal
    

Python tokens are commonly classified as keywords, identifiers, literals, operators, and delimiters or punctuators. Comments and whitespace also affect how source code is processed, but are not all classified as the same kind of token.

### Token classification example

|Token|Category|
|---|---|
|`if`|Keyword|
|`marks`|Identifier|
|`>=`|Operator|
|`40`|Integer literal|
|`:`|Punctuator/delimiter|
|`print`|Identifier (built-in function name)|
|`"Pass"`|String literal|
|`(` `)`|Punctuators/delimiters|

Exam tip: `print` is a built-in function name, not a Python keyword.

## 7. Keywords

Keywords are reserved words that have special meaning in Python's syntax. They cannot be used as ordinary identifiers.

Examples include:

`if`, `else`, `elif`, `for`, `while`, `break`, `continue`, `def`, `return`, `class`, `try`, `except`, `import`, `from`, `as`, `pass`, `lambda`, `yield`, `with`, `raise`, `global`, `nonlocal`, `assert`, `del`, `and`, `or`, `not`, `in`, `is`, `True`, `False`, and `None`.

The exact keyword set depends on the Python version; soft keywords are a separate category.

### Example

This causes a `SyntaxError` because `if` is a keyword.

By contrast:

Output:

### How to check keywords

Output:

Exam trap: Python is case-sensitive. `True` is a keyword, but `true` is not the same name and can be used as an identifier.

## 8. Identifiers

An identifier is a name used for a variable, function, class, module, or another named entity.

Examples:

Here, `name`, `total_marks`, and `calculate_total` are identifiers.

### Rules for identifiers

1. They can contain letters, underscores (`_`), and digits.
    
2. They cannot start with a digit.
    
3. They cannot be Python keywords.
    
4. They are case-sensitive.
    
5. Python also permits many Unicode letters in identifiers, although ordinary English letters are common in practice.
    

### Valid vs invalid identifiers

|Identifier|Valid?|Reason|
|---|---|---|
|`marks`|Yes|Letters are permitted|
|`_count`|Yes|Can start with `_`|
|`marks2`|Yes|Digits are permitted after the first character|
|`total_marks`|Yes|Underscores are permitted|
|`2marks`|No|Starts with a digit|
|`total-marks`|No|Hyphen is not allowed in an identifier|
|`class`|No|Reserved keyword|
|`my name`|No|Contains a space|

### Case sensitivity

Output:

`age` and `Age` are two different identifiers.

## 9. Literals

A literal is a value written directly in source code.

### A. Numeric literals

Python supports integers, floating-point numbers, and complex numbers.

### B. String literals

Strings can use single or double quotes:

Multiline strings can use triple quotes:

### C. Boolean literals

Python's Boolean literals are `True` and `False`, with capital first letters.

### D. Special literal `None`

`None` represents the absence of a value or a null-like value.

Output:

### E. Collection literals

Exam trap: `{}` creates an empty dictionary, not an empty set. Use `set()` for an empty set.

## 10. Operators

Operators perform operations on values and variables.

### A. Arithmetic operators

|Operator|Meaning|Example|
|---|---|---|
|`+`|Addition|`5 + 2` → `7`|
|`-`|Subtraction|`5 - 2` → `3`|
|`*`|Multiplication|`5 * 2` → `10`|
|`/`|True division|`5 / 2` → `2.5`|
|`//`|Floor division|`5 // 2` → `2`|
|`%`|Remainder|`5 % 2` → `1`|
|`**`|Exponentiation|`2 ** 3` → `8`|

### B. Comparison operators

`==`, `!=`, `<`, `>`, `<=`, `>=`

They return Boolean results.

Output:

### C. Logical operators

`and`, `or`, `not`

Output:

Python's `and` and `or` use short-circuit evaluation and can return one of their operands, not necessarily a Boolean.

### D. Assignment operators

Examples: `=`, `+=`, `-=`, `*=`, `/=`, `//=`, `%=`, `**=`

Output:

### E. Bitwise operators

`&`, `|`, `^`, `~`, `<<`, `>>`

They operate on integer bits.

Output:

For `5` (`0101`) and `3` (`0011`):

- AND gives `0001` → `1`.
    
- OR gives `0111` → `7`.
    
- XOR gives `0110` → `6`.
    

### F. Membership operators

`in` and `not in`

Output:

### G. Identity operators

`is` and `is not` test object identity, not ordinary value equality.

Output:

The lists have equal contents, but they are distinct list objects.

### H. Unary operators

Examples include unary plus, unary minus, and bitwise inversion:

Output:

For Python integers, `~x` is equivalent to `-(x + 1)`.

### Important operator traps

- `=` assigns; `==` compares.
    
- `/` performs true division; `//` performs floor division.
    
- `**` is exponentiation.
    
- `is` tests identity; `==` tests equality.
    
- `not`, `and`, and `or` are keywords as well as logical operators in Python terminology.
    

## 11. Punctuators (delimiters)

Punctuators are symbols that organize Python syntax, separate elements, or mark boundaries.

Common examples include:

|Symbol|Typical use|
|---|---|
|`(` `)`|Function calls and grouping expressions|
|`[` `]`|Lists, indexing, and slicing|
|`{` `}`|Dictionaries and sets|
|`:`|Introduces a suite after statements such as `if`, `for`, `def`, and `class`|
|`,`|Separates arguments and elements|
|`.`|Attribute access, as in `obj.name`|
|`;`|Can separate simple statements on the same line|
|`@`|Decorator syntax|
|`=`|Assignment; also used in keyword arguments|
|`->`|Function return annotation syntax|

Example:

Output

In this example:

- delimit the list and its indexing operation.
    
- `:` introduces the `if` suite.
    
- `()` delimit the function call's arguments.
    

### Why punctuators matter

Python relies on punctuation and indentation together to determine program structure. A missing colon in an `if` statement, for example, causes a syntax error.

This is invalid because the colon is missing after `True`.

Exam note: Some Python references classify these symbols as delimiters or operators in the formal token system. For exam revision, learn their roles in the syntax rather than relying only on the label.

## 12. Comments

Comments are explanatory notes in source code. Python ignores comments when executing the program.

### A. Single-line comments

Use `#`:

Output:

### B. Inline comments

A comment can appear after a statement:

Everything from the `#` to the end of the physical line is treated as a comment, outside a string literal.

### C. Multiline comments

Python does not have a separate multiline-comment delimiter equivalent to `/* ... */` in C. You can use consecutive `#` comment lines:

Triple-quoted strings are often used for documentation, but they are strings, not formal comment syntax:

This string is the function's docstring because it appears as the first statement in the function body.

Exam trap: `"""..."""` is a string literal. When used as a docstring, it has a documentation purpose; it is not the same as a `#` comment.

## 13. Variables

A variable is a name bound to an object. Python variables do not need a separate type declaration in ordinary code.

### A. Creating variables

Output:

The assignment operator `=` binds each name to the corresponding object.

### B. Dynamic typing

Output:

The same name can be rebound to objects of different types.

### C. Multiple assignment

Output:

You can also assign one value to multiple names:

All three names refer to the same integer object `0` in this example. Because integers are immutable, there is no shared-mutation issue here.

### D. Variables refer to objects

Output:

Both names refer to the same list object. Modifying that list through `b` is visible when accessing it through `a`.

### E. Checking a variable's type

Use `type()`:

Output:

You can also use `isinstance()` when checking whether an object is an instance of a type or class.

Exam trap: A variable name is not the object itself; it refers to an object. Assignment can bind multiple names to the same object.

# 1. Constants in Python

## 1.1 What is a constant?

A constant is a value intended to remain unchanged throughout a program.

For example, the value of \(\pi\) is approximately 3.14159. If a program uses this value repeatedly, we can store it in a constant-style variable.

```
PI = 3.14159MAX_ATTEMPTS = 3radius = 5area = PI * radius * radiusprint(area)print(MAX_ATTEMPTS)
```

Output:

```
78.53975
3
```

## 1.2 Does Python support true constants?

Important for the exam: Python does not enforce ordinary variables as constants. By convention, programmers use uppercase names to indicate that a value should not be changed.

```
PI = 3.14159PI = 3.14print(PI)
```

Output:

```
3.14
```

Even though `PI` is written in uppercase, Python allows reassignment.

Exam trap: Uppercase naming is a convention, not a restriction enforced by Python.

## 1.3 Types of constants and literals

In Python, a literal is a value written directly in the code. Examples include numbers, strings and Boolean values.

|Type|Examples|Meaning|
|---|---|---|
|Integer|`10`, `-5`, `0`|Whole numbers|
|Float|`3.14`, `2.0`|Floating-point numbers|
|Complex|`2+3j`|Complex number|
|String|`"Hello"`, `'Python'`|Text|
|Boolean|`True`, `False`|Truth values|
|Special value|`None`|Absence of a value|

Example:

```
age = 25price = 99.5number = 2 + 3jname = "Python"is_valid = Trueresult = Noneprint(type(age))print(type(price))print(type(number))print(type(name))print(type(is_valid))print(type(result))
```

Output:

```
<class 'int'>
<class 'float'>
<class 'complex'>
<class 'str'>
<class 'bool'>
<class 'NoneType'>
```

Remember that `None` is a special singleton value representing the absence of a value. `NoneType` is its type.

## 1.4 Constants versus variables

|Feature|Constant-style name|Variable|
|---|---|---|
|Purpose|Value intended to remain unchanged|Value that may change|
|Naming convention|Usually uppercase|Often lowercase|
|Example|`MAX_SIZE = 100`|`count = 10`|
|Can Python reassign it?|Yes|Yes|
|Enforced as immutable binding by ordinary assignment?|No|No|

Do not confuse a constant-style name with an immutable object. These are different concepts.

For example, a tuple cannot have its elements reassigned, but a list can be modified even when its variable name is uppercase.

```
MAX_VALUES = [10, 20, 30]MAX_VALUES.append(40)print(MAX_VALUES)
```

Output:

```
[10, 20, 30, 40]
```

The list was modified despite its uppercase variable name.

## 1.5 How can Python indicate constants more formally?

Python's `typing` module provides `Final` as a type-checking hint.

```
from typing import FinalPI: Final[float] = 3.14159
```

A type checker can flag attempts to reassign `PI`, but `Final` does not prevent reassignment at runtime by itself.

### Exam revision: Constants

- Python has no general built-in mechanism that makes ordinary variable names constant merely through uppercase spelling.
    
- `PI`, `MAX_SIZE`, and `TOTAL_MARKS` are common constant naming conventions.
    
- A literal is a value written directly in source code.
    
- `True`, `False`, and `None` are special built-in values.
    
- `Final` is a typing annotation, not runtime enforcement.
    

# 2. L-value and R-value

This concept is especially important for understanding assignment statements and for comparing Python with C/C++.

## 2.1 What is an L-value?

An L-value is traditionally an expression that identifies a storage location or an assignable object.

Example in Python:

```
x = 10x = 20print(x)
```

Output:

```
20
```

Here, `x` is the target of assignment. It refers to the object to which the name is bound.

## 2.2 What is an R-value?

An R-value is traditionally an expression that supplies a value, such as a literal or the result of a calculation.

Example:

```
x = 10y = x + 5print(y)
```

Output:

```
15
```

In `y = x + 5`:

- `y` is the assignment target.
    
- `x + 5` is the expression whose value is calculated and assigned to `y`.
    
- `10` and `5` are literal values.
    

Important nuance: L-value and R-value are formal categories in languages such as C and C++. In Python, these terms are often used informally to explain assignment targets and values; Python's assignment model is based on names and object references.

## 2.3 Easy way to remember

## L-value

Left side of assignment (simplified rule)

The target receiving the assignment.

## R-value

Right-side value (simplified rule)

The value or result being assigned.

Consider:

```
a = 10b = 20a = b + 5
```

In the final statement, `a` is the target and `b + 5` is the value-producing expression. The result is `25`, so `a` becomes `25`.

## 2.4 Valid and invalid assignment targets

### Example 1: Valid assignment

```
x = 100print(x)
```

Output:

```
100
```

`x` is a valid assignment target.

### Example 2: Invalid assignment

```
10 = x
```

This produces a `SyntaxError`.

Why? A numeric literal such as `10` cannot be used as the assignment target.

### Example 3: Valid assignment to a list element

```
numbers = [10, 20, 30]numbers[1] = 99print(numbers)
```

Output:

```
[10, 99, 30]
```

`numbers[1]` is a valid assignment target because it identifies an element of a mutable list.

### Example 4: Invalid assignment to a function call result

```
get_number = lambda: 10get_number() = 20
```

This produces a `SyntaxError`. A function call result cannot be used as an ordinary assignment target.

## 2.5 L-value/R-value in C versus Python

This distinction can be tested through language comparisons.

|Expression or concept|Python|C|
|---|---|---|
|`x = 10`|Valid|Valid|
|`10 = x`|Invalid|Invalid|
|`a[0] = 5`|Valid if `a` is a mutable list|Valid if `a` is an appropriate array|
|Function call on assignment left side, e.g. `f() = 5`|Invalid|Invalid in ordinary C|
|Meaning of variable name|Name bound to an object|Identifier designating an object, in this context|

One important difference: Python names do not behave exactly like C variables. For example, assigning `b = a` in Python binds another name to the same object; it does not automatically copy the object.

```
a = [1, 2]b = ab.append(3)print(a)print(b)
```

Output:

```
[1, 2, 3]
[1, 2, 3]
```

Both names refer to the same list. This is an important Python assignment concept, although it is not itself the definition of an L-value or R-value.