## 1. Sample table: STUDENT

|StudentID|Name|City|Marks|
|---|---|---|---|
|101|Amit|Delhi|85|
|102|Neha|Patna|92|
|103|Ravi|Delhi|76|
|104|Priya|Jaipur|88|
|105|Karan|Delhi|92|
|106|Sana|Patna|67|

## 2. WHERE clause

The WHERE clause filters individual rows according to a condition. Only rows for which the condition evaluates to true are included in the result.

### Syntax

```
SELECT column1, column2
FROM table_name
WHERE condition;
```

### Example 1: Find students scoring above 80

```
SELECT Name, Marks
FROM Student
WHERE Marks > 80;
```

Result:

|Name|Marks|
|---|---|
|Amit|85|
|Neha|92|
|Priya|88|
|Karan|92|

Ravi and Sana are excluded because their marks do not satisfy the condition.

### Example 2: Combine conditions with AND

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

Both conditions must be true.

### Example 3: Use OR

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

At least one condition must be true.

### Example 4: Use BETWEEN

```
SELECT Name, Marks
FROM Student
WHERE Marks BETWEEN 80 AND 92;
```

`BETWEEN` includes both endpoints, so marks equal to 80 and 92 also qualify.

### Example 5: Use IN

```
SELECT Name, City
FROM Student
WHERE City IN ('Delhi', 'Jaipur');
```

This is equivalent to checking whether the city matches either listed value.

### Example 6: Use LIKE

```
SELECT Name
FROM Student
WHERE Name LIKE 'A%';
```

This matches names beginning with `A`.

|Pattern|Meaning|
|---|---|
|`'A%'`|Starts with A|
|`'%a'`|Ends with a|
|`'%mit%'`|Contains `mit`|
|`'_m%'`|Second character is `m`|

`%` matches zero or more characters, while `_` matches one character. Case sensitivity depends on the database and collation.

### Example 7: Check NULL

```
SELECT Name
FROM Student
WHERE City IS NULL;
```

Use `IS NULL` or `IS NOT NULL` to check for missing values.

Exam traps for WHERE:

- `WHERE` filters rows, not groups.
    
- `WHERE` normally cannot use aggregate functions directly in the same query level, such as `WHERE COUNT(*) > 2`.
    
- Use `IS NULL`, not `= NULL`.
    
- `AND` has higher precedence than `OR`; use parentheses when the intended logic could be unclear.
    

## 3. GROUP BY clause

The GROUP BY clause groups rows that have the same values in one or more specified columns. It is commonly used with aggregate functions.

Important aggregate functions include:

|Function|Purpose|
|---|---|
|`COUNT(*)`|Counts rows|
|`SUM(column)`|Adds non-NULL values|
|`AVG(column)`|Calculates the average of non-NULL values|
|`MAX(column)`|Finds the largest value|
|`MIN(column)`|Finds the smallest value|

### Example 1: Count students in each city

```
SELECT City, COUNT(*) AS StudentCount
FROM Student
GROUP BY City;
```

Result:

|City|StudentCount|
|---|---|
|Delhi|3|
|Jaipur|1|
|Patna|2|

The six rows are grouped into three city groups.

### Example 2: Find average marks by city

```
SELECT City, AVG(Marks) AS AverageMarks
FROM Student
GROUP BY City;
```

Result:

|City|AverageMarks|
|---|---|
|Delhi|84.33|
|Jaipur|88.00|
|Patna|79.50|

Calculations:

- Delhi: \((85+76+92)/3 = 84.33\)
    
- Jaipur: \(88/1 = 88\)
    
- Patna: \((92+67)/2 = 79.50\)
    

### Example 3: Group using multiple columns

```
SELECT City, Marks, COUNT(*) AS Total
FROM Student
GROUP BY City, Marks;
```

This creates a group for each distinct `(City, Marks)` combination.

Important: When using `GROUP BY`, selected expressions generally need to be grouping expressions, aggregates, or otherwise valid under the DBMS's grouping rules.

### Example 4: Filter rows before grouping

```
SELECT City, AVG(Marks) AS AverageMarks
FROM Student
WHERE Marks >= 80
GROUP BY City;
```

First, students scoring below 80 are excluded. The remaining students are then grouped by city and their average marks are calculated.

Exam traps for GROUP BY:

- `GROUP BY` creates groups; it does not sort the final result.
    
- Grouping by `City` produces one output group per distinct city value, including a single group for NULL city values if any exist.
    
