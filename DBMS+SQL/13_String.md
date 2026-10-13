## 1. `NOW()` — Current date and time

`NOW()` returns the current date and time according to the database session's time zone.

### Syntax

```
SELECT NOW();
```

Example output:

|NOW()|
|---|
|2026-10-12 21:30:00|

This is an illustrative output; the actual result depends on when the query runs and the database session's time zone.

### Important points

- Returns both a date and a time.
    
- The typical MySQL display format is `YYYY-MM-DD HH:MM:SS`.
    
- Calling `NOW()` does not store the date in a table; it returns a value.
    
- In MySQL, `NOW()` generally remains constant throughout the statement in which it is evaluated.
    

Example:

```
SELECT NOW() AS CurrentDateTime;
```

Exam trap: `NOW()` is not just the date. It includes the time component.

## 2. `DATE()` — Extract the date portion

In MySQL, `DATE()` extracts the date portion of a date-time value, excluding the time.

### Syntax

```
DATE(expression)
```

### Example

```
SELECT DATE('2026-10-12 21:30:45');
```

Output:

|Result|
|---|
|2026-10-12|

The time portion, `21:30:45`, is removed.

### Another example

```
SELECT DATE(NOW());
```

This returns the current date without the time.

### `NOW()` vs `DATE()`

|Function|Typical output|Meaning|
|---|---|---|
|`NOW()`|`2026-10-12 21:30:45`|Current date and time|
|`DATE('2026-10-12 21:30:45')`|`2026-10-12`|Date portion only|
|`DATE(NOW())`|`2026-10-12`|Today's date according to the session|

Exam trap: In the MySQL examples here, `DATE()` extracts the date from an expression; it is not the function used to return the current date and time.

## 3. `MONTH()` — Extract the month number

`MONTH()` returns the numeric month from a date.

### Syntax

```
MONTH(date)
```

### Example

```
SELECT MONTH('2025-08-17');
```

Output:

|Result|
|---|
|8|

August is the eighth month, so the result is `8`.

### Month-number reference

|Month|MONTH() result|
|---|---|
|January|1|
|February|2|
|March|3|
|April|4|
|May|5|
|June|6|
|July|7|
|August|8|
|September|9|
|October|10|
|November|11|
|December|12|

Exam trap: `MONTH()` returns a number, not the month name.

## 4. `MONTHNAME()` — Extract the month name

`MONTHNAME()` returns the name of the month corresponding to a date.

### Syntax

```
MONTHNAME(date)
```

### Example

```
SELECT MONTHNAME('2025-08-17');
```

Output:

|Result|
|---|
|August|

### Compare `MONTH()` and `MONTHNAME()`

```
SELECT
    MONTH('2025-08-17') AS MonthNumber,
    MONTHNAME('2025-08-17') AS MonthName;
```

Output:

|MonthNumber|MonthName|
|---|---|
|8|August|

The returned month name can depend on the database's language or locale settings.

Exam trap: `MONTH()` produces a numeric value; `MONTHNAME()` produces text.

## 5. `YEAR()` — Extract the year

`YEAR()` returns the year component of a date.

### Syntax

```
YEAR(date)
```

### Example

```
SELECT YEAR('2025-08-17');
```

Output:

|Result|
|---|
|2025|

Another example:

```
SELECT YEAR('2000-01-01');
```

Output: `2000`

Exam trap: `YEAR()` returns the year component, not the number of years elapsed since a particular date.

## 6. `DAY()` — Extract the day of the month

`DAY()` returns the day number within the month, typically from 1 to 31 for valid dates.

### Syntax

```
DAY(date)
```

### Example

```
SELECT DAY('2025-08-17');
```

Output:

|Result|
|---|
|17|

For example:

|Date|DAY() result|
|---|---|
|`2025-01-01`|1|
|`2025-02-28`|28|
|`2025-08-17`|17|
|`2025-12-31`|31|

Important distinction: `DAY()` returns the day within the month, not the day of the week.

In MySQL, `DAY(date)` is synonymous with `DAYOFMONTH(date)`.

## 7. `DAYNAME()` — Extract the weekday name

`DAYNAME()` returns the weekday name for a date.

### Syntax

```
DAYNAME(date)
```

### Example

```
SELECT DAYNAME('2025-08-17');
```

Output:

|Result|
|---|
|Sunday|

Another example:

```
SELECT DAYNAME('2025-08-18');
```

Output: `Monday`

The language of the returned weekday name may depend on database locale settings.

### `DAY()` vs `DAYNAME()`

|Function|Returns|Example for `2025-08-17`|
|---|---|---|
|`DAY()`|Day of the month as a number|`17`|
|`DAYNAME()`|Weekday name as text|`Sunday`|

Exam trap: The date is the 17th of the month, but the weekday is Sunday. These functions answer different questions.

## 8. All seven date functions at a glance

|Function|Purpose|Example|Result|
|---|---|---|---|
|`NOW()`|Current date and time|`NOW()`|Current date-time|
|`DATE()`|Extract date portion|`DATE('2025-08-17 10:30:00')`|`2025-08-17`|
|`MONTH()`|Month number|`MONTH('2025-08-17')`|`8`|
|`MONTHNAME()`|Month name|`MONTHNAME('2025-08-17')`|`August`|
|`YEAR()`|Year number|`YEAR('2025-08-17')`|`2025`|
|`DAY()`|Day of month|`DAY('2025-08-17')`|`17`|
|`DAYNAME()`|Weekday name|`DAYNAME('2025-08-17')`|`Sunday`|

## 9. Combined SQL example

Suppose an `EMPLOYEE` table contains a `JoiningDate` column.

|EmpID|EmpName|JoiningDate|
|---|---|---|
|101|Amit|2024-01-15|
|102|Neha|2025-08-17|
|103|Ravi|2026-10-12|

You can retrieve different date components together:

```
SELECT
    EmpName,
    JoiningDate,
    YEAR(JoiningDate) AS JoinYear,
    MONTH(JoiningDate) AS JoinMonth,
    MONTHNAME(JoiningDate) AS MonthName,
    DAY(JoiningDate) AS JoinDay,
    DAYNAME(JoiningDate) AS Weekday
FROM Employee;
```

For Neha, the relevant output is:

|EmpName|JoinYear|JoinMonth|MonthName|JoinDay|Weekday|
|---|---|---|---|---|---|
|Neha|2025|8|August|17|Sunday|

### SQL dialect note

These examples use MySQL-style functions. Other databases may use different functions or syntax for some tasks. For instance, SQL Server uses `GETDATE()` for the current date and time, and date formatting or extraction syntax can differ between systems. In your exam, follow the SQL dialect stated in the question.