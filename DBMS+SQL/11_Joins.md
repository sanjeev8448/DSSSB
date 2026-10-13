## 1. Understand joins using two tables

We will use these tables in every example.

STUDENT

|StudentID|Name|DeptID|
|---|---|---|
|101|Amit|10|
|102|Neha|20|
|103|Ravi|10|
|104|Priya|NULL|

DEPARTMENT

|DeptID|DeptName|
|---|---|
|10|CSE|
|20|ECE|
|40|HR|

Notice that Priya has no assigned department, and HR has no students in this sample.

The common column is `DeptID`. A join can use this column to match students with their department details.

## 2. INNER JOIN

An INNER JOIN returns only rows that satisfy the join condition in both tables.

### Syntax

```
SELECT columns
FROM table1
INNER JOIN table2
    ON table1.column = table2.column;
```

### Example

```
SELECT s.StudentID, s.Name, d.DeptName
FROM Student AS s
INNER JOIN Department AS d
    ON s.DeptID = d.DeptID;
```

Result:

|StudentID|Name|DeptName|
|---|---|---|
|101|Amit|CSE|
|102|Neha|ECE|
|103|Ravi|CSE|

Why is Priya missing? Her `DeptID` is NULL, so it does not match a department ID through ordinary equality.

Why is HR missing? There is no student whose `DeptID` matches 40.

### Key points

- Returns matching rows only.
    
- Unmatched rows from either side are excluded.
    
- Can return multiple rows for a match if the join column has duplicate values.
    
- `INNER JOIN` can be written as `JOIN` in common SQL syntax.
    

Exam memory trick: INNER = matching rows only.

## 3. LEFT JOIN (LEFT OUTER JOIN)

A LEFT JOIN returns every row from the left table and matching rows from the right table. If there is no match, columns from the right table are filled with NULLs.

### Example

```
SELECT s.StudentID, s.Name, d.DeptName
FROM Student AS s
LEFT JOIN Department AS d
    ON s.DeptID = d.DeptID;
```

Result:

|StudentID|Name|DeptName|
|---|---|---|
|101|Amit|CSE|
|102|Neha|ECE|
|103|Ravi|CSE|
|104|Priya|NULL|

Priya remains in the result because all rows from `STUDENT`, the left table, are preserved.

### Key points

- Every left-table row is returned.
    
- Matching right-table data is included.
    
- If no right-table match exists, right-side columns contain NULL.
    
- `LEFT JOIN` and `LEFT OUTER JOIN` mean the same thing.
    

Exam memory trick: LEFT = keep every row from the left table.

## 4. RIGHT JOIN (RIGHT OUTER JOIN)

A RIGHT JOIN returns every row from the right table and matching rows from the left table. When no match exists, left-table columns contain NULL.

### Example

```
SELECT s.StudentID, s.Name, d.DeptID, d.DeptName
FROM Student AS s
RIGHT JOIN Department AS d
    ON s.DeptID = d.DeptID;
```

Result:

|StudentID|Name|DeptID|DeptName|
|---|---|---|---|
|101|Amit|10|CSE|
|103|Ravi|10|CSE|
|102|Neha|20|ECE|
|NULL|NULL|40|HR|

HR appears even though no student belongs to that department.

### Key points

- Every row from the right table is preserved.
    
- Matching left-table rows are included.
    
- Missing left-side values are filled with NULL.
    
- `RIGHT JOIN` and `RIGHT OUTER JOIN` mean the same thing.
    

Exam memory trick: RIGHT = keep every row from the right table.

## 5. FULL OUTER JOIN (FULL JOIN)

A FULL OUTER JOIN returns all matching rows plus all unmatched rows from both tables.

It combines the preservation behavior of LEFT and RIGHT joins.

### Example

```
SELECT s.StudentID, s.Name, d.DeptID, d.DeptName
FROM Student AS s
FULL OUTER JOIN Department AS d
    ON s.DeptID = d.DeptID;
```

Result:

|StudentID|Name|DeptID|DeptName|
|---|---|---|---|
|101|Amit|10|CSE|
|103|Ravi|10|CSE|
|102|Neha|20|ECE|
|104|Priya|NULL|NULL|
|NULL|NULL|40|HR|

The result contains:

- All three students matched to departments.
    
- Priya, who has no matching department.
    
- HR, which has no matching student.
    

The output order is illustrative; SQL does not guarantee row order without `ORDER BY`.

### Important exam point

`FULL OUTER JOIN` preserves unmatched rows from both sides.

### Visual comparison

INNER

Only the intersection: matching rows

LEFT

Whole left circle plus matching data

RIGHT

Whole right circle plus matching data

FULL

Both circles: all rows from both sides

### DBMS-specific support

Some databases support `FULL OUTER JOIN` directly; others do not. For example, MySQL does not provide native `FULL OUTER JOIN` syntax. In MySQL, you can emulate it with a `LEFT JOIN` combined with the unmatched right-side rows, commonly using `UNION ALL` and an anti-match condition.

Exam trap: Do not assume `FULL OUTER JOIN` syntax is available in every database product.

## 6. SELF JOIN

A SELF JOIN joins a table with itself. It is useful when rows in the same table are related to other rows in that table.

