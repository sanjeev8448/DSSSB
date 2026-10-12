# SQL Operators — Complete Notes for DSSSB TGT Computer Science

These SQL operators are used to filter records and build conditions in `WHERE`, `HAVING`, and other SQL expressions. For the exam, focus on operator syntax, output-based questions, logical operator precedence, wildcard patterns, inclusive ranges, and NULL-related traps.

We will use the same `STUDENT` table throughout.

|StudentID|Name|City|Marks|
|---|---|---|---|
|101|Amit|Delhi|85|
|102|Neha|Patna|92|
|103|Ravi|Delhi|76|
|104|Priya|Jaipur|88|
|105|Karan|Delhi|92|
|106|Sana|Patna|67|

## 1. IN operator

The `IN` operator checks whether a value matches any value in a specified list or the result of a subquery.

### Syntax

```
SELECT column_name
FROM table_name
WHERE column_name IN (value1, value2, ...);
```

### Example 1: Find students from Delhi or Patna

```
SELECT Name, City
FROM Student
WHERE City IN ('Delhi', 'Patna');
```

Result:

|Name|City|
|---|---|
|Amit|Delhi|
|Neha|Patna|
|Ravi|Delhi|
|Karan|Delhi|
|Sana|Patna|

This is equivalent to:

```
SELECT Name, City
FROM Student
WHERE City = 'Delhi'
   OR City = 'Patna';
```

### Example 2: IN with numbers

```
SELECT Name, Marks
FROM Student
WHERE Marks IN (76, 85, 92);
```

Result:

|Name|Marks|
|---|---|
|Amit|85|
|Neha|92|
|Ravi|76|
|Karan|92|

### Example 3: NOT IN

`NOT IN` checks whether a value does not match any value in the specified set.

```
SELECT Name, City
FROM Student
WHERE City NOT IN ('Delhi', 'Patna');
```

Result:

|Name|City|
|---|---|
|Priya|Jaipur|

### Example 4: IN with a subquery

```
SELECT Name
FROM Student
WHERE City IN (
    SELECT City
    FROM Student
    WHERE Marks > 90
);
```

The inner query returns the cities of students scoring above 90. In our example, both qualifying rows belong to Patna, so the outer query returns students from Patna.

Important exam traps:

- `IN` is a convenient alternative to multiple equality conditions joined by `OR`.
    
- `NOT IN` and `IN` can be used with subqueries.
    
- Be careful if a `NOT IN` list or subquery includes `NULL`: the result can become `UNKNOWN`, causing otherwise expected rows to be filtered out.
    
- Text values should normally be enclosed in single quotes.
    

## 2. BETWEEN operator

`BETWEEN` checks whether a value falls within a specified range.

### Syntax

```
SELECT column_name
FROM table_name
WHERE column_name BETWEEN lower_value AND upper_value;
```

The endpoints are inclusive.

### Example 1: Marks between 80 and 90

```
SELECT Name, Marks
FROM Student
WHERE Marks BETWEEN 80 AND 90;
```

Result:

|Name|Marks|
|---|---|
|Amit|85|
|Priya|88|

Marks of exactly 80 or 90 would also qualify.

### Equivalent condition

```
WHERE Marks >= 80 AND Marks <= 90
```

Thus:

\[ A\ \text{BETWEEN}\ x\ \text{AND}\ y \]

is equivalent to:

\[ A \geq x\ \text{AND}\ A \leq y \]

for ordinary non-NULL comparisons.

### Example 2: NOT BETWEEN

```
SELECT Name, Marks
FROM Student
WHERE Marks NOT BETWEEN 80 AND 90;
```

Result:

|Name|Marks|
|---|---|
|Neha|92|
|Ravi|76|
|Karan|92|
|Sana|67|

Important exam traps:

- `BETWEEN 80 AND 90` includes both 80 and 90.
    
- `NOT BETWEEN 80 AND 90` excludes the range endpoints as well.
    
- If the tested value is `NULL`, the range comparison is `UNKNOWN`, not `TRUE`.
    
- `BETWEEN` can also be used with dates and other comparable values. For timestamps, remember that time components affect which values fall within the range.
    

## 3. LIKE operator

The `LIKE` operator is used to match text against a pattern. It is commonly used for searching names, email addresses, and other character data.

SQL provides two main wildcards for `LIKE`:

- `%` matches zero or more characters.
    
- `_` matches exactly one character.
    

### Example 1: Names beginning with A

```
SELECT Name
FROM Student
WHERE Name LIKE 'A%';
```

Result:

|Name|
|---|
|Amit|

`A%` means the name begins with `A`, followed by any sequence of characters, including an empty sequence.

### Example 2: Names ending with a

```
SELECT Name
FROM Student
WHERE Name LIKE '%a';
```

