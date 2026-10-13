# DSSSB TGT Computer Science — Algorithm Analysis Notes

## Topic: Algorithms, Complexity Analysis, Asymptotic Notations and Recursion

# 1. What Is an Algorithm?

An **algorithm** is a finite sequence of well-defined steps used to solve a problem or perform a computation.

### Example: Find the largest element in an array

Steps:

1. Assume the first element is the largest.
    
2. Examine each remaining element.
    
3. If an element is larger than the current maximum, update the maximum.
    
4. Return the maximum after examining all elements.
    

Python implementation:

```
def find_maximum(arr):
    if not arr:
        raise ValueError("Array must not be empty")

    maximum = arr[0]

    for value in arr[1:]:
        if value > maximum:
            maximum = value

    return maximum


print(find_maximum([10, 45, 20, 75, 30]))
```

Output:

```
75
```

The algorithm works for sorted or unsorted arrays, provided the array contains at least one element.

## 1.1 Characteristics of an algorithm

The conventional textbook characteristics are input, output, definiteness, finiteness, effectiveness and generality.

|Characteristic|Meaning|Example|
|---|---|---|
|Input|Accepts zero or more inputs|An array of numbers|
|Output|Produces at least one result|The maximum number|
|Definiteness|Every step is clear and unambiguous|Compare two numbers|
|Finiteness|Terminates after a finite number of steps|Examine each array element once|
|Effectiveness|Each step is basic and executable|Add, compare, assign|
|Generality|Solves a class of problems, not just one instance|Finds the maximum in any non-empty numeric array|

### Important examples

- **Definiteness:** “Choose a reasonably large number” is ambiguous. “Choose the maximum of the current number and the previous maximum” is precise.
    
- **Finiteness:** An algorithm that repeats forever without producing a result fails the finiteness requirement.
    
- **Generality:** An algorithm that finds the maximum of any non-empty array is more general than one that only prints 75.
    
- **Output:** An algorithm must produce at least one result, although it may accept zero inputs.
    

## 1.2 Algorithm vs program

|Algorithm|Program|
|---|---|
|A step-by-step problem-solving method|An implementation of instructions in a programming language|
|Can be expressed using pseudocode, flowcharts or plain language|Written in Python, C, C++, Java, etc.|
|Describes the logic|Executes on a computer when run|
|Language-independent in principle|Uses a specific language's syntax and semantics|

An algorithm is not the same as the code used to implement it.

# 2. Algorithm Complexity

Complexity describes the computational resources an algorithm requires as the input size grows.

The two most important types are:

- **Time complexity:** How the amount of work grows with input size.
    
- **Space complexity:** How memory requirements grow with input size.
    

Let `n` represent the number of elements in the input.

## 2.1 Time complexity

Consider:

```
def display_numbers(n):
    for i in range(n):
        print(i)
```

The loop runs `n` times. As `n` increases, the number of iterations grows proportionally.

Therefore, the time complexity is **Θ(n)**.

Examples:

- If `n = 10`, there are 10 iterations.
    
- If `n = 1000`, there are 1000 iterations.
    

The exact runtime in seconds depends on the machine, programming language, implementation and environment. Complexity describes the growth trend rather than a fixed number of seconds.

## 2.2 Space complexity

Space complexity describes memory requirements as a function of input size.

Example 1:

```
def sum_numbers(arr):
    total = 0

    for value in arr:
        total += value

    return total
```

The function uses a fixed number of additional variables. Its **auxiliary space complexity is O(1)**, excluding the input array.

Example 2:

```
def make_squares(n):
    result = []

    for i in range(n):
        result.append(i * i)

    return result
```

The function stores `n` square values in a list. Its auxiliary space complexity is **O(n)**.

### Auxiliary space vs total space

- **Auxiliary space:** Extra memory used by the algorithm, usually excluding the input.
    
- **Total space:** Includes input storage and additional memory.
    

For exam questions, identify which definition is being used.

# 3. Common Time-Complexity Classes

Learn to recognize these growth rates and compare their relative efficiency.

