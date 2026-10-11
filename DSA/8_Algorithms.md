# 1. What is an algorithm?

An algorithm is a finite sequence of well-defined steps used to solve a problem or perform a computation.

For example, an algorithm to find the largest element in an array is:

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

The algorithm works regardless of whether the array is sorted or unsorted, provided it contains at least one element.

## 1.1 Characteristics of an algorithm

The conventional textbook characteristics are input, output, definiteness, finiteness, effectiveness, and generality.

|Characteristic|Meaning|Example|
|---|---|---|
|Input|Accepts zero or more inputs|An array of numbers|
|Output|Produces at least one result|The maximum number|
|Definiteness|Every step is clear and unambiguous|Compare two numbers|
|Finiteness|Terminates after a finite number of steps|Examine each array element once|
|Effectiveness|Each step is basic and executable|Add, compare, assign|
|Generality|Solves a class of problems, not only one fixed instance|Finds the maximum in any non-empty numeric array|

### Important examples

Definiteness: “Choose a reasonably large number” is ambiguous. “Choose the maximum of the current number and the previous maximum” is precise.

Finiteness: An algorithm that repeats forever without producing a result fails the finiteness requirement.

Generality: An algorithm that finds the maximum of any non-empty array is more general than one that only prints `75`.

Output: An algorithm must produce at least one result, although it may accept zero inputs.

### Algorithm vs program

|Algorithm|Program|
|---|---|
|A step-by-step problem-solving method|An implementation of instructions in a programming language|
|Can be expressed using pseudocode, flowcharts, or plain language|Written in Python, C, C++, Java, etc.|
|Describes the logic|Executes on a computer when run|
|Language-independent in principle|Uses a specific language's syntax and semantics|

An algorithm is not the same as the code used to implement it.

# 2. Algorithm complexity

Complexity describes the computational resources an algorithm requires as the input size grows.

The two most important types are:

- Time complexity: How the amount of work grows with input size.
    
- Space complexity: How memory requirements grow with input size.
    

Let \(n\) represent the number of elements in the input.

## 2.1 Time complexity

Consider this example:

```
def display_numbers(n):
    for i in range(n):
        print(i)

```

The loop runs \(n\) times. As \(n\) increases, the number of iterations grows proportionally.

Therefore, the time complexity is:

\[ \boxed{\Theta(n)} \]

If `n = 10`, there are 10 iterations. If `n = 1,000`, there are 1,000 iterations.

The exact runtime in seconds depends on the machine, programming language, implementation, and environment. Complexity describes the growth trend, rather than a fixed number of seconds.

## 2.2 Space complexity

Space complexity describes the memory required as a function of the input size.

Consider:

```
def sum_numbers(arr):    
total = 0    
for value in arr:        
total += value    
return total
```

The function uses a fixed number of additional variables: `total` and `value`.

Its auxiliary space complexity is \(O(1)\), excluding the input array.

Now consider:

```
def make_squares(n):    
result = []    
for i in range(n):        
result.append(i * i)    
return result
```

The function stores \(n\) square values in a list.

Its auxiliary space complexity is \(O(n)\).

### Auxiliary space vs total space

- Auxiliary space: Extra memory used by the algorithm, usually excluding the input.
    
- Total space: Includes input storage and additional memory.
    

For exam questions, identify which definition is being used. Some textbooks use “space complexity” to mean total memory, while many algorithm analyses emphasize auxiliary space.

# 3. Common time-complexity classes

You should be able to recognize these growth rates from code and compare their relative efficiency.

|Complexity|Name|Typical example|
|---|---|---|
|\(O(1)\)|Constant|Accessing an array element by index|
|\(O(\log n)\)|Logarithmic|Binary search|
|\(O(n)\)|Linear|Single traversal of an array|
|\(O(n\log n)\)|Linearithmic|Merge sort|
|\(O(n^2)\)|Quadratic|Two nested loops over \(n\) elements|
|\(O(n^3)\)|Cubic|Three nested loops over \(n\) elements|
|\(O(2^n)\)|Exponential|Naive recursive Fibonacci|
|\(O(n!)\)|Factorial|Generating all permutations by brute force|

The table uses Big-O as a common upper-bound classification. Many of these examples also have matching tight bounds, such as \(\Theta(n)\) for a full array traversal.

## 3.1 Visualizing growth

