## 1. Data types in C

### 1.1 What is a data type?

A data type tells the compiler what kind of value a variable stores, how that value is interpreted, and which operations are appropriate for it.

For example:

- An age is usually stored as an integer.
    
- A percentage may be stored as a floating-point value.
    
- A single grade can be stored as a character.
    
- A true/false condition can be represented using an integer or `_Bool`.
    

Think of a variable as a box and its data type as the rule defining what kind of information the box holds.

### 1.2 Basic data types

|Data type|Purpose|Example|
|---|---|---|
|`char`|Character or small integer|`'A'`|
|`int`|Integer numbers|`25`|
|`float`|Single-precision floating-point|`87.5f`|
|`double`|Double-precision floating-point|`87.56789`|
|`void`|No value / no return value|`void display(void)`|
|`_Bool`|Boolean value, `0` or `1`|`_Bool passed = 1;`|

C also supports integer variations such as `short`, `long`, `signed` and `unsigned`.

### 1.3 Code example

```

#include <stdio.h>

int main(void) {
    int age = 21;
    float percentage = 87.5f;
    double pi = 3.1415926535;
    char grade = 'A';

    printf("Age: %d\n", age);
    printf("Percentage: %.1f\n", percentage);
    printf("Pi: %.10f\n", pi);
    printf("Grade: %c\n", grade);

    return 0;
}
```

Output:

```
Age: 21
Percentage: 87.5
Pi: 3.1415926535
Grade: A
```

Notice the `\n`: it moves the cursor to a new line. The `%d`, `%f` and `%c` parts tell `printf()` how to display the corresponding values.

### 1.4 Signed and unsigned integers

A signed integer can represent negative and positive values. An unsigned integer represents non-negative values.

```
#include <stdio.h>

int main(void) {
    signed int temperature = -5;
    unsigned int count = 10;

    printf("%d\n", temperature);
    printf("%u\n", count);

    return 0;
}
```

Output:

```
-5
10
```

An important exam distinction: `unsigned` does not mean that a value must be positive and nonzero. It can represent zero.

### 1.5 What are the sizes of data types?

Use `sizeof` to obtain the size of a type or object in bytes.

```
#include <stdio.h>

int main(void) {
    printf("%zu\n", sizeof(char));
    printf("%zu\n", sizeof(int));
    printf("%zu\n", sizeof(float));
    printf("%zu\n", sizeof(double));

    return 0;
}
```

`sizeof(char)` is guaranteed to be `1` byte. The sizes of `int`, `float` and `double` can depend on the implementation; a common system uses 4, 4 and 8 bytes, respectively.

Do not memorise those common sizes as universal rules. For exams, distinguish between guarantees in C and typical implementation values.

### 1.6 Important data-type concepts

- Integer division: `7 / 2` produces `3` when both operands are integers.
    
- Floating-point division: `7.0 / 2` produces `3.5`.
    
- Character representation: `'A'` is a character constant; in C, character constants have type `int`.
    
- Boolean values: In a condition, zero is false and nonzero is true. C's `_Bool` stores `0` or `1`.
    
- Overflow: An out-of-range result for a signed integer can cause undefined behaviour. Do not assume it always wraps around.
    

## 2. Variables

### 2.1 What is a variable?

A variable is a named object that stores a value which can generally be changed during program execution.

```
int marks = 70;
marks = 85;
```

After the second statement, `marks` holds `85`, not `70`.

### 2.2 Declaration, initialization and assignment

These terms are frequently confused.

```
int age;       // Declaration
int score = 90; // Declaration with initialization

age = 21;      // Assignment
score = 95;    // Assignment: replaces the previous value
```

- Declaration: Introduces a variable and specifies its type.
    
- Initialization: Gives an initial value when the object is initialized.
    
- Assignment: Stores a new value in an existing modifiable object.
    

### 2.3 Code tracing