|Complexity|Name|Typical example|
|---|---|---|
|O(1)|Constant|Accessing an array element by index|
|O(log n)|Logarithmic|Binary search|
|O(n)|Linear|Single traversal of an array|
|O(n log n)|Linearithmic|Merge sort|
|O(n²)|Quadratic|Two nested loops over n elements|
|O(n³)|Cubic|Three nested loops over n elements|
|O(2ⁿ)|Exponential|Naive recursive Fibonacci, as a common upper bound|
|O(n!)|Factorial|Generating all permutations by brute force|

The table uses Big-O as an upper-bound classification. Many examples also have matching tight bounds, such as Θ(n) for a full array traversal.

## 3.1 Comparing growth rates

As the input size becomes large:

- Logarithmic growth is usually much slower than linear growth.
    
- Quadratic growth becomes much more expensive than linear growth.
    
- Exponential and factorial growth can become impractical very quickly.
    

For example, when `n = 1000`:

|Complexity|Illustrative operation count|
|---|---|
|O(1)|Constant-scale work|
|O(log₂ n)|Approximately 10 logarithmic steps|
|O(n)|1000-scale work|
|O(n²)|1,000,000-scale work|

These are illustrative operation counts, not exact runtime predictions.

## 3.2 How to calculate complexity from code

### Example A: Constant time

```
def get_first(arr):
    return arr[0]
```

Only one indexed access is performed, regardless of the array's length.

**Time complexity: Θ(1)**

Assume the array is non-empty.

### Example B: Linear time

```
def traverse(arr):
    for x in arr:
        print(x)
```

Each element is processed once.

**Time complexity: Θ(n)**

### Example C: Quadratic time

```
def pairs(n):
    for i in range(n):
        for j in range(n):
            print(i, j)
```

The outer loop runs `n` times. For every outer iteration, the inner loop also runs `n` times.

`T(n) = n × n = n²`

**Time complexity: Θ(n²)**

For `n = 5`, the body executes `5 × 5 = 25` times.

### Example D: Two consecutive loops

```
def example(n):
    for i in range(n):
        print(i)

    for j in range(n):
        print(j)
```

The first loop runs `n` times, and the second also runs `n` times.

`T(n) = n + n = 2n`

Ignoring constant factors gives:

**Time complexity: Θ(n)**

**Exam rule:** Consecutive loops are generally added, while nested loops are multiplied when their iteration counts are independent in the stated way.

### Example E: A loop that doubles its variable

```
i = 1

while i < n:
    print(i)
    i *= 2
```

The values of `i` are:

`1, 2, 4, 8, 16, 32, ...`

After `k` iterations, `i = 2ᵏ`. The loop reaches or passes `n` when:

`2ᵏ ≥ n`

Taking logarithms:

`k ≥ log₂ n`

Therefore, the time complexity is **Θ(log n)** for the usual increasing input size.

**Exam trap:** A loop that doubles or halves a value on each iteration commonly has logarithmic complexity, not linear complexity.

# 4. Big-O Notation — Upper Bound

Big-O notation describes an asymptotic upper bound on an algorithm's growth.

We write:

`f(n) ∈ O(g(n))`

when there are positive constants `c` and `n₀` such that:

`0 ≤ f(n) ≤ c × g(n)` for all `n ≥ n₀`.

In simple terms, once the input becomes sufficiently large, `f(n)` does not grow faster than a constant multiple of `g(n)`.

## 4.1 Example of Big-O

Consider:

`f(n) = 3n² + 5n + 2`

For `n ≥ 1`, we have `n ≤ n²` and `1 ≤ n²`.

Therefore:

`3n² + 5n + 2 ≤ 10n²`

We can choose `c = 10` and `n₀ = 1`.

So:

**f(n) ∈ O(n²)**

## 4.2 Simplifying Big-O expressions

Common rules:

- Ignore constant multipliers.
    
- Ignore lower-order terms when a higher-order term dominates.
    
- For independent consecutive parts, add the work before simplifying.
    

|Function|Simplified Big-O|
|---|---|
|5|O(1)|
|3n + 10|O(n)|
|4n² + 3n + 8|O(n²)|
|n³ + 100n² + n|O(n³)|
|7 log n + 20|O(log n)|
|n log n + n|O(n log n)|

Why is `4n² + 3n + 8` classified as O(n²)? Because the n² term eventually dominates the smaller growth terms.

