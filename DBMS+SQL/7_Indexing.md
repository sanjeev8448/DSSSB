## 1. What is indexing?

Indexing is a technique used by a DBMS to locate records more quickly without scanning every row of a table.

Think of the index at the back of a textbook: instead of reading every page to find a topic, you look up the topic and go directly to the relevant page.

Suppose you have a table with 100,000 employee records. Without a suitable index, finding one employee may require scanning many rows. An appropriate index can help the database locate the record much faster.

### How an index works

Query: Find employee with ID 105

### Index

ID 105 → Record location

### Employee record found

The DBMS follows the index to retrieve the row.

An index commonly stores search-key values and pointers or references to records or data pages. The exact structure depends on the DBMS and index type.

## 2. Purpose of indexing

The main purpose is to improve data retrieval performance.

|Advantage|Explanation|
|---|---|
|Faster searches|Reduces the need to scan the entire table|
|Efficient sorting|Can help satisfy `ORDER BY` without a separate sort|
|Faster joins|Can help locate matching rows|
|Efficient range queries|Can help find values within a range, especially with ordered indexes|

### Disadvantages

|Disadvantage|Explanation|
|---|---|
|Extra storage|Index structures use disk space|
|Slower INSERT|Index entries may need to be added|
|Slower UPDATE|Indexes may need maintenance when indexed values change|
|Slower DELETE|Corresponding index entries may need to be removed|

Exam trap: Indexing generally improves read/search performance, but it is not free. Too many unnecessary indexes can reduce write performance and consume additional storage.

## 3. Primary index

A primary index, in the traditional file-organization terminology, is built on the ordering key field of a data file whose records are physically ordered by that key.

Example: Employee records are stored in `EmployeeID` order.

|EmployeeID|Name|Department|
|---|---|---|
|101|Amit|IT|
|102|Neha|HR|
|103|Ravi|IT|
|104|Priya|Finance|
|105|Karan|HR|

An illustrative primary index might be:

|EmployeeID key|Data block pointer|
|---|---|
|101|Block 1|
|103|Block 2|
|105|Block 3|

This example uses one entry per block as a simplified sparse index illustration. In a traditional primary index, the entries may identify the first key value in each data block.

### Important characteristics

- The data file is ordered on the index's search-key field.
    
- The ordering field is typically a primary key.
    
- A traditional primary index is commonly sparse, with entries for blocks rather than every individual record.
    
- Sparse indexing can save index storage, but the DBMS may need to search within the selected block.
    

Exam trap: A primary index is not simply another name for a primary key. The primary key is a constraint that uniquely identifies rows; a primary index is an indexing concept.

## 4. Secondary index

A secondary index, in traditional file-organization terminology, is built on a field that does not determine the physical ordering of the data file.

Suppose employee records are stored in `EmployeeID` order, but users often search by department.

Example secondary index:

|Department|Matching EmployeeID values|
|---|---|
|Finance|104|
|HR|102, 105|
|IT|101, 103|

This index can help locate employees by department without scanning the entire employee table.

### Important characteristics

- It is built on a non-ordering field of the data file.
    
- It can be created on a unique or non-unique attribute.
    
- A secondary index is commonly dense in traditional textbook examples.
    
- If multiple rows share a search-key value, the index can reference multiple records or a list of record pointers.
    

Exam trap: A secondary index does not necessarily mean an index on a foreign key. It means an index on a field that is not the file's ordering field in the traditional terminology.

## 5. Primary index vs secondary index

|Feature|Primary index|Secondary index|
|---|---|---|
|Traditional file ordering|Built on the ordering key field|Built on a non-ordering field|
|Data file sorted on indexed field?|Yes|Not necessarily|
|Traditional textbook structure|Commonly sparse|Commonly dense|
|Example|File ordered by `EmployeeID`|File ordered by `EmployeeID`, indexed additionally by `Department`|
|Main use|Search on the ordering field|Search using another field|

The terms primary index and secondary index above follow the traditional DBMS file-organization model taught in many computer-science syllabi. Modern DBMS products use their own index terminology and implementations.

## 6. Dense index vs sparse index

These concepts are closely related to primary and secondary indexing and are common MCQ material.

### Dense index

A dense index has an index entry for every search-key value or every record, depending on the index design.

Example: one index entry for each employee ID.

|Index key|Record pointer|
|---|---|
|101|Record 101|
|102|Record 102|
|103|Record 103|
|104|Record 104|

Key point: Dense indexes generally require more space, but they provide a direct index entry for each search-key value or record.

