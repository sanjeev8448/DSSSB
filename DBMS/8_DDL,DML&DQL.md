## 1. SQL command classification

SQL (Structured Query Language) is used to define database structures, manipulate data, and retrieve information.

|Category|Full form|Main purpose|Commands|
|---|---|---|---|
|DDL|Data Definition Language|Defines or changes database structures|`CREATE`, `ALTER`, `DROP`, `TRUNCATE`|
|DML|Data Manipulation Language|Inserts, changes, or removes records|`INSERT`, `UPDATE`, `DELETE`|
|DQL|Data Query Language|Retrieves data|`SELECT`|

Important exam nuance: Many textbooks classify `SELECT` under DQL. Some broader classifications include it within DML. Follow the classification explicitly used in your question or textbook; the commands' functions remain the same.

We'll use this table throughout the examples.

STUDENT

|StudentID|Name|Age|City|Marks|
|---|---|---|---|---|
|101|Amit|21|Delhi|85|
|102|Neha|22|Patna|92|
|103|Ravi|20|Delhi|76|
|104|Priya|21|Jaipur|88|

The examples assume a SQL database supporting the shown syntax. Some details vary among MySQL, PostgreSQL, SQL Server, Oracle, and SQLite.

# Part A — DDL (Data Definition Language)

DDL commands define or modify database objects such as tables and indexes.

## 2. CREATE

`CREATE` is used to create a database object, such as a database, table, or index.

### A. Create a database

```
CREATE DATABASE College;
```

This creates a database named `College` in systems supporting this syntax.

### B. Create a table

```
CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(50) NOT NULL,
    Age INT,
    City VARCHAR(50),
    Marks DECIMAL(5,2)
);
```

Explanation:

|SQL element|Purpose|
|---|---|
|`CREATE TABLE Student`|Creates a table named Student|
|`StudentID INT`|Defines an integer column|
|`PRIMARY KEY`|Enforces unique, non-NULL row identification|
|`VARCHAR(50)`|Allows variable-length character data up to the specified limit|
|`NOT NULL`|Requires a value for that column|
|`DECIMAL(5,2)`|Allows up to five digits in total, with two digits after the decimal point|

For example, `999.99` fits in `DECIMAL(5,2)`, whereas `1000.00` requires six digits in total and does not fit.

## 3. SQL constraints in CREATE

Constraints enforce rules on data stored in tables. These are commonly tested along with DDL.

### PRIMARY KEY

Uniquely identifies each row and does not allow `NULL`.

```
StudentID INT PRIMARY KEY
```

A table has one primary key constraint, which can consist of multiple columns.

### NOT NULL

Requires a column to have a value.

```
Name VARCHAR(50) NOT NULL
```

### UNIQUE

Prevents duplicate values in the constrained column or column combination.

```
Email VARCHAR(100) UNIQUE
```

NULL handling for `UNIQUE` depends on the database system and constraint design.

### CHECK

Requires a value to satisfy a condition.

```
Age INT CHECK (Age >= 0)
```

### DEFAULT

Supplies a default value when an insert omits the column or requests the default.

```
City VARCHAR(50) DEFAULT 'Delhi'
```

### FOREIGN KEY

Enforces a reference to a key in another table or, where supported, the same table.

```
CREATE TABLE Department (
    DeptID INT PRIMARY KEY,
    DeptName VARCHAR(50) NOT NULL
);

CREATE TABLE Employee (
    EmpID INT PRIMARY KEY,
    EmpName VARCHAR(50),
    DeptID INT,
    FOREIGN KEY (DeptID) REFERENCES Department(DeptID)
);
```

A foreign key can have duplicate values. Unless separately prohibited, it can also be `NULL`.

### Quick comparison

|Constraint|Main purpose|
|---|---|
|`PRIMARY KEY`|Unique identification; no NULL|
|`UNIQUE`|Prevent duplicate constrained values|
|`NOT NULL`|Require a value|
|`CHECK`|Restrict values to a condition|
|`DEFAULT`|Supply a default value|
|`FOREIGN KEY`|Enforce referential integrity|

## 4. ALTER

`ALTER` changes the structure of an existing database object, such as adding, modifying, or removing a column.

### A. Add a column

```
ALTER TABLE Student
ADD Email VARCHAR(100);
```

Now the table has a new `Email` column.

### B. Change a column's definition

The syntax varies by DBMS.

For example, MySQL commonly supports:

