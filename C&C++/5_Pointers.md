# C Programming: Pointers — Complete DSSSB TGT Computer Science Notes

Pointers are one of the most important C programming topics because they connect variables, memory addresses, arrays, and functions. For DSSSB preparation, focus on understanding memory diagrams, tracing outputs, pointer arithmetic, and the difference between `p` and `*p`.

We will cover your six topics:

1. Pointer basics
    
2. Address operator (`&`)
    
3. Dereference operator (`*`)
    
4. Pointer arithmetic
    
5. Arrays and pointers
    
6. Functions and pointers
    

## 1. Pointer basics

A pointer is a variable that stores the memory address of an object.

Ordinary variables store values. Pointer variables store addresses.

Ordinary variable

## x = 10

Stores the integer value 10

Pointer variable

## p = &x

Stores the address of x

The actual memory addresses depend on the program and system. These are conceptual relationships, not real addresses.

### A. Pointer declaration

Syntax:

```
data_type *pointer_name;
```

Examples:

```
int *p;
float *q;
char *r;
```

- `int *p;` declares `p` as a pointer to an `int`.
    
- `float *q;` declares `q` as a pointer to a `float`.
    
- `char *r;` declares `r` as a pointer to a `char`.
    

The pointer's type tells C what kind of object it points to and how operations such as dereferencing should interpret that object.

### B. First complete pointer program

```

#include <stdio.h>

int main(void)
{
    int x = 10;
    int *p = &x;

    printf("x = %d\n", x);
    printf("*p = %d\n", *p);

    return 0;
}
```

Output

```
x = 10
*p = 10
```

Why are both values `10`?

- `x` contains `10`.
    
- `p` stores the address of `x`.
    
- `*p` accesses the integer stored at that address, which is `10`.
    

Remember this relationship:

\[ p = \&x \quad \Longrightarrow \quad *p = x \]

This relationship holds while `p` validly points to `x`.

### C. Understanding the declaration `int *p`

Consider:

```
int x = 10;
int *p = &x;
```

Here, the `*` in `int *p` indicates that `p` is a pointer to an integer. In an expression such as `*p`, the `*` instead acts as the dereference operator.

Be careful with declarations involving multiple variables:

```
int *p, q;
```

Only `p` is a pointer. `q` is an ordinary `int`.

To declare both as pointers, write:

```
int *p, *q;
```

Exam trap: The `*` belongs to each declarator, not automatically to every variable in the declaration.

## 2. Address operator (`&`)

The address-of operator `&` gives the memory address of an object.

Example:

```
int x = 25;
printf("%p", (void *)&x);
```

This prints the address of `x`. The actual address varies between program runs and systems.

To store that address in a pointer:

```
int x = 25;
int *p = &x;
```

The `&x` expression produces the address of `x`, and `p` stores that address.

### A. Address operator with multiple variables

```

#include <stdio.h>

int main(void)
{
    int a = 10;
    int b = 20;

    printf("%p\n", (void *)&a);
    printf("%p\n", (void *)&b);

    return 0;
}
```

Output: Two address representations, which will depend on the execution environment.

You should not predict exact addresses in an MCQ unless they are explicitly given in the question.

### B. Why does `scanf()` use `&`?

```

#include <stdio.h>

int main(void)
{
    int age;

    scanf("%d", &age);
    printf("%d\n", age);

    return 0;
}
```

If the input is `21`, the output is:

```
21
```

`scanf()` needs the address of `age` so it can write the entered integer into that variable.

Compare:

- `age` is the integer value.
    
- `&age` is the address of the integer variable.
    

For `%d`, `scanf()` expects an `int *` argument, which is why `&age` is used.

## 3. Dereference operator (`*`)

The dereference operator `*` accesses the object to which a valid pointer points.

Suppose:

```
int x = 10;
int *p = &x;
```

Then:

- `p` is the address of `x`.
    
- `*p` is the value stored in `x`.
    
- `&x` is the address of `x`.
    

### A. Read a value through a pointer