```

#include <stdio.h>

int main(void) {
    int x = 10;
    int y = x + 5;

    x = 20;

    printf("%d %d\n", x, y);
    return 0;
}
```

Output:

```
20 15
```

Why? `y` was calculated when `x` was `10`. Changing `x` later does not automatically recalculate `y`.

### 2.4 Rules for naming variables

Valid names:

```
int age;
int student_marks;
int marks2;
int _count;
```

Invalid names:

```
// int 2marks;    // Cannot begin with a digit
// int student marks; // Spaces are not allowed
// int float;     // float is a keyword
```

C identifiers are case-sensitive: `marks`, `Marks` and `MARKS` are three different identifiers.

### 2.5 Scope: local and global variables

A local variable is declared inside a function or block and is accessible within its scope. A global variable is declared outside functions.

```

#include <stdio.h>

int total = 100;  // Global variable

int main(void) {
    int total = 50;  // Local variable

    printf("%d\n", total);
    return 0;
}
```

Output:

```
50
```

The local variable hides the global variable with the same name within that scope.

Exam trap: An ordinary uninitialized local variable does not automatically contain zero. Reading its indeterminate value can cause undefined behaviour. Global variables and static-storage variables are initialized to zero by default if no explicit initializer is provided.

## 3. Constants

### 3.1 What is a constant?

A constant is a value that is not intended to change during program execution. C has several ways to express constant values and to restrict modification.

For example:

```
int age = 21;       // 21 is an integer constant
char grade = 'A';   // 'A' is a character constant
double pi = 3.14;   // 3.14 is a floating constant
```

### 3.2 Types of constants

|Constant type|Example|Meaning|
|---|---|---|
|Integer|`100`, `-25`|Whole-number value|
|Floating-point|`3.14`, `2.5e3`|Fractional or exponential value|
|Character|`'A'`, `'\n'`|Character constant|
|String literal|`"Hello"`|Sequence of characters ending with a null character in storage|
|Enumeration constant|`RED`|Named value from an `enum`|

A string literal uses double quotes, while a character constant uses single quotes.

```
char grade = 'A';
printf("Grade = %c\n", grade);
printf("Message = %s\n", "Hello");
```

Output:

```
Grade = A
Message = Hello
```

### 3.3 `const` versus `#define`

These are both important for objective questions.

Method A — `const`

```
#include <stdio.h>

int main(void) {
    const int MAX_MARKS = 100;

    printf("%d\n", MAX_MARKS);
    // MAX_MARKS = 90;  // Not allowed

    return 0;
}
```

Output:

```
100
```

`const` qualifies an object as non-modifiable through that identifier.

Method B — `#define`

```
#include <stdio.h>

#define MAX_MARKS 100

int main(void) {
    printf("%d\n", MAX_MARKS);
    return 0;
}
```

Output:

```
100
```

The preprocessor replaces occurrences of the macro name with its replacement text before compilation.

|`const`|`#define`|
|---|---|
|Declares a qualified object when used in a declaration|Defines a preprocessor macro|
|Has a declared type|Does not itself declare a typed object|
|Follows C scope rules|Macro replacement is governed by preprocessing and is not ordinary block-scoped variable behaviour|
|Object storage depends on context and implementation|A simple object-like macro need not allocate storage|

Exam trap: `const int x = 10;` is not the same thing as a preprocessor macro. Also, a `const` object in C is not automatically an integer constant expression usable everywhere that a C integer constant expression is required.

## 4. Keywords

### 4.1 What is a keyword?

A keyword is a reserved word with a predefined meaning in C. You cannot use a keyword as an ordinary variable or function name.

Examples:

```
int age = 21;
if (age >= 18) {
    printf("Adult\n");
}
```

Here, `int` and `if` are keywords. `age` is an identifier.

### 4.2 Important groups of C keywords

The following are standard C keywords, grouped by purpose for easier revision.