```
ALTER TABLE Student
MODIFY COLUMN Name VARCHAR(100);
```

PostgreSQL commonly uses:

```
ALTER TABLE Student
ALTER COLUMN Name TYPE VARCHAR(100);
```

Exam trap: The general purpose of `ALTER` is consistent, but the exact syntax for changing a column's type is not identical across all database systems.

### C. Drop a column

```
ALTER TABLE Student
DROP COLUMN Email;
```

This removes the column from the table, including its stored values.

### D. Add a constraint

```
ALTER TABLE Student
ADD CONSTRAINT chk_marks
CHECK (Marks BETWEEN 0 AND 100);
```

This adds a constraint that restricts marks to the specified range. Existing data must satisfy the constraint when the DBMS validates it.

Remember: `ALTER` changes table structure; `UPDATE` changes values in existing rows.

## 5. DROP

`DROP` removes a database object itself.

### Drop a table

```
DROP TABLE Student;
```

This removes the `Student` table's definition and its data.

### Drop a database

```
DROP DATABASE College;
```

This removes the database and its contained objects, subject to the DBMS and dependency rules.

Important: `DROP` is different from `DELETE`. `DROP TABLE` removes the table itself, while `DELETE` removes rows but keeps the table structure.

If other database objects depend on a table, the DBMS may require those dependencies to be handled first, or may offer options to cascade the removal.

## 6. TRUNCATE

`TRUNCATE` removes all rows from a table while preserving the table definition.

```
TRUNCATE TABLE Student;
```

After a successful truncation:

- The table still exists.
    
- Its columns and table definition remain.
    
- Its rows are removed.
    
- You cannot use a `WHERE` clause to truncate only selected rows.
    

For example, the following is not valid standard-style truncation syntax:

```
TRUNCATE TABLE Student
WHERE City = 'Delhi';
```

To remove only Delhi students, use `DELETE` instead.

### DELETE vs TRUNCATE vs DROP

|Feature|`DELETE`|`TRUNCATE`|`DROP`|
|---|---|---|---|
|Removes rows|Yes|All rows|Removes table and its data|
|Keeps table structure|Yes|Yes|No|
|Supports `WHERE`|Yes|No|No|
|Can target selected rows|Yes|No|No|
|Typically logs work|Row changes are generally logged|Often more efficient; implementation varies|DDL operation; behavior varies|
|Transaction rollback|Depends on transaction/DBMS|Depends on DBMS|Depends on DBMS|
|Common purpose|Delete selected records|Empty a table|Remove a table entirely|

Very important exam trap: Textbooks often describe `TRUNCATE` as faster than `DELETE` for removing all rows. This is commonly true, but actual performance and transaction behavior depend on the DBMS, table type, triggers, and constraints.

Do not assume every `TRUNCATE` can be rolled back, or that no `TRUNCATE` can ever be rolled back. For example, PostgreSQL supports transactional truncation, while MySQL's `TRUNCATE TABLE` generally causes an implicit commit.

### DDL revision

- `CREATE` → create an object.
    
- `ALTER` → modify an object's structure.
    
- `DROP` → remove the object.
    
- `TRUNCATE` → remove all rows while retaining the table definition.
    

# Part B — DML (Data Manipulation Language)

DML commands change records stored inside tables.

## 7. INSERT

`INSERT` adds new rows to a table.

Assume the table already exists:

```
CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(50),
    Age INT,
    City VARCHAR(50),
    Marks DECIMAL(5,2)
);
```

### A. Insert one complete row

```
INSERT INTO Student
VALUES (101, 'Amit', 21, 'Delhi', 85);
```

If you omit the column list, you normally need to provide values in the table's expected column order and satisfy its constraints.

### B. Insert values using a column list

```
INSERT INTO Student
    (StudentID, Name, Age, City, Marks)
VALUES
    (102, 'Neha', 22, 'Patna', 92);
```

This is generally the clearer, safer approach because the columns are explicitly specified.

### C. Insert only some columns

```
INSERT INTO Student
    (StudentID, Name, City)
VALUES
    (103, 'Ravi', 'Delhi');
```

The omitted columns receive their defined default values, or `NULL` if permitted and no default applies. The insert fails if a required column has neither an acceptable supplied value nor an applicable default.

### D. Insert multiple rows

```
INSERT INTO Student
    (StudentID, Name, Age, City, Marks)
VALUES
    (104, 'Priya', 21, 'Jaipur', 88),
    (105, 'Karan', 23, 'Delhi', 81);
```

