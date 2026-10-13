# PANDAS DATAFRAME — DSSSB TGT COMPUTER SCIENCE

A **DataFrame** is a two-dimensional, labeled data structure consisting of rows and columns. It is similar to a spreadsheet or a database table.

**Important exam areas:**

- Creating DataFrames from dictionaries and lists
    
- Reading and writing CSV files
    
- Selecting rows and columns
    
- Adding, deleting, and renaming columns
    
- Row operations and sorting
    
- Boolean indexing
    
- Iterating over rows and columns
    

## 1. Creating a DataFrame

```
import pandas as pd

data = {
    "Name": ["Amit", "Riya", "Neha", "Raj"],
    "Marks": [85, 92, 78, 35],
    "Age": [21, 22, 20, 23]
}

df = pd.DataFrame(data)
print(df)
```

Output:

```
   Name  Marks  Age
0  Amit     85   21
1  Riya     92   22
2  Neha     78   20
3   Raj     35   23
```

Each dictionary key becomes a column name. The lists supply the values in each column.

## 2. Creating a DataFrame from a Dictionary of Series

A dictionary of Series contains key-value pairs in which each key becomes a column name and each value is a Pandas Series.

### Example

```
import pandas as pd

names = pd.Series(["Amit", "Riya", "Neha"], index=[0, 1, 2])
marks = pd.Series([85, 92, 78], index=[0, 1, 2])

df = pd.DataFrame({
    "Name": names,
    "Marks": marks
})

print(df)
```

Output:

```
   Name  Marks
0  Amit     85
1  Riya     92
2  Neha     78
```

### Important concept: Index alignment

Pandas aligns Series by their index labels when creating a DataFrame.

```
names = pd.Series(["Amit", "Riya"], index=[0, 1])
marks = pd.Series([85, 92], index=[1, 2])

df = pd.DataFrame({
    "Name": names,
    "Marks": marks
})

print(df)
```

Output:

```
   Name  Marks
0  Amit    NaN
1  Riya   85.0
2   NaN   92.0
```

Explanation:

- Index `0`: only `Name` has a value.
    
- Index `1`: `Riya` aligns with marks `85`.
    
- Index `2`: only `Marks` has a value.
    

**Exam trap:** Pandas aligns Series using index labels rather than combining their values purely by physical position.

## 3. Creating a DataFrame from a List of Dictionaries

Each dictionary generally represents one row. Dictionary keys become column names.

```
data = [
    {"Name": "Amit", "Marks": 85},
    {"Name": "Riya", "Marks": 92},
    {"Name": "Neha", "Marks": 78}
]

df = pd.DataFrame(data)
print(df)
```

Output:

```
   Name  Marks
0  Amit     85
1  Riya     92
2  Neha     78
```

### What happens when a dictionary is missing a key?

```
data = [
    {"Name": "Amit", "Marks": 85},
    {"Name": "Riya"},
    {"Name": "Neha", "Marks": 78}
]

df = pd.DataFrame(data)
print(df)
```

Output:

```
   Name  Marks
0  Amit   85.0
1  Riya    NaN
2  Neha   78.0
```

Riya's missing `Marks` value becomes `NaN`.

### Dictionary of Series vs. List of Dictionaries

|Feature|Dictionary of Series|List of dictionaries|
|---|---|---|
|Basic structure|Column-oriented|Row-oriented|
|Dictionary keys|Column names|Column names|
|Index alignment|Series align by index labels|Each dictionary usually represents a row|
|Missing values|Possible when Series indexes differ|Possible when dictionary keys are missing|

## 4. Creating and Reading CSV Files

CSV stands for **Comma-Separated Values**. It is a plain-text format commonly used to store tabular data.

Example file, `students.csv`:

```
Name,Marks,Age
Amit,85,21
Riya,92,22
Neha,78,20
Raj,35,23
```

### A. Read a CSV file

```
df = pd.read_csv("students.csv")
print(df)
```

`pd.read_csv()` reads a CSV file into a DataFrame. By default, the first row is treated as the column header.

### B. Read selected columns

