# C Programming: Control Flow — Complete Guide for DSSSB TGT Computer Science

Control flow determines which statement executes, when a statement executes, and how many times a block of code repeats.

For your DSSSB exam, learn each concept in three ways:

1. Understand the syntax and purpose.
    
2. Trace the code line by line to predict the output.
    
3. Recognize common MCQ traps, such as off-by-one errors, missing `break`, and the difference between `while` and `do-while`.
    

We'll cover all nine topics in your syllabus using C code, expected outputs, and exam-oriented explanations.

## 1. `if` statement

### What is `if`?

The `if` statement executes a block of code only when a condition is true.

Syntax:

```
if (condition) {
    // Executes when condition is true
}
```

In C, a condition evaluates as false when its value is zero and true when its value is nonzero.

### Example: Check whether a student passed

```

#include <stdio.h>

int main(void) {
    int marks = 75;

    if (marks >= 40) {
        printf("Pass\n");
    }

    printf("Exam completed\n");

    return 0;
}
```

Output:

```
Pass
Exam completed
```

How it works:

- `marks >= 40` evaluates to true because `75 >= 40`.
    
- Therefore, `printf("Pass\n")` executes.
    
- The statement after the `if` executes regardless of the condition.
    

### What if the condition is false?

```
int marks = 30;

if (marks >= 40) {
    printf("Pass\n");
}

printf("Exam completed\n");
```

Output:

```
Exam completed
```

The `Pass` message is skipped, but the next statement still executes.

### Important exam traps

- `if (x = 5)` performs an assignment, not a comparison. The assigned value is 5, which is nonzero, so the condition is true.
    
- `if (x == 5)` checks equality.
    
- Braces `{}` are optional for a single statement, but recommended to avoid mistakes.
    
- A semicolon immediately after `if (condition)` creates an empty controlled statement and can change the program's behavior.
    

## 2. `if-else` statement

### What is `if-else`?

`if-else` allows a program to choose between two alternatives.

Syntax:

```
if (condition) {
    // Executes when true
} else {
    // Executes when false
}
```

### Example: Even or odd

```

#include <stdio.h>

int main(void) {
    int number = 7;

    if (number % 2 == 0) {
        printf("Even\n");
    } else {
        printf("Odd\n");
    }

    return 0;
}
```

Output:

```
Odd
```

Explanation:

- `number % 2` calculates the remainder after division by 2.
    
- For `7`, the remainder is `1`.
    
- The condition `number % 2 == 0` is false.
    
- Therefore, the `else` block executes.
    

### Example: Positive or non-positive

```
int number = 0;

if (number > 0) {
    printf("Positive");
} else {
    printf("Zero or negative");
}
```

Output:

```
Zero or negative
```

Notice that this program does not distinguish zero from negative numbers; the `else` block handles both.

### `if` versus `if-else`

|`if`|`if-else`|
|---|---|
|Executes a block when the condition is true|Selects between two alternatives|
|Does nothing for the false branch unless later code handles it|Executes the `else` branch when the condition is false|
|Useful for optional actions|Useful for two-way decisions|

## 3. Nested `if`

### What is nested `if`?

A nested `if` is an `if` statement inside another `if` or `else` block.

It is useful when a decision depends on another decision.

### Example: Eligibility for an exam

```

#include <stdio.h>

int main(void) {
    int age = 22;
    int marks = 75;

    if (age >= 18) {
        if (marks >= 40) {
            printf("Eligible\n");
        } else {
            printf("Insufficient marks\n");
        }
    } else {
        printf("Underage\n");
    }

    return 0;
}
```

Output:

```
Eligible
```

Execution flow:

Check `age >= 18`

True

Check `marks >= 40`

False

Print `Underage`

If the inner condition is true, print `Eligible`; otherwise print `Insufficient marks`.

### The dangling `else` trap

Consider:

```
int x = 5, y = 10;

if (x > 0)
    if (y > 0)
        printf("A");
    else
        printf("B");
```

Output:

```
A
```

The `else` belongs to the nearest unmatched `if`, which is `if (y > 0)`.

This is a classic C syntax question. Use braces to make the intended association clear.

### When should you use nested `if`?

Use it when the second decision should only be considered after the first condition is satisfied. If there are several mutually exclusive alternatives, an `if-else-if` ladder may be easier to read.

