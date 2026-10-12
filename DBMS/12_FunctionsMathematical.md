# SQL Functions: Mathematical Functions — DSSSB TGT Computer Science

These three mathematical SQL functions are useful for query-writing and output-based MCQs:

- `POWER()` — raises a number to a power.
    
- `ROUND()` — rounds a number to a specified number of decimal places.
    
- `MOD()` — returns the remainder after division.
    

The examples below use common SQL syntax. Small differences in behavior can occur across MySQL, PostgreSQL, Oracle, SQL Server and SQLite.

## 1. `POWER()` function

`POWER()` calculates a number raised to a specified exponent.

### Syntax

```
POWER(base, exponent)
```

- `base`: The number being raised to a power.
    
- `exponent`: The power to which the base is raised.
    

### Examples

```
SELECT POWER(2, 3);
```

Output:

|Result|
|---|
|8|

Because:

\[ 2^3 = 2 \times 2 \times 2 = 8 \]

More examples:

|Query|Result|Explanation|
|---|---|---|
|`POWER(5, 2)`|25|\(5^2\)|
|`POWER(3, 3)`|27|\(3^3\)|
|`POWER(10, 0)`|1|\(10^0\)|
|`POWER(4, 0.5)`|2|Square root of 4|
|`POWER(2, -2)`|0.25|\(1/2^2\)|

### Example with table data

Suppose a table `NUMBERS` contains:

|N|
|---|
|2|
|3|
|5|

Query:

```
SELECT N, POWER(N, 2) AS Square
FROM Numbers;
```

Output:

|N|Square|
|---|---|
|2|4|
|3|9|
|5|25|

Exam traps:

- `POWER(2, 3)` is 8, not 6.
    
- Any nonzero number raised to the power 0 equals 1.
    
- A negative exponent gives a reciprocal for a nonzero base.
    
- `POWER()` may be available under the name `POW()` in some DBMSs.
    
- Negative bases with fractional exponents can produce errors or non-real results, depending on the system.
    

## 2. `ROUND()` function

`ROUND()` rounds a numeric value to a specified number of decimal places.

### Syntax

```
ROUND(number, decimal_places)
```

The second argument specifies the number of decimal places to retain in common SQL implementations.

### Example 1: Round to two decimal places

```
SELECT ROUND(123.456, 2);
```

Output:

|Result|
|---|
|123.46|

The third decimal digit is `6`, so the hundredths digit is rounded upward.

### Example 2: Round to one decimal place

```
SELECT ROUND(123.456, 1);
```

Output:

|Result|
|---|
|123.5|

### Example 3: Round to zero decimal places

```
SELECT ROUND(123.456, 0);
```

Output:

|Result|
|---|
|123|

### Example 4: Round to the nearest tens or hundreds

In many SQL implementations, a negative second argument rounds to the left of the decimal point.

```
SELECT ROUND(127.45, -1);
```

Typical output:

|Result|
|---|
|130|

```
SELECT ROUND(127.45, -2);
```

Typical output:

|Result|
|---|
|100|

Support for negative precision and exact rounding rules can vary by DBMS and numeric type.

### Quick reference

|Query|Typical result|
|---|---|
|`ROUND(45.678, 2)`|45.68|
|`ROUND(45.678, 1)`|45.7|
|`ROUND(45.678, 0)`|46|
|`ROUND(45.678, -1)`|50|
|`ROUND(12.34, 1)`|12.3|

### Important: `ROUND()` vs `TRUNCATE()`

`ROUND()` rounds the value; truncation discards digits beyond the specified precision without rounding.

For example, under common SQL semantics:

```
SELECT ROUND(12.78, 1);
```

Result: `12.8`

A truncation operation at one decimal place would typically produce `12.7`. The exact truncation function and syntax depend on the DBMS.

Exam traps:

- The second argument of `ROUND()` is the number of decimal places, not the number of digits in the entire number.
    
- Rounding rules at exact halfway values, especially for approximate floating-point numbers, can vary by DBMS and data type.
    
- Do not confuse rounding with truncation.
    

## 3. `MOD()` function

`MOD()` returns the remainder after division of one number by another.

### Syntax

```
MOD(dividend, divisor)
```

- `dividend`: The number being divided.
    
- `divisor`: The number by which it is divided.
    

### Example 1

```
SELECT MOD(10, 3);
```

Output:

|Result|
|---|
|1|

Explanation:

\[ 10 = (3 \times 3) + 1 \]

The remainder is 1.

### Example 2: Exact division

```
SELECT MOD(12, 4);
```

Output:

|Result|
|---|
|0|

Since 12 is divisible by 4, the remainder is zero.

### Example 3: Odd or even numbers

`MOD()` can be used to test whether an integer is odd or even.

```
SELECT MOD(8, 2);
```

Result: `0`, so 8 is even.

```
SELECT MOD(7, 2);
```

Result: `1`, so 7 is odd.

Typical query to find even student IDs:

```
SELECT StudentID, Name
FROM Student
WHERE MOD(StudentID, 2) = 0;
```

### Example 4: MOD with table data

Suppose `NUMBERS` contains `7`, `10` and `15`.

```
SELECT N, MOD(N, 2) AS Remainder
FROM Numbers;
```

Output:

|N|Remainder|
|---|---|
|7|1|
|10|0|
|15|1|

### MOD versus division

|Expression|Result|Meaning|
|---|---|---|
|`10 / 3`|Approximately 3.333|Division|
|`MOD(10, 3)`|1|Remainder|
|`MOD(12, 4)`|0|No remainder|
|`MOD(9, 2)`|1|Odd number|

Exam traps:

- `MOD(10, 3)` returns 1, not 3.
    
- If `MOD(N, 2) = 0`, an integer `N` is even.
    
- If `MOD(N, 2) = 1`, a nonnegative integer `N` is odd.
    
- Using zero as the divisor can cause an error or produce a special result, depending on the DBMS.
    
- With negative numbers, remainder conventions may differ across DBMSs. Use positive values for straightforward exam calculations unless the question specifies the database's rules.
    

## 4. Comparison of all three functions

| Function  | Purpose                | Example           | Result |
| --------- | ---------------------- | ----------------- | ------ |
| `POWER()` | Exponentiation         | `POWER(2, 4)`     | 16     |
| `ROUND()` | Rounds a numeric value | `ROUND(5.678, 2)` | 5.68   |
| `MOD()`   | Remainder              | `MOD(17, 5)`      | 2      |
### Last-minute revision

- `POWER(a, b)` → \(a^b\)
    
- `ROUND(n, d)` → rounds `n` to `d` decimal places; negative precision may round to tens, hundreds, etc.
    
- `MOD(a, b)` → remainder when `a` is divided by `b`.
    

Quick memory trick: POWER raises, ROUND rounds, MOD gives the remainder.