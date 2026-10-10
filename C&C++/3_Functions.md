# C Programming: Functions — Complete DSSSB TGT Computer Science Notes

Functions are an important topic in C programming. For your DSSSB preparation, understand not only the definitions but also output-based questions, declaration vs definition, parameters vs arguments, recursion, and scope rules.

## 1. What is a function?

A function is a named block of code that performs a particular task. You can call it whenever you need that task instead of writing the same code repeatedly.

Think of a function like a machine:

Input — arguments

Function — performs a task

Output — return value, if any

For example, a function can accept two numbers and return their sum.

```

#include <stdio.h>

int add(int a, int b)
{
    return a + b;
}

int main(void)
{
    int result = add(10, 20);
    printf("%d\n", result);

    return 0;
}
```

Output

```
30
```

Here:

- `int` before `add` specifies its return type.
    
- `add` is the function name.
    
- `int a, int b` are parameters.
    
- `return a + b;` sends the result back to the caller.
    
- `add(10, 20)` calls the function.
    
- `result` stores the returned value.
    

## 2. Function declaration (prototype)

A function declaration informs the compiler about the function's name, return type, and parameter types before the function is used.

Syntax:

```
return_type function_name(parameter_types);
```

Example:

```

#include <stdio.h>

int add(int, int);  // Function declaration

int main(void)
{
    printf("%d\n", add(5, 3));
    return 0;
}

int add(int a, int b)
{
    return a + b;
}
```

Output

```
8
```

Important points:

- A prototype normally ends with a semicolon.
    
- Parameter names are optional in a prototype: `int add(int, int);` is valid.
    
- The compiler uses the declaration to check calls made before the definition appears.
    
- In modern C, don't rely on calling a function without a proper declaration.
    

## 3. Function definition

A function definition contains the actual code that performs the task.

Syntax:

```
return_type function_name(parameters)
{
    // Statements
    return value;
}
```

Example:

```
int multiply(int a, int b)
{
    return a * b;
}
```

This is a definition because it includes the function body.

### Declaration vs definition

|Function declaration|Function definition|
|---|---|
|Announces the function's interface|Implements the function|
|Usually ends with `;`|Has a body inside `{ }`|
|Body is absent|Body is present|
|Example: `int square(int);`|Example: `int square(int x) { return x*x; }`|

Exam trap: A function definition also provides a declaration of that function, but a declaration by itself does not provide the implementation.

## 4. Function calling

A function call transfers control to the function so its statements can execute.

Example:

```

#include <stdio.h>

void greet(void)
{
    printf("Hello!\n");
}

int main(void)
{
    printf("Start\n");
    greet();
    printf("End\n");

    return 0;
}
```

Output

```
Start
Hello!
End
```

Execution order:

1. `main()` begins.
    
2. `Start` is printed.
    
3. `greet()` is called.
    
4. Control enters `greet()` and prints `Hello!`.
    
5. Control returns to `main()`.
    
6. `End` is printed.
    

The function `greet` uses `void` as its return type because it does not return a value. The `void` inside `greet(void)` means it takes no parameters.

## 5. Parameters and arguments

These terms are often confused in MCQs.

- Parameters (formal parameters): Variables listed in the function definition that receive input.
    
- Arguments (actual arguments): Values or expressions supplied when the function is called.
    

```

#include <stdio.h>

int subtract(int x, int y)
{
    return x - y;
}

int main(void)
{
    int answer = subtract(10, 4);
    printf("%d\n", answer);

    return 0;
}
```

Output

```
6
```

In `int subtract(int x, int y)`, `x` and `y` are parameters.

In `subtract(10, 4)`, `10` and `4` are arguments.

### Call by value in C

C passes ordinary arguments by value. The function receives copies of the argument values, so changing a parameter does not directly change the original variable.

```

#include <stdio.h>

void change(int x)
{
    x = 100;
}

int main(void)
{
    int n = 10;
    change(n);
    printf("%d\n", n);

    return 0;
}
```

Output

```
10
```

Why? `x` is a separate local variable initialized with a copy of `n`. Changing `x` does not change `n`.

