## 1. `UCASE()` — Convert to uppercase

`UCASE()` converts lowercase letters in a string to uppercase. It is synonymous with `UPPER()` in MySQL.

### Syntax

```
UCASE(string)
```

### Example

```
SELECT UCASE('Hello World');
```

Output:

|Result|
|---|
|HELLO WORLD|

More examples:

|SQL expression|Result|
|---|---|
|`UCASE('sql')`|`SQL`|
|`UCASE('Dsssb Tgt')`|`DSSSB TGT`|
|`UCASE('Computer123')`|`COMPUTER123`|

Numbers and punctuation are not converted into letters; they remain unchanged.

Exam trap: `UCASE()` changes the text returned by the expression, not the stored column values themselves.

For example:

```
SELECT UCASE(Name)
FROM Student;
```

This returns uppercase names without updating the original table.

## 2. `LCASE()` — Convert to lowercase

`LCASE()` converts uppercase letters in a string to lowercase. In MySQL, it is synonymous with `LOWER()`.

### Syntax

```
LCASE(string)
```

### Example

```
SELECT LCASE('HELLO SQL');
```

Output:

|Result|
|---|
|hello sql|

|SQL expression|Result|
|---|---|
|`LCASE('PYTHON')`|`python`|
|`LCASE('Dsssb TGT')`|`dsssb tgt`|
|`LCASE('Hello123')`|`hello123`|

### `UCASE()` vs `LCASE()`

|Function|Purpose|Example|Result|
|---|---|---|---|
|`UCASE()`|Uppercase conversion|`UCASE('Sql')`|`SQL`|
|`LCASE()`|Lowercase conversion|`LCASE('Sql')`|`sql`|

Exam trap: These functions return transformed text; they do not automatically modify the database column.

## 3. `MID()` — Extract part of a string

`MID()` extracts a substring from a string, starting at a specified position.

### Syntax

```
MID(string, start, length)
```

- `string`: The original text.
    
- `start`: The starting character position.
    
- `length`: The number of characters to extract.
    

In the MySQL-style syntax used here, positions start at 1, not 0.

### Example 1

```
SELECT MID('COMPUTER', 2, 3);
```

Output:

|Result|
|---|
|OMP|

Position breakdown:

|Character|C|O|M|P|U|T|E|R|
|---|---|---|---|---|---|---|---|---|
|Position|1|2|3|4|5|6|7|8|

Starting at position 2 and taking 3 characters gives `OMP`.

### Example 2

```
SELECT MID('DATABASE', 5, 4);
```

Output:

|Result|
|---|
|BASE|

### Example 3: Start near the end

```
SELECT MID('COMPUTER', 6, 10);
```

Output:

|Result|
|---|
|TER|

Only the available characters from the starting position are returned.

Exam traps:

- String positions in common SQL substring functions start at 1.
    
- The third argument is the number of characters to extract, not the ending position.
    
- If the requested length exceeds the available text, the result is generally limited to the remaining characters.
    
- `MID()` is not supported by every DBMS. SQL Server commonly uses `SUBSTRING(expression, start, length)` instead.
    

## 4. `LENGTH()` — Find the length of a string

`LENGTH()` returns the length of a string according to the DBMS's length semantics.

### Syntax

```
LENGTH(string)
```

### Examples

```
SELECT LENGTH('COMPUTER');
```

Output: `8`

```
SELECT LENGTH('SQL');
```

Output: `3`

```
SELECT LENGTH('');
```

Output: `0` in MySQL-style behavior for an empty string.

### Example with table data

```
SELECT Name, LENGTH(Name) AS NameLength
FROM Student;
```

For names in our sample table:

|Name|NameLength|
|---|---|
|Amit|4|
|Neha|4|
|Ravi|4|
|Priya|5|
|Karan|5|
|Sana|4|

### Important DBMS difference

Do not assume `LENGTH()` always counts characters in every SQL product.

|Function / DBMS|Important behavior|
|---|---|
|MySQL `LENGTH()`|Returns the string's length in bytes|
|MySQL `CHAR_LENGTH()`|Counts characters|
|SQL Server `LEN()`|Counts characters, excluding trailing spaces|
|Oracle `LENGTH()`|Counts characters in the string under its character-set semantics|

For example, a multibyte UTF-8 character may occupy multiple bytes in MySQL, so `LENGTH()` and `CHAR_LENGTH()` can return different results.

Exam trap: In a basic ASCII example such as `LENGTH('COMPUTER')`, both byte count and character count are 8. Differences appear with multibyte text or trailing-space behavior in certain functions.

## 5. `LEFT()` — Extract characters from the beginning

`LEFT()` returns a specified number of characters from the left side of a string.