- `COUNT(*)` counts rows in each group.
    
- `COUNT(Marks)` counts only rows with non-NULL marks in each group.
    

## 4. HAVING clause

The HAVING clause filters groups, usually after `GROUP BY` has created them. It is commonly used to apply conditions to aggregate results.

### Example 1: Show cities having more than one student

```
SELECT City, COUNT(*) AS StudentCount
FROM Student
GROUP BY City
HAVING COUNT(*) > 1;
```

Result:

|City|StudentCount|
|---|---|
|Delhi|3|
|Patna|2|

Jaipur is excluded because its group contains only one student.

### Example 2: Cities with average marks above 80

```
SELECT City, AVG(Marks) AS AverageMarks
FROM Student
GROUP BY City
HAVING AVG(Marks) > 80;
```

Result:

|City|AverageMarks|
|---|---|
|Delhi|84.33|
|Jaipur|88.00|

Patna is excluded because its average is 79.50.

### Example 3: Use WHERE and HAVING together

```
SELECT City, AVG(Marks) AS AverageMarks
FROM Student
WHERE Marks >= 70
GROUP BY City
HAVING AVG(Marks) > 80;
```

Follow the steps:

1. `WHERE Marks >= 70` removes Sana, whose marks are 67.
    
2. `GROUP BY City` groups the remaining students by city.
    
3. `AVG(Marks)` calculates each city's average.
    
4. `HAVING AVG(Marks) > 80` keeps only cities whose average is greater than 80.
    

Result:

|City|AverageMarks|
|---|---|
|Delhi|84.33|
|Jaipur|88.00|

Delhi's average remains 84.33. Patna's average is now 92.00 because Sana was filtered out; therefore Patna also qualifies.

Correct final result:

|City|AverageMarks|
|---|---|
|Delhi|84.33|
|Jaipur|88.00|
|Patna|92.00|

This is a useful exam lesson: WHERE can change the rows contributing to an aggregate, which can change whether a group passes HAVING.

### Example 4: HAVING without GROUP BY

SQL also permits `HAVING` without an explicit `GROUP BY` in common DBMSs. In that case, aggregate evaluation generally treats the filtered input as one group.

```
SELECT COUNT(*) AS TotalStudents
FROM Student
HAVING COUNT(*) > 5;
```

With the six rows in our sample table, the result is:

|TotalStudents|
|---|
|6|

If the count condition were false, the query would return no rows.

Exam trap: `HAVING` is not required to be paired with a written `GROUP BY` in every valid SQL query.

## 5. WHERE vs HAVING — most important comparison

|Feature|WHERE|HAVING|
|---|---|---|
|Filters|Individual rows|Groups|
|Conceptual stage|Before grouping|After grouping|
|Commonly used with aggregate conditions|Not directly at the same query level|Yes|
|Used without `GROUP BY`|Yes|Yes, in common SQL implementations|
|Example|`WHERE Marks > 80`|`HAVING AVG(Marks) > 80`|

Think of it this way:

- WHERE: Which students should be included?
    
- HAVING: Which city groups should be included?
    

A query can use both:

```
SELECT City, COUNT(*) AS Total
FROM Student
WHERE Marks >= 80
GROUP BY City
HAVING COUNT(*) >= 2;
```

The query first keeps students with marks at least 80, then groups them by city, and finally retains groups having at least two qualifying students.

For our data, Delhi has two qualifying students (Amit and Karan); the other city groups have only one each. So Delhi is the only group returned.

## 6. ORDER BY clause

The ORDER BY clause sorts the final query result by one or more expressions.

### Example 1: Sort marks in ascending order

```
SELECT Name, Marks
FROM Student
ORDER BY Marks ASC;
```

Result:

|Name|Marks|
|---|---|
|Sana|67|
|Ravi|76|
|Amit|85|
|Priya|88|
|Neha|92|
|Karan|92|

`ASC` means ascending. It is the default direction if neither `ASC` nor `DESC` is written.

### Example 2: Sort marks in descending order

```
SELECT Name, Marks
FROM Student
ORDER BY Marks DESC;
```

The highest marks appear first.

|Name|Marks|
|---|---|
|Neha|92|
|Karan|92|
|Priya|88|
|Amit|85|
|Ravi|76|
|Sana|67|

The relative order of Neha and Karan is not guaranteed when their marks are equal. To get a deterministic order, add another sort key.