### Important distinction

If `f(n) = n`, it is also true that `f(n) ∈ O(n²)`. However, O(n) is a tighter upper bound.

Big-O alone does not promise the tightest possible bound. In exam questions, “find the complexity” usually expects the simplest tight classification unless the question explicitly asks only for an upper bound.

# 5. Big-Ω Notation — Lower Bound

Big-Ω (Omega) notation describes an asymptotic lower bound on a function's growth.

We write:

`f(n) ∈ Ω(g(n))`

when positive constants `c` and `n₀` exist such that:

`0 ≤ c × g(n) ≤ f(n)` for all `n ≥ n₀`.

In simple terms, `f(n)` grows at least as fast as a constant multiple of `g(n)` for sufficiently large inputs.

## 5.1 Example of Big-Ω

Take:

`f(n) = 3n² + 5n + 2`

For every positive integer `n`:

`3n² ≤ 3n² + 5n + 2`

Therefore:

**f(n) ∈ Ω(n²)**

The function grows at least on the order of n².

Another example:

For `f(n) = 5n + 10`, we can establish:

**f(n) ∈ Ω(n)**

because the function grows at least linearly.

**Exam trap:** Big-Ω means a lower bound on the specified function. It does not automatically mean best-case complexity. Best-case complexity can itself be described using Big-O, Big-Ω or Big-Θ.

# 6. Big-Θ Notation — Tight Bound

Big-Θ (Theta) notation describes a tight asymptotic bound. The function is both upper-bounded and lower-bounded by constant multiples of the same comparison function.

We write:

`f(n) ∈ Θ(g(n))`

if positive constants `c₁`, `c₂` and `n₀` exist such that:

`0 ≤ c₁g(n) ≤ f(n) ≤ c₂g(n)` for all `n ≥ n₀`.

In simpler terms, the two functions grow at the same asymptotic rate, up to constant factors.

## 6.1 Example of Big-Θ

For:

`f(n) = 3n² + 5n + 2`

We can establish, for `n ≥ 1`:

`3n² ≤ f(n) ≤ 10n²`

The function therefore has both an O(n²) upper bound and an Ω(n²) lower bound.

Hence:

**f(n) ∈ Θ(n²)**

## 6.2 Big-O vs Big-Ω vs Big-Θ

|Notation|Meaning|Interpretation|
|---|---|---|
|Big-O|Upper bound|The function grows no faster than a constant multiple of the comparison function, eventually|
|Big-Ω|Lower bound|The function grows at least as fast as a constant multiple of the comparison function, eventually|
|Big-Θ|Tight bound|The function is bounded above and below by constant multiples of the same comparison function|

### Comparison table

|Function|Big-O|Big-Ω|Big-Θ|
|---|---|---|---|
|3n² + 5n + 2|O(n²)|Ω(n²)|Θ(n²)|
|5n + 10|O(n)|Ω(n)|Θ(n)|
|7 log n + 3|O(log n)|Ω(log n)|Θ(log n)|
|4n³ + 2n²|O(n³)|Ω(n³)|Θ(n³)|

These are tight classifications for the listed functions.

### Common MCQ trap

Suppose an algorithm runs in Θ(n²) time.

It is also correct to say its time is O(n³), but that is a loose upper bound. If asked for its tight asymptotic bound, the appropriate answer is Θ(n²).

Remember:

**Θ(g(n)) = O(g(n)) ∩ Ω(g(n))**

Big-Θ implies both the corresponding Big-O and Big-Ω bounds.

# 7. Best Case, Average Case and Worst Case

These describe how an algorithm performs on different inputs of the same size.

- **Best case:** The least work required for any input of size `n`.
    
- **Average case:** The expected work over a specified distribution of inputs of size `n`.
    
- **Worst case:** The greatest work required for any input of size `n`.
    

These concepts differ from Big-O, Big-Ω and Big-Θ, which describe asymptotic bounds on a specified function.

## 7.1 Example: Linear search

Linear search examines an array from left to right until it finds the target or reaches the end.

```
def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i

    return -1
```

Suppose the array is:

`[10, 20, 30, 40, 50]`

### Best case

Search for `10`.

Only one comparison is required.

**Best-case time: Θ(1)**

### Worst case