|Category|Keywords|
|---|---|
|Data types|`char`, `int`, `float`, `double`, `void`, `_Bool`|
|Type modifiers|`short`, `long`, `signed`, `unsigned`|
|Decision and loops|`if`, `else`, `switch`, `case`, `default`, `for`, `while`, `do`|
|Flow control|`break`, `continue`, `goto`, `return`|
|User-defined types|`struct`, `union`, `enum`, `typedef`|
|Qualifiers|`const`, `volatile`, `restrict`|
|Storage classes|`auto`, `extern`, `register`, `static`|
|Other important keywords|`sizeof`, `static_assert`, `inline`, `_Atomic`|

C versions introduce additional keywords. The table includes keywords from modern standard C, including C11; it is not a list of only the original C90 keywords.

### 4.3 Keyword versus identifier

```
int main(void) {
    int number = 10;
    int result = number + 5;
    return 0;
}
```

- `int`, `void`, `return`: keywords.
    
- `main`, `number`, `result`: identifiers.
    
- `10`, `5`, `0`: integer constants.
    

### 4.4 Quick rules

- Keywords are reserved and case-sensitive.
    
- `int` is a keyword; `Int` is not the same keyword.
    
- `printf` is a standard library function name, not a C keyword.
    
- `main` is not a C keyword.
    
- `#include` is a preprocessor directive, not a keyword.
    
- `true` and `false` are not traditional C keywords; standard C provides them as macros through `<stdbool.h>` in C99 through C17. C23 changes their status.
    

## 5. Operators

Operators perform calculations, comparisons, logical tests, assignments and other operations.

This is one of the most important areas for output-based MCQs.

### 5.1 Arithmetic operators

|Operator|Meaning|Example|
|---|---|---|
|`+`|Addition|`5 + 2 = 7`|
|`-`|Subtraction|`5 - 2 = 3`|
|`*`|Multiplication|`5 * 2 = 10`|
|`/`|Division|`7 / 2 = 3` for integer operands|
|`%`|Remainder|`7 % 2 = 1`|

Example:

```

#include <stdio.h>

int main(void) {
    int a = 7, b = 2;

    printf("%d\n", a / b);
    printf("%d\n", a % b);

    return 0;
}
```

Output:

```
3
1
```

C integer division truncates the fractional part toward zero. The `%` operator is used with integer operands.

### 5.2 Relational operators

These compare two values.

|Operator|Meaning|
|---|---|
|`==`|Equal to|
|`!=`|Not equal to|
|`>`|Greater than|
|`<`|Less than|
|`>=`|Greater than or equal to|
|`<=`|Less than or equal to|

```
int a = 10, b = 20;

printf("%d\n", a < b);
printf("%d\n", a == b);
```

Output:

```
1
0
```

In C, relational and equality expressions produce an integer value of `1` for true or `0` for false.

Exam trap: `=` assigns a value; `==` compares values.

### 5.3 Logical operators

| Operator | Meaning | |---|---| | `&&` | Logical AND | | `||` | Logical OR | | `!` | Logical NOT |

```
#include <stdio.h>

int main(void) {
    int age = 21;

    printf("%d\n", age >= 18 && age <= 60);
    printf("%d\n", age < 18 || age > 60);
    printf("%d\n", !0);

    return 0;
}
```

Output:

```
1
0
1
```

Logical operators use truth values: zero is false, and nonzero is true. The result is `0` or `1`.

Short-circuiting: In `A && B`, if `A` is false, `B` is not evaluated. In `A || B`, if `A` is true, `B` is not evaluated.

### 5.4 Increment and decrement

- `++x`: increment first, then use the new value.
    
- `x++`: use the old value, then increment.
    

```
#include <stdio.h>

int main(void) {
    int x = 5;

    printf("%d\n", ++x);

    x = 5;
    printf("%d\n", x++);

    printf("%d\n", x);

    return 0;
}
```

