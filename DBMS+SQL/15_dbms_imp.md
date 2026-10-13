# Part A — Constraints

## 1. What are constraints?

Constraints are rules applied to table columns or groups of columns to maintain the correctness and integrity of data.

For example, a student should not have a duplicate student ID, a required name should not be missing, and a department reference should point to an existing department.

### Common SQL constraints

|Constraint|Purpose|
|---|---|
|`NOT NULL`|Prevents NULL values|
|`UNIQUE`|Prevents duplicate constrained values|
|`PRIMARY KEY`|Uniquely identifies rows; cannot contain NULL|
|`FOREIGN KEY`|Enforces valid references to another key|
|`CHECK`|Requires values to satisfy a condition|
|`DEFAULT`|Supplies a default when a value is omitted or DEFAULT is requested|

Example:

```

CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(50) NOT NULL,
    Email VARCHAR(100) UNIQUE,
    Age INT CHECK (Age >= 0),
    City VARCHAR(50) DEFAULT 'Delhi'
);
```

Here, `StudentID` is the primary key, `Name` is required, email values are constrained to be unique, age must be nonnegative, and the default city is Delhi.

Exam trap: A `DEFAULT` is not the same as `NOT NULL`. A default provides a value in specified circumstances; `NOT NULL` prevents a NULL value from being stored.

## 2. NOT NULL

`NOT NULL` requires a column to contain a non-NULL value.

```
CREATE TABLE Employee (
    EmpID INT PRIMARY KEY,
    EmpName VARCHAR(50) NOT NULL
);
```

This insert fails because the required name is missing:

```
INSERT INTO Employee (EmpID, EmpName)
VALUES (101, NULL);
```

But an empty string is not necessarily NULL:

```
INSERT INTO Employee (EmpID, EmpName)
VALUES (102, '');
```

In DBMSs that distinguish empty strings from NULL, the second insert can satisfy `NOT NULL`. Oracle treats a zero-length character string as NULL, so behavior differs there.

Remember: `NOT NULL` means a value must be present; it does not mean the value must be unique.

## 3. UNIQUE

`UNIQUE` prevents duplicate values in a column or combination of columns.

```
CREATE TABLE Employee (
    EmpID INT PRIMARY KEY,
    Email VARCHAR(100) UNIQUE
);
```

The same non-NULL email cannot normally be stored in two rows under this constraint.

### UNIQUE vs NOT NULL

|`UNIQUE`|`NOT NULL`|
|---|---|
|Restricts duplicates|Prohibits NULL|
|Does not automatically mean non-NULL|Does not automatically prohibit duplicates|
|NULL behavior depends on DBMS and constraint design|A NULL value is prohibited|

For example, a table can have `Email UNIQUE` and allow NULL emails unless another constraint prohibits them. Different DBMSs have different rules for how many NULL values a unique constraint permits.

### Composite UNIQUE constraint

```
CREATE TABLE Enrollment (
    StudentID INT,
    CourseID INT,
    UNIQUE (StudentID, CourseID)
);
```

This prohibits duplicate pairs of `StudentID` and `CourseID`. It does not necessarily require each StudentID or CourseID to be unique by itself.

## 4. PRIMARY KEY

A primary key uniquely identifies every row in a table.

```
CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(50) NOT NULL
);
```

Important properties:

- Primary-key values must be unique.
    
- Primary-key columns cannot contain NULL.
    
- A table has at most one primary-key constraint.
    
- That primary key can consist of multiple columns.
    

### Composite primary key

```
CREATE TABLE Enrollment (
    StudentID INT,
    CourseID INT,
    Grade CHAR(1),
    PRIMARY KEY (StudentID, CourseID)
);
```

The pair `(StudentID, CourseID)` uniquely identifies an enrollment. Multiple rows may share the same StudentID or the same CourseID, but not the same pair.

### PRIMARY KEY vs UNIQUE

|Feature|PRIMARY KEY|UNIQUE|
|---|---|---|
|Prevents duplicate key values|Yes|Yes|
|Allows NULL in constrained key columns|No|Depends on DBMS and constraint design|
|Number of constraints per table|At most one primary key|Multiple unique constraints allowed|
|Can use multiple columns|Yes|Yes|

## 5. FOREIGN KEY

A foreign key establishes a referential relationship between tables.

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

This ensures that a non-NULL `Employee.DeptID` must refer to a valid department key.

Key points:

- Multiple employees can have the same `DeptID`.
    
