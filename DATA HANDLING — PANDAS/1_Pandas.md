# PANDAS — PYTHON DATA ANALYSIS LIBRARY

## 1. Introduction to Pandas

Pandas is a Python library used for data handling, analysis, cleaning, and manipulation.

For DSSSB preparation, focus on definitions, syntax, output-based questions, indexing, and the differences between a Series and a DataFrame.

Pandas provides two main data structures:

### A. Series

A **Series** is a one-dimensional labeled array. It stores values with an associated index.

Example: Marks of students in one subject.

### B. DataFrame

A **DataFrame** is a two-dimensional labeled data structure with rows and columns.

Example: Students' names, marks, and roll numbers.

Pandas is commonly used with NumPy and can work with data from CSV files, Excel files, SQL databases, and other sources.

### Importing Pandas

The standard import statement is:

```
import pandas as pd

print(pd.__version__)
```

Output: The installed Pandas version, which depends on your environment.

- `import` loads the library.
    
- `pandas` is the library name.
    
- `as pd` creates the conventional alias `pd`.
    

**Exam trap:** `pd` is an alias, not a separate library or a Python keyword. You can choose another alias, but `pd` is the standard convention.

## 2. Series in Pandas

A Series is a one-dimensional array-like object containing values and an index.

### A. Creating a Series

```
import pandas as pd

s = pd.Series([10, 20, 30, 40])
print(s)
```

Output:

```
0    10
1    20
2    30
3    40
dtype: int64
```

Understand each part:

- `0, 1, 2, 3` are the default index labels.
    
- `10, 20, 30, 40` are the values.
    
- `dtype: int64` indicates the integer data type used for the values.
    

The default index starts at `0` when you do not provide an index.

### B. Creating a Series with a custom index

```
import pandas as pd

s = pd.Series(
    [85, 90, 78],
    index=["Amit", "Riya", "Neha"]
)

print(s)
```

Output:

```
Amit    85
Riya    90
Neha    78
dtype: int64
```

Here, the index labels are names rather than integers.

### C. Accessing Series elements

```
import pandas as pd

s = pd.Series([10, 20, 30], index=["a", "b", "c"])

print(s["b"])
print(s.iloc[1])
```

Output:

```
20
20
```

|Method|Meaning|
|---|---|
|`s["b"]`|Access by index label `"b"`|
|`s.loc["b"]`|Explicitly access by label|
|`s.iloc[1]`|Access by integer position; position 1 is the second element|

**Remember:** `loc` is label-based, while `iloc` is position-based.

### D. Useful Series properties and methods

```
import pandas as pd

s = pd.Series([10, 20, 30, 40])

print(s.index)
print(s.values)
print(s.dtype)
print(s.size)
print(s.sum())
print(s.mean())
print(s.max())
print(s.min())
```

|Property or method|Purpose|
|---|---|
|`s.index`|Returns index labels|
|`s.values`|Returns the underlying values as an array-like object|
|`s.dtype`|Returns the data type|
|`s.size`|Returns the total number of elements|
|`s.sum()`|Calculates the sum|
|`s.mean()`|Calculates the arithmetic mean|
|`s.max()`|Returns the maximum value|
|`s.min()`|Returns the minimum value|

For the example above:

- `s.size` → `4`
    
- `s.sum()` → `100`
    
- `s.mean()` → `25.0`
    
- `s.max()` → `40`
    
- `s.min()` → `10`
    

## 3. DataFrame in Pandas

A DataFrame is a two-dimensional, labeled data structure with rows and columns. It is similar to a database table or spreadsheet.

### A. Creating a DataFrame from a dictionary

```
import pandas as pd

data = {
    "Name": ["Amit", "Riya", "Neha"],
    "Age": [21, 22, 20],
    "Marks": [85, 90, 78]
}

df = pd.DataFrame(data)
print(df)
```

Output:

```
   Name  Age  Marks
0  Amit   21     85
1  Riya   22     90
2  Neha   20     78
```

How to read this example:

- Dictionary keys (`Name`, `Age`, `Marks`) become column labels.
    
- Dictionary values become the data in each column.
    
- By default, the row index is `0, 1, 2`.
    
- Each dictionary value list must have the same length when constructing a DataFrame this way.
    

### B. Creating a DataFrame with a custom index

```
import pandas as pd

df = pd.DataFrame(
    {
        "Name": ["Amit", "Riya"],
        "Marks": [85, 90]
    },
    index=["S1", "S2"]
)

print(df)
```

Output:

```
    Name  Marks
S1  Amit     85
S2  Riya     90
```

The `index` parameter specifies row labels.

### C. Selecting columns

```
print(df["Name"])
```

This returns a Series containing the `Name` column.

To select multiple columns:

```
print(df[["Name", "Marks"]])
```

This returns a DataFrame because two columns are selected.

