## 1. What is hashing?

Suppose you want to store students' records using their roll numbers. Instead of searching through every record, a hash function calculates a location where each record should be stored.

### How hashing works

## Key = 25

Hash function

h(key) = key mod 7

## Index = 4

25 % 7 = 4

A hash table uses this calculated index to locate a storage position. This can make insertion, searching, and deletion very efficient.

Example: If \(h(k)=k\bmod 7\), then key `25` maps to index `4`.

## 2. Hash function

A hash function maps a key to a hash value or table index.

For a table of size \(m\), a simple hash function for non-negative integer keys is:

\[ h(k)=k\bmod m \]

Here:

- \(k\) = key
    
- \(m\) = table size
    
- \(h(k)\) = calculated index, from \(0\) to \(m-1\)
    

### Example: Division method

Suppose the table size is \(7\).

|Key \(k\)|Calculation|Index|
|---|---|---|
|10|\(10\bmod7\)|3|
|22|\(22\bmod7\)|1|
|25|\(25\bmod7\)|4|
|31|\(31\bmod7\)|3|
|44|\(44\bmod7\)|2|

Notice that both `10` and `31` map to index `3`. This produces a collision, which we will study next.

### Common hash function methods

|Method|Basic idea|Example|
|---|---|---|
|Division method|Use remainder after division by table size|\(h(k)=k\bmod m\)|
|Multiplication method|Multiply the key by a constant and use the fractional part to calculate an index|\(h(k)=\lfloor m\cdot \operatorname{frac}(kA)\rfloor\)|
|Mid-square method|Square the key and extract selected middle digits|Square a key, then take middle digits|
|Folding method|Divide the key into parts and combine those parts|Add groups of digits|

For typical introductory exam questions, the division method is especially important because it is straightforward to calculate.

### Properties of a good hash function

A good hash function should:

- Be deterministic for the same key under the same hashing context.
    
- Distribute keys reasonably uniformly across the table.
    
- Be efficient to calculate.
    
- Reduce clustering and collisions where possible.
    

Exam trap: A hash function does not guarantee that every key maps to a unique index. Collisions are possible and require a resolution method.

## 3. Collision

A collision occurs when two different keys produce the same hash table index.

For example, if

\[ h(k)=k\bmod7 \]

then:

\[ h(10)=10\bmod7=3 \]

\[ h(17)=17\bmod7=3 \]

Both keys want index `3`, so a collision occurs.

### Collision example

### —

0

### —

1

### —

2

### 10

3

### —

4

### —

5

### —

6

Key 10 occupies index 3. Key 17 also hashes to index 3, which is already occupied.

### Why do collisions occur?

The number of possible keys is usually much larger than the number of available table slots. Multiple keys therefore can map to the same index.

According to the pigeonhole principle, if more keys are mapped into a finite number of slots than there are slots, at least two keys must share a slot.

Important distinction: A collision means the keys have the same hash table location. It does not mean the keys themselves are equal.

### What happens during a collision?

The hash table needs a collision resolution technique. The main approaches are:

1. Separate chaining
    
2. Open addressing
    
    - Linear probing
        
    - Quadratic probing
        
    - Double hashing
        
    

These are central concepts to remember for the exam.

# 4. Collision resolution

Collision resolution determines how a hash table stores a new key when its calculated location is already occupied.

## 4.1 Separate chaining

In separate chaining, each hash table position stores a collection of entries, commonly a linked list or another bucket structure.

If several keys map to the same index, they are stored together in that bucket.

Suppose the hash function is \(h(k)=k\bmod7\) and the keys are `10`, `17`, and `24`.

All three map to index `3`.

### Separate chaining

### 0

→ Empty

### 1

→ Empty

### 2

→ Empty

### 3

### 10

### 17

### 24

### 4–6

→ Empty

All three entries can be stored in the bucket at index `3`.

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
    
- It is simple to implement.
    
- Long chains can slow down searches.
    

With a good hash function and a controlled load factor, average search, insertion, and deletion are typically \(O(1)\). In the worst case, if all keys land in one chain, operations can take \(O(n)\).

## 4.2 Open addressing

In open addressing, all entries are stored directly inside the hash table itself. When a collision occurs, the algorithm searches for another available slot according to a probing rule.

The major techniques are:

- Linear probing
    
- Quadratic probing
    
- Double hashing
    

Unlike separate chaining, these techniques do not need an external linked list at each table index.

### A. Linear probing

Linear probing checks the next table position, then the next one, until it finds an available slot.

The probing formula is:

\[ h_i(k)=(h(k)+i)\bmod m \]

where \(i=0,1,2,\ldots\).

Example: table size \(m=7\), hash function \(h(k)=k\bmod7\).

Insert keys `10`, `17`, and `24`.

|Key|Initial hash|Action|Final index|
|---|---|---|---|
|10|3|Index 3 is empty|3|
|17|3|Index 3 occupied; try 4|4|
|24|3|Indexes 3 and 4 occupied; try 5|5|

Final table:

### —

0

### —

1

### —

2

### 10

3

### 17

4

### 24

5

### —

6

Exam trap: In linear probing, keys `10`, `17`, and `24` all have original hash index `3`, but they are stored at indexes `3`, `4`, and `5`.

#### Primary clustering

Linear probing can create groups of consecutive occupied slots called primary clusters. New keys that hash into or near a cluster may extend it.

This can make future insertions and searches slower.

### B. Quadratic probing

Quadratic probing changes the jump size using a quadratic expression.

A common simplified formula is:

\[ h_i(k)=(h(k)+i^2)\bmod m \]

It checks positions using increasing squared offsets rather than consecutive indexes.

