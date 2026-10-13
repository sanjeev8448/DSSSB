
A Karnaugh map (K-map) is a graphical method for simplifying Boolean expressions. It helps reduce the number of terms and literals, which can reduce the number of logic gates required in a circuit.

For DSSSB, practise these five areas:

- 2-variable K-map
    
- 3-variable K-map
    
- 4-variable K-map
    
- SOP and POS simplification
    
- Don't-care conditions
    

## 1. K-map Rules You Must Remember

1. Place each truth-table output in its corresponding K-map cell.
    
2. Group adjacent 1s for SOP simplification.
    
3. Group adjacent 0s for POS simplification.
    
4. Groups must contain 1, 2, 4, 8, 16, ... cells.
    
5. Make groups as large as possible while covering every required 1 (for SOP) or 0 (for POS).
    
6. Overlapping groups are allowed when they help simplify the expression.
    
7. Diagonal cells are not adjacent.
    
8. The first and last rows or columns can be adjacent because K-maps wrap around.
    
9. Use don't-care cells as either 0 or 1 if that helps produce a simpler expression.
    

**Most important:** K-map ordering follows Gray code, not ordinary binary counting.

For two-bit labels, use:

00, 01, 11, 10

This ensures adjacent cells differ in only one bit.

## 2. Two-Variable K-map

For two variables A and B, there are 2² = 4 cells.

### K-map layout

|A \ B|0|1|
|---|---|---|
|0|m₀|m₁|
|1|m₂|m₃|

Minterm indices follow binary order AB: 00, 01, 10, 11.

### Worked Example

Simplify:

F(A, B) = Σm(1, 3)

Minterms:

- m₁ = 01
    
- m₃ = 11
    

Fill the map:

|A \ B|0|1|
|---|---|---|
|0|0|1|
|1|0|1|

The two 1s are adjacent vertically. In this group, A changes, but B = 1 remains constant.

Therefore:

**F = B**

Shortcut: Keep the variable that remains constant within a group; eliminate the variable that changes.

## 3. Three-Variable K-map

For three variables A, B, and C, there are 2³ = 8 cells.

Use A for the row and BC for the columns. The column order must be Gray code: 00, 01, 11, 10.

### K-map layout

|A \ BC|00|01|11|10|
|---|---|---|---|---|
|0|m₀|m₁|m₃|m₂|
|1|m₄|m₅|m₇|m₆|

Notice the minterm order: 0, 1, 3, 2, 4, 5, 7, 6.

### Worked Example: Simplify Using SOP

F(A, B, C) = Σm(1, 3, 5, 7)

Place 1s in cells m₁, m₃, m₅, and m₇.

|A \ BC|00|01|11|10|
|---|---|---|---|---|
|0|0|1|1|0|
|1|0|1|1|0|

All four 1s form a group of 4.

- A changes from 0 to 1.
    
- B changes from 0 to 1.
    
- C remains 1.
    

The changing variables disappear, leaving:

**F = C**

### Another Example

F(A, B, C) = Σm(0, 2, 4, 6)

These minterms correspond to:

- 000
    
- 010
    
- 100
    
- 110
    

Here, C = 0 in all four cells.

Therefore:

**F = C′**

Exam tip: In SOP simplification, a variable that stays at 0 appears complemented; a variable that stays at 1 appears uncomplemented.

## 4. Four-Variable K-map

For four variables A, B, C, and D, there are 2⁴ = 16 cells.

Both row labels AB and column labels CD use Gray-code order: 00, 01, 11, 10.

### K-map layout

|AB \ CD|00|01|11|10|
|---|---|---|---|---|
|00|m₀|m₁|m₃|m₂|
|01|m₄|m₅|m₇|m₆|
|11|m₁₂|m₁₃|m₁₅|m₁₄|
|10|m₈|m₉|m₁₁|m₁₀|

### Worked Example

Simplify:

F(A, B, C, D) = Σm(0, 1, 2, 3)

These minterms occupy the entire first row, where AB = 00.

In that row:

- A = 0
    
- B = 0
    
- C changes.
    
- D changes.
    

Thus, C and D disappear.

Therefore:

**F = A′B′**

### Group Sizes

|Number of Cells|Variables Eliminated|Literals Remaining|
|---|---|---|
|1|0|4|
|2|1|3|
|4|2|2|
|8|3|1|
|16|4|0; result is 1|

Rule: A group of 2ᵏ cells eliminates k variables when those variables vary across the group.

### Wrap-Around Adjacency

- The leftmost and rightmost columns are adjacent.
    
- The top and bottom rows are adjacent.
    
- The four corner cells of a 4-variable K-map can form a group of 4.
    
- Diagonal cells are never directly adjacent.
    