```
df = pd.read_csv(
    "students.csv",
    usecols=["Name", "Marks"]
)
```

Only the `Name` and `Marks` columns are loaded.

### C. Save a DataFrame to CSV

```
df.to_csv("output.csv", index=False)
```

- `to_csv()` writes a DataFrame to a CSV file.
    
- `index=False` prevents the row index from being written as an additional column.
    
- Without `index=False`, the index is included by default.
    

### D. Common CSV methods and parameters

|Method or parameter|Purpose|
|---|---|
|`pd.read_csv("file.csv")`|Read a CSV file|
|`df.to_csv("file.csv")`|Write a DataFrame to CSV|
|`usecols=[...]`|Read selected columns|
|`nrows=5`|Read up to five data rows|
|`header=None`|Treat the file as having no header row|
|`index=False`|Do not write the index when saving|

**Exam trap:** `read_csv()` reads; `to_csv()` writes.

## 5. Selecting Rows and Columns

Consider the following DataFrame:

```
df = pd.DataFrame({
    "Name": ["Amit", "Riya", "Neha", "Raj"],
    "Marks": [85, 92, 78, 35],
    "Age": [21, 22, 20, 23]
})
```

### A. Select one column

```
print(df["Name"])
```

This returns a **Series**.

### B. Select multiple columns

```
print(df[["Name", "Marks"]])
```

This returns a **DataFrame**.

### C. Select rows using `loc`

```
print(df.loc[1])
```

This selects the row with index label `1`, containing Riya.

Select multiple rows:

```
print(df.loc[1:2])
```

For this default integer index, rows with labels `1` and `2` are selected, including both endpoints.

### D. Select rows using `iloc`

```
print(df.iloc[0])
```

This selects the first row by position.

```
print(df.iloc[0:2])
```

This selects the first two rows. The ending position is excluded.

### E. Select a particular cell

```
print(df.loc[1, "Marks"])  # 92
print(df.iloc[1, 1])       # 92
```

Both expressions access Riya's marks.

### F. Select rows and columns together

```
print(df.loc[0:2, ["Name", "Marks"]])
```

This selects rows with labels `0`, `1`, and `2`, displaying only the `Name` and `Marks` columns.

**Remember:**

- `loc` uses labels.
    
- `iloc` uses integer positions.
    
- `df["Marks"]` returns a Series.
    
- `df[["Marks"]]` returns a DataFrame.
    

## 6. Adding a Column

### A. Add a column using a list

```
df["City"] = ["Delhi", "Noida", "Delhi", "Gurugram"]
print(df)
```

The `City` column is added. The list must contain the correct number of values to match the rows.

### B. Add a column using a scalar

```
df["Country"] = "India"
```

The value `"India"` is repeated for every row.

### C. Add a calculated column

```
df["Bonus"] = df["Marks"] + 5
```

For the first row, Amit's calculated value is `90`.

### D. Add a column using a condition

```
df["Result"] = df["Marks"] >= 40
```

This creates a Boolean column:

- `True` if marks are at least 40.
    
- `False` otherwise.
    

### E. Insert a column at a particular position

```
df.insert(1, "RollNo", [101, 102, 103, 104])
```

`insert()` adds `RollNo` at position `1`, which is the second column.

**Exam trap:** Assigning to an existing column name replaces its values; assigning to a new column name creates a column.

## 7. Deleting a Column

Pandas provides `drop()`, `del`, and `pop()` for removing columns.

### A. Delete using `drop()`

```
df.drop(columns=["Age"], inplace=True)
```

- `columns=["Age"]` identifies the column to remove.
    
- `inplace=True` modifies the original DataFrame.
    

Without `inplace=True`, `drop()` normally returns a new DataFrame.

```
new_df = df.drop(columns=["Age"])
```

Here, `df` remains unchanged, and the result is stored in `new_df`.

### B. Delete using `del`

```
del df["Age"]
```

This removes the `Age` column from the original DataFrame.

### C. Delete using `pop()`

```
removed = df.pop("Age")
```

This removes the `Age` column and returns the removed column as a Series.

### Comparison