## 4. `switch` statement

### What is `switch`?

The `switch` statement selects a block of code based on the value of an integral expression, such as an integer, character, or enumeration value.

It is useful when one variable is compared against several fixed values.

Syntax:

```
switch (expression) {
    case constant1:
        // Statements
        break;

    case constant2:
        // Statements
        break;

    default:
        // If no case matches
}
```

### Example: Menu selection

```

#include <stdio.h>

int main(void) {
    int choice = 2;

    switch (choice) {
        case 1:
            printf("Add\n");
            break;

        case 2:
            printf("Subtract\n");
            break;

        case 3:
            printf("Multiply\n");
            break;

        default:
            printf("Invalid choice\n");
    }

    return 0;
}
```

Output:

```
Subtract
```

Since `choice` is `2`, execution jumps to `case 2`. The `break` statement then exits the `switch`.

### Why is `break` important in `switch`?

Look at this example:

```
int x = 2;

switch (x) {
    case 1:
        printf("A ");
    case 2:
        printf("B ");
    case 3:
        printf("C ");
    default:
        printf("D ");
}
```

Output:

```
B C D
```

This is called fall-through. Once `case 2` matches, execution continues into subsequent cases because there are no `break` statements.

With `break` after each case, the output would be just `B`.

### Multiple cases can share a block

```
char grade = 'A';

switch (grade) {
    case 'A':
    case 'B':
        printf("Good result\n");
        break;

    case 'C':
        printf("Average result\n");
        break;

    default:
        printf("Other result\n");
}
```

Output:

```
Good result
```

Both `'A'` and `'B'` lead to the same block.

### Important `switch` rules for the exam

- `case` labels must use constant expressions of an appropriate integer type.
    
- Duplicate case values are not allowed.
    
- `default` is optional.
    
- `break` is optional syntactically, but omitting it may cause fall-through.
    
- In traditional C, `switch` does not directly accept floating-point or string expressions.
    
- You cannot use ranges such as `case 1 ... 5:` in standard C; that is a compiler extension in some implementations.
    

### `if-else` versus `switch`

|`if-else`|`switch`|
|---|---|
|Handles ranges and complex conditions|Handles matching integral case values|
|Supports conditions such as `marks >= 40`|Uses case labels such as `case 1:`|
|Can compare floating-point expressions|Cannot directly switch on a floating-point value|
|Does not have case fall-through|Can fall through without `break`|

# 5. `for` loop

### What is a loop?

A loop repeats a block of code while a condition permits it to continue.

The `for` loop is especially useful when the number of repetitions is known or controlled by a counter.

Syntax:

```
for (initialization; condition; update) {
    // Repeated statements
}
```

The three parts are:

1. Initialization: Runs once at the beginning.
    
2. Condition: Checked before each iteration.
    
3. Update: Runs after each iteration of the body.
    

### Example: Print numbers from 1 to 5

```

#include <stdio.h>

int main(void) {
    for (int i = 1; i <= 5; i++) {
        printf("%d ", i);
    }

    return 0;
}
```

Output:

```
1 2 3 4 5
```

### How the loop executes

|Iteration|`i`|Condition `i <= 5`|Action|
|---|---|---|---|
|1|1|True|Print 1|
|2|2|True|Print 2|
|3|3|True|Print 3|
|4|4|True|Print 4|
|5|5|True|Print 5|
|Exit check|6|False|Stop|

The update `i++` occurs after the body. After printing `5`, `i` becomes `6`, and the next condition check fails.

### Example: Sum of the first five natural numbers

```
#include <stdio.h>

int main(void) {
    int sum = 0;

    for (int i = 1; i <= 5; i++) {
        sum += i;
    }

    printf("%d\n", sum);
    return 0;
}
```

Output:

```
15
```

The loop calculates \(1+2+3+4+5=15\).

### Common `for` loop variations

Count down:

```
for (int i = 5; i >= 1; i--) {
    printf("%d ", i);
}
```

Output: `5 4 3 2 1`

Print even numbers:

```
for (int i = 2; i <= 10; i += 2) {
    printf("%d ", i);
}
```

Output: `2 4 6 8 10`

Infinite loop:

```
for (;;) {
    // Repeats until exited, for example with break
}
```

All three expressions in the `for` header are optional.