Do not assume that cells must touch only in the ordinary rectangular layout.

## 5. SOP — Sum of Products

SOP means Sum of Products.

- A product term is an AND combination, such as AB′.
    
- The sum means ORing product terms together.
    

Example:

F = A′B + AC

Here, A′B and AC are product terms joined by OR.

### SOP Using a K-map

1. Place the function's 1s in the K-map.
    
2. Group adjacent 1s into the largest possible groups of size 1, 2, 4, 8, or 16.
    
3. Every required 1 must be covered.
    
4. Write one product term per group.
    
5. OR the product terms together.
    

### Worked Example

F(A, B, C) = Σm(3, 7)

The minterms are:

- m₃ = 011
    
- m₇ = 111
    

In both cells, B = 1 and C = 1, while A changes.

The simplified SOP expression is:

**F = BC**

## 6. POS — Product of Sums

POS means Product of Sums.

- A sum term is an OR combination, such as (A + B′).
    
- The product means ANDing sum terms together.
    

Example:

F = (A + B)(B′ + C)

### POS Simplification Rules

1. Place the function's 0s in the K-map.
    
2. Group adjacent 0s into the largest possible groups.
    
3. Every required 0 must be covered.
    
4. Write one sum term per group.
    
5. AND the sum terms together.
    

### Important Rule for Writing POS Terms

When forming a term from a group of 0s:

- Variable constant at 0 → write it uncomplemented.
    
- Variable constant at 1 → write it complemented.
    
- Variables that change → eliminate them.
    

This is the opposite polarity from SOP terms.

### Worked Example

F(A, B) = ΠM(0, 2)

The function is 0 at minterms 0 and 2.

|A \ B|0|1|
|---|---|---|
|0|0|1|
|1|0|1|

The two 0s form a vertical group. In that group, B = 0 remains constant and A changes.

For a POS group, B = 0 gives the sum term B.

Therefore:

**F = B**

### SOP vs POS

|Feature|SOP|POS|
|---|---|---|
|Full form|Sum of Products|Product of Sums|
|Group|1s|0s|
|Result|AND terms ORed together|OR terms ANDed together|
|Standard notation|Σm(...)|ΠM(...)|
|Constant 0 in a group|Complemented variable|Uncomplemented variable|
|Constant 1 in a group|Uncomplemented variable|Complemented variable|

Exam tip: Σm lists minterms where the function is 1; ΠM lists maxterms where the function is 0.

## 7. Don't-Care Conditions

A don't-care condition represents an input combination for which the output does not matter or which is not expected to occur in the specified application.

It is commonly written as d, X, or a separate set of minterm indices.

Example:

F(A, B, C) = Σm(1, 3, 7), d(5)

Here, the function must be 1 at minterms 1, 3, and 7. The output for minterm 5 is a don't-care.

### How to Use Don't-Cares

- Treat a don't-care as 1 if it helps form a larger SOP group.
    
- Treat it as 0 if it helps form a larger POS group.
    
- Leave it unused if it does not help simplify the expression.
    
- Never use a don't-care in a way that leaves a required 1 uncovered in SOP or a required 0 uncovered in POS.
    

### Worked Example

F(A, B, C) = Σm(1, 3, 7), d(5)

The 1s occur at 1, 3, and 7. Minterm 5 is a don't-care.

The cells 1, 3, 5, and 7 all have C = 1. By using minterm 5 as a 1, we can make a group of four.

Therefore:

**F = C**

Without using the don't-care, a larger group may not be possible.

Important: A don't-care is not automatically 0 or automatically 1. Choose whichever value gives a simpler valid expression.

## 8. K-map Exam Shortcuts

### Group the Largest Possible Blocks

Prefer groups of 8 over 4, and 4 over 2, when they cover the required cells correctly.

### Use Gray-Code Order

K-map labels go:

00, 01, 11, 10

Not:

00, 01, 10, 11

### Know the Grouping Direction

- SOP → group 1s.
    
- POS → group 0s.
    

### Count Variables That Remain Constant

In a 4-variable map:

- Group of 1 → 4 literals may remain.
    
- Group of 2 → 3 literals may remain.
    
- Group of 4 → 2 literals may remain.
    
- Group of 8 → 1 literal may remain.
    
- Group of 16 → result is 1.
    

### What You Should Practise Next

Solve at least five K-map simplifications by hand:

1. One 2-variable SOP problem.
    
2. One 3-variable SOP problem.
    
3. One 4-variable SOP problem involving wrap-around.
    
4. One POS problem grouping 0s.
    
5. One don't-care problem.
    

The goal is not merely to memorize the final expression. Practise identifying minterms, placing them correctly, choosing the largest valid groups, and deriving the simplified expression.