Multi-row `VALUES` syntax is supported by common DBMSs, though exact capabilities may vary.

### E. Insert from another query

```
INSERT INTO StudentArchive
    (StudentID, Name, Age, City, Marks)
SELECT StudentID, Name, Age, City, Marks
FROM Student
WHERE Marks >= 85;
```

This copies qualifying query results into another table, provided the target structure and constraints are compatible.

Exam traps:

- Text values are normally enclosed in single quotes.
    
- The number and types of values must match the target columns.
    
- A duplicate primary key generally causes a constraint violation.
    
- `INSERT` adds data; `CREATE` defines the table.
    

## 8. UPDATE

`UPDATE` modifies existing values in one or more rows.

### A. Update a single student's marks

```
UPDATE Student
SET Marks = 95
WHERE StudentID = 102;
```

Only the row matching `StudentID = 102` is targeted.

### B. Update multiple columns

```
UPDATE Student
SET Age = 23,
    City = 'Delhi'
WHERE StudentID = 102;
```

Both values are updated for the matching row.

### C. Update multiple rows

```
UPDATE Student
SET Marks = Marks + 5
WHERE City = 'Delhi';
```

This adds five marks to every Delhi student's existing mark value. A proper `WHERE` clause is important when only selected rows should change.

### D. What happens if WHERE is omitted?

```
UPDATE Student
SET City = 'Delhi';
```

Every row in the table is targeted. This does not update just one student.

### UPDATE example

Before:

|StudentID|Name|City|Marks|
|---|---|---|---|
|101|Amit|Delhi|85|
|102|Neha|Patna|92|
|103|Ravi|Delhi|76|

Execute:

```
UPDATE Student
SET Marks = Marks + 5
WHERE City = 'Delhi';
```

After:

|StudentID|Name|City|Marks|
|---|---|---|---|
|101|Amit|Delhi|90|
|102|Neha|Patna|92|
|103|Ravi|Delhi|81|

Neha's marks stay unchanged because her city is Patna.

Exam trap: `UPDATE` changes existing rows. It does not insert new rows or alter the table's column definitions.

## 9. DELETE

`DELETE` removes rows from a table.

### A. Delete one selected row

```
DELETE FROM Student
WHERE StudentID = 103;
```

This deletes the row with ID 103, if it exists and deletion is permitted by the database's constraints.

### B. Delete rows matching a condition

```
DELETE FROM Student
WHERE Marks < 40;
```

This targets all students with marks below 40.

### C. Delete all rows

```
DELETE FROM Student;
```

This targets every row but leaves the table structure in place.

Compare:

```
DELETE FROM Student
WHERE City = 'Delhi';
```

This removes only Delhi students.

```
DELETE FROM Student;
```

This removes every row.

Important: If you omit `WHERE`, `DELETE` targets all rows. Always inspect the condition before executing a destructive statement.

### DML comparison

|Command|Purpose|Changes table structure?|
|---|---|---|
|`INSERT`|Add rows|No|
|`UPDATE`|Change values in rows|No|
|`DELETE`|Remove rows|No|

# Part C — DQL (Data Query Language)

## 10. SELECT

`SELECT` retrieves data from a table or query result. It is the command you will use most often when practising SQL questions.

### A. Select all columns

```
SELECT *
FROM Student;
```

`*` means all columns in the result.

### B. Select specific columns

```
SELECT Name, Marks
FROM Student;
```

Only `Name` and `Marks` are returned.

### C. Use WHERE to filter rows

```
SELECT *
FROM Student
WHERE City = 'Delhi';
```

`WHERE` determines which rows qualify.

### D. Comparison operators

|Operator|Meaning|
|---|---|
|`=`|Equal to|
|`<>`|Not equal to|
|`!=`|Not equal to in many DBMSs|
|`>`|Greater than|
|`<`|Less than|
|`>=`|Greater than or equal to|
|`<=`|Less than or equal to|

Example:

```
SELECT Name, Marks
FROM Student
WHERE Marks >= 85;
```

Returns the names and marks of students scoring at least 85.

### E. AND, OR and NOT

```
SELECT *
FROM Student
WHERE City = 'Delhi' AND Marks > 80;
```

Both conditions must be true.

```
SELECT *
FROM Student
WHERE City = 'Delhi' OR Marks > 90;
```

At least one condition must be true.

```
SELECT *
FROM Student
WHERE NOT City = 'Delhi';
```