Illustrative growth of common complexities

How operation counts grow as n increases. These are mathematical functions, not measured runtime data.

1log₂ nnn log₂ nn²

070140210280124816

As the input size becomes large, logarithmic growth is usually much slower than linear growth, and quadratic growth becomes much more expensive than linear growth.

For example, if \(n=1,000\):

- \(O(1)\): constant-scale work.
    
- \(O(\log_2 n)\): approximately 10 logarithmic steps.
    
- \(O(n)\): 1,000-scale work.
    
- \(O(n^2)\): 1,000,000-scale work.
    

These are illustrative operation counts, not exact runtime predictions.

## 3.2 How to calculate complexity from code

### Example A: Constant time

```
def get_first(arr):    return arr[0]
```

Only one indexed access is performed, regardless of how many elements are in the array.

\[ \boxed{\Theta(1)} \]

Assume the array is non-empty.

### Example B: Linear time

```
def traverse(arr):    for x in arr:        print(x)
```

Each element is processed once.

\[ \boxed{\Theta(n)} \]

### Example C: Quadratic time

```
def pairs(n):    
for i in range(n):        
	for j in range(n):            
		print(i, j)
```

The outer loop runs \(n\) times. For every outer iteration, the inner loop also runs \(n\) times.

\[ T(n)=n\times n=n^2 \]

Therefore:

\[ \boxed{\Theta(n^2)} \]

For `n = 5`, the body executes \(5\times5=25\) times.

### Example D: Two consecutive loops

```

def example(n):
    for i in range(n):
        print(i)

    for j in range(n):
        print(j)

```

The first loop runs \(n\) times, and the second also runs \(n\) times.

\[ T(n)=n+n=2n \]

Discarding constant factors gives:

\[ \boxed{\Theta(n)} \]

Exam rule: Consecutive loops are generally added, while nested loops are multiplied when their iteration counts are independent in the stated way.

### Example E: A loop that doubles its variable

```
i = 1while i < n:    print(i)    i *= 2
```

The values of `i` are:

```
1, 2, 4, 8, 16, 32, ...
```

After \(k\) iterations, `i` is \(2^k\). It reaches or passes \(n\) when:

\[ 2^k\ge n \]

Taking logarithms:

\[ k\ge\log_2 n \]

Thus, the time complexity is \(O(\log n)\), and for the usual loop over increasing \(n\), it is \(\Theta(\log n)\).

Exam trap: A loop that doubles or halves a value on each iteration commonly gives logarithmic complexity, not linear complexity.

# 4. Big-O notation — upper bound

Big-O notation describes an asymptotic upper bound on an algorithm's growth.

We write:

\[ f(n)\in O(g(n)) \]

when there are positive constants \(c\) and \(n_0\) such that:

\[ 0\le f(n)\le c\,g(n) \quad\text{for all }n\ge n_0 \]

In simple words, once the input becomes sufficiently large, \(f(n)\) does not grow faster than a constant multiple of \(g(n)\).

## 4.1 Example of Big-O

Consider:

\[ f(n)=3n^2+5n+2 \]

For \(n\ge1\), we have \(n\le n^2\) and \(1\le n^2\). Therefore:

\[ 3n^2+5n+2\le10n^2 \]

We can choose \(c=10\) and \(n_0=1\).

So:

\[ \boxed{f(n)\in O(n^2)} \]

In ordinary exam terms, we say the function is \(O(n^2)\).

## 4.2 Simplifying Big-O expressions

When determining asymptotic complexity, the common rules are:

- Ignore constant multipliers.
    
- Ignore lower-order terms when a higher-order term dominates.
    
- For independent consecutive parts, add the work before simplifying.
    

Examples:

|Function|Simplified Big-O|
|---|---|
|\(5\)|\(O(1)\)|
|\(3n+10\)|\(O(n)\)|
|\(4n^2+3n+8\)|\(O(n^2)\)|
|\(n^3+100n^2+n\)|\(O(n^3)\)|
|\(7\log n+20\)|\(O(\log n)\)|
|\(n\log n+n\)|\(O(n\log n)\)|

Why is \(4n^2+3n+8\) classified as \(O(n^2)\)? Because the \(n^2\) term eventually dominates the smaller growth terms.

### A subtle but important point

If \(f(n)=n\), it is also true that \(f(n)\in O(n^2)\). However, \(O(n)\) is a tighter upper bound.