|Method|Removes column?|Returns removed column?|Modifies original?|
|---|---|---|---|
|`df.drop(columns=["Age"])`|Yes, in returned DataFrame|No|No, by default|
|`df.drop(columns=["Age"], inplace=True)`|Yes|No|Yes|
|`del df["Age"]`|Yes|No|Yes|
|`df.pop("Age")`|Yes|Yes, as a Series|Yes|

**Important:** `drop()` can also delete rows. Use `columns=` when removing a column.

## 8. Renaming Columns and Indexes

Use `rename()` to change column names or index labels.

### A. Rename one column

```
df.rename(
    columns={"Marks": "Score"},
    inplace=True
)
```

The column `Marks` is renamed to `Score`.

### B. Rename multiple columns

```
df.rename(
    columns={
        "Name": "Student",
        "Age": "StudentAge"
    },
    inplace=True
)
```

### C. Rename row index labels

```
df.rename(
    index={0: "A", 1: "B"},
    inplace=True
)
```

The row labels `0` and `1` become `A` and `B`.

### D. Replace all column names

```
df.columns = ["Student", "Score", "StudentAge"]
```

The number of names must match the number of columns.

**Exam trap:** `rename()` changes the specified labels; unspecified labels remain unchanged.

## 9. Row and Column Operations

### A. Add a row using `loc`

```
df.loc[4] = ["Karan", 88, 21]
```

If index label `4` does not exist, this adds a row with that label. The values must match the columns and their intended order.

### B. Update an existing row

```
df.loc[0, "Marks"] = 95
```

This changes the marks in the row labeled `0`.

### C. Delete a row

```
df.drop(index=3, inplace=True)
```

This removes the row with index label `3`.

### D. Delete multiple rows

```
df.drop(index=[1, 2], inplace=True)
```

This removes rows with labels `1` and `2`.

### E. Count rows and columns

```
print(df.shape)
print(len(df))
print(len(df.columns))
```

- `df.shape` returns `(number_of_rows, number_of_columns)`.
    
- `len(df)` returns the number of rows.
    
- `len(df.columns)` returns the number of columns.
    

### F. Transpose a DataFrame

```
print(df.T)
```

`.T` swaps rows and columns. The original row labels become column labels, and the original column labels become row labels.

### G. Sort rows

```
df.sort_values(
    by="Marks",
    ascending=False,
    inplace=True
)
```

This sorts rows by marks from highest to lowest.

- `ascending=True`: smallest to largest.
    
- `ascending=False`: largest to smallest.
    

Sorting changes row order; it does not delete rows.

## 10. Boolean Indexing

Boolean indexing filters rows using conditions.

```
df = pd.DataFrame({
    "Name": ["Amit", "Riya", "Neha", "Raj"],
    "Marks": [85, 92, 78, 35],
    "Age": [21, 22, 20, 23]
})
```

### A. Single condition

```
print(df[df["Marks"] > 80])
```

This returns Amit and Riya because their marks are greater than 80.

### B. AND condition

```
print(
    df[
        (df["Marks"] >= 80) &
        (df["Age"] < 22)
    ]
)
```

This returns rows satisfying both conditions. Here, Amit qualifies.

### C. OR condition

```
print(
    df[
        (df["Marks"] < 40) |
        (df["Age"] == 20)
    ]
)
```

This returns Raj and Neha.

### D. Negation

```
print(df[~(df["Marks"] >= 80)])
```

The `~` operator negates the Boolean condition, selecting rows whose marks are below 80.

### E. Filter using `isin()`

```
print(df[df["Name"].isin(["Amit", "Neha"])])
```

This selects rows where the name is either Amit or Neha.

### Boolean indexing operators

|Operator|Meaning|
|---|---|
|`&`|AND — both conditions must be true|
|`\|`|OR — at least one condition must be true|
|`~`|NOT — reverses a Boolean condition|
|`.isin([...])`|Checks whether values belong to a given collection|

**Very common exam trap:** Put each condition inside parentheses when using `&` or `|`.

Correct:

```
df[(df["Marks"] > 70) & (df["Age"] < 22)]
```

Avoid:

```
df[df["Marks"] > 70 and df["Age"] < 22]
```