Returns rows where the city comparison is true as negated. For rows where `City` is `NULL`, the condition evaluates to unknown, so those rows are not returned by `WHERE`.

Use parentheses when combining multiple `AND` and `OR` expressions to make the intended logic explicit.

### F. BETWEEN

```
SELECT *
FROM Student
WHERE Marks BETWEEN 80 AND 90;
```

`BETWEEN` includes both endpoints. This example selects values from 80 through 90, inclusive.

### G. IN

```
SELECT *
FROM Student
WHERE City IN ('Delhi', 'Patna');
```

Matches either of the listed city values.

### H. LIKE

`LIKE` matches text patterns.

|Pattern|Meaning|
|---|---|
|`'A%'`|Starts with A|
|`'%a'`|Ends with a|
|`'%mit%'`|Contains `mit`|
|`'_m%'`|Second character is `m`|

Example:

```
SELECT *
FROM Student
WHERE Name LIKE 'A%';
```

`%` matches zero or more characters, and `_` matches a single character. Case sensitivity depends on the database and collation.

### I. NULL checks

Incorrect for testing NULL:

```
SELECT *
FROM Student
WHERE City = NULL;
```

Correct:

```
SELECT *
FROM Student
WHERE City IS NULL;
```

To find rows with a non-NULL city:

```
SELECT *
FROM Student
WHERE City IS NOT NULL;
```

Exam trap: `NULL` represents missing or unknown information. Use `IS NULL` / `IS NOT NULL`, rather than `= NULL`.

## 11. DISTINCT

`DISTINCT` removes duplicate rows from the query result.

Suppose `Student` contains:

|StudentID|Name|City|
|---|---|---|
|101|Amit|Delhi|
|102|Neha|Patna|
|103|Ravi|Delhi|
|104|Priya|Jaipur|

Query:

```
SELECT DISTINCT City
FROM Student;
```

Result:

|City|
|---|
|Delhi|
|Patna|
|Jaipur|

Delhi appears only once.

### DISTINCT on multiple columns

```
SELECT DISTINCT City, Age
FROM Student;
```

This removes duplicate combinations of City and Age, not duplicates of either column considered independently.

Exam trap: `DISTINCT` applies to the complete set of selected expressions in each result row.

## 12. Column aliases using AS

An alias gives a column or table a temporary name in a query.

```
SELECT Name AS StudentName,
       Marks AS Score
FROM Student;
```

Result column headings become `StudentName` and `Score`.

You can also alias a table:

```
SELECT s.Name, s.Marks
FROM Student AS s;
```

Here, `s` is a table alias.

Aliases generally change the name used in the query result or query expression; they do not rename the underlying table column.

## 13. ORDER BY

`ORDER BY` sorts the query result.

### Ascending order

```
SELECT Name, Marks
FROM Student
ORDER BY Marks ASC;
```

`ASC` means ascending. It is the default sort direction in standard SQL when no direction is specified.

### Descending order

```
SELECT Name, Marks
FROM Student
ORDER BY Marks DESC;
```

`DESC` means descending.

### Sort by multiple columns

```
SELECT Name, City, Marks
FROM Student
ORDER BY City ASC, Marks DESC;
```

First, rows are sorted by city in ascending order. Within each city, they are sorted by marks in descending order.

Exam trap: A relational table has no guaranteed row order unless the query specifies an order. Do not assume `SELECT *` returns rows in insertion order.

## 14. Restricting the number of rows

Different DBMSs use different syntax to limit query results.

### MySQL and PostgreSQL

```
SELECT *
FROM Student
ORDER BY Marks DESC
LIMIT 3;
```

Returns up to three rows with the highest marks, assuming the chosen ordering.

### SQL Server

```
SELECT TOP 3 *
FROM Student
ORDER BY Marks DESC;
```

### Standard-style FETCH syntax

```
SELECT *
FROM Student
ORDER BY Marks DESC
FETCH FIRST 3 ROWS ONLY;
```

Support and syntax details vary among database systems.

Exam trap: When a question asks for the top three marks, combine the correct limiting syntax with `ORDER BY Marks DESC`. Without ordering, the selected three rows are not necessarily the highest-scoring rows.

## 15. Aggregate functions

Aggregate functions calculate a result using values from multiple rows.