- The foreign key can be NULL unless prohibited separately.
    
- A table can have multiple foreign keys.
    
- The referenced column or column combination must meet the DBMS's requirements for a referenced key, commonly a primary or unique candidate key.
    
- Deleting a referenced department may be restricted unless the foreign-key action or database design allows it.
    

### Referential actions

Some common foreign-key actions are:

- `ON DELETE CASCADE`: deleting a referenced row can delete dependent rows.
    
- `ON DELETE SET NULL`: dependent foreign-key values are set to NULL, where allowed.
    
- `ON DELETE RESTRICT` or `NO ACTION`: blocks deletion when dependent rows prevent it, subject to DBMS semantics.
    

Exam trap: A foreign key does not have to be unique. Many employees can belong to the same department.

# Part B — SQL Data Types

## 6. What are data types?

A data type specifies what kind of value a database column can store and influences its storage, comparison, and permitted operations.

Common categories include numeric, character, date/time and Boolean-related types. Availability and behavior vary by DBMS.

### A. Numeric data types

|Data type|Purpose|Example|
|---|---|---|
|`INT` / `INTEGER`|Whole numbers|`25`|
|`SMALLINT`|Smaller-range integer|`100`|
|`BIGINT`|Larger-range integer|`9000000000`|
|`DECIMAL(p,s)`|Exact decimal numeric values|`DECIMAL(7,2)`|
|`NUMERIC(p,s)`|Exact numeric values in systems supporting it|`NUMERIC(8,2)`|
|`FLOAT`|Approximate floating-point values|`3.14`|
|`REAL`|Approximate floating-point values|`2.5`|
|`DOUBLE` / `DOUBLE PRECISION`|Wider-precision approximate floating point|`123.456`|

For `DECIMAL(p,s)`:

- `p` is the total number of decimal digits.
    
- `s` is the number of digits after the decimal point.
    

Example:

```
Salary DECIMAL(8,2)
```

This allows up to eight digits in total, with two digits after the decimal point, such as `123456.78`.

Exam trap: Use an exact decimal type such as `DECIMAL` for values like money when exact decimal storage is needed. `FLOAT` and `DOUBLE` use approximate binary floating-point representation.

### B. Character and string data types

|Data type|Purpose|Example|
|---|---|---|
|`CHAR(n)`|Fixed-length character field|`CHAR(5)`|
|`VARCHAR(n)`|Variable-length character field up to the specified limit|`VARCHAR(100)`|
|`TEXT`|Longer text in DBMSs that support it|Descriptions|
|`NCHAR(n)`|Fixed-length national character data where supported|`NCHAR(10)`|
|`NVARCHAR(n)`|Variable-length national character data where supported|`NVARCHAR(100)`|

#### CHAR vs VARCHAR

|`CHAR(n)`|`VARCHAR(n)`|
|---|---|
|Fixed-length character type|Variable-length character type|
|Commonly used for fixed-size codes|Commonly used for names and email addresses|
|Padding and storage details depend on DBMS|Stores variable-length values, subject to DBMS implementation|

Example:

```
CREATE TABLE Person (
    CountryCode CHAR(2),
    FullName VARCHAR(100)
);
```

A two-character country code is a natural use for a fixed-length field, whereas names usually vary in length.

### C. Date and time types

|Data type|Purpose|Example|
|---|---|---|
|`DATE`|Calendar date|`2026-10-12`|
|`TIME`|Time of day or time value, depending on DBMS|`14:30:00`|
|`DATETIME`|Date and time in systems supporting this type|`2026-10-12 14:30:00`|
|`TIMESTAMP`|Timestamp type; exact semantics vary by DBMS|Depends on DBMS|
|`INTERVAL`|Duration or interval in DBMSs supporting it|A period of time|

Exam trap: A `DATE` usually stores the calendar date, whereas a date-time type can also store a time component. `TIMESTAMP` is not identical across all DBMSs; its time-zone and storage semantics vary.

### D. Boolean-related types

A Boolean value represents a logical state, usually `TRUE` or `FALSE`.

```
CREATE TABLE Attendance (
    StudentID INT,
    IsPresent BOOLEAN
);
```

The exact support for `BOOLEAN` varies. For example, MySQL treats `BOOLEAN` as a synonym for `TINYINT(1)`, while other DBMSs have their own Boolean implementations.

## 7. Quick data-type MCQs facts