Big-O alone does not promise the tightest possible bound. In exam questions, “find the complexity” usually expects the simplest tight classification unless the question explicitly asks only for an upper bound.

# 5. Big-Ω notation — lower bound

Big-Ω (Omega) notation describes an asymptotic lower bound on a function's growth.

We write:

\[ f(n)\in\Omega(g(n)) \]

when there are positive constants \(c\) and \(n_0\) such that:

\[ 0\le c\,g(n)\le f(n) \quad\text{for all }n\ge n_0 \]

In simple terms, \(f(n)\) grows at least as fast as a constant multiple of \(g(n)\), for sufficiently large inputs.

## 5.1 Example of Big-Ω

Take:

\[ f(n)=3n^2+5n+2 \]

For every positive integer \(n\):

\[ 3n^2\le 3n^2+5n+2 \]

Therefore:

\[ \boxed{f(n)\in\Omega(n^2)} \]

The function grows at least on the order of \(n^2\).

### Another example

For \(f(n)=5n+10\), we can establish:

\[ f(n)\in\Omega(n) \]

because the function grows at least linearly.

Exam trap: Big-Ω means a lower bound on the specified function. It does not automatically mean best-case complexity. The best case itself can be described using Big-O, Big-Ω, or Big-Θ.

# 6. Big-Θ notation — tight bound

Big-Θ (Theta) notation describes a tight asymptotic bound. The function is both upper-bounded and lower-bounded by constant multiples of the same comparison function.

We write:

\[ f(n)\in\Theta(g(n)) \]

if there exist positive constants \(c_1,c_2\), and \(n_0\) such that:

\[ 0\le c_1g(n)\le f(n)\le c_2g(n) \]

for all \(n\ge n_0\).

In simpler terms, the two functions grow at the same asymptotic rate, up to constant factors.

## 6.1 Example of Big-Θ

For:

\[ f(n)=3n^2+5n+2 \]

We can establish that, for \(n\ge1\):

\[ 3n^2\le f(n)\le10n^2 \]

So the function has both an \(O(n^2)\) upper bound and an \(\Omega(n^2)\) lower bound.

Therefore:

\[ \boxed{f(n)\in\Theta(n^2)} \]

## 6.2 Big-O vs Big-Ω vs Big-Θ

## O

Upper bound

Big-O

The function grows no faster than a constant multiple of the comparison function, eventually.

## Ω

Lower bound

Big-Ω

The function grows at least as fast as a constant multiple of the comparison function, eventually.

## Θ

Tight bound

Big-Θ

The function's growth is bounded above and below by constant multiples of the same comparison function.

### Comparison table

|Function|Big-O|Big-Ω|Big-Θ|
|---|---|---|---|
|\(3n^2+5n+2\)|\(O(n^2)\)|\(\Omega(n^2)\)|\(\Theta(n^2)\)|
|\(5n+10\)|\(O(n)\)|\(\Omega(n)\)|\(\Theta(n)\)|
|\(7\log n+3\)|\(O(\log n)\)|\(\Omega(\log n)\)|\(\Theta(\log n)\)|
|\(4n^3+2n^2\)|\(O(n^3)\)|\(\Omega(n^3)\)|\(\Theta(n^3)\)|

These are tight classifications for the listed functions.

### A common MCQ trap

Suppose an algorithm runs in \(\Theta(n^2)\) time.

It is also correct to say its time is \(O(n^3)\), but that is a loose upper bound. If asked for its tight asymptotic bound, the appropriate answer is \(\Theta(n^2)\).

Remember:

\[ \boxed{\Theta(g(n))=O(g(n))\cap\Omega(g(n))} \]

Big-Θ implies both the corresponding Big-O and Big-Ω bounds.

# 7. Best case, average case, and worst case

These describe how an algorithm performs on different inputs of the same size.

- Best case: The least work required for any input of size \(n\).
    
- Average case: The expected work over a specified distribution of inputs of size \(n\).
    
- Worst case: The greatest work required for any input of size \(n\).
    

These are different from Big-O, Big-Ω, and Big-Θ, which describe asymptotic bounds on a specified function.

## 7.1 Example: Linear search

Consider the algorithm that searches for a target in an array of \(n\) elements, checking from left to right.