### Exam trap: Off-by-one errors

```
for (int i = 1; i < 5; i++) {
    printf("%d ", i);
}
```

Output:

```
1 2 3 4
```

The condition is `< 5`, not `<= 5`.

# 6. `while` loop

### What is `while`?

A `while` loop repeats its body as long as the condition is true.

Syntax:

```
while (condition) {
    // Repeated statements
}
```

The condition is checked before the body executes. Therefore, the body may execute zero times.

### Example: Print 1 to 5

```

#include <stdio.h>

int main(void) {
    int i = 1;

    while (i <= 5) {
        printf("%d ", i);
        i++;
    }

    return 0;
}
```

Output:

```
1 2 3 4 5
```

This produces the same output as the earlier `for` loop.

### How it works

1. Initialize `i` to `1`.
    
2. Check whether `i <= 5`.
    
3. If true, print `i`.
    
4. Increment `i`.
    
5. Repeat from the condition check.
    

### Example: What if the condition is initially false?

```
int i = 10;

while (i < 5) {
    printf("Hello");
    i++;
}
```

Output: nothing.

Since `10 < 5` is false, the body is never executed.

### Example: Sum digits using `while`

```
#include <stdio.h>

int main(void) {
    int n = 1234;
    int sum = 0;

    while (n > 0) {
        sum += n % 10;
        n /= 10;
    }

    printf("%d\n", sum);
    return 0;
}
```

Output:

```
10
```

Explanation:

- `1234 % 10` gives `4`.
    
- `123 / 10` gives `123` after integer division.
    
- The next digits are `3`, `2` and `1`.
    
- Their sum is `4 + 3 + 2 + 1 = 10`.
    

This example also combines loops, arithmetic operators and integer division.

### Common mistake: Forgetting the update

```
int i = 1;

while (i <= 5) {
    printf("%d ", i);
}
```

This loop does not terminate normally because `i` remains `1`. The condition stays true forever unless execution is interrupted externally.

# 7. `do-while` loop

### What is `do-while`?

A `do-while` loop executes its body first and checks the condition afterward.

Key exam fact: a `do-while` loop executes its body at least once, even if the condition is initially false.

Syntax:

```
do {
    // Statements
} while (condition);
```

Notice the semicolon after `while (condition);`. It is required.

### Example: Print 1 to 5

```

#include <stdio.h>

int main(void) {
    int i = 1;

    do {
        printf("%d ", i);
        i++;
    } while (i <= 5);

    return 0;
}
```

Output:

```
1 2 3 4 5
```

### The most important difference: `while` versus `do-while`

```
#include <stdio.h>

int main(void) {
    int a = 10;
    int b = 10;

    while (a < 5) {
        printf("A ");
    }

    do {
        printf("B ");
    } while (b < 5);

    return 0;
}
```

Output:

```
B
```

Why?

- `while` checks `a < 5` before entering the body. It is false, so nothing prints.
    
- `do-while` executes the body once, printing `B`, then checks `b < 5`. It is false, so the loop stops.
    

### Example: Menu-driven program

A menu often uses `do-while` because the menu should appear at least once.

```
#include <stdio.h>

int main(void) {
    int choice;

    do {
        printf("1. Hello\n");
        printf("0. Exit\n");
        printf("Enter choice: ");

        if (scanf("%d", &choice) != 1) {
            return 1;
        }

        if (choice == 1) {
            printf("Hello!\n");
        }

    } while (choice != 0);

    return 0;
}
```

If the user enters `0`, the loop terminates after the first menu display.

### Comparison of all three loops

|Feature|`for`|`while`|`do-while`|
|---|---|---|---|
|Condition checked|Before each iteration|Before each iteration|After each iteration|
|Minimum executions|Zero|Zero|One|
|Initialization|Commonly in loop header|Usually before loop|Usually before loop|
|Update|Commonly in loop header|Usually in body|Usually in body|
|Typical use|Counter-controlled repetition|Condition-controlled repetition|At-least-once execution|

# 8. `break` statement

### What does `break` do?

`break` immediately terminates the nearest enclosing loop or `switch` statement.

Execution continues with the first statement after that loop or `switch`.

### Example: Stop when the counter reaches 4