|Question|Key point|
|---|---|
|Store whole numbers|`INT`|
|Store exact decimal values|`DECIMAL`|
|Store approximate fractional values|`FLOAT` or `DOUBLE`|
|Store fixed-length character values|`CHAR`|
|Store variable-length character values|`VARCHAR`|
|Store a calendar date|`DATE`|
|Store a date with time|A suitable date-time/timestamp type, depending on DBMS|

# Part C — Subqueries

## 8. What is a subquery?

A subquery is a query nested inside another SQL statement. It can supply a value, a set of values, or a derived table for the outer query.

Consider this table:

EMPLOYEE

|EmpID|EmpName|DeptID|Salary|
|---|---|---|---|
|101|Amit|10|40000|
|102|Neha|20|60000|
|103|Ravi|10|50000|
|104|Priya|30|70000|
|105|Sana|20|45000|

## 9. Single-value (scalar) subquery

A scalar subquery returns one value, usually one row and one column.

### Example: Employees earning above the average salary

```
SELECT EmpName, Salary
FROM Employee
WHERE Salary > (
    SELECT AVG(Salary)
    FROM Employee
);
```

The average salary is:

\[ \frac{40000+60000+50000+70000+45000}{5} =53000 \]

Output:

|EmpName|Salary|
|---|---|
|Neha|60000|
|Priya|70000|

The inner query calculates the average. The outer query retrieves employees whose salaries exceed it.

Exam trap: A scalar subquery must produce one column and at most one row. If it returns more than one row in a scalar context, the DBMS normally raises an error.

## 10. Multi-row subquery with IN

`IN` tests whether a value matches any value returned by a subquery.

### Example: Employees in departments that have employees earning above 55,000

```
SELECT EmpName, DeptID
FROM Employee
WHERE DeptID IN (
    SELECT DeptID
    FROM Employee
    WHERE Salary > 55000
);
```

The inner query returns department IDs 20 and 30.

Output:

|EmpName|DeptID|
|---|---|
|Neha|20|
|Priya|30|
|Sana|20|

Both employees in department 20 qualify because at least one employee in that department earns above 55,000.

## 11. Subquery with EXISTS

`EXISTS` tests whether a subquery returns at least one row.

Example tables:

DEPARTMENT

|DeptID|DeptName|
|---|---|
|10|CSE|
|20|ECE|
|30|HR|
|40|Finance|

### Find departments with at least one employee

```
SELECT d.DeptID, d.DeptName
FROM Department AS d
WHERE EXISTS (
    SELECT 1
    FROM Employee AS e
    WHERE e.DeptID = d.DeptID
);
```

The result contains departments 10, 20 and 30. Department 40 has no matching employee, so its `EXISTS` condition is false.

`SELECT 1` is a common convention inside `EXISTS` because it tests row existence, not the selected value.

### NOT EXISTS

To find departments with no employees:

```
SELECT d.DeptID, d.DeptName
FROM Department AS d
WHERE NOT EXISTS (
    SELECT 1
    FROM Employee AS e
    WHERE e.DeptID = d.DeptID
);
```

Output:

|DeptID|DeptName|
|---|---|
|40|Finance|

Exam trap: `EXISTS` checks whether any row exists. It does not require the inner query to return a particular value.

## 12. Correlated subquery

A correlated subquery refers to a column from the outer query. Its result is logically dependent on the current outer row.

### Example: Employees earning above their own department's average

```
SELECT e.EmpName, e.DeptID, e.Salary
FROM Employee AS e
WHERE e.Salary > (
    SELECT AVG(e2.Salary)
    FROM Employee AS e2
    WHERE e2.DeptID = e.DeptID
);
```

Output:

|EmpName|DeptID|Salary|
|---|---|---|
|Ravi|10|50000|
|Neha|20|60000|

Why?

- Department 10 average: ₹45,000, so Ravi qualifies.
    
- Department 20 average: ₹52,500, so Neha qualifies.
    
- Department 30 has only Priya, who earns exactly the department average; she does not qualify under `>`.
    

A correlated query is often explained as being evaluated for each outer row, though optimizers may transform it into a more efficient execution plan.

### Subquery types — comparison

|Type|Main characteristic|
|---|---|
|Scalar subquery|Returns one value|
|Multi-row subquery|Returns multiple values or rows for an appropriate outer operator|
|`EXISTS` subquery|Checks whether at least one row exists|
|Correlated subquery|Refers to columns from the outer query|
|Non-correlated subquery|Can be evaluated independently of the outer row|

# Part D — Aggregate Functions

## 13. What are aggregate functions?