Search for `50`, or for a value that is absent.

The algorithm may examine all `n` elements.

**Worst-case time: Θ(n)**

### Average case

Assume the target exists and is equally likely to appear at any position.

The expected number of comparisons is:

`(1 + 2 + ... + n) / n = (n + 1) / 2`

Therefore:

**Average-case time: Θ(n)**

This result depends on the stated assumption about the target's position.

### Linear-search summary

|Case|Number of comparisons|Tight bound|
|---|---|---|
|Best|1|Θ(1)|
|Average, uniformly distributed successful target|(n + 1) / 2|Θ(n)|
|Worst|n|Θ(n)|

## 7.2 Example: Binary search

Binary search requires sorted data.

|Case|Time complexity|Explanation|
|---|---|---|
|Best|Θ(1)|Target matches the first middle element|
|Average|Θ(log n)|Search interval repeatedly halves|
|Worst|Θ(log n)|Search continues until the target is found or ruled out|

The search space shrinks approximately as:

`n, n/2, n/4, n/8, ...`

After `k` halvings, the remaining size is approximately `n / 2ᵏ`.

Solving `n / 2ᵏ ≤ 1` gives `k ≥ log₂ n`.

## 7.3 How Big-O and cases relate

|Concept|Answers which question?|
|---|---|
|Best case|What is the minimum work for inputs of size n?|
|Average case|What is the expected work under a stated distribution?|
|Worst case|What is the maximum work for inputs of size n?|
|Big-O|Is this function asymptotically upper-bounded by another function?|
|Big-Ω|Is this function asymptotically lower-bounded by another function?|
|Big-Θ|Does this function have a tight asymptotic bound?|

For example, worst-case linear search is Θ(n), and therefore also O(n) and Ω(n).

**Exam trap:** Big-O is not synonymous with worst case. Big-O can describe an upper bound on best-case, average-case or worst-case complexity functions.

# 8. Recursion

**Recursion** is a programming technique in which a function calls itself to solve a problem by reducing it into smaller subproblems.

A recursive function normally needs two essential parts:

1. **Base case:** The condition that stops further recursive calls.
    
2. **Recursive case:** The part that calls the function again, usually with a smaller or simpler input.
    

Without a reachable base case, recursion can continue until the program hits a recursion limit or otherwise fails.

## 8.1 Example: Countdown

```
def countdown(n):
    if n == 0:       # Base case
        print("Done")
        return

    print(n)
    countdown(n - 1)  # Recursive case


countdown(3)
```

Output:

```
3
2
1
Done
```

Trace:

```
countdown(3)
    └── countdown(2)
            └── countdown(1)
                    └── countdown(0)  ← Base case
```

The function calls become simpler because the argument decreases by one on each call.

## 8.2 Factorial using recursion

The factorial of a non-negative integer `n` is:

`n! = n × (n - 1) × (n - 2) × ... × 2 × 1`

By definition:

`0! = 1`

The recursive definition is:

- `n! = 1`, when `n = 0`
    
- `n! = n × (n - 1)!`, when `n > 0`
    

Python implementation:

```
def factorial(n):
    if n < 0:
        raise ValueError("n must be non-negative")

    if n == 0:
        return 1

    return n * factorial(n - 1)


print(factorial(5))
print(factorial(0))
```

Output:

```
120
1
```

### How factorial(4) executes

Calls are made downward until the base case:

```
factorial(4)
4 * factorial(3)
4 * 3 * factorial(2)
4 * 3 * 2 * factorial(1)
4 * 3 * 2 * 1 * factorial(0)
```

Then the results return upward:

```
factorial(0) = 1
factorial(1) = 1 * 1 = 1
factorial(2) = 2 * 1 = 2
factorial(3) = 3 * 2 = 6
factorial(4) = 4 * 6 = 24
```

Final result: `24`

### Factorial complexity

For this recursive implementation:

- Time complexity: Θ(n), because there are n + 1 calls, up to constant differences.
    
- Auxiliary space complexity: Θ(n), because each recursive call occupies a call-stack frame.
    
- Recursion depth: n + 1 calls when the base case is `n == 0`.
    

## 8.3 How the call stack works

Each active function call maintains information such as its local variables, parameters and where execution should resume.