|Function|Purpose|Example|
|---|---|---|
|`COUNT(*)`|Counts rows|Total students|
|`COUNT(column)`|Counts non-NULL values in a column|Students with a recorded city|
|`SUM(column)`|Adds non-NULL values|Total marks|
|`AVG(column)`|Calculates average of non-NULL values|Average marks|
|`MAX(column)`|Largest value|Highest marks|
|`MIN(column)`|Smallest value|Lowest marks|

Examples:

```
SELECT COUNT(*) AS TotalStudents
FROM Student;
```

```
SELECT AVG(Marks) AS AverageMarks
FROM Student;
```

```
SELECT MAX(Marks) AS HighestMarks,
       MIN(Marks) AS LowestMarks
FROM Student;
```

### COUNT(*) vs COUNT(column)

Suppose a table has five rows, but one row has `Marks = NULL`.

- `COUNT(*)` returns 5.
    
- `COUNT(Marks)` returns 4.
    

`COUNT(*)` counts rows. `COUNT(column)` counts non-NULL values in that column.

For most aggregate functions such as `SUM`, `AVG`, `MIN`, and `MAX`, NULL values are ignored.

## 16. GROUP BY

`GROUP BY` groups rows sharing the same value or combination of values, usually so aggregate functions can be applied to each group.

Suppose these are the city values in the student table:

|StudentID|City|Marks|
|---|---|---|
|101|Delhi|85|
|102|Patna|92|
|103|Delhi|76|
|104|Jaipur|88|

Query:

```
SELECT City, COUNT(*) AS StudentCount
FROM Student
GROUP BY City;
```

Possible result:

|City|StudentCount|
|---|---|
|Delhi|2|
|Patna|1|
|Jaipur|1|

The database makes one group per city and counts the rows in each group.

## 17. HAVING

`HAVING` filters groups, often according to an aggregate condition.

```
SELECT City, COUNT(*) AS StudentCount
FROM Student
GROUP BY City
HAVING COUNT(*) >= 2;
```

Result:

|City|StudentCount|
|---|---|
|Delhi|2|

Only groups with at least two rows are returned.

### WHERE vs HAVING

|Feature|WHERE|HAVING|
|---|---|---|
|Filters|Individual rows|Groups|
|Applied conceptually|Before grouping|After grouping|
|Can filter using aggregate conditions|Not directly in the usual same-level query|Yes|
|Example|`WHERE Marks >= 80`|`HAVING AVG(Marks) >= 80`|

Exam trap: `WHERE` filters rows before grouping; `HAVING` filters groups after grouping.

A complete example:

```
SELECT City, AVG(Marks) AS AverageMarks
FROM Student
WHERE Marks >= 70
GROUP BY City
HAVING AVG(Marks) >= 80
ORDER BY AverageMarks DESC;
```

This query:

1. Filters students with marks of at least 70.
    
2. Groups the remaining rows by city.
    
3. Calculates average marks for each group.
    
4. Keeps groups whose average is at least 80.
    
5. Sorts the resulting groups by average marks, highest first.
    

## 18. SQL query clause order — high-value exam topic

A typical query can be written in this syntax order:

```
SELECT City, AVG(Marks) AS AverageMarks
FROM Student
WHERE Marks >= 70
GROUP BY City
HAVING AVG(Marks) >= 80
ORDER BY AverageMarks DESC
LIMIT 5;
```

The `LIMIT` part is supported in systems such as MySQL and PostgreSQL, but not in the same form in all DBMSs.

For the clauses most commonly tested, remember:

SELECT → FROM → WHERE → GROUP BY → HAVING → ORDER BY

A limiting clause may then appear at the end, depending on the DBMS.

The logical processing order is different from the written syntax order. A simplified logical order is:

FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → row limiting

This helps explain why aggregate conditions are normally placed in `HAVING` rather than `WHERE`, and why a `SELECT` alias may not be available to `WHERE`.

## 19. Most important differences for MCQs

|Command|Category|Operates on|Can use `WHERE`?|
|---|---|---|---|
|`CREATE`|DDL|Creates an object|No|
|`ALTER`|DDL|Changes object structure|No|
|`DROP`|DDL|Removes an object|No|
|`TRUNCATE`|DDL in common classifications|All rows in a table|No|
|`INSERT`|DML|Adds rows|No `WHERE` in ordinary `INSERT ... VALUES`|
|`UPDATE`|DML|Changes existing rows|Yes|
|`DELETE`|DML|Removes rows|Yes|
|`SELECT`|DQL in common classifications|Retrieves data|Yes|