Result:

|Name|
|---|
|Neha|
|Priya|
|Sana|

The pattern `%a` means any sequence of characters followed by `a`.

### Example 3: Names containing `an`

```
SELECT Name
FROM Student
WHERE Name LIKE '%an%';
```

Result:

|Name|
|---|
|Karan|

`%an%` finds the sequence `an` anywhere in the name.

### Example 4: Use the single-character wildcard `_`

```
SELECT Name
FROM Student
WHERE Name LIKE '_a%';
```

Result:

|Name|
|---|
|Karan|
|Sana|

Explanation:

- `_` matches the first character.
    
- `a` must be the second character.
    
- `%` matches whatever follows.
    

`Karan` and `Sana` both have `a` as their second character.

### LIKE pattern revision

|Pattern|Meaning|Example match|
|---|---|---|
|`'A%'`|Starts with A|Amit|
|`'%a'`|Ends with a|Neha|
|`'%an%'`|Contains `an`|Karan|
|`'_a%'`|Second character is a|Karan|
|`'____'`|Exactly four characters|Neha|
|`'A_i%'`|Begins with A, third character is i|Amit|

### NOT LIKE

```
SELECT Name
FROM Student
WHERE Name NOT LIKE 'A%';
```

This excludes names beginning with `A`.

Important exam traps:

- `%` can match zero characters; `_` matches one character.
    
- `'____'` matches four characters under the usual `LIKE` pattern rules.
    
- Case sensitivity depends on the DBMS and collation.
    
- `LIKE` is generally used for character-pattern matching; do not confuse it with numeric range comparisons.
    

### Bonus: Matching a literal wildcard

If you need to search for a literal `%` or `_`, use an escape character where supported.

```
SELECT ProductName
FROM Product
WHERE ProductName LIKE '%\%%' ESCAPE '\';
```

This example matches product names containing a literal percent sign. The escape syntax and string-literal rules can vary by DBMS.

## 4. IS NULL operator

In SQL, `NULL` represents missing, unknown, or unavailable information. It is not the same as zero, an empty string, or a normal text value.

To test for NULL, SQL uses `IS NULL` and `IS NOT NULL`.

### Example 1: Find students whose city is missing

```
SELECT Name
FROM Student
WHERE City IS NULL;
```

This returns names for rows where `City` has a NULL value.

Our sample table has no NULL city values, so the result is empty.

### Example 2: Find students with a known city

```
SELECT Name
FROM Student
WHERE City IS NOT NULL;
```

All six students in our current sample qualify.

### The most important NULL trap

This is not the correct way to test for NULL:

```
WHERE City = NULL
```

Use:

```
WHERE City IS NULL
```

Why? A comparison such as `City = NULL` evaluates to `UNKNOWN`, rather than `TRUE`, under SQL's NULL logic.

For the same reason:

```
WHERE City <> NULL
```

does not correctly find non-NULL cities either. Use `IS NOT NULL`.

### NULL vs common values

|Value|Meaning|
|---|---|
|`NULL`|Missing or unknown value|
|`0`|Numeric zero|
|`''`|Empty string in systems that distinguish it from NULL|
|`'NULL'`|Literal text containing the word NULL|

Exam note: Oracle traditionally treats a zero-length character string as NULL, unlike many other DBMSs. The distinction between an empty string and NULL is therefore database-dependent.

## 5. AND operator

`AND` combines two conditions. The combined condition is `TRUE` only when both conditions are true.

### Example

```
SELECT Name, City, Marks
FROM Student
WHERE City = 'Delhi'
  AND Marks > 80;
```

Result:

|Name|City|Marks|
|---|---|---|
|Amit|Delhi|85|
|Karan|Delhi|92|

The student must both belong to Delhi and have marks above 80.

### AND truth table

|A|B|A AND B|
|---|---|---|
|TRUE|TRUE|TRUE|
|TRUE|FALSE|FALSE|
|FALSE|TRUE|FALSE|
|FALSE|FALSE|FALSE|

SQL also has `UNKNOWN` because of NULL values. For example:

|A|B|A AND B|
|---|---|---|
|TRUE|UNKNOWN|UNKNOWN|
|FALSE|UNKNOWN|FALSE|
|UNKNOWN|UNKNOWN|UNKNOWN|

A `WHERE` clause includes only rows where the condition evaluates to `TRUE`. Rows evaluating to `FALSE` or `UNKNOWN` are not returned.

## 6. OR operator

`OR` combines conditions. The result is `TRUE` when at least one condition is true.

### Example

```
SELECT Name, City
FROM Student
WHERE City = 'Jaipur'
   OR City = 'Patna';
```

Result:

|Name|City|
|---|---|
|Neha|Patna|
|Priya|Jaipur|
|Sana|Patna|

### OR truth table

|A|B|A OR B|
|---|---|---|
|TRUE|TRUE|TRUE|
|TRUE|FALSE|TRUE|
|FALSE|TRUE|TRUE|
|FALSE|FALSE|FALSE|

With SQL's three-valued logic:

|A|B|A OR B|
|---|---|---|
|TRUE|UNKNOWN|TRUE|
|FALSE|UNKNOWN|UNKNOWN|
|UNKNOWN|UNKNOWN|UNKNOWN|

Exam trap: `OR` does not require both conditions to be true.

## 7. NOT operator

`NOT` reverses a logical condition:

- `NOT TRUE` becomes `FALSE`.
    
- `NOT FALSE` becomes `TRUE`.
    
- `NOT UNKNOWN` remains `UNKNOWN`.
    

### Example 1: Exclude Delhi students

```
SELECT Name, City
FROM Student
WHERE NOT City = 'Delhi';
```

This returns rows whose city is known and is not Delhi. It does not return a row with `City = NULL`, because the negated comparison remains `UNKNOWN`.

A common alternative is:

```
SELECT Name, City
FROM Student
WHERE City <> 'Delhi';
```

For ordinary non-NULL city values, these are equivalent.

### Example 2: NOT with IN

```
SELECT Name, City
FROM Student
WHERE City NOT IN ('Delhi', 'Patna');
```

This returns Priya from Jaipur in our sample.

### Example 3: NOT with LIKE

```
SELECT Name
FROM Student
WHERE Name NOT LIKE 'A%';
```

This excludes names beginning with A.

### Example 4: NOT with BETWEEN

```
SELECT Name, Marks
FROM Student
WHERE Marks NOT BETWEEN 80 AND 90;
```

This returns students with marks below 80 or above 90, excluding NULL marks because the condition would be `UNKNOWN`.

## 8. Operator precedence — very important

When a SQL condition contains several logical operators, precedence determines how the expression is evaluated unless parentheses specify otherwise.

For the operators in your syllabus, remember:

\[ \boxed{\text{NOT} > \text{AND} > \text{OR}} \]

`NOT` has higher precedence than `AND`, and `AND` has higher precedence than `OR`.

### Example 1: Without parentheses

```
SELECT Name, City, Marks
FROM Student
WHERE City = 'Delhi'
   OR City = 'Patna'
  AND Marks > 90;
```

SQL interprets this as:

```
WHERE City = 'Delhi'
   OR (City = 'Patna' AND Marks > 90);
```

It returns:

|Name|City|Marks|
|---|---|---|
|Amit|Delhi|85|
|Ravi|Delhi|76|
|Neha|Patna|92|
|Karan|Delhi|92|

Why? Every Delhi student qualifies regardless of marks. For Patna students, marks must exceed 90.

### Example 2: With parentheses

```
SELECT Name, City, Marks
FROM Student
WHERE (City = 'Delhi' OR City = 'Patna')
  AND Marks > 90;
```

Result:

|Name|City|Marks|
|---|---|---|
|Neha|Patna|92|
|Karan|Delhi|92|

The parentheses change the logic: the student must be from Delhi or Patna, and must also score above 90.

Exam trap: The same conditions can return different rows depending on parentheses.

## 9. All seven operators at a glance

|Operator|Purpose|Example|
|---|---|---|
|`IN`|Matches any listed value|`City IN ('Delhi', 'Patna')`|
|`BETWEEN`|Tests an inclusive range|`Marks BETWEEN 80 AND 90`|
|`LIKE`|Matches a text pattern|`Name LIKE 'A%'`|
|`IS NULL`|Tests for a NULL value|`City IS NULL`|
|`AND`|Both conditions must be true|`City='Delhi' AND Marks>80`|
|`OR`|At least one condition must be true|`City='Delhi' OR City='Patna'`|
|`NOT`|Negates a condition|`City NOT LIKE 'A%'`|

### Key facts to memorize

- `IN` is convenient for several possible values.
    
- `BETWEEN` includes both boundaries.
    
- `LIKE`: `%` means zero or more characters; `_` means exactly one.
    
- NULL checks use `IS NULL` and `IS NOT NULL`.
    
- `AND` requires both conditions to be true.
    
- `OR` needs at least one condition to be true.
    
- `NOT` reverses TRUE and FALSE, while UNKNOWN remains UNKNOWN.
    
- Precedence: `NOT > AND > OR`.
    
- Use parentheses whenever a logical expression could be ambiguous.
Final revision trick: `IN` = choices; `BETWEEN` = inclusive range; `LIKE` = text pattern; `IS NULL` = missing value; `AND` = both; `OR` = either; `NOT` = opposite.