In recursive calls, those frames remain active until deeper calls return.

For `factorial(3)`, calls are made downward until `factorial(0)` returns 1. Each pending call then completes its multiplication and returns its result to its caller.

**Exam trap:** Recursion uses the call stack. Deep recursion can exhaust the available recursion depth even if the algorithm's logic is otherwise valid.

## 8.4 Direct and indirect recursion

### Direct recursion

A function calls itself.

```
def direct(n):
    if n <= 0:
        return

    print(n)
    direct(n - 1)


direct(2)
```

Output:

```
2
1
```

### Indirect recursion

One function calls another function, which eventually calls the first function again.

```
def function_a(n):
    if n <= 0:
        return

    print("A", n)
    function_b(n - 1)


def function_b(n):
    if n <= 0:
        return

    print("B", n)
    function_a(n - 1)


function_a(2)
```

Output:

```
A 2
B 1
```

## 8.5 Tail recursion vs non-tail recursion

In **tail recursion**, the recursive call is the final operation performed by the function.

Example:

```
def countdown_tail(n):
    if n == 0:
        return

    print(n)
    return countdown_tail(n - 1)
```

In **non-tail recursion**, some work remains after the recursive call returns.

Example:

```
def factorial(n):
    if n == 0:
        return 1

    return n * factorial(n - 1)
```

In `factorial`, the multiplication by `n` remains to be performed after the recursive call returns. Therefore, this implementation is not tail-recursive.

**Python exam trap:** Python does not generally optimize tail-recursive calls into constant-space loops. Tail recursion still consumes call-stack space.

## 8.6 Fibonacci recursion

The Fibonacci sequence begins:

`0, 1, 1, 2, 3, 5, 8, 13, ...`

Its mathematical definition is:

- F(0) = 0
    
- F(1) = 1
    
- F(n) = F(n - 1) + F(n - 2), when n ≥ 2
    

A direct recursive implementation:

```
def fibonacci(n):
    if n < 0:
        raise ValueError("n must be non-negative")

    if n <= 1:
        return n

    return fibonacci(n - 1) + fibonacci(n - 2)


print(fibonacci(6))
```

Output:

```
8
```

### Why is naive Fibonacci inefficient?

The recursive calls overlap. For example, `fibonacci(5)` calls both `fibonacci(4)` and `fibonacci(3)`, and the computation for `fibonacci(3)` is repeated in other branches.

The naive recursive algorithm takes exponential time, commonly expressed as O(2ⁿ). A tighter bound for its number of calls is Θ(φⁿ), up to constant factors, where φ is the golden ratio.

Its recursion depth is O(n), so its auxiliary call-stack space is O(n).

**Important lesson:** Recursion does not automatically make an algorithm efficient.

# 9. Recurrence Relations and Complexity

A **recurrence relation** describes the cost for an input size `n` in terms of the cost for smaller inputs.

## 9.1 Factorial recurrence

The recursive factorial function makes one smaller recursive call and performs constant additional work.

`T(n) = T(n - 1) + Θ(1)`

Expanding the recurrence:

`T(n) = T(n - 2) + 2Θ(1)`

Continuing until the base case results in n steps.

Therefore:

**T(n) = Θ(n)**

## 9.2 Binary search recurrence

Binary search reduces the problem to approximately half the array at each step and performs constant additional work.

`T(n) = T(n/2) + Θ(1)`

The number of halvings required to reduce n to a constant is proportional to log₂ n.

Therefore:

**T(n) = Θ(log n)**

## 9.3 Merge sort recurrence

Merge sort divides the array into two halves, sorts each half recursively and merges the two sorted halves.

`T(n) = 2T(n/2) + Θ(n)`

The merging step takes linear time per level. There are approximately log₂ n levels.

Therefore:

**T(n) = Θ(n log n)**

### Recurrence revision table

|Algorithm|Typical recurrence|Time complexity|
|---|---|---|
|Factorial recursion|T(n) = T(n - 1) + Θ(1)|Θ(n)|
|Binary search|T(n) = T(n/2) + Θ(1)|Θ(log n)|
|Merge sort|T(n) = 2T(n/2) + Θ(n)|Θ(n log n)|
|Naive Fibonacci|T(n) = T(n - 1) + T(n - 2) + Θ(1)|Exponential|

