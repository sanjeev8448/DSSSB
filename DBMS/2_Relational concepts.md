## 1. Understand using one example

Consider the following `STUDENT` relation (table):

|RollNo|Name|Age|City|
|---|---|---|---|
|101|Amit|21|Delhi|
|102|Neha|22|Patna|
|103|Ravi|20|Jaipur|

Here, a relation represents data organized into rows and columns.

## 2. Six important concepts

### 1. Relation

A relation is a table consisting of rows and columns in the relational database model.

Example: `STUDENT` is the relation name.

- A relation has attributes (columns).
    
- A relation contains tuples (rows).
    
- In the formal relational model, a relation is a set of unique tuples, and row order is irrelevant.
    

Exam trap: A relation is not the same as a tuple. A relation is the entire table; a tuple is one row.

### 2. Tuple

A tuple is a single row or record in a relation.

For example:

|RollNo|Name|Age|City|
|---|---|---|---|
|101|Amit|21|Delhi|

This row is one tuple.

In the given `STUDENT` relation, there are 3 tuples.

Remember: Tuple = Row = Record.

### 3. Attribute

An attribute is a column or field of a relation. It represents a property of the entity being stored.

In the `STUDENT` relation, the attributes are:

`RollNo`, `Name`, `Age`, `City`

Therefore, there are 4 attributes.

Remember: Attribute = Column = Field.

### 4. Domain

A domain is the set of permitted values for an attribute.

Examples:

|Attribute|Possible domain|
|---|---|
|Age|Integers within the permitted age range|
|Name|Valid character strings|
|RollNo|Positive integers|
|City|Valid city names|

A domain restricts the values that an attribute can contain. The precise domain depends on the database's defined rules.

For example, if `Age` is defined as an integer greater than or equal to zero, a value such as `-5` violates that domain.

Exam trap: Domain is not the number of rows or columns. It specifies the allowed values of an attribute.

### 5. Degree

The degree of a relation is the total number of attributes (columns) in that relation.

Our `STUDENT` relation has:

`RollNo`, `Name`, `Age`, `City`

Therefore:

\[ \boxed{\text{Degree}=4} \]

Remember: Degree = Number of columns.

### 6. Cardinality

The cardinality of a relation is the total number of tuples (rows) in that relation.

Our `STUDENT` relation contains three student records.

Therefore:

\[ \boxed{\text{Cardinality}=3} \]

Remember: Cardinality = Number of rows.

## 3. Degree vs Cardinality — most important comparison

|Concept|Meaning|In our example|
|---|---|---|
|Relation|Entire table|`STUDENT`|
|Tuple|One row|3 tuples|
|Attribute|One column|4 attributes|
|Domain|Allowed values for an attribute|E.g. permitted age values|
|Degree|Number of columns|4|
|Cardinality|Number of rows|3|

Degree = Columns

Count the headings: RollNo, Name, Age, City = 4.

Cardinality = Rows

Count the student records = 3.

### Quick formula

For a relation with \(m\) tuples and \(n\) attributes:

\[ \text{Cardinality}=m \]

\[ \text{Degree}=n \]

If a table contains 8 columns and 50 rows, its degree is 8 and its cardinality is 50.

## 4. Additional exam traps

- Adding a column: Usually increases the degree by 1.
    
- Adding a row: Increases the cardinality by 1, provided the tuple is a new distinct tuple in the formal relational model.
    
- Changing row order: Does not change degree or cardinality.
    
- Changing column order: Does not change degree or cardinality.
    
- Empty relation: A relation with zero tuples can have cardinality 0 while still having attributes and a positive degree.
    
- SQL distinction: SQL tables can contain duplicate rows unless prevented by constraints. A plain `SELECT` can return duplicates, whereas the formal relational model treats a relation as a set of tuples.
    

Also, in ER modelling, the term cardinality can refer to relationships such as one-to-one or one-to-many. In the current topic—relational concepts—it means the number of tuples in a relation.

Final revision line: Relation = table; tuple = row; attribute = column; domain = allowed values; degree = columns; cardinality = rows.