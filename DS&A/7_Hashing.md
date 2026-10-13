# DSSSB TGT Computer Science — Data Structures Notes

## Topic: Hashing, Hash Functions, Collision Resolution and Load Factor

# 1. What Is Hashing?

**Hashing** is a technique used to store and retrieve data efficiently using a calculated index.

Suppose you want to store students' records using their roll numbers. Instead of searching through every record, a hash function calculates a location where each record should be stored.

### How hashing works

Example:

- Key = 25
    
- Hash function: `h(key) = key % 7`
    
- Calculation: `25 % 7 = 4`
    
- Index = 4
    

A hash table uses this calculated index to locate the storage position.

Hashing can make insertion, searching and deletion very efficient.

# 2. Hash Function

A **hash function** maps a key to a hash value or table index.

For a table of size `m`, a simple hash function for non-negative integer keys is:

**h(k) = k % m**

Where:

- `k` = key
    
- `m` = table size
    
- `h(k)` = calculated index, ranging from `0` to `m - 1`
    

## 2.1 Division method

Suppose the table size is 7.

|Key (k)|Calculation|Index|
|---|---|---|
|10|10 % 7|3|
|22|22 % 7|1|
|25|25 % 7|4|
|31|31 % 7|3|
|44|44 % 7|2|

Notice that both 10 and 31 map to index 3. This produces a **collision**.

## 2.2 Common hash function methods

|Method|Basic idea|Example|
|---|---|---|
|Division method|Use the remainder after division by table size|`h(k) = k % m`|
|Multiplication method|Multiply the key by a constant and use its fractional part|`floor(m * frac(kA))`|
|Mid-square method|Square the key and extract selected middle digits|Square the key, then take middle digits|
|Folding method|Divide the key into parts and combine them|Add groups of digits|

For introductory exam questions, the division method is especially important.

## 2.3 Properties of a good hash function

A good hash function should:

- Be deterministic for the same key under the same hashing context.
    
- Distribute keys reasonably uniformly across the table.
    
- Be efficient to calculate.
    
- Reduce clustering and collisions where possible.
    

**Exam trap:** A hash function does not guarantee that every key maps to a unique index. Collisions are possible and require a resolution method.

# 3. Collision

A **collision** occurs when two different keys produce the same hash table index.

For example, if:

`h(k) = k % 7`

Then:

- `h(10) = 10 % 7 = 3`
    
- `h(17) = 17 % 7 = 3`
    

Both keys map to index 3, so a collision occurs.

### Why do collisions occur?

The number of possible keys is usually much larger than the number of available table slots. Multiple keys can therefore map to the same index.

According to the **pigeonhole principle**, if more keys are mapped into a finite number of slots than there are slots, at least two keys must share a slot.

**Important distinction:** A collision means two keys have the same hash table location. It does not mean the keys themselves are equal.

## 3.1 Collision resolution techniques

The main approaches are:

1. Separate chaining
    
2. Open addressing
    
    - Linear probing
        
    - Quadratic probing
        
    - Double hashing
        

These are central concepts for the exam.

# 4. Collision Resolution

Collision resolution determines how a hash table stores a new key when its calculated location is already occupied.

## 4.1 Separate chaining

In **separate chaining**, each hash table position stores a collection of entries, commonly a linked list or another bucket structure.

If several keys map to the same index, they are stored together in that bucket.

Suppose:

- Hash function: `h(k) = k % 7`
    
- Keys: 10, 17, 24
    

All three map to index 3.

```
Index 0: Empty
Index 1: Empty
Index 2: Empty
Index 3: 10 → 17 → 24
Index 4: Empty
Index 5: Empty
Index 6: Empty
```

### Python demonstration

```
table = [[] for _ in range(7)]

def insert(key):
    index = key % 7
    table[index].append(key)

for key in [10, 17, 24, 22]:
    insert(key)

print(table[3])
print(table[1])
```

Output:

```
[10, 17, 24]
[22]
```

### Advantages and disadvantages

- Multiple keys can share the same bucket.
    
- The table can store more elements than it has buckets.
    
- It is relatively simple to implement.
    
- Long chains can slow down searches.
    

With a good hash function and a controlled load factor, average search, insertion and deletion are typically O(1). If all keys land in one chain, operations can take O(n).

## 4.2 Open addressing

In **open addressing**, all entries are stored directly inside the hash table. When a collision occurs, the algorithm searches for another available slot according to a probing rule.

The main techniques are:

- Linear probing
    
- Quadratic probing
    
- Double hashing
    

Unlike separate chaining, these methods do not need an external linked list at each index.

### A. Linear probing

Linear probing checks the next table position, then the next one, until it finds an available slot.

Formula:

**hᵢ(k) = (h(k) + i) % m**

Where:

- `i = 0, 1, 2, ...`
    
- `m` = table size
    
- `h(k)` = original hash index
    

Example: Table size `m = 7`, hash function `h(k) = k % 7`.

Insert keys 10, 17 and 24.

|Key|Initial hash|Action|Final index|
|---|---|---|---|
|10|3|Index 3 is empty|3|
|17|3|Index 3 occupied; try 4|4|
|24|3|Indexes 3 and 4 occupied; try 5|5|

Final table:

```
Index:  0   1   2   3   4   5   6
Value:  -   -   -  10  17  24   -
```

**Exam trap:** All three keys have original hash index 3, but linear probing stores them at indexes 3, 4 and 5.

#### Primary clustering

Linear probing can create groups of consecutive occupied slots called **primary clusters**.

New keys that hash into or near a cluster may extend it, making future insertions and searches slower.

### B. Quadratic probing

Quadratic probing changes the jump size using a quadratic expression.

A common simplified formula is:

**hᵢ(k) = (h(k) + i²) % m**

It checks positions using increasing squared offsets rather than consecutive indexes.

Example: Initial index 3 and table size 7.

|Probe (i)|Calculation|Index|
|---|---|---|
|0|(3 + 0²) % 7|3|
|1|(3 + 1²) % 7|4|
|2|(3 + 2²) % 7|0|
|3|(3 + 3²) % 7|5|

The exact sequence depends on the chosen quadratic formula and table size.

**Exam trap:** Quadratic probing can reduce primary clustering, but it does not necessarily visit every table slot. Its effectiveness depends on the formula, table size and load factor.

### C. Double hashing

Double hashing uses a second hash function to determine the step size.

Formula:

**hᵢ(k) = (h₁(k) + i × h₂(k)) % m**

Where:

- `h₁(k)` determines the initial slot.
    
- `h₂(k)` determines the step size.
    

Example of possible hash functions:

- `h₁(k) = k % 7`
    
- `h₂(k) = 1 + (k % 5)`
    

The second hash value is used to jump through the table when a collision occurs.

A well-chosen step size helps probe different parts of the table. To guarantee visiting every slot, the step size should be nonzero and relatively prime to the table size.

### Comparison of open-addressing methods

|Method|How it finds another slot|Main issue|
|---|---|---|
|Linear probing|Checks consecutive slots|Primary clustering|
|Quadratic probing|Uses squared or other quadratic offsets|May not cover every slot|
|Double hashing|Uses a second hash function as the step size|Requires careful choice of both hash functions|

**Remember:** Separate chaining stores collided entries in buckets. Open addressing stores all entries inside the table and resolves collisions by probing.

# 5. Load Factor

The **load factor** measures how full a hash table is.

Formula:

**α = n / m**

Where:

- `n` = number of stored entries
    
- `m` = number of slots or buckets, depending on the table design
    

Example: A hash table has 7 slots and stores 5 entries.

`α = 5 / 7 ≈ 0.714`

### Why load factor matters

- **Separate chaining:** Load factor can exceed 1 because a bucket can hold multiple entries.
    
- **Open addressing:** The table must have an empty slot for a new insertion, so its load factor must remain below 1 for a successful insertion.
    
- **Rehashing:** When a table becomes too full, a larger table is created and entries are inserted again using the new table size and hash function.
    

**Exam trap:** Load factor is not the number of collisions. It measures table occupancy.

# 6. Deletion in Hashing

Deletion depends on the collision resolution method.

## 6.1 Separate chaining

An entry can be removed from its bucket without affecting the other buckets.

Before deleting 17:

```
Index 3: 10 → 17 → 24
```

After deletion:

```
Index 3: 10 → 24
```

## 6.2 Open addressing

Simply making a deleted slot empty can break searches for entries further along the probe sequence.

Implementations often mark the slot as deleted using a special marker called a **tombstone**.

Example with linear probing:

```
Index:  3    4    5
       10   17   24
```

If 17 is deleted, the search for 24 must still continue past index 4. A tombstone indicates that the slot previously held an entry and should not terminate a search.

**Exam trap:** In open addressing, deletion needs special handling to preserve the correctness of searches.

# 7. Hashing in Python

Python dictionaries and sets use hashing internally. Usually, you use them directly rather than implementing the entire hash table yourself.

## 7.1 Dictionary example

```
student_marks = {
    "Amit": 85,
    "Neha": 92,
    "Ravi": 78
}

print(student_marks["Neha"])
print("Amit" in student_marks)
```

Output:

```
92
True
```

Dictionaries use keys to find associated values efficiently on average.

## 7.2 The built-in `hash()` function

```
print(hash(100))
print(hash("Python"))
```

Important observations:

- `hash(100)` is `100` in standard Python integer hashing.
    
- The numeric result of `hash("Python")` may vary across processes because Python randomizes hashes for some types, including strings.
    

### Important facts

- Equal hashable objects must have equal hash values.
    
- Objects with the same hash are not necessarily equal.
    
- Lists and dictionaries cannot be used as dictionary keys because they are unhashable.
    
- A tuple can be a dictionary key if all its elements are hashable.
    
- `hash(key)` is not necessarily the final internal dictionary-table index.
    

**Exam trap:** Do not assume `hash("Python")` has one universal fixed value across separate Python executions.

# 8. Hashing Complexity Summary

|Operation|Average/expected case|Worst case|
|---|---|---|
|Search|O(1)|O(n)|
|Insertion|O(1)|O(n)|
|Deletion|O(1)|O(n)|

These are common hash-table complexity bounds, assuming a suitable implementation. Poor hash distribution or many collisions can cause worst-case linear behavior.

# 9. Final Revision Sheet

|Topic|Must remember|
|---|---|
|Hash function|Maps a key to a hash value or table location|
|Division method|`h(k) = k % m`|
|Collision|Different keys map to the same location|
|Separate chaining|Stores collided entries in the same bucket|
|Linear probing|Checks consecutive slots|
|Quadratic probing|Uses quadratic offsets|
|Double hashing|Uses a second hash function for step size|
|Load factor|`α = n / m`|
|Tombstone|Marks a deleted slot in open addressing|
|Expected operation time|O(1) with suitable distribution and load|
|Worst-case operation time|O(n)|
|Python `dict` and `set`|Use hashing internally|

## Highest-priority exam concepts

1. Calculate hash indexes using modulo.
    
2. Distinguish separate chaining from open addressing.
    
3. Trace linear probing step by step.
    
4. Compare quadratic probing with double hashing.
    
5. Calculate load factor.
    
6. Understand why tombstones are needed during deletion.
    
7. Memorize average and worst-case time complexities.