```

#include <stdio.h>

int main(void)
{
    int x = 50;
    int *p = &x;

    printf("%d\n", *p);

    return 0;
}
```

Output

```
50
```

`*p` follows the pointer to the object and reads its value.

### B. Modify a variable through a pointer

```

#include <stdio.h>

int main(void)
{
    int x = 10;
    int *p = &x;

    *p = 99;

    printf("%d\n", x);

    return 0;
}
```

Output

```
99
```

This line is the key:

```
*p = 99;
```

It means: store `99` in the object pointed to by `p`. Because `p` points to `x`, the value of `x` changes.

### C. Pointer tracing — very important for MCQs

```

#include <stdio.h>

int main(void)
{
    int x = 5;
    int *p = &x;

    *p = *p + 3;
    printf("%d %d\n", x, *p);

    return 0;
}
```

Output

```
8 8
```

Trace:

|Step|`x`|`p` points to|`*p`|
|---|---|---|---|
|Initially|5|`x`|5|
|After `*p = *p + 3`|8|`x`|8|

Since `*p` accesses `x`, adding 3 through `*p` changes `x`.

### D. Uninitialized pointers — a major trap

```
int *p;
*p = 10;  // Undefined behavior
```

This is unsafe because `p` has not been initialized to a valid address. Dereferencing it may crash the program or corrupt memory.

Safe alternative:

```
int x;
int *p = &x;
*p = 10;
```

Now `p` points to a valid integer object, and the assignment initializes `x` to `10`.

A null pointer is also not dereferenceable:

```
int *p = NULL;
// *p = 10;  // Undefined behavior
```

Remember: Declaring a pointer does not automatically make it point to a valid object.

## 4. Pointer arithmetic

Pointer arithmetic means moving a pointer between elements of an array or, more generally, within the same array object and its one-past-the-end position.

For an `int *p`, the expression `p + 1` advances by one `int` element, not necessarily one byte.

If `sizeof(int)` is 4 on a particular system, advancing by one `int` moves the address by 4 bytes. The size of `int` is implementation-dependent.

### A. Basic pointer arithmetic

```

#include <stdio.h>

int main(void)
{
    int a[] = {10, 20, 30};
    int *p = a;

    printf("%d\n", *p);
    printf("%d\n", *(p + 1));
    printf("%d\n", *(p + 2));

    return 0;
}
```

Output

```
10
20
30
```

Because `p` points to the first element:

- `*p` is `a[0]`.
    
- `*(p + 1)` is `a[1]`.
    
- `*(p + 2)` is `a[2]`.
    

For a pointer to an array element, moving forward by one advances to the next element.

Conceptual pointer movement

## 10

a[0]

p

## 20

a[1]

p + 1

## 30

a[2]

p + 2

Pointer arithmetic is scaled by the size of the pointed-to type.

### B. Incrementing a pointer

```

#include <stdio.h>

int main(void)
{
    int a[] = {100, 200, 300};
    int *p = a;

    printf("%d\n", *p);

    p++;

    printf("%d\n", *p);

    return 0;
}
```

Output

```
100
200
```

Initially, `p` points to `a[0]`. After `p++`, it points to `a[1]`.

Notice the difference:

- `p++` moves the pointer.
    
- `(*p)++` increments the value currently pointed to.
    

For example:

```
int x = 10;
int *p = &x;

(*p)++;
printf("%d\n", x);
```

Output:

```
11
```

### C. Pointer addition and subtraction

If `p` points to the first element of an array:

- `p + 2` points two elements forward.
    
- `p - 1` points one element backward only when the resulting pointer remains within the same array or its one-past boundary rules; dereferencing an invalid position is not allowed.
    
- `p2 - p1` gives the difference in element positions when both pointers point into the same array (or one past it), with a result of type `ptrdiff_t`.
    

Example:

```

#include <stdio.h>
#include <stddef.h>

int main(void)
{
    int a[] = {10, 20, 30, 40};
    int *p = &a[1];
    int *q = &a[3];

    printf("%td\n", q - p);

    return 0;
}
```

