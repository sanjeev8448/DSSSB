
## 1. Basic Concepts

Boolean algebra deals with variables that can have only two values:

- 0 = False / LOW
    
- 1 = True / HIGH
    

The three basic operations are:

|Operation|Symbol|Meaning|Example|
|---|---|---|---|
|AND|A · B or AB|1 only if both inputs are 1|1 · 1 = 1|
|OR|A + B|1 if at least one input is 1|1 + 0 = 1|
|NOT|A′|Reverses the input|0′ = 1|

Important: In Boolean algebra, 1 + 1 = 1 because + represents OR, not ordinary arithmetic addition.

## 2. Basic Boolean Laws

These laws should be memorized because they are used repeatedly in simplification problems.

### A. Identity Laws

A + 0 = A

A · 1 = A

Example: X + 0 = X

### B. Null or Domination Laws

A + 1 = 1

A · 0 = 0

Example: X · 0 = 0, regardless of the value of X.

### C. Idempotent Laws

A + A = A

A · A = A

Repeating the same variable in an OR or AND operation does not change the result.

### D. Complement Laws

A + A′ = 1

A · A′ = 0

A variable OR its complement is always 1. A variable AND its complement is always 0.

### E. Involution Law

(A′)′ = A

Taking the complement twice returns the original variable.

### F. Commutative Laws

A + B = B + A

AB = BA

The order of variables does not matter.

### G. Associative Laws

(A + B) + C = A + (B + C)

(AB)C = A(BC)

The grouping of variables can change without changing the result.

### H. Distributive Laws

A(B + C) = AB + AC

A + BC = (A + B)(A + C)

The second identity is particularly important because it differs from the distributive rule students usually learn first in ordinary algebra.

### I. Absorption Laws

A + AB = A

A(A + B) = A

Example:

X + XY = X(1 + Y)

Since 1 + Y = 1:

X(1 + Y) = X · 1 = X

Therefore, X + XY = X.

## 3. Boolean Expressions and Truth Tables

A Boolean expression combines Boolean variables using operations such as AND, OR, and NOT.

Example:

F = A + B′C

This means:

1. Complement B to obtain B′.
    
2. AND B′ with C.
    
3. OR the result with A.
    

### Truth Table for the AND Gate

|A|B|AB|
|---|---|---|
|0|0|0|
|0|1|0|
|1|0|0|
|1|1|1|

### Truth Table for the OR Gate

|A|B|A + B|
|---|---|---|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|1|

### Truth Table for the NOT Gate

|A|A′|
|---|---|
|0|1|
|1|0|

### Worked Example: Evaluate F = A + B′C

Suppose A = 0, B = 0, and C = 1.

Step 1: B′ = 1

Step 2: B′C = 1 · 1 = 1

Step 3: F = 0 + 1 = 1

Therefore, F = 1.

For an expression with n Boolean variables, a complete truth table contains 2ⁿ input combinations.

- 2 variables → 4 rows
    
- 3 variables → 8 rows
    
- 4 variables → 16 rows
    
- 5 variables → 32 rows
    

## 4. De Morgan's Laws

These laws explain how to distribute a complement across an AND or OR expression.

### First Law: Complement of OR

(A + B)′ = A′B′

Meaning: The complement of an OR expression equals the AND of the individual complements.

Example:

(X + Y)′ = X′Y′

### Second Law: Complement of AND

(AB)′ = A′ + B′

Meaning: The complement of an AND expression equals the OR of the individual complements.

Example:

(XY)′ = X′ + Y′

### Three-Variable Forms

(A + B + C)′ = A′B′C′

(ABC)′ = A′ + B′ + C′

### How to Remember De Morgan's Laws

When the complement moves inside the brackets:

1. Complement each variable.
    
2. Change OR to AND.
    
3. Change AND to OR.
    

|Original Expression|Equivalent Expression|
|---|---|
|(A + B)′|A′B′|
|(AB)′|A′ + B′|
|(A + B + C)′|A′B′C′|
|(ABC)′|A′ + B′ + C′|
|(A + B′)′|A′B|
|(AB′)′|A′ + B|

Common exam trap: (A + B)′ is NOT equal to A′ + B′. The operator must also change.

## 5. Boolean Expression Simplification

The objective is to obtain an equivalent expression with fewer variables, operations, or logic gates.

### Example 1: Simplify A + AB

Using the absorption law:

A + AB = A

Final answer: A

### Example 2: Simplify A(A + B)

Apply the absorption law:

A(A + B) = A

Final answer: A

### Example 3: Simplify AB + AB′

Take A common:

AB + AB′ = A(B + B′)

Using B + B′ = 1:

= A · 1

= A

Final answer: A

### Example 4: Simplify (A + B)(A + B′)

Using the identity:

(X + Y)(X + Z) = X + YZ

Therefore:

(A + B)(A + B′) = A + BB′

Since BB′ = 0:

= A + 0

= A

Final answer: A

### Example 5: Simplify A + A′B

Using the distributive identity:

A + A′B = (A + A′)(A + B)

Since A + A′ = 1:

= 1(A + B)

= A + B

Final answer: A + B

### Example 6: Simplify (A + B)′ + A

Apply De Morgan's law:

(A + B)′ = A′B′

Therefore:

F = A′B′ + A

Using the identity A + A′X = A + X:

F = A + B′

Final answer: A + B′

### Example 7: Simplify AB + A′C + BC

Use the consensus theorem:

XY + X′Z + YZ = XY + X′Z

Here, X = A, Y = B, and Z = C.

Therefore, the term BC is redundant:

AB + A′C + BC = AB + A′C

Final answer: AB + A′C

This is a useful higher-value simplification rule for MCQs.

## 6. Logic Gates: Quick Comparison

|Gate|Boolean Expression|Output Is 1 When|
|---|---|---|
|AND|AB|Both inputs are 1|
|OR|A + B|At least one input is 1|
|NOT|A′|Input is 0|
|NAND|(AB)′|At least one input is 0|
|NOR|(A + B)′|Both inputs are 0|
|XOR|A ⊕ B|Inputs are different|
|XNOR|(A ⊕ B)′|Inputs are the same|

### Quick Practice

Evaluate the following expressions:

1. A AND B when A = 1 and B = 0.
    
2. A OR B when A = 0 and B = 1.
    
3. NOT A when A = 1.
    
4. NAND when A = 1 and B = 1.
    
5. XOR when A = 1 and B = 0.
    

Answers:

1. 0
    
2. 1
    
3. 0
    
4. 0
    
5. 1
    

## 7. High-Yield Laws for Quick Revision

|Law|Formula|
|---|---|
|Identity|A + 0 = A; A · 1 = A|
|Domination|A + 1 = 1; A · 0 = 0|
|Idempotent|A + A = A; AA = A|
|Complement|A + A′ = 1; AA′ = 0|
|Involution|(A′)′ = A|
|Absorption|A + AB = A; A(A + B) = A|
|De Morgan's First Law|(A + B)′ = A′B′|
|De Morgan's Second Law|(AB)′ = A′ + B′|
|Consensus|AB + A′C + BC = AB + A′C|

### Final Exam Revision Tips

- Memorize all basic Boolean laws.
    
- Practise De Morgan's laws until you can apply them without hesitation.
    
- Learn the truth tables of AND, OR, NOT, NAND, NOR, XOR, and XNOR.
    
- Practise simplification questions using absorption, distributive, complement, and consensus laws.
    
- Remember that Boolean addition represents OR and Boolean multiplication represents AND.