### Syntax

```
LEFT(string, number_of_characters)
```

### Example 1

```
SELECT LEFT('COMPUTER', 3);
```

Output:

|Result|
|---|
|COM|

### Example 2

```
SELECT LEFT('DATABASE', 4);
```

Output:

|Result|
|---|
|DATA|

### Example 3

```
SELECT LEFT('SQL', 10);
```

Output:

|Result|
|---|
|SQL|

When the requested number is greater than the available string length, common implementations return the available string rather than adding extra characters.

Exam memory trick: LEFT = take characters from the beginning.

## 6. `RIGHT()` — Extract characters from the end

`RIGHT()` returns a specified number of characters from the right side of a string.

### Syntax

```
RIGHT(string, number_of_characters)
```

### Example 1

```
SELECT RIGHT('COMPUTER', 3);
```

Output:

|Result|
|---|
|TER|

### Example 2

```
SELECT RIGHT('DATABASE', 4);
```

Output:

|Result|
|---|
|BASE|

### Example 3

```
SELECT RIGHT('SQL', 10);
```

Output:

|Result|
|---|
|SQL|

### `LEFT()` vs `RIGHT()` vs `MID()`

|Function|Starting side or position|Example|Result|
|---|---|---|---|
|`LEFT()`|Beginning|`LEFT('COMPUTER', 3)`|`COM`|
|`RIGHT()`|End|`RIGHT('COMPUTER', 3)`|`TER`|
|`MID()`|Specified position|`MID('COMPUTER', 2, 3)`|`OMP`|

## 7. `INSTR()` — Find the position of a substring

`INSTR()` searches for one string inside another and returns the position of the first occurrence of the searched substring.

### Syntax

```
INSTR(string, substring)
```

### Example 1

```
SELECT INSTR('COMPUTER', 'PUT');
```

Output:

|Result|
|---|
|4|

Why? `PUT` starts at position 4 in `COMPUTER`.

### Example 2

```
SELECT INSTR('DATABASE', 'BASE');
```

Output:

|Result|
|---|
|5|

`BASE` begins at position 5.

### Example 3: Substring not found

```
SELECT INSTR('COMPUTER', 'XYZ');
```

In MySQL-style behavior, the result is `0` because the substring is not found.

### Example 4: Repeated substring

```
SELECT INSTR('BANANA', 'ANA');
```

Output: `2`

The first occurrence of `ANA` begins at character position 2.

### `INSTR()` vs `MID()`

- `INSTR()` searches for text and returns a position.
    
- `MID()` extracts text and returns the selected characters.
    

Important DBMS difference: MySQL uses `INSTR(string, substring)`. SQL Server commonly uses `CHARINDEX(substring, string)`. Oracle also provides `INSTR`, with additional optional arguments for searching positions and occurrences.

Exam trap: In MySQL-style syntax, positions start at 1, and not-found returns 0. Do not confuse the returned position with the number of characters matched.

## 8. `LTRIM()` — Remove leading spaces

`LTRIM()` removes spaces from the beginning (left side) of a string.

### Example

```
SELECT LTRIM('   SQL');
```

Output:

`SQL`

Another example:

```
SELECT LTRIM('   DSSSB   ');
```

Output, with remaining trailing spaces shown using delimiters:

`[DSSSB ]`

The spaces before `DSSSB` are removed; the trailing spaces remain.

### When is it useful?

Suppose user-entered data contains unwanted spaces at the beginning of names. `LTRIM()` can clean the leading whitespace in a query result.

Exam memory trick: LTRIM = remove left-side spaces.

## 9. `RTRIM()` — Remove trailing spaces

`RTRIM()` removes spaces from the end (right side) of a string.

### Example

```
SELECT RTRIM('SQL   ');
```

Output:

`SQL`

Another example:

```
SELECT RTRIM('   DSSSB   ');
```

Output, showing remaining spaces:

`[ DSSSB]`

The leading spaces remain, but the trailing spaces are removed.

Exam memory trick: RTRIM = remove right-side spaces.

## 10. `TRIM()` — Remove spaces from both ends

`TRIM()` removes leading spaces and trailing spaces from a string. In standard SQL syntax, you can also specify a trim direction and a trim character or set of trim characters, though exact syntax varies by DBMS.

### Example

```
SELECT TRIM('   SQL   ');
```

Output:

`SQL`

### Compare all three trimming functions

Start with the string:

`[ DSSSB ]`

|Function|Output with delimiters|What was removed?|
|---|---|---|
|`LTRIM()`|`[DSSSB ]`|Leading spaces|
|`RTRIM()`|`[ DSSSB]`|Trailing spaces|
|`TRIM()`|`[DSSSB]`|Leading and trailing spaces|