### Sparse index

A sparse index has entries for only some search-key values, often one entry per data block.

|First key in block|Block pointer|
|---|---|
|101|Block 1|
|104|Block 2|

The DBMS uses the index to find an appropriate block and then searches within that block.

Key point: Sparse indexes generally require fewer index entries, but normally depend on the relevant data being ordered by the search key.

### Dense vs sparse comparison

|Feature|Dense|Sparse|
|---|---|---|
|Index entries|Every search-key value or record, depending on design|Only selected values|
|Space requirement|Generally higher|Generally lower|
|Locating records|More direct index entry|May require searching within a data block|
|Traditional suitability|Secondary indexes are often dense|Primary indexes on ordered files are often sparse|

Memory trick: Dense = more entries; Sparse = fewer entries.

## 7. Clustered concepts

The term clustered is used in two closely related ways in DBMS teaching. Be sure to recognize the terminology used in the question.

### A. Clustering index — traditional textbook meaning

A clustering index is built on an ordering non-key field of a data file. The records are physically ordered by that field, but the field does not uniquely identify each record.

Example: Employee records are stored grouped by `Department`.

|EmployeeID|Name|Department|
|---|---|---|
|101|Amit|Finance|
|104|Priya|Finance|
|102|Neha|HR|
|105|Karan|HR|
|103|Ravi|IT|

An illustrative clustering index could be:

|Department|Pointer to first record in group|
|---|---|
|Finance|First Finance record|
|HR|First HR record|
|IT|First IT record|

There can be many employees per department, so the department field is not unique. The index points to the beginning of each group.

Traditional clustering indexes often have one index entry per distinct ordering-field value.

### B. Clustered index — common modern DBMS meaning

In many modern database products, a clustered index describes how table rows are organized according to the index's key order.

This can make range searches and ordered retrieval efficient. The exact physical implementation is DBMS-specific.

A table's data can normally be clustered by only one key order at a time, although secondary/nonclustered indexes can also exist.

### Clustered vs nonclustered index

|Feature|Clustered index|Nonclustered index|
|---|---|---|
|Data organization|Rows are organized according to the clustered key order in common implementations|Separate index structure points to the underlying rows|
|Number per table|Normally one clustered ordering|Multiple nonclustered indexes may exist|
|Range retrieval|Often efficient for ranges on the clustered key|Also useful, but may require extra row lookups|
|Storage|Data organization is tied to the index structure|Additional index storage is required|

Exam trap: Do not automatically assume that clustering index in a traditional textbook question means exactly the same thing as clustered index in every commercial DBMS. Use the definition implied by the question.

## 8. Quick examples of SQL indexes

These examples use common SQL syntax; exact options vary by database system.

Create an index on an employee ID:

```

CREATE INDEX idx_employee_id
ON Employee(EmployeeID);
```

Create an index on department:

```

CREATE INDEX idx_employee_dept
ON Employee(Department);
```

Create a composite index:

```

CREATE INDEX idx_dept_salary
ON Employee(Department, Salary);
```

The composite index is on two columns. Depending on the index structure and query, it can help with searches on `Department` and with searches on `Department` together with `Salary`. It may not be equally useful for a search on `Salary` alone because index column order matters.

Important: `CREATE INDEX` syntax does not, by itself, mean that the index is clustered. Clustered-index creation is DBMS-specific.

## 9. Most important exam traps

| Statement                                                                       | Correct?       |
| ------------------------------------------------------------------------------- | -------------- |
| Indexing can improve search performance.                                        | True           |
| An index always makes every database operation faster.                          | False          |
| A traditional primary index is built on the ordered key field of the data file. | True           |
| A secondary index must be on the primary key.                                   | False          |
| A sparse index contains fewer entries than a corresponding dense index.         | Generally true |
| A traditional clustering index uses a non-key ordering field.                   | True           |
| Multiple nonclustered indexes can exist on a table.                             | True           |
| Indexes consume additional storage.                                             | True           |
| Every index must contain one entry per record.                                  | False          |
| Modern clustered-index terminology is identical across every DBMS.              | False          |
### Last-minute revision

- Purpose: Faster retrieval.
    
- Primary index: Traditional index on the ordering key field.
    
- Secondary index: Traditional index on a non-ordering field.
    
- Clustering index: Traditional index on an ordering non-key field.
    
- Dense index: More index entries.
    
- Sparse index: Fewer index entries.
    
- Trade-off: Faster reads versus extra storage and write-maintenance cost.