Output

```
2
```

`q` points to index 3, and `p` points to index 1. Their difference is `3 - 1 = 2` elements, not bytes.

### D. Which pointer operations are valid?

|Operation|Meaning|
|---|---|
|`p++`|Move to the next element position|
|`p--`|Move to the previous element position|
|`p + n`|Move forward by `n` elements|
|`p - n`|Move backward by `n` elements|
|`q - p`|Difference in elements, for pointers into the same array|
|`p + q`|Invalid: adding two pointers is not allowed|
|`p * 2`|Invalid: multiplying a pointer is not allowed|

Exam trap: A pointer may be formed to one position past the last element of an array, but that pointer must not be dereferenced.

## 5. Arrays and pointers

Arrays and pointers are closely related in C, but an array is not the same thing as a pointer.

In most expressions, an array name is converted to a pointer to its first element. There are exceptions, such as when the array is used with `sizeof` or unary `&`.

### A. Array name and pointer

```

#include <stdio.h>

int main(void)
{
    int a[] = {10, 20, 30};
    int *p = a;

    printf("%d\n", a[0]);
    printf("%d\n", *a);
    printf("%d\n", *p);

    return 0;
}
```

Output

```
10
10
10
```

Why do all three print the same value?

- `a[0]` accesses the first element.
    
- `*a` dereferences the pointer obtained when `a` converts to a pointer to its first element.
    
- `*p` accesses the first element because `p = a`.
    

### B. Relationship between array indexing and pointers

A key C rule is:

\[ a[i] \equiv *(a+i) \]

For example:

```
int a[] = {10, 20, 30};

printf("%d\n", a[1]);
printf("%d\n", *(a + 1));
```

Both print:

```
20
```

Similarly, `i[a]` is also defined by the language's indexing rule as `*(i + a)`, though it is unusual and should generally be avoided in normal code.

### C. Using a pointer to traverse an array

```

#include <stdio.h>

int main(void)
{
    int a[] = {5, 10, 15, 20};
    int *p = a;

    for (int i = 0; i < 4; i++)
    {
        printf("%d ", *(p + i));
    }

    return 0;
}
```

Output

```
5 10 15 20
```

The expression `*(p + i)` reads the element at offset `i` from the location where `p` points.

### D. Pointer notation vs array notation

|Array notation|Equivalent pointer expression|
|---|---|
|`a[0]`|`*(a + 0)`|
|`a[1]`|`*(a + 1)`|
|`a[2]`|`*(a + 2)`|
|`&a[0]`|`a` after array-to-pointer conversion|
|`a[i]`|`*(a + i)`|

### E. Important difference between an array and a pointer

```

#include <stdio.h>

int main(void)
{
    int a[] = {10, 20, 30};
    int *p = a;

    printf("%zu\n", sizeof(a));
    printf("%zu\n", sizeof(p));

    return 0;
}
```

The exact output depends on the implementation. On a common system where `int` is 4 bytes and a pointer is 8 bytes, the output is:

```
12
8
```

Why?

- `sizeof(a)` is the total size of the three integers: `3 * sizeof(int)`.
    
- `sizeof(p)` is the size of the pointer itself, not the size of the array it points to.
    

Do not assume all pointers are 8 bytes. Pointer size is implementation-dependent.

Also, you can assign a different address to `p` later, but you cannot assign a new array address to the array name `a`:

```
p = &a[1];  // Valid
// a = &a[1];  // Invalid
```

### F. Passing an array to a function

When an array is used as a function parameter, the parameter is adjusted to a pointer parameter.

```

#include <stdio.h>

void printArray(int a[], int n)
{
    for (int i = 0; i < n; i++)
        printf("%d ", a[i]);
}

int main(void)
{
    int numbers[] = {2, 4, 6, 8};

    printArray(numbers, 4);

    return 0;
}
```

Output

```
2 4 6 8
```

Inside a function, `int a[]` as a parameter is effectively `int *a`. The function does not automatically know the array's length, which is why `n` is passed separately.

## 6. Functions and pointers