Aggregate functions calculate a result from a set of rows, often producing one result for an entire table or one result per group.

The five core aggregate functions for DSSSB are:

|Function|Purpose|
|---|---|
|`COUNT()`|Counts rows or non-NULL values|
|`SUM()`|Calculates a sum|
|`AVG()`|Calculates an average|
|`MAX()`|Finds the maximum value|
|`MIN()`|Finds the minimum value|

We will use the `EMPLOYEE` table from the previous section.

### A. COUNT()

```
SELECT COUNT(*) AS TotalEmployees
FROM Employee;
```

Result:

|TotalEmployees|
|---|
|5|

`COUNT(*)` counts rows, including rows that have NULL in some columns.

Compare:

```
SELECT COUNT(DeptID) AS EmployeesWithDept
FROM Employee;
```

`COUNT(DeptID)` counts only rows where `DeptID` is non-NULL.

Remember:

- `COUNT(*)` → counts rows.
    
- `COUNT(column)` → counts non-NULL values in that column.
    
- `COUNT(DISTINCT column)` → counts distinct, non-NULL values in common SQL implementations.
    

### B. SUM()

```
SELECT SUM(Salary) AS TotalSalary
FROM Employee;
```

Result:

|TotalSalary|
|---|
|265000|

`SUM()` adds non-NULL values. If there are no non-NULL input values, the result is generally NULL.

### C. AVG()

```
SELECT AVG(Salary) AS AverageSalary
FROM Employee;
```

Result:

|AverageSalary|
|---|
|53000|

`AVG()` calculates the average using non-NULL values; it does not count NULL as zero.

### D. MAX() and MIN()

```
SELECT
    MAX(Salary) AS HighestSalary,
    MIN(Salary) AS LowestSalary
FROM Employee;
```

Result:

|HighestSalary|LowestSalary|
|---|---|
|70000|40000|

They return the maximum and minimum values, respectively, ignoring NULLs in common SQL implementations.

## 14. Aggregate functions with GROUP BY

Find the average salary per department:

```
SELECT DeptID, AVG(Salary) AS AvgSalary
FROM Employee
GROUP BY DeptID;
```

Result:

|DeptID|AvgSalary|
|---|---|
|10|45000|
|20|52500|
|30|70000|

Each department is treated as a separate group.

### Filter aggregate groups with HAVING

```
SELECT DeptID, AVG(Salary) AS AvgSalary
FROM Employee
GROUP BY DeptID
HAVING AVG(Salary) > 50000;
```

Result:

|DeptID|AvgSalary|
|---|---|
|20|52500|
|30|70000|

### Aggregate function traps

|Question|Correct point|
|---|---|
|Does `COUNT(*)` ignore rows with NULL columns?|No|
|Does `COUNT(column)` count NULL values?|No|
|Does `AVG(column)` treat NULL as zero?|No|
|What filters groups?|`HAVING`|
|What filters rows before grouping?|`WHERE`|
|What does `COUNT(DISTINCT DeptID)` count?|Distinct, non-NULL department IDs|

# Part E — Views

## 15. What is a view?

A view is a named query that presents data from one or more underlying tables as a virtual table.

A conventional view stores the query definition rather than maintaining its own independent copy of the query result. A materialized view, where supported, is different because it stores the result data.

### Example: Create a view

```
CREATE VIEW HighSalaryEmployees AS
SELECT EmpID, EmpName, DeptID, Salary
FROM Employee
WHERE Salary >= 55000;
```

The view presents employees earning at least 55,000.

Query it like a table:

```
SELECT *
FROM HighSalaryEmployees;
```

Output:

|EmpID|EmpName|DeptID|Salary|
|---|---|---|---|
|102|Neha|20|60000|
|104|Priya|30|70000|

### Benefits of views

- Simplicity: Hides complex joins or filters behind a reusable query.
    
- Security: Can expose only selected rows or columns to a user.
    
- Logical abstraction: Can provide a stable presentation of underlying data.
    
- Reusability: Allows a query definition to be referenced by name.
    

### Important exam traps

- A conventional view does not ordinarily store a separate copy of every result row.
    
- The underlying tables continue to hold the data.
    
- A view can be based on one table or multiple tables.
    
- Whether a view is updatable depends on the definition and DBMS rules. Views involving grouping, aggregates, `DISTINCT`, or complex joins often have restrictions.
    
- A materialized view stores query results and must be refreshed or maintained according to its database implementation.
    