**High-value MCQ rule**

|Expression|Return type|
|---|---|
|`df["Name"]`|Series|
|`df[["Name"]]`|DataFrame|
|`df[["Name", "Marks"]]`|DataFrame|

Even `df[["Name"]]`, which selects just one column, returns a DataFrame because the column selection is supplied as a list.

### D. Selecting rows and values

Consider this DataFrame:

```
import pandas as pd

df = pd.DataFrame({
    "Name": ["Amit", "Riya", "Neha"],
    "Marks": [85, 90, 78]
})
```

**1. Select a row by label using** `**loc**`**:**

```
print(df.loc[1])
```

Output:

```
Name     Riya
Marks      90
Name: 1, dtype: object
```

**2. Select a row by position using** `**iloc**`**:**

```
print(df.iloc[0])
```

This selects the first row, containing Amit and 85.

**3. Select a particular cell:**

```
print(df.loc[1, "Marks"])
print(df.iloc[1, 1])
```

Both print:

```
90
90
```

### E. Important DataFrame attributes and methods

```
print(df.shape)
print(df.columns)
print(df.index)
print(df.size)
print(df.head())
print(df.tail())
print(df.info())
print(df.describe())
```

|Attribute/method|What it does|
|---|---|
|`df.shape`|Returns `(rows, columns)`|
|`df.columns`|Returns column labels|
|`df.index`|Returns row labels|
|`df.size`|Returns the total number of cells|
|`df.head()`|Returns the first 5 rows by default|
|`df.tail()`|Returns the last 5 rows by default|
|`df.info()`|Displays column names, data types, and non-null counts|
|`df.describe()`|Produces descriptive statistics for applicable columns|

**Exam trap:** `df.shape` is an attribute, so write `df.shape`, not `df.shape()`. `df.head()` and `df.describe()` are methods and require parentheses.

For a DataFrame with 3 rows and 2 columns:

- `df.shape` → `(3, 2)`
    
- `df.size` → `6`
    

### F. Adding and modifying columns

Add a Boolean column:

```
df["Passed"] = df["Marks"] >= 40
```

This creates a column called `Passed`. For the example data, all three values are `True`.

To update a value:

```
df.loc[0, "Marks"] = 95
```

This changes Amit's marks from 85 to 95.

### G. Filtering rows

Select rows where marks are greater than 80:

```
print(df[df["Marks"] > 80])
```

For multiple conditions, use parentheses and `&` for AND:

```
print(df[(df["Marks"] > 80) & (df["Marks"] < 95)])
```

Use `|` for OR.

**Exam trap:** In Pandas Boolean filtering, use `&` and `|` with parenthesized conditions rather than Python's `and` and `or`.

## 4. Series vs DataFrame — Quick Revision

|Feature|Series|DataFrame|
|---|---|---|
|Dimensions|1D|2D|
|Structure|One labeled sequence of values|Rows and columns|
|Labels|Index|Row index and column labels|
|Typical creation|`pd.Series([1, 2, 3])`|`pd.DataFrame({"A": [1, 2]})`|
|Selecting one column|Not applicable|Usually returns a Series|
|Selecting a list of columns|Not applicable|Returns a DataFrame|

## 5. Common MCQ Traps

- Pandas is imported conventionally using `import pandas as pd`.
    
- A Series is one-dimensional; a DataFrame is two-dimensional.
    
- A default Series index begins at zero.
    
- `loc` selects by label; `iloc` selects by integer position.
    
- `df.shape` returns a tuple, while `df.size` returns a single number.
    
- `df["A"]` returns a Series, while `df[["A"]]` returns a DataFrame.
    
- `head()` returns the first five rows by default, not necessarily the entire DataFrame.
    
- A DataFrame can contain columns with different data types.
    
- `df.info()` displays information; it is not the same as `df.describe()`.
    
- `df.describe()` summarizes data rather than printing every row.
    

## 6. Last-Minute Revision Table

| Question                                  | Answer       |     |
| ----------------------------------------- | ------------ | --- |
| Pandas standard alias                     | `pd`         |     |
| One-dimensional Pandas structure          | Series       |     |
| Two-dimensional Pandas structure          | DataFrame    |     |
| Default index start                       | `0`          |     |
| Select by label                           | `loc`        |     |
| Select by integer position                | `iloc`       |     |
| Number of rows and columns                | `shape`      |     |
| Total number of cells                     | `size`       |     |
| First five rows by default                | `head()`     |     |
| Last five rows by default                 | `tail()`     |     |
| Summary of data types and non-null counts | `info()`     |     |
| Descriptive statistics                    | `describe()` |     |
| Select one column as a Series             | `df["A"]`    |     |
| Select one column as a DataFrame          | `df[["A"]]`  |     |
| Boolean AND in filtering                  | `&`          |     |
| Boolean OR in filtering                   | `            | `   |