Output:

```
6
5
6
```

The difference matters when the expression's value is used. Avoid complicated expressions that modify the same variable multiple times without a sequencing guarantee.

### 5.5 Assignment operators

```
int x = 10;

x += 5;  // x = x + 5
x -= 2;  // x = x - 2
x *= 3;  // x = x * 3
x /= 2;  // x = x / 2
```

The final value is `19`.

Other compound assignment operators include `%=` and the bitwise assignments `&=`, `|=`, `^=`, `<<=` and `>>=`.

### 5.6 Bitwise operators

Bitwise operators work on integer bits, rather than treating the whole value as a single true/false condition.

For example, consider `5` and `3` in binary:

```
5 = 0101
3 = 0011
```

| Operator | Example | Result | |---|---|---| | `&` | `5 & 3` | `1` | | `|` | `5 | 3` | `7` | | `^` | `5 ^ 3` | `6` | | `<<` | `5 << 1` | `10` | | `>>` | `5 >> 1` | `2` |

```
#include <stdio.h>

int main(void) {
    printf("%d\n", 5 & 3);
    printf("%d\n", 5 | 3);
    printf("%d\n", 5 ^ 3);
    printf("%d\n", 5 << 1);
    printf("%d\n", 5 >> 1);

    return 0;
}
```

Output:

```
1
7
6
10
2
```

These examples use positive integer operands and well-defined shifts.

### 5.7 Conditional (ternary) operator

The 2017 DSSSB paper explicitly asks what the conditional operator is also called. The answer is ternary operator because it uses three operands.

Syntax:

```
condition ? expression_if_true : expression_if_false
```

Example:

```
#include <stdio.h>

int main(void) {
    int a = 15, b = 20;
    int maximum = (a > b) ? a : b;

    printf("%d\n", maximum);
    return 0;
}
```

Output:

```
20
```

Read it as: if `a > b` is true, choose `a`; otherwise choose `b`.

### 5.8 Operator precedence

Precedence determines how an expression is grouped; associativity determines grouping when operators of the same precedence occur together.

```
int result = 2 + 3 * 4;
```

Multiplication has higher precedence than addition, so `result` is `14`.

Use parentheses to make expressions clear:

```
int result = (2 + 3) * 4;  // 20
```

For exam preparation, learn the precedence order of arithmetic, shifts, relational, equality, bitwise, logical and assignment operators. Do not confuse precedence with the order in which every operand is evaluated.

## 6. Type conversion

### 6.1 What is type conversion?

Type conversion means changing a value from one data type to another.

C has two main forms:

1. Implicit conversion: Performed automatically by the language.
    
2. Explicit conversion (type casting): Requested by the programmer using a cast.
    

### 6.2 Implicit conversion

```
#include <stdio.h>

int main(void) {
    int a = 10;
    double b = a;

    printf("%d\n", a);
    printf("%.1f\n", b);

    return 0;
}
</CodeBlock>
```

Output:

```
10
10.0
```

The integer value `10` is converted to a `double` when assigned to `b`.

### 6.3 Integer division versus type conversion

This is a common exam pattern.

```
#include <stdio.h>

int main(void) {
    int a = 7, b = 2;

    printf("%d\n", a / b);
    printf("%.2f\n", (double)a / b);

    return 0;
}
```

Output:

```
3
3.50
```

Explanation:

- `a / b` performs integer division because both operands are integers.
    
- `(double)a / b` converts `a` to `double`. The other operand is then converted for the arithmetic operation, so the division produces `3.5`.
    

Important: Casting after division does not recover the lost fractional part.

```
(double)(7 / 2)  // 3.0, not 3.5
```

### 6.4 Narrowing conversion

A narrowing conversion can lose information when converting to a type with a more limited range or precision.

```
int x = 9;
int y = 2;
double result = x / y;
```

Here `result` is `4.0`, not `4.5`, because the division happens before the assignment.

