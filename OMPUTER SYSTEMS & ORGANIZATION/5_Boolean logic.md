# BOOLEAN LOGIC — DSSSB TGT COMPUTER SCIENCE

Boolean logic is a branch of mathematics in which variables have only two possible values:

- `0` = False
    
- `1` = True
    

It is fundamental to digital electronics, computer organization, logic circuits, and programming.

**DSSSB exam focus:** Logic gates, truth tables, Boolean expressions, De Morgan’s laws, universal gates, and gate-output calculations.

## 1. Basic Boolean Operators

The three fundamental operations are NOT, AND, and OR.

### NOT — Complement

Reverses the input.

[  
Y=\overline A  
]

- If (A=0), then (Y=1).
    
- If (A=1), then (Y=0).
    

### AND — Logical multiplication

Output is 1 only when both inputs are 1.

[  
Y=A\cdot B=AB  
]

### OR — Logical addition

Output is 1 when at least one input is 1.

[  
Y=A+B  
]

**Exam trap:** In Boolean algebra, `+` represents OR and multiplication represents AND. These symbols do not follow ordinary arithmetic rules.

## 2. Logic Gates and Truth Tables

A logic gate is an electronic circuit that performs a Boolean operation on one or more binary inputs.

### A. NOT Gate

The NOT gate has one input and one output.

[  
Y=\overline A  
]

|Input (A)|Output (Y)|
|---|---|
|0|1|
|1|0|

**Exam point:** NOT is also called an **inverter**. Complement notation includes (\overline A), (A'), and `NOT A`.

### B. AND Gate

The AND gate produces 1 only when both inputs are 1.

[  
Y=A\cdot B  
]

|(A)|(B)|(Y=AB)|
|---|---|---|
|0|0|0|
|0|1|0|
|1|0|0|
|1|1|1|

**Memory trick:** AND means both conditions must be satisfied.

### C. OR Gate

The OR gate produces 1 if at least one input is 1.

[  
Y=A+B  
]

|(A)|(B)|(Y=A+B)|
|---|---|---|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|1|

**Exam trap:** Boolean OR is not ordinary arithmetic addition. For example, (1+1=1) in Boolean algebra.

### D. NAND Gate

NAND means **NOT AND**. It is the complement of the AND gate.

[  
Y=\overline{AB}  
]

|(A)|(B)|(Y=\overline{AB})|
|---|---|---|
|0|0|1|
|0|1|1|
|1|0|1|
|1|1|0|

**Remember:** NAND produces 0 only when both inputs are 1.

### E. NOR Gate

NOR means **NOT OR**.

[  
Y=\overline{A+B}  
]

|(A)|(B)|(Y=\overline{A+B})|
|---|---|---|
|0|0|1|
|0|1|0|
|1|0|0|
|1|1|0|

**Remember:** NOR produces 1 only when both inputs are 0.

### F. XOR Gate

XOR stands for Exclusive OR. Its output is 1 when the inputs are different.

[  
Y=A\oplus B  
]

|(A)|(B)|(Y=A\oplus B)|
|---|---|---|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|0|

**Memory trick:** XOR means “different inputs produce 1.”

### G. XNOR Gate

XNOR is the complement of XOR. Its output is 1 when both inputs are the same.

[  
Y=\overline{A\oplus B}  
]

|(A)|(B)|(Y=\overline{A\oplus B})|
|---|---|---|
|0|0|1|
|0|1|0|
|1|0|0|
|1|1|1|

**Memory trick:** XNOR means “matching inputs produce 1.”

## 3. All Gates — Quick Comparison

|Gate|Boolean expression|Output is 1 when…|
|---|---|---|
|NOT|(\overline A)|Input is 0|
|AND|(AB)|Both inputs are 1|
|OR|(A+B)|At least one input is 1|
|NAND|(\overline{AB})|At least one input is 0|
|NOR|(\overline{A+B})|Both inputs are 0|
|XOR|(A\oplus B)|Inputs differ|
|XNOR|(\overline{A\oplus B})|Inputs match|

### Universal Gates

**NAND and NOR are called universal gates** because any Boolean function can be implemented using only NAND gates or only NOR gates.

#### NOT using NAND

Connect both NAND inputs to (A):

[  
Y=\overline{A\cdot A}=\overline A  
]

#### NOT using NOR

Connect both NOR inputs to (A):

[  
Y=\overline{A+A}=\overline A  
]

This is a common digital-electronics MCQ topic.

## 4. De Morgan’s Laws

De Morgan’s laws describe how negation interacts with AND and OR. They are useful for simplifying Boolean expressions and understanding NAND/NOR circuits.

### First Law: Complement of AND

[  
\boxed{\overline{AB}=\overline A+\overline B}  
]

**In words:** The complement of AND equals the OR of the complemented inputs.

**Example:** Let (A=1) and (B=0).

Left side:

[  
\overline{1\cdot0}=\overline0=1  
]

Right side:

[  
\overline1+\overline0=0+1=1  
]

Both sides equal 1.

### Second Law: Complement of OR

[  
\boxed{\overline{A+B}=\overline A\cdot\overline B}  
]

**In words:** The complement of OR equals the AND of the complemented inputs.

**Example:** Let (A=1) and (B=0).

Left side:

[  
\overline{1+0}=\overline1=0  
]

Right side:

[  
\overline1\cdot\overline0=0\cdot1=0  
]

Both sides equal 0.

### Verify Both Laws Using a Truth Table

|(A)|(B)|(\overline{AB})|(\overline A+\overline B)|(\overline{A+B})|(\overline A\cdot\overline B)|
|---|---|---|---|---|---|
|0|0|1|1|1|1|
|0|1|1|1|0|0|
|1|0|1|1|0|0|
|1|1|0|0|0|0|

The matching columns verify both laws.

### How to Apply De Morgan’s Laws

Whenever a complement covers an entire expression:

1. Complement each variable.
    
2. Change AND to OR, or OR to AND.
    
3. Preserve the resulting complement on every variable.
    

**Examples:**

[  
\overline{A+B+C}=\overline A\cdot\overline B\cdot\overline C  
]

[  
\overline{ABC}=\overline A+\overline B+\overline C  
]

[  
\overline{A+\overline B}=\overline A\cdot B  
]

**Common exam trap:** Do not simply swap AND and OR. You must also complement every term inside the expression.

## 5. Last-Minute Revision

- **AND:** Output 1 only if all inputs are 1.
    
- **OR:** Output 1 if at least one input is 1.
    
- **NOT:** Reverses the input.
    
- **NAND:** Complement of AND.
    
- **NOR:** Complement of OR.
    
- **XOR:** Output 1 when inputs differ.
    
- **XNOR:** Output 1 when inputs match.
    
- **Universal gates:** NAND and NOR.
    
- **De Morgan’s first law:** ((AB)'=A'+B').
    
- **De Morgan’s second law:** ((A+B)'=A'B').
    

## 6. Recommended Next Topics

Study these topics next, in order:

1. Boolean algebra laws and simplification.
    
2. Half adders and full adders.
    
3. Multiplexers and demultiplexers.
    
4. Encoders and decoders.
    

These topics build directly on Boolean logic and are useful for digital-electronics preparation.