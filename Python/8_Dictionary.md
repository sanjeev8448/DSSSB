## 1. Key-value pairs

Each dictionary entry contains a key and its corresponding value.

```
student = {    "name": "Amit",    "age": 22,    "marks": 85}print(student["name"])print(student["age"])print(student["marks"])
```

Output:

```
Amit
22
85
```

Here:

- `"name"`, `"age"`, and `"marks"` are keys.
    
- `"Amit"`, `22`, and `85` are their corresponding values.
    

### Important properties of dictionaries

|Property|Explanation|
|---|---|
|Mutable|Entries can be added, updated, or deleted.|
|Keys are unique|Assigning an existing key replaces its value.|
|Values can repeat|Multiple keys can have the same value.|
|Keys must be hashable|Strings, integers, and suitable tuples can be keys. Lists and dictionaries cannot be keys.|
|Insertion order|Dictionaries preserve insertion order in modern Python.|
|Heterogeneous data|Keys and values can have different types, subject to key restrictions.|

### Duplicate keys

```
d = {    "a": 10,    "b": 20,    "a": 99}print(d)print(d["a"])
```

Output:

```
{'a': 99, 'b': 20}
99
```

The second value associated with `"a"` replaces the earlier value. It does not create a second `"a"` key.

Exam trap: Dictionary keys must be unique, but dictionary values do not have to be unique.

## 2. Dictionary creation

### Method 1: Using curly braces `{}`

```
student = {    "name": "Ravi",    "age": 23,    "city": "Delhi"}print(student)
```

Output:

```
{'name': 'Ravi', 'age': 23, 'city': 'Delhi'}
```

### Method 2: Using `dict()`

```
a = dict(name="Ravi", age=23)b = dict([("x", 10), ("y", 20)])print(a)print(b)
```

Output:

```
{'name': 'Ravi', 'age': 23}
{'x': 10, 'y': 20}
```

The keyword-argument form of `dict()` requires valid identifier-style names for its keyword keys.

### Method 3: Creating an empty dictionary

```
a = {}b = dict()print(type(a))print(type(b))
```

Output:

```
<class 'dict'>
<class 'dict'>
```

Remember that `{}` creates an empty dictionary, not a set. An empty set is created using `set()`.

### Accessing values

```
student = {"name": "Amit", "age": 22}print(student["name"])print(student["age"])
```

Output:

```
Amit
22
```

Using square brackets is a direct way to access a key's value. If the key is absent, Python raises a `KeyError`. The `get()` method provides an alternative, covered below.

## 3. Dictionary traversal

Traversal means visiting the dictionary's keys, values, or key-value pairs one at a time.

### A. Traversing keys

```
student = {"name": "Amit", "age": 22, "marks": 85}for key in student:    print(key)
```

Output:

```
name
age
marks
```

A `for` loop over a dictionary iterates over its keys by default.

The following is equivalent:

```
for key in student.keys():    print(key)
```

### B. Traversing values

```
student = {"name": "Amit", "age": 22, "marks": 85}for value in student.values():    print(value)
```

Output:

```
Amit
22
85
```

### C. Traversing keys and values together

Use `items()` when you need both the key and its value.

```
student = {"name": "Amit", "age": 22, "marks": 85}for key, value in student.items():    print(key, value)
```

Output:

```
name Amit
age 22
marks 85
```

This is called tuple unpacking: each item returned by `items()` is a two-element key-value pair.

### D. Traversing with conditions

```
marks = {    "Amit": 85,    "Ravi": 42,    "Neha": 91}for name, score in marks.items():    if score >= 50:        print(name, score)
```

Output:

```
Amit 85
Neha 91
```

Exam trap: In `for x in d`, `x` receives each key, not each value or key-value pair.

## 4. `keys()`

`keys()` returns a dictionary view containing the keys.

```
d = {"a": 10, "b": 20, "c": 30}print(d.keys())print(list(d.keys()))
```

Output:

```
dict_keys(['a', 'b', 'c'])
['a', 'b', 'c']
```

Notice that `d.keys()` returns a dictionary view, not a list.

### Dictionary views are dynamic

A view reflects changes made to its underlying dictionary.

```
d = {"a": 10, "b": 20}k = d.keys()d["c"] = 30print(k)
```

Output:

```
dict_keys(['a', 'b', 'c'])
```

Although `k` was created before `"c"` was added, it reflects the current keys.

Exam trap: `keys()` does not return an independent list. Use `list(d.keys())` when you specifically need a list.

## 5. `values()`

`values()` returns a dictionary view containing the values.

```
d = {"a": 10, "b": 20, "c": 10}print(d.values())print(list(d.values()))
```

Output:

```
dict_values([10, 20, 10])
[10, 20, 10]
```

Important points:

- Values may be duplicated.
    
- The values appear in the order of their corresponding dictionary entries.
    
- The returned view is dynamic.
    

Example:

```
d = {"a": 10, "b": 20}v = d.values()d["a"] = 99print(list(v))
```

Output:

```
[99, 20]
```

The view reflects the updated value.

Exam trap: Unlike keys, values are not required to be unique.

## 6. `items()`

`items()` returns a view of the dictionary's key-value pairs. Each pair behaves like a two-element tuple.

```
d = {"a": 10, "b": 20}print(d.items())print(list(d.items()))
```

Output:

```
dict_items([('a', 10), ('b', 20)])
[('a', 10), ('b', 20)]
```

### Using `items()` in a loop