```
def linear_search(arr, target):    for i in range(len(arr)):        if arr[i] == target:            return i    return -1
```

Suppose the array is:

```
[10, 20, 30, 40, 50]
```

### Best case

Search for `10`.

Only one comparison is required.

\[ T_{\text{best}}(n)\in\Theta(1) \]

### Worst case

Search for `50`, or for a value that is absent.

The algorithm may examine all five elements in this example, or all \(n\) elements in a general array.

\[ T_{\text{worst}}(n)\in\Theta(n) \]

### Average case

Assume the target exists and is equally likely to appear at any position. The expected number of comparisons is:

\[ \frac{1+2+\cdots+n}{n} =\frac{n+1}{2} \]

Therefore:

\[ T_{\text{avg}}(n)\in\Theta(n) \]

This average-case result depends on the stated assumption about the target's position. A different input distribution can produce a different average.

### Linear-search summary

|Case|Number of comparisons|Tight bound|
|---|---|---|
|Best|1|\(\Theta(1)\)|
|Average, uniformly distributed successful target|\((n+1)/2\)|\(\Theta(n)\)|
|Worst|\(n\)|\(\Theta(n)\)|

## 7.2 Example: Binary search

Binary search requires sorted data.

|Case|Time complexity|Explanation|
|---|---|---|
|Best|\(\Theta(1)\)|Target matches the first middle element|
|Average|\(\Theta(\log n)\)|Search interval repeatedly halves|
|Worst|\(\Theta(\log n)\)|Search continues until the target is found or ruled out|

For the worst case, the search space shrinks approximately as:

\[ n,\frac n2,\frac n4,\frac n8,\ldots \]

After \(k\) halvings, the remaining size is approximately \(n/2^k\). Solving \(n/2^k\le1\) gives \(k\ge\log_2 n\).

## 7.3 How Big-O and best/worst case relate

This distinction matters:

|Concept|Answers which question?|
|---|---|
|Best case|What is the minimum work for inputs of size \(n\)?|
|Average case|What is the expected work under a stated distribution?|
|Worst case|What is the maximum work for inputs of size \(n\)?|
|Big-O|Is this function asymptotically upper-bounded by another function?|
|Big-Ω|Is this function asymptotically lower-bounded by another function?|
|Big-Θ|Does this function have a tight asymptotic bound?|

For example, the worst-case time for linear search is \(\Theta(n)\). It is therefore also \(O(n)\) and \(\Omega(n)\).

Exam trap: Big-O is not synonymous with worst case. Worst-case time is one kind of complexity function, and Big-O can be used to describe upper bounds on best-case, average-case, or worst-case functions.

# 8. Recursion

Recursion is a programming technique in which a function calls itself to solve a problem by reducing it into smaller subproblems.

A recursive function normally needs two essential parts:

1. Base case: The condition that stops further recursive calls.
    
2. Recursive case: The part that calls the function again, usually with a smaller or simpler input.
    

Without a reachable base case, recursion can continue until the program hits a recursion limit or otherwise fails.

## 8.1 Example: Countdown