Pointers are especially useful with functions when you need to modify a caller's variable, work with arrays efficiently, or pass addresses of objects.

### A. Passing a pointer to a function

First, remember: C passes arguments by value. When you pass a pointer, the function receives a copy of the address, but that address can still let it access the original object.

```

#include <stdio.h>

void update(int *p)
{
    *p = 100;
}

int main(void)
{
    int x = 10;

    update(&x);

    printf("%d\n", x);

    return 0;
}
```

Output

```
100
```

Step by step:

1. `x` is initialized to `10`.
    
2. `update(&x)` passes the address of `x`.
    
3. Parameter `p` receives that address.
    
4. `*p = 100` changes the original variable.
    
5. `main()` prints `100`.
    

### B. Swapping two numbers using pointers

This is a classic function-and-pointer problem.

```

#include <stdio.h>

void swap(int *a, int *b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

int main(void)
{
    int x = 10;
    int y = 20;

    swap(&x, &y);

    printf("x = %d, y = %d\n", x, y);

    return 0;
}
```

Output

```
x = 20, y = 10
```

How it works:

- `temp = *a` saves the original value of `x`, which is `10`.
    
- `*a = *b` puts `20` into `x`.
    
- `*b = temp` puts `10` into `y`.
    

Without pointers, a function that receives only two ordinary integer arguments would modify only its local copies.

### C. Returning a value through a pointer parameter

A function can return an integer normally and also modify an object through a pointer.

```

#include <stdio.h>

int divide(int a, int b, int *remainder)
{
    *remainder = a % b;
    return a / b;
}

int main(void)
{
    int r;
    int q = divide(17, 5, &r);

    printf("Quotient = %d\n", q);
    printf("Remainder = %d\n", r);

    return 0;
}
```

Output

```
Quotient = 3
Remainder = 2
```

This function returns the quotient and stores the remainder through the pointer parameter. In real code, the divisor must be checked to ensure it is not zero.

### D. Pointer to a function vs function that takes a pointer

These are different concepts:

Function that takes a pointer:

```
void update(int *p);
```

This function accepts an integer pointer.

Pointer to a function:

```
int (*operation)(int, int);
```

This declares `operation` as a pointer to a function that accepts two `int` parameters and returns an `int`.

Example:

```

#include <stdio.h>

int add(int a, int b)
{
    return a + b;
}

int main(void)
{
    int (*operation)(int, int) = add;

    printf("%d\n", operation(4, 6));

    return 0;
}
```

Output

```
10
```

Here, `operation` points to the function `add`, and `operation(4, 6)` calls that function through the pointer.

Exam trap: In `int (*operation)(int, int)`, the parentheses around `*operation` matter. Without them, `int *operation(int, int)` declares a function returning an integer pointer, not a pointer to a function.

## 7. Pointer mistakes to avoid in the exam

|Incorrect or risky code|Why?|
|---|---|
|`int *p; *p = 10;`|Pointer is uninitialized|
|`int x = 5; int *p = &x; p = 10;`|Integer `10` is not a valid pointer assignment|
|`int a[3] = {1,2,3}; a[3]`|Out-of-bounds access|
|`p + q`|Adding two pointers is not allowed|
|`int *p = NULL; *p`|Dereferencing a null pointer is undefined behavior|
|`int *p = &x; *p = 20;`|Valid if `x` is a live, writable `int` object|

## 8. Quick revision sheet

|Symbol or expression|Meaning|
|---|---|
|`&x`|Address of `x`|
|`int *p`|Declare `p` as a pointer to `int`|
|`*p`|Access the object pointed to by `p`|
|`p++`|Move pointer to the next element position|
|`(*p)++`|Increment the pointed-to value|
|`p + 1`|Advance by one element of the pointed-to type|
|`a[i]`|Equivalent to `*(a + i)`|
|`int *p = a`|Point to the first element of array `a`|
|`void update(int *p)`|Function accepts an integer pointer|
|`int (*f)(int,int)`|Pointer to a function accepting two integers and returning an integer|