### Important exam trap: trimming is not replacement

For ordinary space-trimming behavior, these functions remove spaces at the ends, not spaces in the middle.

For example:

```
SELECT TRIM('  SQL SERVER  ');
```

Result:

`SQL SERVER`

The internal space between `SQL` and `SERVER` remains.

### `TRIM()` with a specified character

Some DBMSs support syntax that removes a specified character from the ends of a string. For example, standard-style syntax:

```
SELECT TRIM(BOTH 'x' FROM 'xxxSQLxxx');
```

Result:

`SQL`

This is a separate feature from simply trimming spaces. Support for the exact syntax varies by database system.

## 11. Full comparison table

|Function|Purpose|Example|Result|
|---|---|---|---|
|`UCASE()`|Convert to uppercase|`UCASE('sql')`|`SQL`|
|`LCASE()`|Convert to lowercase|`LCASE('SQL')`|`sql`|
|`MID()`|Extract characters by position and length|`MID('COMPUTER', 2, 3)`|`OMP`|
|`LENGTH()`|Return length under DBMS-specific semantics|`LENGTH('SQL')`|`3`|
|`LEFT()`|Extract characters from the beginning|`LEFT('COMPUTER', 3)`|`COM`|
|`RIGHT()`|Extract characters from the end|`RIGHT('COMPUTER', 3)`|`TER`|
|`INSTR()`|Find the position of a substring|`INSTR('COMPUTER', 'PUT')`|`4`|
|`LTRIM()`|Remove leading spaces|`LTRIM(' SQL')`|`SQL`|
|`RTRIM()`|Remove trailing spaces|`RTRIM('SQL ')`|`SQL`|
|`TRIM()`|Remove leading and trailing spaces|`TRIM(' SQL ')`|`SQL`|

## 12. Combined SQL practice

Consider this query:

```
SELECT
    UCASE(Name) AS UpperName,
    LENGTH(Name) AS NameLength,
    LEFT(Name, 2) AS FirstTwo,
    RIGHT(Name, 2) AS LastTwo,
    INSTR(Name, 'a') AS PositionOfA
FROM Student;
```

For `Karan`, the outputs would be:

|UpperName|NameLength|FirstTwo|LastTwo|PositionOfA|
|---|---|---|---|---|
|KARAN|5|Ka|an|2|

In MySQL-style behavior, `INSTR()` searches case-sensitively according to the function's string-comparison behavior, so searching for lowercase `'a'` in `'Karan'` returns the position of the first lowercase `a`, which is 2.

Note: String comparison and case sensitivity can differ according to the DBMS and collation. For exam questions, follow the behavior stated in the question or assumed by the relevant SQL dialect.

## 13. Common DSSSB exam traps

|Question trap|Correct concept|
|---|---|
|`MID('COMPUTER', 2, 3)`|Returns `OMP` in the syntax used here|
|`LEFT('COMPUTER', 4)`|Returns `COMP`|
|`RIGHT('COMPUTER', 4)`|Returns `UTER`|
|`INSTR('BANANA', 'ANA')`|Returns `2` in MySQL-style syntax|
|`INSTR('SQL', 'XYZ')`|Returns `0` in MySQL-style syntax|
|`LTRIM(' SQL ')`|Removes leading spaces only|
|`RTRIM(' SQL ')`|Removes trailing spaces only|
|`TRIM(' SQL ')`|Removes spaces from both ends|
|`UCASE('Dsssb')`|Returns `DSSSB`|
|`LCASE('DSSSB')`|Returns `dsssb`|

Remember that the exact functions supported and their behavior can depend on the SQL dialect—particularly `MID()`, `INSTR()` and `LENGTH()`.

### Last-minute memory trick

- `UCASE` = uppercase.
    
- `LCASE` = lowercase.
    
- `MID` = extract from a specified position.
    
- `LENGTH` = measure string length.
    
- `LEFT` / `RIGHT` = extract from either end.
    
- `INSTR` = find a substring's position.
    
- `LTRIM` / `RTRIM` = remove spaces from one end.
    
- `TRIM` = remove spaces from both ends.
### Last-minute memory trick

- `NOW()` → current date and time.
    
- `DATE()` → date portion only.
    
- `MONTH()` → month number.
    
- `MONTHNAME()` → month name.
    
- `YEAR()` → year.
    
- `DAY()` → day of the month.
    
- `DAYNAME()` → weekday name.
    

Quick distinction to memorize: `MONTH()` returns `8`, `MONTHNAME()` returns `August`, `DAY()` returns `17`, and `DAYNAME()` returns `Sunday` for `2025-08-17`.