```
SELECT Name, Marks
FROM Student
ORDER BY Marks DESC, Name ASC;
```

Now students are ordered by marks descending and, when marks are equal, by name ascending.

### Example 3: ORDER BY with GROUP BY

```
SELECT City, AVG(Marks) AS AverageMarks
FROM Student
GROUP BY City
ORDER BY AverageMarks DESC;
```

Result:

|City|AverageMarks|
|---|---|
|Jaipur|88.00|
|Delhi|84.33|
|Patna|79.50|

Grouping creates the city-level results. Ordering sorts those results by average marks.

### Example 4: Sort by column position

```
SELECT Name, Marks
FROM Student
ORDER BY 2 DESC;
```

In common SQL implementations, `2` refers to the second selected expression, which is `Marks`.

For exam and production queries, using the column name or alias is usually clearer.

Exam traps for ORDER BY:

- `ORDER BY` does not eliminate duplicates.
    
- `ORDER BY` does not group rows.
    
- `ASC` is generally the default direction.
    
- Without `ORDER BY`, SQL does not guarantee a particular result order.
    
- NULL ordering can differ across database systems, so don't assume it is always first or always last.
    

## 7. DISTINCT keyword

`DISTINCT` removes duplicate rows from the query result.

### Example 1: Get unique cities

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

Delhi appears three times in the source data, but only once in this result. The order of these distinct cities is not guaranteed unless `ORDER BY` is used.

### Example 2: DISTINCT on multiple columns

```
SELECT DISTINCT City, Marks
FROM Student;
```

This removes duplicate City-and-Marks combinations. It does not independently make both columns unique.

Consider this data:

|City|Marks|
|---|---|
|Delhi|85|
|Delhi|85|
|Delhi|92|
|Patna|85|

After `SELECT DISTINCT City, Marks`, the result contains:

|City|Marks|
|---|---|
|Delhi|85|
|Delhi|92|
|Patna|85|

`Delhi, 85` appears once, but 85 can still appear in a different city.

### Example 3: DISTINCT with COUNT

```
SELECT COUNT(DISTINCT City) AS UniqueCities
FROM Student;
```

Result:

|UniqueCities|
|---|
|3|

This counts distinct, non-NULL city values.

### Example 4: DISTINCT vs GROUP BY

For this query:

```
SELECT DISTINCT City
FROM Student;
```

and this query:

```
SELECT City
FROM Student
GROUP BY City;
```

the outputs are equivalent for our purpose when only unique city values are needed. However, `GROUP BY` is especially useful when calculating aggregates per group.

Exam traps for DISTINCT:

- `DISTINCT` applies to the combination of all selected expressions.
    
- `DISTINCT` removes duplicate result rows, not duplicate records from the original table.
    
- `COUNT(DISTINCT column)` counts distinct non-NULL values.
    
- `SELECT DISTINCT *` removes rows that are identical across all selected columns.
    
- `DISTINCT` does not guarantee output order.
    

## 8. SQL clauses: written order vs logical processing order

This is a common MCQ area.

### Written syntax order

```
SELECT DISTINCT City, AVG(Marks) AS AverageMarks
FROM Student
WHERE Marks >= 70
GROUP BY City
HAVING AVG(Marks) > 80
ORDER BY AverageMarks DESC;
```

### Simplified logical processing order

1

FROM

Identify the data source

2

WHERE

Filter individual rows

3

GROUP BY

Create groups

4

HAVING

Filter groups

5

SELECT

Calculate and choose output expressions

6

DISTINCT

Remove duplicate result rows

7

ORDER BY

Sort the result

This is a simplified logical model for learning. The database optimizer may execute operations differently as long as the query's required results are preserved. Row limiting, such as `LIMIT`, is typically applied after ordering.

## 9. Last-minute comparison sheet

|Clause / keyword|Main function|Remember|
|---|---|---|
|`WHERE`|Filters rows|Before grouping|
|`GROUP BY`|Groups rows with matching values|Commonly used with aggregates|
|`HAVING`|Filters groups|Can test aggregate conditions|
|`ORDER BY`|Sorts query results|`ASC` or `DESC`|
|`DISTINCT`|Removes duplicate result rows|Applies to all selected expressions together|
Remember this one-line rule: `WHERE` filters rows, `GROUP BY` forms groups, `HAVING` filters groups, `ORDER BY` sorts results, and `DISTINCT` removes duplicate result rows.