## 16. Updating a view

A simple view may be updatable.

```
CREATE VIEW Dept10Employees AS
SELECT EmpID, EmpName, DeptID, Salary
FROM Employee
WHERE DeptID = 10;
```

Some database systems allow an update through this view:

```
UPDATE Dept10Employees
SET Salary = 52000
WHERE EmpID = 103;
```

If allowed, the underlying employee row is updated.

However, the ability to update a view depends on the DBMS and the view's definition. For a view with grouping or aggregate output, updating the view is generally restricted.

### Related commands

```
CREATE VIEW ViewName AS
SELECT ...;
```

Creates a view.

```
DROP VIEW ViewName;
```

Removes the view definition; it does not normally remove the underlying tables or their stored data.

# Part F — Transactions in SQL

Transactions were covered in your earlier DBMS notes. Here is the SQL-focused revision, including transaction commands and important exam distinctions.

## 17. What is a transaction?

A transaction is a logical unit of database work that should complete successfully as a unit.

For example, transferring money between accounts needs a debit and a credit. If one operation succeeds but the other fails, the system must handle the transaction to maintain correct balances.

### ACID properties

|Property|Meaning|Example|
|---|---|---|
|Atomicity|All-or-nothing|Debit and credit are treated as one unit|
|Consistency|Maintains database rules|Integrity constraints remain satisfied|
|Isolation|Controls interference between concurrent transactions|Concurrent updates do not create unintended results|
|Durability|Committed changes persist|A completed transfer survives a restart under the DBMS's durability guarantees|

## 18. COMMIT

`COMMIT` finalizes a successful transaction.

```
START TRANSACTION;

UPDATE Employee
SET Salary = Salary + 1000
WHERE EmpID = 101;

COMMIT;
```

The salary increase is committed if the transaction completes successfully.

## 19. ROLLBACK

`ROLLBACK` undoes uncommitted work in the current transaction.

```
START TRANSACTION;

UPDATE Employee
SET Salary = Salary + 1000
WHERE EmpID = 101;

ROLLBACK;
```

The salary change is undone if it remains part of the current uncommitted transaction and is covered by the rollback.

## 20. SAVEPOINT

A `SAVEPOINT` marks a point within a transaction to which you can roll back without necessarily undoing the entire transaction.

```
START TRANSACTION;

UPDATE Employee
SET Salary = Salary + 1000
WHERE EmpID = 101;

SAVEPOINT BeforeSecondUpdate;

UPDATE Employee
SET Salary = Salary + 2000
WHERE EmpID = 102;

ROLLBACK TO SAVEPOINT BeforeSecondUpdate;

COMMIT;
```

Assuming the DBMS supports this syntax and the operations succeed:

- The first update is retained and committed.
    
- The second update is undone.
    
- The transaction is committed.
    

Exam trap: Rolling back to a savepoint does not necessarily roll back the entire transaction. Transaction syntax and behavior vary among DBMSs.

## 21. Transactions — important distinctions

|Command / concept|Purpose|
|---|---|
|`COMMIT`|Finalizes transaction changes|
|`ROLLBACK`|Undoes uncommitted transaction changes|
|`SAVEPOINT`|Creates a point for partial rollback|
|`START TRANSACTION`|Begins a transaction in systems supporting the syntax|
|Autocommit|Can make each statement its own committed transaction, depending on DBMS settings|
|Isolation|Controls how concurrent transactions interact|

Important: DDL operations such as `TRUNCATE`, `DROP` and `ALTER` can cause implicit commits or behave differently across database systems. Do not assume every DDL operation can be undone with `ROLLBACK`.

## Final revision checklist

Before moving to the next DBMS topic, make sure you can explain:

- Constraints: `NOT NULL`, `UNIQUE`, `PRIMARY KEY`, `FOREIGN KEY`, `CHECK` and `DEFAULT`.
    
- Data types: numeric, character, date/time and Boolean-related types.
    
- Subqueries: scalar, multi-row, `IN`, `EXISTS`, `NOT EXISTS` and correlated subqueries.
    
- Aggregate functions: `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`, including `COUNT(*)` versus `COUNT(column)`.
    
- Views: creation, benefits, limitations and how views relate to underlying tables.
    
- Transactions: ACID, `COMMIT`, `ROLLBACK`, `SAVEPOINT` and concurrency concepts.
    

For exam preparation, practise writing each query yourself and predicting its output before executing it. This is especially helpful for subqueries, aggregation and constraints-based MCQs.