```

#include <stdio.h>

int main(void) {
    for (int i = 1; i <= 10; i++) {
        if (i == 4) {
            break;
        }

        printf("%d ", i);
    }

    return 0;
}
```

Output:

```
1 2 3
```

Execution proceeds as follows:

- `i = 1`: condition false, print `1`.
    
- `i = 2`: condition false, print `2`.
    
- `i = 3`: condition false, print `3`.
    
- `i = 4`: condition true, execute `break` and leave the loop.
    

The value `4` is not printed because `break` occurs before `printf()`.

### Example: `break` inside a `while` loop

```
int i = 1;

while (i <= 5) {
    if (i == 3) {
        break;
    }

    printf("%d ", i);
    i++;
}
```

Output:

```
1 2
```

### `break` in nested loops

```
for (int i = 1; i <= 2; i++) {
    for (int j = 1; j <= 3; j++) {
        if (j == 2) {
            break;
        }

        printf("%d%d ", i, j);
    }
}
```

Output:

```
11 21
```

The `break` terminates only the inner loop, not both loops. The outer loop continues with its next iteration.

### Important rules

- `break` can be used inside a loop or `switch`.
    
- It exits only the nearest enclosing loop or `switch`.
    
- It is not valid as an ordinary jump statement outside such a construct.
    
- It is different from `return`, which exits the current function.
    

# 9. `continue` statement

### What does `continue` do?

`continue` skips the remaining statements in the current loop iteration and proceeds to the next iteration.

Unlike `break`, it does not terminate the loop.

### Example: Skip number 3

```

#include <stdio.h>

int main(void) {
    for (int i = 1; i <= 5; i++) {
        if (i == 3) {
            continue;
        }

        printf("%d ", i);
    }

    return 0;
}
```

Output:

```
1 2 4 5
```

When `i` is `3`, the `continue` skips `printf()`. The `for` loop then performs its update (`i++`) and checks the condition again.

### `continue` in a `while` loop

Be careful: the loop update must still happen when needed.

```

#include <stdio.h>

int main(void) {
    int i = 0;

    while (i < 5) {
        i++;

        if (i == 3) {
            continue;
        }

        printf("%d ", i);
    }

    return 0;
}
```

Output:

```
1 2 4 5
```

Here, `i++` happens before `continue`, so the loop progresses normally.

Common mistake: If the increment were placed after the `if` block, `continue` could skip the increment and create an infinite loop when `i == 3`.

### `continue` versus `break`

|`break`|`continue`|
|---|---|
|Terminates the nearest enclosing loop or `switch`|Skips the current loop iteration|
|Does not start another iteration of that loop|Proceeds toward the next iteration|
|In a `for` loop, skips the update expression by exiting|In a `for` loop, proceeds to the update expression|
|In a `while` loop, exits immediately|In a `while` loop, proceeds to the next condition check|

Remember: `continue` applies to loops, not to a `switch` statement by itself.

# 10. Combined example: understand the flow of execution

This example combines `for`, `if`, `continue` and `break`.

```

#include <stdio.h>

int main(void) {
    for (int i = 1; i <= 10; i++) {
        if (i % 2 == 0) {
            continue;
        }

        if (i == 7) {
            break;
        }

        printf("%d ", i);
    }

    return 0;
}
```

Output:

```
1 3 5
```

Trace the program:

|`i`|What happens?|
|---|---|
|1|Odd; print `1`|
|2|Even; `continue` skips printing|
|3|Odd; print `3`|
|4|Even; skip|
|5|Odd; print `5`|
|6|Even; skip|
|7|`break` terminates the loop|

The output does not contain `7` because the `break` executes before `printf()`.

## 11. Quick revision sheet for DSSSB

## Control-flow rules to memorise

1. `if` executes its body when its condition is true.
    
2. `if-else` selects between two branches.
    
3. A nested `if` places one decision inside another. An `else` matches the nearest unmatched `if`.
    
4. `switch` selects among matching constant case labels; missing `break` can cause fall-through.
    
5. A `for` loop is commonly used for counter-controlled repetition.
    
6. A `while` loop checks its condition before executing its body.
    
7. A `do-while` loop checks its condition after executing its body, so it executes at least once.
    
8. `break` exits the nearest enclosing loop or `switch`.
    
9. `continue` skips the rest of the current loop iteration; the next iteration proceeds according to that loop's rules.