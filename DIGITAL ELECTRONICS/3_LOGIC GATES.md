
Logic gates are the basic building blocks of digital circuits. They take binary inputs (0 or 1) and produce a binary output according to a Boolean operation.

For DSSSB, focus on gate symbols, Boolean expressions, truth tables, universal gates, and XOR/XNOR differences.

## 1. AND Gate

**Boolean expression:** Y = A · B = AB

Output is 1 only when both inputs are 1.

Think of two switches connected in series: both must be ON.

|A|B|Y = AB|
|---|---|---|
|0|0|0|
|0|1|0|
|1|0|0|
|1|1|1|

**Shortcut:** AND gives 1 only for input combination 11.

## 2. OR Gate

**Boolean expression:** Y = A + B

Output is 1 when at least one input is 1.

Think of two switches connected in parallel: either one can turn the output ON.

|A|B|Y = A + B|
|---|---|---|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|1|

**Shortcut:** OR gives 0 only for input combination 00.

## 3. NOT Gate

**Boolean expression:** Y = A′

NOT has one input and reverses it.

|A|Y = A′|
|---|---|
|0|1|
|1|0|

**Exam tip:** A small circle (bubble) at a gate's input or output usually indicates inversion.

## 4. NAND Gate

**Boolean expression:** Y = (AB)′

NAND means NOT AND. It is an AND gate followed by a NOT operation.

|A|B|Y = (AB)′|
|---|---|---|
|0|0|1|
|0|1|1|
|1|0|1|
|1|1|0|

**Shortcut:** NAND gives 0 only for input combination 11.

## 5. NOR Gate

**Boolean expression:** Y = (A + B)′

NOR means NOT OR. It is an OR gate followed by a NOT operation.

|A|B|Y = (A + B)′|
|---|---|---|
|0|0|1|
|0|1|0|
|1|0|0|
|1|1|0|

**Shortcut:** NOR gives 1 only for input combination 00.

## 6. XOR Gate — Exclusive OR

**Boolean expression:**

Y = A ⊕ B = A′B + AB′

Output is 1 when the two inputs are different.

|A|B|Y = A ⊕ B|
|---|---|---|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|0|

**Applications:** Half adders and parity-generation circuits.

**Shortcut:** XOR gives 1 for 01 and 10.

## 7. XNOR Gate — Exclusive NOR

**Boolean expression:**

Y = (A ⊕ B)′ = AB + A′B′

Output is 1 when the two inputs are the same.

|A|B|Y = (A ⊕ B)′|
|---|---|---|
|0|0|1|
|0|1|0|
|1|0|0|
|1|1|1|

**Applications:** Equality comparison of bits.

**Shortcut:** XNOR gives 1 for 00 and 11.

## 8. Master Truth Table — All Seven Gates

This is one of the most important tables to memorize for objective questions.

|A|B|AND|OR|NAND|NOR|XOR|XNOR|
|---|---|---|---|---|---|---|---|
|0|0|0|0|1|1|0|1|
|0|1|0|1|1|0|1|0|
|1|0|0|1|1|0|1|0|
|1|1|1|1|0|0|0|1|

NOT is a single-input gate and has a separate truth table.

## 9. Universal Gates — NAND and NOR

A universal gate can be used by itself, in combinations, to construct any Boolean function.

### A. Constructing Gates Using NAND

**NOT using NAND**

A NAND A = A′

**AND using NAND**

Let X = A NAND B = (AB)′.

Then:

X NAND X = X′ = AB

Therefore:

AB = (A NAND B) NAND (A NAND B)

**OR using NAND**

Using De Morgan's law:

A + B = (A′B′)′

Therefore:

A + B = (A NAND A) NAND (B NAND B)

### B. Constructing Gates Using NOR

**NOT using NOR**

A NOR A = A′

**OR using NOR**

Let X = A NOR B = (A + B)′.

Then:

X NOR X = X′ = A + B

Therefore:

A + B = (A NOR B) NOR (A NOR B)

**AND using NOR**

Using De Morgan's law:

AB = (A′ + B′)′

Therefore:

AB = (A NOR A) NOR (B NOR B)

**Exam fact:** Both NAND and NOR are universal gates.

## 10. Important Applications of Logic Gates

|Gate|Typical Application|
|---|---|
|AND|Enable circuits and conditions that must all be true|
|OR|Combining alternative conditions|
|NOT|Inversion and signal complementing|
|NAND|Universal logic implementation|
|NOR|Universal logic implementation|
|XOR|Sum output in a half adder; parity generation|
|XNOR|Equality comparison of bits|

For a half adder:

Sum = A ⊕ B

Carry = AB

## 11. Quick Revision Table

|Gate|Output Rule|Output Is 1 When|
|---|---|---|
|AND|AB|Both inputs are 1|
|OR|A + B|At least one input is 1|
|NOT|A′|Input is 0|
|NAND|(AB)′|At least one input is 0|
|NOR|(A + B)′|Both inputs are 0|
|XOR|A ⊕ B|Inputs are different|
|XNOR|(A ⊕ B)′|Inputs are equal|

### Final Revision Trick

- AND: Both inputs 1 → output 1.
    
- OR: At least one input 1 → output 1.
    
- NOT: Reverses the input.
    
- NAND: AND followed by NOT.
    
- NOR: OR followed by NOT.
    
- XOR: Different inputs → 1.
    
- XNOR: Equal inputs → 1.
    
- Universal gates: NAND and NOR.