```
def countdown(n):    if n == 0:          # Base case        print("Done")        return    print(n)    countdown(n - 1)    # Recursive casecountdown(3)
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

The factorial of a non-negative integer \(n\) is:

\[ n!=n(n-1)(n-2)\cdots2\cdot1 \]

By definition:

\[ 0!=1 \]

The recursive definition is:

\[ n!= \begin{cases} 1,&n=0\\ n(n-1)!,&n>0 \end{cases} \]

Python implementation:

```
def factorial(n):    if n < 0:        raise ValueError("n must be non-negative")    if n == 0:        return 1    return n * factorial(n - 1)print(factorial(5))print(factorial(0))
```

Output:

```
120
1
```

### How `factorial(4)` executes

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

This produces the final result, `24`.

### Factorial complexity

For the recursive implementation:

- Time complexity: \(\Theta(n)\), because there are \(n+1\) calls up to constant differences.
    
- Auxiliary space complexity: \(\Theta(n)\), because each recursive call occupies a call-stack frame.
    

The recursion depth for `factorial(n)` is \(n+1\) calls when the base case is `n == 0`.

## 8.3 How the call stack works

Each active function call maintains information such as its local variables, parameters, and where execution should resume.

In recursive calls, those frames remain active until the deeper calls return.

### Call stack for `factorial(3)`

factorial(0) — returns 1

factorial(1) — waits for 1

factorial(2) — waits for 2

factorial(3) — waits for 6

Once the base case returns, each pending call finishes its multiplication and returns the result to its caller.

Exam trap: Recursion uses the call stack. Deep recursion can exhaust the available recursion depth even if the algorithm's logic is otherwise valid.

## 8.4 Direct and indirect recursion

Direct recursion: A function calls itself.

```
def direct(n):    if n <= 0:        return    print(n)    direct(n - 1)direct(2)
```

Output:

```
2
1
```

Indirect recursion: One function calls another function, which eventually calls the first function again.

```
def function_a(n):    if n <= 0:        return    print("A", n)    function_b(n - 1)def function_b(n):    if n <= 0:        return    print("B", n)    function_a(n - 1)function_a(2)
```

Output:

```
A 2
B 1
```

## 8.5 Tail recursion vs non-tail recursion

In tail recursion, the recursive call is the final operation performed by the function.

Tail-recursive example:

```
def countdown_tail(n):    if n == 0:        return    print(n)    return countdown_tail(n - 1)
```

In non-tail recursion, some work remains after the recursive call returns.

```
def factorial(n):    if n == 0:        return 1    return n * factorial(n - 1)
```

In `factorial`, the multiplication by `n` remains to be performed after the recursive call returns. Therefore, this implementation is not tail-recursive.

Python exam trap: Python does not generally optimize tail-recursive calls into constant-space loops. Tail recursion still consumes call-stack space.

## 8.6 Fibonacci recursion

The Fibonacci sequence begins:

```
0, 1, 1, 2, 3, 5, 8, 13, ...
```

Its mathematical definition is:

\[ F(n)= \begin{cases} 0,&n=0\\ 1,&n=1\\ F(n-1)+F(n-2),&n\ge2 \end{cases} \]

A direct recursive implementation is:

```
def fibonacci(n):    if n < 0:        raise ValueError("n must be non-negative")    if n <= 1:        return n    return fibonacci(n - 1) + fibonacci(n - 2)print(fibonacci(6))
```

Output:

```
8
```

### Why is naive Fibonacci inefficient?

The calls overlap. For example, `fibonacci(5)` calls both `fibonacci(4)` and `fibonacci(3)`, but the computation for `fibonacci(3)` is repeated within the other branches.

The naive recursive algorithm takes exponential time, commonly expressed as \(O(2^n)\), with a tighter bound of \(\Theta(\varphi^n)\) for its number of calls up to constant factors, where \(\varphi\) is the golden ratio.

Its recursion depth is \(O(n)\), so its auxiliary call-stack space is \(O(n)\).

This is an important lesson: recursion does not automatically make an algorithm efficient.

# 9. Recurrence relations and complexity

When analyzing recursive algorithms, we often express their running time using a recurrence relation.

A recurrence describes the cost for an input size \(n\) in terms of the cost for smaller inputs.

## 9.1 Factorial recurrence

The recursive factorial function makes one smaller recursive call and performs constant additional work:

\[ T(n)=T(n-1)+\Theta(1) \]

with a constant-size base case.

Expanding the recurrence gives approximately:

\[ T(n)=T(n-2)+2\Theta(1) \]

Continuing until the base case results in \(n\) steps, so:

\[ \boxed{T(n)=\Theta(n)} \]

## 9.2 Binary search recurrence

Binary search reduces the problem to approximately half of the array at each step and performs constant additional work.

\[ T(n)=T(n/2)+\Theta(1) \]

The number of halvings required to reduce \(n\) to a constant is proportional to \(\log_2 n\).

Therefore:

\[ \boxed{T(n)=\Theta(\log n)} \]

## 9.3 Merge sort recurrence

Merge sort divides the array into two halves, sorts each half recursively, and merges the two sorted halves.

\[ T(n)=2T(n/2)+\Theta(n) \]

The merging step takes linear time per level. There are approximately \(\log_2 n\) levels, so:

\[ \boxed{T(n)=\Theta(n\log n)} \]

For many exam questions, recognizing the recurrence pattern is more important than deriving every step.

### Recurrence revision table

|Algorithm|Typical recurrence|Time complexity|
|---|---|---|
|Factorial recursion|\(T(n)=T(n-1)+\Theta(1)\)|\(\Theta(n)\)|
|Binary search|\(T(n)=T(n/2)+\Theta(1)\)|\(\Theta(\log n)\)|
|Merge sort|\(T(n)=2T(n/2)+\Theta(n)\)|\(\Theta(n\log n)\)|
|Naive Fibonacci|\(T(n)=T(n-1)+T(n-2)+\Theta(1)\)|Exponential|

# 10. Recursion vs iteration

Iteration repeats a block using loops such as `for` or `while`. Recursion repeats a computation through function calls.

Consider summing the first \(n\) positive integers.

### Iterative version

```
def sum_iterative(n):    total = 0    for i in range(1, n + 1):        total += i    return totalprint(sum_iterative(5))
```

Output:

```
15
```

### Recursive version

```
def sum_recursive(n):    if n <= 0:        return 0    return n + sum_recursive(n - 1)print(sum_recursive(5))
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
|Memory usage|Often \(O(1)\) auxiliary space|Often uses call-stack space|
|Function-call overhead|Usually lower|Often higher|
|Natural fit|Repetitive linear processing|Trees, divide-and-conquer, backtracking|
|Risk|Infinite loop|Missing base case or excessive call depth|