Correct version:

```
double result = (double)x / y;
```

Now the result is `4.5`.

### 6.5 Character-to-integer conversion

```
#include <stdio.h>

int main(void) {
    char ch = 'A';

    printf("%c\n", ch);
    printf("%d\n", ch);

    return 0;
}
```

On an ASCII-compatible system, the output is:

```
A
65
```

The numeric result depends on the character encoding. C does not require every implementation to use ASCII.

In Python, `ord('A')` returns `65` because Python's `ord()` returns the Unicode code point. The 2024 DSSSB paper asks about this Python function, so distinguish it from C's character conversion.

### 6.6 Explicit casts

The general syntax is:

```
(type) expression
```

Examples:

```
(double)5       // 5.0
(int)3.9        // 3
(char)65        // Result depends on the execution character set
```

For conversion from floating point to integer, the fractional part is discarded toward zero when the resulting integer is representable.

### 6.7 Type conversion rules to remember

- Integer division can discard the fractional part.
    
- An assignment can implicitly convert the right-hand value to the left-hand type.
    
- A cast affects the expression it is applied to, not an earlier calculation.
    
- Converting to an unsigned type follows unsigned conversion rules; it is not the same as taking the absolute value.
    
- Out-of-range conversion to a signed integer can be implementation-defined or otherwise subject to the rules for that conversion, depending on the source type and C version.
    

## 7. Input/output in C

Input/output allows a program to receive data and display results. The standard functions are declared in the header file `stdio.h`.

### 7.1 `printf()` — displaying output

```
#include <stdio.h>

int main(void) {
    int age = 21;
    printf("My age is %d\n", age);
    return 0;
}
```

Output:

```
My age is 21
```

`printf()` displays text and formatted values.

### 7.2 `scanf()` — receiving input

```
#include <stdio.h>

int main(void) {
    int age;

    printf("Enter age: ");

    if (scanf("%d", &age) == 1) {
        printf("Your age is %d\n", age);
    }

    return 0;
}
```

If the user enters `21`, the output is:

```
Enter age: 21
Your age is 21
```

The `&age` expression gives the address of `age`, allowing `scanf()` to store the entered value there.

The condition `scanf(...) == 1` checks whether one input item was successfully assigned.

### 7.3 Why do we use `&` in `scanf()`?

Compare these two expressions:

- `age` means the current value of the variable.
    
- `&age` means the address of the variable.
    

For a normal integer variable, `scanf("%d", &age)` is the correct pattern.

### 7.4 Important exception: character arrays

For a character array, you normally do not use `&` with `%s`.

```
#include <stdio.h>

int main(void) {
    char name[20];

    if (scanf("%19s", name) == 1) {
        printf("Hello, %s\n", name);
    }

    return 0;
}
```

If the input is `Sarthak`, the output is:

```
Hello, Sarthak
```

The width `19` limits how many characters are read, leaving space for the terminating `'\0'` character in the 20-element array. `%s` reads only up to whitespace.

### 7.5 Escape sequences

|Sequence|Meaning|
|---|---|
|`\n`|New line|
|`\t`|Horizontal tab|
|`\\`|Backslash|
|`\"`|Double quote|
|`\0`|Null character|

Example:

```
printf("Hello\nWorld\n");
```

Output:

```
Hello
World
```

### 7.6 Character input

```
#include <stdio.h>

int main(void) {
    char ch;

    if (scanf(" %c", &ch) == 1) {
        printf("Character: %c\n", ch);
    }

    return 0;
}
```

The leading space in `" %c"` tells `scanf()` to skip leading whitespace, including a newline left over from earlier input.

Exam trap: `%c` normally reads the next character, even if that character is a space or newline. `" %c"` behaves differently because of the leading whitespace directive.

### 7.7 Input/output functions to know

