# DIGITAL ELECTRONICS — NUMBER SYSTEMS

## 1. The Four Number Systems

A number system has a base (radix) that determines the digits it can use.

|Number System|Base|Permitted Digits|Example|
|---|---|---|---|
|Binary|2|0, 1|1011₂|
|Octal|8|0–7|57₈|
|Decimal|10|0–9|25₁₀|
|Hexadecimal|16|0–9, A–F|2F₁₆|

In hexadecimal:

A = 10, B = 11, C = 12, D = 13, E = 14, F = 15.

### Positional Value

Each digit's value depends on its position and the base.

Example: Convert 1011₂ to decimal.

1011₂ = 1 × 2³ + 0 × 2² + 1 × 2¹ + 1 × 2⁰

= 8 + 0 + 2 + 1

= 11₁₀

The rightmost digit has position 0, followed by positions 1, 2, 3, and so on.

## 2. Binary to Decimal

Multiply each binary digit by its corresponding power of 2, then add the results.

Example: Convert 110101₂ to decimal.

|Binary Digit|Power of 2|Value|
|---|---|---|
|1|2⁵|32|
|1|2⁴|16|
|0|2³|0|
|1|2²|4|
|0|2¹|0|
|1|2⁰|1|

Therefore:

110101₂ = 32 + 16 + 0 + 4 + 0 + 1

110101₂ = 53₁₀

## 3. Decimal to Binary

Repeatedly divide the decimal number by 2. Record the remainders and read them from bottom to top.

Example: Convert 25₁₀ to binary.

|Division|Quotient|Remainder|
|---|---|---|
|25 ÷ 2|12|1|
|12 ÷ 2|6|0|
|6 ÷ 2|3|0|
|3 ÷ 2|1|1|
|1 ÷ 2|0|1|

Reading the remainders from bottom to top:

25₁₀ = 11001₂

Exam tip: Never read the remainders from top to bottom.

## 4. Binary to Octal

Shortcut: Group binary digits into sets of 3, starting from the right. Add leading zeros if necessary.

Example: Convert 1101011₂ to octal.

Step 1: Group the digits.

001 101 011

Step 2: Convert each group.

001₂ = 1₈

101₂ = 5₈

011₂ = 3₈

Therefore:

1101011₂ = 153₈

## 5. Octal to Binary

Replace each octal digit with its 3-bit binary equivalent.

Example: Convert 572₈ to binary.

5₈ = 101₂

7₈ = 111₂

2₈ = 010₂

Combine the groups:

572₈ = 101111010₂

## 6. Binary to Hexadecimal

Shortcut: Group binary digits into sets of 4, starting from the right. Add leading zeros if necessary.

|Binary|Hexadecimal|Binary|Hexadecimal|
|---|---|---|---|
|0000|0|1000|8|
|0001|1|1001|9|
|0010|2|1010|A|
|0011|3|1011|B|
|0100|4|1100|C|
|0101|5|1101|D|
|0110|6|1110|E|
|0111|7|1111|F|

Example: Convert 11010111₂ to hexadecimal.

Group into 4-bit sets:

1101 0111

1101₂ = D₁₆

0111₂ = 7₁₆

Therefore:

11010111₂ = D7₁₆

## 7. Hexadecimal to Binary

Replace every hexadecimal digit with its 4-bit binary equivalent.

Example: Convert 3A7₁₆ to binary.

3₁₆ = 0011₂

A₁₆ = 1010₂

7₁₆ = 0111₂

Therefore:

3A7₁₆ = 001110100111₂

Leading zeros may be removed when the bit width does not need to be preserved.

## 8. Octal and Hexadecimal to Decimal

Use positional powers of the relevant base.

### Example A: Convert 157₈ to decimal

157₈ = 1 × 8² + 5 × 8¹ + 7 × 8⁰

= 64 + 40 + 7

= 111₁₀

### Example B: Convert 2F₁₆ to decimal

Remember: F = 15.

2F₁₆ = 2 × 16¹ + 15 × 16⁰

= 32 + 15

= 47₁₀

### Example C: Convert 254₁₀ to hexadecimal

Divide repeatedly by 16.