To modify the caller's variable, you can pass its address using a pointer.

```

#include <stdio.h>

void change(int *x)
{
    *x = 100;
}

int main(void)
{
    int n = 10;
    change(&n);
    printf("%d\n", n);

    return 0;
}
```

Output

```
100
```

Here, `&n` provides the address of `n`, and `*x = 100` modifies the value stored at that address. Technically, C still passes the pointer value by value; the pointer allows the function to access the original object.

## 6. Return value

A return value is the result a function sends back to its caller using the `return` statement.

### Example A: Function returns an integer

```
int square(int n)
{
    return n * n;
}
```

Calling `square(4)` produces the value `16`.

### Example B: Function returns nothing

```

#include <stdio.h>

void display(void)
{
    printf("DSSSB TGT\n");
}

int main(void)
{
    display();
    return 0;
}
```

Output

```
DSSSB TGT
```

A `void` function does not return a value. It may use `return;` to exit early, but it must not return a value.

### Example C: Return ends the function

```

#include <stdio.h>

int test(void)
{
    printf("A\n");
    return 5;
    printf("B\n");
}

int main(void)
{
    printf("%d\n", test());
    return 0;
}
```

Output

```
A
5
```

`B` is not printed because execution leaves `test()` at `return 5;`.

Exam traps

- `return` sends a value back and ends that function's execution.
    
- `printf()` displays a value; `return` sends a value to the caller.
    
- The returned value should match the function's declared return type, subject to C's conversion rules.
    
- A non-`void` function should return a value of the appropriate type on every path where its caller needs a result. Reaching the end of `main()` is a special case: it is equivalent to returning `0`.
    

## 7. Recursion

Recursion occurs when a function calls itself, either directly or indirectly.

A recursive function generally needs two things:

1. Base case: Stops recursion.
    
2. Recursive case: Calls the function again with a smaller or otherwise progressing problem.
    

### Example: Factorial

Factorial of a positive integer \(n\) is:

\[ n! = n \times (n-1) \times \cdots \times 1 \]

For example, \(5! = 5 \times 4 \times 3 \times 2 \times 1 = 120\).

```

#include <stdio.h>

int factorial(int n)
{
    if (n <= 1)       // Base case
        return 1;

    return n * factorial(n - 1);  // Recursive case
}

int main(void)
{
    printf("%d\n", factorial(5));
    return 0;
}
```

Output

```
120
```

### How the recursion works

`factorial(5)`

`5 × factorial(4)`

`4 × factorial(3)`

`3 × factorial(2)`

`2 × factorial(1)`

`factorial(1) = 1`

The base case returns 1; the pending multiplications then resolve to 120.

The calculation unwinds as follows:

- `factorial(1)` returns `1`.
    
- `factorial(2)` returns `2 × 1 = 2`.
    
- `factorial(3)` returns `3 × 2 = 6`.
    
- `factorial(4)` returns `4 × 6 = 24`.
    
- `factorial(5)` returns `5 × 24 = 120`.
    

### What happens without a base case?

If a function keeps calling itself without reaching a stopping condition, it can recurse indefinitely until resources are exhausted, commonly resulting in a stack overflow.

### Recursion vs iteration

|Recursion|Iteration|
|---|---|
|Function calls itself|Uses loops such as `for` or `while`|
|Uses function-call stack frames|Usually uses loop control and local variables|
|Can be natural for tree traversal and divide-and-conquer problems|Often simpler for straightforward repetition|
|May incur additional call overhead|Often has lower overhead for simple repeated operations|

Exam tip: For recursive output questions, write down every function call and then trace the return values in reverse order.

## 8. Scope of variables

Scope means the region of a program where an identifier, such as a variable, can be accessed by its name.

For DSSSB, focus on local scope, global scope, block scope, and variable lifetime.

### A. Local variable

A variable declared inside a function is local to that function.

```

#include <stdio.h>

void display(void)
{
    int x = 10;
    printf("%d\n", x);
}

int main(void)
{
    display();
    return 0;
}
```

Output