Common examples include employees and their managers, people and their supervisors, or categories and their parent categories.

### Example: Employee and manager

Suppose we have this `EMPLOYEE` table:

|EmpID|EmpName|ManagerID|
|---|---|---|
|1|Asha|NULL|
|2|Bharat|1|
|3|Charu|1|
|4|Deepak|2|

Here, `ManagerID` refers to another employee's `EmpID`.

### SQL query

```
SELECT
    e.EmpName AS Employee,
    m.EmpName AS Manager
FROM Employee AS e
LEFT JOIN Employee AS m
    ON e.ManagerID = m.EmpID;
```

Result:

|Employee|Manager|
|---|---|
|Asha|NULL|
|Bharat|Asha|
|Charu|Asha|
|Deepak|Bharat|

### How does it work?

- `e` is one reference to the `EMPLOYEE` table.
    
- `m` is a second reference to the same table.
    
- `e.ManagerID = m.EmpID` connects each employee to their manager.
    
- Asha has no manager in this sample, so `LEFT JOIN` preserves her row and returns NULL for the manager.
    

### Exam traps

- A self join is not a separate join keyword; it is an ordinary join involving the same table twice.
    
- Table aliases are especially useful to distinguish the two references.
    
- Self joins can be INNER, LEFT, or other supported join types depending on the requirement.
    

Memory trick: SELF = table joined with itself.

## 7. CROSS JOIN

A CROSS JOIN returns the Cartesian product of two tables. Every row of the first table is paired with every row of the second table.

### Example

Our tables contain:

- `STUDENT`: 4 rows.
    
- `DEPARTMENT`: 3 rows.
    

Therefore:

\[ 4 \times 3 = 12 \text{ result rows} \]

### SQL query

```
SELECT s.Name, d.DeptName
FROM Student AS s
CROSS JOIN Department AS d;
```

Result — all 12 combinations:

|Name|DeptName|
|---|---|
|Amit|CSE|
|Amit|ECE|
|Amit|HR|
|Neha|CSE|
|Neha|ECE|
|Neha|HR|
|Ravi|CSE|
|Ravi|ECE|
|Ravi|HR|
|Priya|CSE|
|Priya|ECE|
|Priya|HR|

Notice that Priya appears with all three departments even though her `DeptID` is NULL. A CROSS JOIN does not check department membership; it generates every combination.

### Formula

If table A contains \(m\) rows and table B contains \(n\) rows, then:

\[ \boxed{\text{CROSS JOIN rows}=m\times n} \]

Examples:

|Rows in A|Rows in B|Result rows|
|---|---|---|
|2|3|6|
|4|3|12|
|10|5|50|
|100|200|20,000|

Exam trap: A CROSS JOIN normally has no `ON` condition. Adding a matching condition turns the query into a different operation, such as an INNER JOIN.

## 8. All six joins — comparison table

|Join|Matching rows|Unmatched left rows|Unmatched right rows|
|---|---|---|---|
|INNER JOIN|Yes|Excluded|Excluded|
|LEFT JOIN|Yes|Preserved|Excluded|
|RIGHT JOIN|Yes|Excluded|Preserved|
|FULL OUTER JOIN|Yes|Preserved|Preserved|
|SELF JOIN|Depends on join type|Depends on join type|Depends on join type|
|CROSS JOIN|All combinations|Not based on matching|Not based on matching|

A SELF JOIN is defined by joining a table to itself. A CROSS JOIN is defined by producing combinations. Unlike INNER, LEFT, RIGHT and FULL joins, they are not simply additional unmatched-row variants of the same matching operation.

## 9. One more important exam trap: ON vs WHERE with LEFT JOIN

Compare these queries.

### Query A

```
SELECT s.Name, d.DeptName
FROM Student AS s
LEFT JOIN Department AS d
    ON s.DeptID = d.DeptID
   AND d.DeptName = 'CSE';
```

This preserves all students. Students whose department is not CSE, or who have no matching department, appear with NULL in the `DeptName` result.

### Query B

```
SELECT s.Name, d.DeptName
FROM Student AS s
LEFT JOIN Department AS d
    ON s.DeptID = d.DeptID
WHERE d.DeptName = 'CSE';
```

This returns only students matched to CSE. The `WHERE` condition removes rows where `d.DeptName` is NULL.

Why this matters: A condition in `WHERE` can remove unmatched rows that a LEFT JOIN would otherwise preserve. This is a common query-output question.

## 10. DSSSB exam revision sheet

|If the question asks…|Choose|
|---|---|
|Only matching rows|`INNER JOIN`|
|All rows from the first/left table|`LEFT JOIN`|
|All rows from the second/right table|`RIGHT JOIN`|
|All rows from both tables, matched where possible|`FULL OUTER JOIN`|
|Compare rows in the same table|`SELF JOIN`|
|All possible row combinations|`CROSS JOIN`|

Remember: unmatched outer-join columns are filled with NULL. A matching key value can return multiple rows if it matches multiple rows on the other side.

Last-minute memory trick: INNER = matches only; LEFT = keep left; RIGHT = keep right; FULL = keep both; SELF = same table twice; CROSS = every combination.