254 ÷ 16 = 15, remainder 14 (E)

15 ÷ 16 = 0, remainder 15 (F)

Read the remainders from bottom to top:

254₁₀ = FE₁₆

## 9. One's Complement

The 1's complement of a binary number is obtained by flipping every bit.

0 becomes 1.

1 becomes 0.

Example using 8 bits:

Original: 00001101

1's complement: 11110010

Therefore, the 1's complement of 00001101 is 11110010.

### Important Facts

- Every 0 becomes 1, and every 1 becomes 0.
    
- The number of bits remains unchanged.
    
- Traditional signed 1's complement has two representations of zero: positive zero and negative zero.
    
- For an n-bit signed 1's-complement number, the range is:
    

−(2ⁿ⁻¹ − 1) to +(2ⁿ⁻¹ − 1)

For 8 bits, the range is −127 to +127.

## 10. Two's Complement

The 2's complement is obtained by taking the 1's complement and adding 1.

2's complement = 1's complement + 1

Example: Find the 2's complement of 00001101.

Step 1: Original number

00001101

Step 2: Flip every bit.

11110010

Step 3: Add 1.

11110010

- 00000001
    

---

11110011

Therefore, the 2's complement is 11110011.

### Why Is Two's Complement Important?

Computers commonly use 2's complement to represent signed integers because addition and subtraction can use the same binary arithmetic hardware.

For an n-bit 2's-complement number, the range is:

−2ⁿ⁻¹ to +(2ⁿ⁻¹ − 1)

For 8 bits, the range is −128 to +127.

Unlike 1's complement, standard 2's complement has only one representation of zero.

## 11. Representing Negative Numbers

To represent a negative number using 2's complement:

1. Write the positive number in binary using the required bit width.
    
2. Flip every bit.
    
3. Add 1.
    

Example: Represent −13 using 8-bit 2's complement.

|Step|Result|
|---|---|
|+13 in 8-bit binary|00001101|
|Flip all bits|11110010|
|Add 1|11110011|

Therefore:

−13 = 11110011 in 8-bit 2's-complement representation.

Verification: Since the most significant bit is 1, the value is negative. Taking the 2's complement again gives 00001101, which is 13.

## 12. Binary Addition and Subtraction

### Binary Addition Rules

|Operation|Result|
|---|---|
|0 + 0|0|
|0 + 1|1|
|1 + 0|1|
|1 + 1|10|
|1 + 1 + 1|11|

Example: Add 1011₂ and 0110₂.

1011

- 0110
    

---

10001

Check in decimal:

11 + 6 = 17

10001₂ = 17₁₀

### Subtraction Using Two's Complement

To calculate A − B:

1. Represent A and B using the same number of bits.
    
2. Find the 2's complement of B.
    
3. Add it to A.
    
4. Discard the carry beyond the fixed bit width, if one occurs.
    
5. Interpret the result according to the signed or unsigned convention.
    

Example: Calculate 9 − 5 using 4-bit arithmetic.

A = 9 = 1001

B = 5 = 0101

1's complement of B = 1010

2's complement of B = 1011

1001

- 1011
    

---

10100

Discard the carry beyond 4 bits:

0100₂ = 4₁₀

Therefore:

9 − 5 = 4

## 13. Quick Conversion Reference

|Decimal|Binary|Octal|Hexadecimal|
|---|---|---|---|
|10|1010|12|A|
|15|1111|17|F|
|16|10000|20|10|
|25|11001|31|19|
|31|11111|37|1F|
|64|1000000|100|40|
|100|1100100|144|64|
|255|11111111|377|FF|

### Final Exam Revision Tips

- Binary to octal: group bits in sets of 3.
    
- Binary to hexadecimal: group bits in sets of 4.
    
- Binary to decimal: multiply each digit by the corresponding power of 2.
    
- Decimal to binary: repeated division by 2.
    
- Decimal to hexadecimal: repeated division by 16.
    
- 1's complement: flip all bits.
    
- 2's complement: flip all bits and add 1.
    
- n-bit 2's-complement range: −2ⁿ⁻¹ to +(2ⁿ⁻¹ − 1).