For many exam questions, recognizing the recurrence pattern is more important than deriving every step.

# 10. Recursion vs Iteration

**Iteration** repeats a block using loops such as `for` or `while`. Recursion repeats a computation through function calls.

Consider summing the first n positive integers.

### Iterative version

```
def sum_iterative(n):
    total = 0

    for i in range(1, n + 1):
        total += i

    return total


print(sum_iterative(5))
```

Output:

```
15
```

### Recursive version

```
def sum_recursive(n):
    if n <= 0:
        return 0

    return n + sum_recursive(n - 1)


print(sum_recursive(5))
```

Output:

```
15
```

### Comparison

|Feature|Iteration|Recursion|
|---|---|---|
|Repetition|Loops|Function calls|
|Stopping condition|Loop condition|Base case|
|Memory usage|Often O(1) auxiliary space|Often uses call-stack space|
|Function-call overhead|Usually lower|Often higher|
|Natural fit|Repetitive linear processing|Trees, divide-and-conquer, backtracking|
|Risk|Infinite loop|Missing base case or excessive call depth|

For these examples, both versions take Θ(n) time.

- Iterative version: O(1) auxiliary space.
    
- Recursive version: O(n) stack space.
    

**Exam trap:** Recursion is a technique for expressing an algorithm, not a complexity class. A recursive algorithm can run in constant, logarithmic, linear, linearithmic or exponential time depending on its structure.

# 11. Consolidated Complexity Examples

These are the main patterns to recognize quickly in MCQs.

|Code or recurrence pattern|Typical tight time complexity|
|---|---|
|Fixed number of operations|Θ(1)|
|One loop from 0 to n - 1|Θ(n)|
|Two independent nested loops of size n|Θ(n²)|
|Three independent nested loops of size n|Θ(n³)|
|Loop variable doubles each iteration|Θ(log n)|
|Two consecutive linear loops|Θ(n)|
|One loop inside another with independent n iterations|Θ(n²)|
|T(n) = T(n - 1) + Θ(1)|Θ(n)|
|T(n) = T(n/2) + Θ(1)|Θ(log n)|
|T(n) = 2T(n/2) + Θ(n)|Θ(n log n)|

These patterns assume the stated loop bounds and recurrence costs. Different loop conditions or recursive subproblem sizes can change the complexity.

## 11.1 Final notation revision

|Notation or concept|Meaning|Remember|
|---|---|---|
|Big-O|Asymptotic upper bound|O(n²)|
|Big-Ω|Asymptotic lower bound|Ω(n)|
|Big-Θ|Tight asymptotic bound|Θ(n log n)|
|Best case|Minimum work for inputs of size n|Linear search finds the first element|
|Average case|Expected work under a specified distribution|Linear search with uniformly located target|
|Worst case|Maximum work for inputs of size n|Linear search target absent|

# 12. Final Revision Sheet

|Topic|Must remember|
|---|---|
|Algorithm characteristics|Input, output, definiteness, finiteness, effectiveness, generality|
|Time complexity|Growth of computational work|
|Space complexity|Growth of memory requirements|
|Big-O|Upper bound|
|Big-Ω|Lower bound|
|Big-Θ|Tight bound|
|Best case|Minimum work for inputs of size n|
|Average case|Expected work under a specified distribution|
|Worst case|Maximum work for inputs of size n|
|Recursion|A function calls itself directly or indirectly|
|Base case|Stops recursive calls|
|Recursive case|Reduces the problem|
|Call stack|Stores active function-call state|
|Recursive factorial|Θ(n) time and Θ(n) stack space|
|Binary search|Θ(log n) time|
|Merge sort|Θ(n log n) time|

## Highest-priority exam concepts

1. Identify complexity from loops.
    
2. Simplify polynomial expressions.
    
3. Distinguish Big-O, Big-Ω and Big-Θ.
    
4. Understand best-case vs average-case vs worst-case complexity.
    
5. Calculate time and space complexity for recursive functions.
    
6. Recognize common recurrence patterns.
    
7. Understand base cases, recursive cases and call-stack behavior.
    

These are the foundations for most algorithm-analysis problems at this level.