```
10
```

Here, `x` can be accessed inside `display()`, but not directly inside `main()`.

### B. Global variable

A variable declared outside all functions, at file scope, is commonly called a global variable.

```

#include <stdio.h>

int x = 50;

void display(void)
{
    printf("%d\n", x);
}

int main(void)
{
    display();
    printf("%d\n", x);
    return 0;
}
```

Output

```
50
50
```

Both functions can access this file-scope variable because it is declared before their use.

### C. Block scope

A variable declared inside a block `{ }` is generally visible from its declaration to the end of that block.

```

#include <stdio.h>

int main(void)
{
    int x = 10;

    {
        int y = 20;
        printf("%d %d\n", x, y);
    }

    printf("%d\n", x);
    return 0;
}
```

Output

```
10 20
10
```

`y` exists only within the inner block. Trying to use `y` after that block would cause a compilation error.

### D. Same variable name in nested scopes

A local variable can hide a variable with the same name from an outer scope. This is called shadowing.

```

#include <stdio.h>

int x = 10;

int main(void)
{
    int x = 20;

    {
        int x = 30;
        printf("%d\n", x);
    }

    printf("%d\n", x);
    return 0;
}
```

Output

```
30
20
```

Why?

- The inner block's `x` is `30`.
    
- Outside the inner block, `main()`'s `x` is `20`.
    
- The global `x` remains `10`, but it is hidden by the local declarations in these regions.
    

### Scope vs lifetime

These terms are related but different.

- Scope: Where the name can be used.
    
- Lifetime (storage duration): How long the object exists in memory during program execution.
    

For example, a normal local variable usually has block scope and automatic storage duration. A global variable has file scope and static storage duration.

### Quick comparison

|Variable|Where declared|Typical scope|Typical lifetime|
|---|---|---|---|
|Local|Inside a function or block|Function/block region|During its block execution|
|Global|Outside functions|File scope|Entire program execution|
|`static` local|Inside a function or block|Local block|Entire program execution|

### E. Static local variable

A `static` local variable retains its value between function calls.

```

#include <stdio.h>

void count(void)
{
    static int x = 0;
    x++;
    printf("%d\n", x);
}

int main(void)
{
    count();
    count();
    count();
    return 0;
}
```

Output

```
1
2
3
```

Compare this with an ordinary local variable:

```

#include <stdio.h>

void count(void)
{
    int x = 0;
    x++;
    printf("%d\n", x);
}

int main(void)
{
    count();
    count();
    count();
    return 0;
}
```

Output

```
1
1
1
```

The ordinary local variable is initialized again each time `count()` is called. The static local variable is initialized only once and retains its value.

## 9. Complete function example

This example combines declaration, definition, calling, parameters, return value, and local scope.

```

#include <stdio.h>

// Declaration
int maximum(int a, int b);

int main(void)
{
    int first = 25;
    int second = 40;

    // Function call
    int result = maximum(first, second);

    printf("Maximum = %d\n", result);
    return 0;
}

// Definition
int maximum(int a, int b)
{
    if (a > b)
        return a;

    return b;
}
```

Output

```
Maximum = 40
```

Remember:

- `int maximum(int a, int b);` — declaration.
    
- `maximum(first, second)` — function call.
    
- `first` and `second` — arguments.
    
- `a` and `b` — parameters.
    
- `return a;` and `return b;` — return values.
    
- `a` and `b` are local to `maximum()`.
    

## 10. DSSSB exam revision sheet

|Concept|Remember this|
|---|---|
|Declaration|Announces function interface; normally ends in `;`|
|Definition|Contains the function body|
|Calling|Transfers control to the function|
|Parameters|Variables receiving input|
|Arguments|Values/expressions supplied in a call|
|Return value|Result sent to caller|
|`void` return type|Function does not return a value|
|Recursion|Function calls itself directly or indirectly|
|Base case|Stops recursive calls|
|Local scope|Name is accessible only in its permitted local region|
|Global variable|Declared outside all functions|
|`static` local|Retains value between calls|
|C argument passing|Arguments are passed by value|