For example, with initial index `3` and table size `7`:

|Probe \(i\)|Calculation|Index|
|---|---|---|
|0|\((3+0^2)\bmod7\)|3|
|1|\((3+1^2)\bmod7\)|4|
|2|\((3+2^2)\bmod7\)|0|
|3|\((3+3^2)\bmod7\)|5|

The exact sequence depends on the chosen quadratic formula and table size.

Exam trap: Quadratic probing can reduce primary clustering, but it does not necessarily visit every table slot. Its effectiveness depends on the formula, table size, and load factor.

### C. Double hashing

Double hashing uses a second hash function to determine the step size.

A common formula is:

\[ h_i(k)=(h_1(k)+i\cdot h_2(k))\bmod m \]

Here:

- \(h_1(k)\) determines the initial slot.
    
- \(h_2(k)\) determines the step size.
    

For instance, one possible choice is:

\[ h_1(k)=k\bmod7 \]

\[ h_2(k)=1+(k\bmod5) \]

The second hash value is used to jump through the table when a collision occurs.

A well-chosen step size helps probe different parts of the table. The step size should be nonzero and relatively prime to the table size if the method is to be guaranteed to visit every slot.

### Compare the three open-addressing methods

|Method|How it finds another slot|Main issue|
|---|---|---|
|Linear probing|Checks consecutive slots|Primary clustering|
|Quadratic probing|Uses squared or other quadratic offsets|May not cover every slot|
|Double hashing|Uses a second hash function as the step size|Requires careful choice of both hash functions|

Remember: Separate chaining stores collided entries in buckets. Open addressing stores all entries inside the table and resolves collisions by probing.

# 5. Load factor

The load factor measures how full a hash table is.

\[ \alpha=\frac{n}{m} \]

Where:

- \(n\) = number of stored entries.
    
- \(m\) = number of slots or buckets, depending on the table design.
    

Example: If a hash table has 7 slots and stores 5 entries:

\[ \alpha=\frac{5}{7}\approx0.714 \]

A higher load factor usually increases collision likelihood and can make operations slower in open-addressed tables.

### Why load factor matters

- Separate chaining: Load factor can exceed 1 because a bucket can hold multiple entries.
    
- Open addressing: The table must have an empty slot for a new insertion, so its load factor must remain below 1 for a successful insertion.
    
- Rehashing: When a table becomes too full, a larger table is created and entries are inserted again using the new table size and hash function.
    

Exam trap: Load factor is not the same as the number of collisions. It is a measure of table occupancy.

# 6. Deletion in hashing

Deletion depends on the collision resolution method.

### Separate chaining

An entry can be removed from its bucket without affecting the other buckets. For example, deleting `17` from the chain

```
Index 3: 10 → 17 → 24
```

leaves:

```
Index 3: 10 → 24
```

### Open addressing

Simply making a deleted slot empty can break searches for entries further along the probe sequence. Instead, implementations often mark the slot as deleted using a special marker called a tombstone.

For example, with linear probing:

```
Index:  3    4    5
        10   17   24
```

If `17` is deleted, the search for `24` must still continue past index `4`. A tombstone marks that the slot previously held an entry and should not terminate a search.

Exam trap: In open addressing, deletion needs special handling to preserve the correctness of searches.

# 7. Hashing in Python

Python dictionaries and sets use hashing internally. You typically use them directly rather than implementing the whole hash table yourself.

### Dictionary example

```
student_marks = {    "Amit": 85,    "Neha": 92,    "Ravi": 78}print(student_marks["Neha"])print("Amit" in student_marks)
```

Output:

```
92
True
```

Dictionaries use keys to find associated values efficiently on average.

### The built-in `hash()` function

```
print(hash(100))print(hash("Python"))
```

`hash(100)` is `100` in standard Python integer hashing. The numeric result of `hash("Python")` may vary across processes because Python randomizes hashes for some types, including strings.

Important facts:

- Equal hashable objects must have equal hash values.
    
- Objects with the same hash are not necessarily equal.
    
- Lists and dictionaries cannot be used as dictionary keys because they are unhashable.
    
- A tuple can be a dictionary key if all its elements are hashable.
    
- `hash(key)` is not necessarily the final internal dictionary-table index.
    

Exam trap: Do not assume `hash("Python")` has one universal fixed value across separate Python executions.

# 8. Hashing complexity summary

|Operation|Average/expected case|Worst case|
|---|---|---|
|Search|\(O(1)\)|\(O(n)\)|
|Insertion|\(O(1)\)|\(O(n)\)|
|Deletion|\(O(1)\)|\(O(n)\)|

These are common hash-table complexity bounds, assuming a suitable implementation. Poor hash distribution or many collisions can cause worst-case linear behavior.

## Final revision sheet

|Topic|Must remember|
|---|---|
|Hash function|Maps a key to a hash value or table location|
|Division method|\(h(k)=k\bmod m\)|
|Collision|Different keys map to the same location|
|Separate chaining|Stores collided entries in the same bucket|
|Linear probing|Checks consecutive slots|
|Quadratic probing|Uses quadratic offsets|
|Double hashing|Uses a second hash function for step size|
|Load factor|\(\alpha=n/m\)|
|Tombstone|Marks a deleted slot in open addressing|
|Expected operation time|\(O(1)\) with suitable distribution and load|
|Worst-case operation time|\(O(n)\)|
|Python `dict` and `set`|Use hashing internally|

Highest-priority exam concepts: Calculate hash indexes using modulo, distinguish separate chaining from open addressing, trace linear probing, compare quadratic probing with double hashing, and calculate load factor.