|Function|Purpose|
|---|---|
|`printf()`|Formatted output|
|`scanf()`|Formatted input|
|`getchar()`|Reads one character|
|`putchar()`|Writes one character|
|`puts()`|Writes a string followed by a newline|
|`fgets()`|Reads a line or bounded string from a stream|
|`sprintf()`|Formats output into a character array|
|`snprintf()`|Formats output into a bounded character array|

Prefer `fgets()` for reading a line containing spaces, and use bounded formatting functions where appropriate.

## 8. Format specifiers

Format specifiers are a particularly important part of C input/output and are directly relevant to the `%ld` question in your 2017 paper.

### 8.1 What is a format specifier?

A format specifier is a directive in a formatted input/output string that specifies how a value is interpreted or displayed.

For example:

```
int age = 21;
printf("%d", age);
```

`%d` tells `printf()` to format the argument as a signed decimal integer.

### 8.2 Important `printf()` format specifiers

|Specifier|Typical use in `printf()`|
|---|---|
|`%d` or `%i`|`int`|
|`%u`|`unsigned int`|
|`%ld`|`long int`|
|`%lu`|`unsigned long int`|
|`%lld`|`long long int`|
|`%llu`|`unsigned long long int`|
|`%c`|Character promoted to `int`|
|`%s`|Null-terminated character string|
|`%f`|`double` argument|
|`%e`|Exponential notation for floating point|
|`%g`|Compact floating-point representation|
|`%p`|Pointer, with argument converted to `void *` for portable use|
|`%zu`|`size_t`|
|`%%`|Literal percent sign|

Crucial distinction: In `printf()`, a `float` argument is promoted to `double`, so `%f` is used for both a `float` value and a `double` value.

### 8.3 `printf()` versus `scanf()`

This is one of the easiest places to make a mistake.

|Data type|`printf()`|`scanf()`|
|---|---|---|
|`int`|`%d`|`%d`|
|`unsigned int`|`%u`|`%u`|
|`long int`|`%ld`|`%ld`|
|`long long int`|`%lld`|`%lld`|
|`float`|`%f`|`%f`|
|`double`|`%f`|`%lf`|
|`long double`|`%Lf`|`%Lf`|
|Character|`%c`|`%c`|
|String|`%s`|`%s`|

In `scanf()`, `%f` expects a `float *`, whereas `%lf` expects a `double *`. In `printf()`, `%f` expects a `double`; `%lf` is also permitted and has the same meaning as `%f` in modern standard C.

### 8.4 Complete example

```

#include <stdio.h>

int main(void) {
    int age = 21;
    long int population = 1000000L;
    float percentage = 87.5f;
    double pi = 3.14159;
    char grade = 'A';
    char city[] = "Delhi";

    printf("Age: %d\n", age);
    printf("Population: %ld\n", population);
    printf("Percentage: %.1f\n", percentage);
    printf("Pi: %.2f\n", pi);
    printf("Grade: %c\n", grade);
    printf("City: %s\n", city);

    return 0;
}
```

Output:

```
Age: 21
Population: 1000000
Percentage: 87.5
Pi: 3.14
Grade: A
City: Delhi
```

### 8.5 Precision and width

Format specifiers can also control the displayed width and precision.

Output:

- `%.2f`: display two digits after the decimal point.
    
- `%8d`: use a minimum field width of eight characters, padding with spaces by default.
    
- `%05d`: use a minimum field width of five characters, padding with zeros for this positive number.
    

A width is a minimum, not a maximum: longer values are not automatically truncated.

### 8.6 Common format-specifier mistakes

- Using `%d` for a `long int` in `printf()`.
    
- Using `%f` with a `double *` in `scanf()` instead of `%lf`.
    
- Forgetting `&` when reading into a normal integer variable.
    
- Using `%s` with a non-null-terminated character array.
    
- Passing an argument whose type does not match the format directive.
    

Mismatched format directives can produce undefined behaviour. Do not treat them as harmless display errors.