For these examples, both versions take \(\Theta(n)\) time. The iterative version uses \(O(1)\) auxiliary space, while the recursive version uses \(O(n)\) stack space.

Exam trap: Recursion is a technique for expressing an algorithm, not a complexity class. A recursive algorithm can run in constant, logarithmic, linear, linearithmic, or exponential time depending on how its subproblems are structured.

# 11. Consolidated complexity examples

Here are the main patterns to recognize quickly in MCQs.

|Code or recurrence pattern|Typical tight time complexity|
|---|---|
|Fixed number of operations|\(\Theta(1)\)|
|One loop from `0` to `n-1`|\(\Theta(n)\)|
|Two independent nested loops of size \(n\)|\(\Theta(n^2)\)|
|Three independent nested loops of size \(n\)|\(\Theta(n^3)\)|
|Loop variable doubles each iteration|\(\Theta(\log n)\)|
|Two consecutive linear loops|\(\Theta(n)\)|
|One loop inside another with independent \(n\)-iterations|\(\Theta(n^2)\)|
|\(T(n)=T(n-1)+\Theta(1)\)|\(\Theta(n)\)|
|\(T(n)=T(n/2)+\Theta(1)\)|\(\Theta(\log n)\)|
|\(T(n)=2T(n/2)+\Theta(n)\)|\(\Theta(n\log n)\)|

These patterns assume the stated loop bounds and recurrence costs. If loop conditions or recursive subproblem sizes differ, the complexity may change.

## 11.1 Final notation revision

|Notation|Meaning|Remember|
|---|---|---|
|Big-O|Asymptotic upper bound|\(O(n^2)\)|
|Big-Ω|Asymptotic lower bound|\(\Omega(n)\)|
|Big-Θ|Tight asymptotic bound|\(\Theta(n\log n)\)|
|Best case|Minimum work for inputs of a given size|Linear search finds the first element|
|Average case|Expected work under a specified input distribution|Linear search with uniformly located target|
|Worst case|Maximum work for inputs of a given size|Linear search target absent|

## Final revision sheet

|Topic|Must remember|
|---|---|
|Algorithm characteristics|Input, output, definiteness, finiteness, effectiveness, generality|
|Time complexity|Growth of computational work|
|Space complexity|Growth of memory requirements|
|Big-O|Upper bound|
|Big-Ω|Lower bound|
|Big-Θ|Tight bound|
|Best case|Minimum work for inputs of size \(n\)|
|Average case|Expected work under a specified distribution|
|Worst case|Maximum work for inputs of size \(n\)|
|Recursion|A function calls itself directly or indirectly|
|Base case|Stops recursive calls|
|Recursive case|Reduces the problem|
|Call stack|Stores active function-call state|
|Recursive factorial|\(\Theta(n)\) time and \(\Theta(n)\) stack space|
|Binary search|\(\Theta(\log n)\) time|
|Merge sort|\(\Theta(n\log n)\) time|

Highest-priority exam concepts: Identify complexity from loops, simplify polynomial expressions, distinguish Big-O/Ω/Θ, understand best vs average vs worst case, and calculate time and space complexity for recursive functions. These are the foundations for most algorithm-analysis problems at this level.