Python's `and` does not perform the required element-wise Boolean operation on Pandas Series.

## 11. Iteration in a DataFrame

Iteration means accessing rows, columns, or values one by one.

```
import pandas as pd

df = pd.DataFrame({
    "Name": ["Amit", "Riya", "Neha"],
    "Marks": [85, 92, 78]
})
```

### A. Iterate over column names

```
for col in df:
    print(col)
```

Output:

```
Name
Marks
```

**Important:** Iterating directly over a DataFrame normally iterates over its column labels, not its rows.

### B. Iterate over column labels and Series

```
for col, series in df.items():
    print(col)
    print(series)
```

`items()` yields each column name along with the corresponding Series.

### C. Iterate over rows using `iterrows()`

```
for index, row in df.iterrows():
    print(index, row["Name"], row["Marks"])
```

Output:

```
0 Amit 85
1 Riya 92
2 Neha 78
```

Each iteration yields an index label and a row represented as a Series.

### D. Iterate over rows using `itertuples()`

```
for row in df.itertuples():
    print(row.Name, row.Marks)
```

Output:

```
Amit 85
Riya 92
Neha 78
```

By default, `itertuples()` includes the row index in each named tuple.

### E. Iterate over individual values

```
for value in df["Marks"]:
    print(value)
```

Output:

```
85
92
78
```

This iterates over the values of the `Marks` Series.

### Iteration methods compared

|Method|What it iterates over|Typical result|
|---|---|---|
|`for col in df`|Column labels|Column name|
|`df.items()`|Columns|`(column_name, Series)`|
|`df.iterrows()`|Rows|`(index, Series)`|
|`df.itertuples()`|Rows|Named tuples by default|
|`df["Marks"]` in a loop|Values of one column|Individual values|

**Exam tip:** Vectorized operations are usually more efficient than row-by-row iteration.

For example, prefer:

```
df["Bonus"] = df["Marks"] + 5
```

over a loop that calculates each bonus separately.

## 12. Quick Revision Sheet

|Concept|Remember|
|---|---|
|Create from dictionary|`pd.DataFrame(data)`|
|Create from list of dictionaries|Each dictionary generally represents a row|
|Read CSV|`pd.read_csv()`|
|Write CSV|`df.to_csv()`|
|Select one column|`df["A"]` returns a Series|
|Select a column as a DataFrame|`df[["A"]]`|
|Select by label|`loc`|
|Select by position|`iloc`|
|Add or replace a column|`df["New"] = ...`|
|Insert a column|`df.insert()`|
|Remove a column|`drop()`, `del`, or `pop()`|
|Rename labels|`rename()`|
|Count rows and columns|`shape`|
|Transpose|`.T`|
|Sort by values|`sort_values()`|
|Boolean filtering|Parenthesized conditions with `&`, `\|`, and `~`|
|Iterate over columns|`items()`|
|Iterate over rows|`iterrows()` or `itertuples()`|

## 13. Important Exam Traps

1. A DataFrame is a **two-dimensional** labeled data structure.
    
2. A dictionary's keys become column names when creating a DataFrame from column-oriented data.
    
3. Series are aligned by index labels when combined into a DataFrame.
    
4. Missing dictionary keys or unmatched Series indexes can produce `NaN`.
    
5. `df["Marks"]` returns a Series, while `df[["Marks"]]` returns a DataFrame.
    
6. `loc` uses labels; `iloc` uses integer positions.
    
7. `loc[1:2]` includes both endpoint labels, while `iloc[1:2]` excludes the ending position.
    
8. `index=False` prevents the index from being saved in a CSV file.
    
9. `inplace=True` applies changes to the original DataFrame for the operations shown.
    
10. `pop()` removes a column and returns it as a Series.
    
11. `shape` returns a tuple containing rows first and columns second.
    
12. `sort_values()` changes row order, not the number of rows.
    
13. Use `&` and `|` instead of Python's `and` and `or` for element-wise Series conditions.
    
14. Iterating directly over a DataFrame normally produces column labels.
    
15. Vectorized operations are generally preferred over manual row-by-row loops.