```
d = {"a": 10, "b": 20}for key, value in d.items():    print(f"{key} = {value}")
```

Output:

```
a = 10
b = 20
```

### `keys()` vs `values()` vs `items()`

|Method|Returns a view of|Example entry|
|---|---|---|
|`keys()`|Keys|`'a'`|
|`values()`|Values|`10`|
|`items()`|Key-value pairs|`('a', 10)`|

All three return views, not ordinary lists.

## 7. `get()`

`get()` retrieves the value associated with a key without raising a `KeyError` when that key is missing.

Syntax:

```
dictionary.get(key, default)
```

The `default` argument is optional. If omitted, the default is `None`.

```
student = {"name": "Amit", "age": 22}print(student.get("name"))print(student.get("age"))print(student.get("marks"))print(student.get("marks", 0))
```

Output:

```
Amit
22
None
0
```

### `get()` vs square brackets

```
d = {"a": 10}print(d.get("x", 0))print(d["x"])
```

The first statement prints `0`. The second raises a `KeyError`, so execution stops before it can print a result for that statement.

|Operation|When key exists|When key is missing|
|---|---|---|
|`d[key]`|Returns its value|Raises `KeyError`|
|`d.get(key)`|Returns its value|Returns `None`|
|`d.get(key, default)`|Returns its value|Returns `default`|

Exam trap: `get()` does not insert the missing key into the dictionary.

```
d = {"a": 10}result = d.get("b", 0)print(result)print(d)
```

Output:

```
0
{'a': 10}
```

## 8. `update()`

`update()` adds new key-value pairs to a dictionary or changes values for existing keys.

Syntax:

```
dictionary.update(other)
```

### Example 1: Updating an existing key

```
d = {"a": 10, "b": 20}d.update({"b": 99, "c": 30})print(d)
```

Output:

```
{'a': 10, 'b': 99, 'c': 30}
```

- `"b"` already exists, so its value changes from `20` to `99`.
    
- `"c"` is new, so it is added.
    
- `"a"` remains unchanged.
    

### Example 2: Using keyword arguments

```
d = {"name": "Amit", "age": 22}d.update(age=23, city="Delhi")print(d)
```

Output:

```
{'name': 'Amit', 'age': 23, 'city': 'Delhi'}
```

### Example 3: Return value of `update()`

```
d = {"a": 1}result = d.update({"b": 2})print(d)print(result)
```

Output:

```
{'a': 1, 'b': 2}
None
```

Exam trap: `update()` modifies the existing dictionary and returns `None`.

### Accepted inputs

`update()` can accept a mapping, an iterable of key-value pairs, or keyword arguments.

```
d = {}d.update([("a", 1), ("b", 2)])print(d)
```

Output:

```
{'a': 1, 'b': 2}
```

## 9. `clear()`

`clear()` removes all key-value pairs from a dictionary. The dictionary object still exists, but it becomes empty.

```
d = {"a": 10, "b": 20, "c": 30}result = d.clear()print(d)print(result)
```

Output:

```
{}
None
```

### `clear()` and aliases

```
a = {"x": 10, "y": 20}b = aa.clear()print(a)print(b)
```

Output:

```
{}
{}
```

Both names refer to the same dictionary object, so clearing it affects what both names see.

Exam trap: `clear()` removes all entries but does not unbind the variable or return a new empty dictionary.

## 10. `del` statement

`del` is a Python statement, not a dictionary method. It can delete a particular dictionary entry or remove a variable binding entirely.

### Example 1: Delete a specific key

```
student = {    "name": "Amit",    "age": 22,    "marks": 85}del student["age"]print(student)
```

Output:

```
{'name': 'Amit', 'marks': 85}
```

Only the key `"age"` and its associated value are removed.

### Example 2: Delete multiple entries

```
d = {"a": 10, "b": 20, "c": 30}del d["a"]del d["c"]print(d)
```

Output:

```
{'b': 20}
```

### Example 3: Delete a missing key

```
d = {"a": 10}del d["b"]
```

This raises a `KeyError` because `"b"` is not present.

### Example 4: Delete the dictionary variable

```
d = {"a": 10}del dprint(d)
```

The final statement raises a `NameError` because the name `d` has been deleted.

### `del` vs `clear()`

|Feature|`del d["a"]`|`d.clear()`|`del d`|
|---|---|---|---|
|Removes one entry|Yes|No|No|
|Removes every entry|No|Yes|The variable binding is removed|
|Leaves an empty dictionary under `d`|If other keys remain, no; if it was the only key, yes|Yes|No|
|Method or statement?|Statement|Method|Statement|

Exam trap: Use `del d["key"]` to delete one entry, `d.clear()` to empty the dictionary, and `del d` to remove the name `d`.

## Final revision sheet

|Topic|Must remember|
|---|---|
|Key-value|Each key maps to a value|
|Creation|`{}` or `dict()`|
|Traversal|`for key in d` traverses keys|
|`keys()`|Returns a keys view|
|`values()`|Returns a values view|
|`items()`|Returns key-value pairs|
|`get()`|Returns a default instead of raising `KeyError` for a missing key|
|`update()`|Adds entries or overwrites existing values; returns `None`|
|`clear()`|Empties the dictionary; returns `None`|
|`del d[key]`|Deletes one entry|
|`del d`|Deletes the variable binding|

Highest-priority traps: `d[key]` vs `d.get(key)`, dictionary traversal, `items()` unpacking, dynamic views, `update()` returning `None`, and `clear()` vs `del`. These are ideal concepts for short DSSSB programming