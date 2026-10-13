# Memory Calculations — DSSSB TGT Computer Science

This topic is important for numerical MCQs. Focus on four areas: addressing, memory size, word size, and cache calculations.

## 1. Addressing and Addressable Memory

An address identifies a location in memory. The number of bits available for an address determines how many distinct locations can be represented.

### Key Formula

Number of addresses = 2ⁿ

Here, n = number of address bits.

### Examples

|Address bits|Number of addresses|
|---|---|
|8|2⁸ = 256|
|10|2¹⁰ = 1,024|
|16|2¹⁶ = 65,536|
|20|2²⁰ = 1,048,576|
|32|2³² = 4,294,967,296|
|64|2⁶⁴|

Important: The number of addresses is not always the same as memory capacity in bytes. It depends on what each address identifies.

### Byte-addressable vs Word-addressable Memory

- Byte-addressable: Each address identifies one byte.
    
- Word-addressable: Each address identifies one word.
    

For byte-addressable memory:

Memory capacity in bytes = 2ⁿ

For word-addressable memory, if each word contains w bytes:

Memory capacity in bytes = 2ⁿ × w

### Example 1: Byte-addressable Memory

A computer has a 12-bit address bus and byte-addressable memory. Find the maximum addressable capacity.

Step 1: Number of addresses = 2¹² = 4,096.

Step 2: Each address identifies one byte.

Memory capacity = 4,096 bytes = 4 KiB.

Answer: 4 KiB.

### Example 2: Word-addressable Memory

A system has 10-bit addresses, with each word containing 4 bytes.

Number of addresses = 2¹⁰ = 1,024.

Memory capacity = 1,024 × 4 = 4,096 bytes = 4 KiB.

Answer: 4 KiB.

## 2. Memory Size Calculations

Memorize these basic units.

|Unit|Equivalent|
|---|---|
|1 bit|One binary digit|
|1 byte (B)|8 bits|
|1 KiB|2¹⁰ = 1,024 bytes|
|1 MiB|2²⁰ = 1,048,576 bytes|
|1 GiB|2³⁰ bytes|
|1 TiB|2⁴⁰ bytes|

Note: KiB, MiB, and GiB use powers of 1,024. KB, MB, and GB normally use powers of 1,000 in precise terminology.

### Example 3: Convert Bits to Bytes

How many bytes are present in 32,768 bits?

Bytes = 32,768 ÷ 8 = 4,096 bytes.

4,096 bytes = 4 KiB.

Answer: 4 KiB.

### Example 4: Find the Number of Address Lines

A byte-addressable memory has a capacity of 64 KiB. How many address bits are required?

Step 1: Convert memory into bytes.

64 KiB = 64 × 1,024 = 65,536 bytes.

Step 2: Find n such that 2ⁿ = 65,536.

65,536 = 2¹⁶.

Answer: 16 address bits.

### Example 5: Find Memory Capacity from Address Lines

A byte-addressable system has 20 address lines.

Number of addresses = 2²⁰ = 1,048,576.

Memory capacity = 1,048,576 bytes = 1 MiB.

Answer: 1 MiB.

## 3. Word Size

A word is the natural unit of data that a processor is designed to handle efficiently. Its exact definition depends on the architecture.

Common word sizes include 8, 16, 32, and 64 bits.

|Word size|Equivalent in bytes|
|---|---|
|8 bits|1 byte|
|16 bits|2 bytes|
|32 bits|4 bytes|
|64 bits|8 bytes|

### Important Formulas

Bytes per word = Word size in bits ÷ 8

Number of words = Total memory in bytes ÷ Bytes per word

### Example 6: Number of Words

A memory contains 8 KiB, and each word is 16 bits. How many words can it store?

Step 1: Convert memory into bytes.

8 KiB = 8 × 1,024 = 8,192 bytes.

Step 2: Convert word size into bytes.

16 ÷ 8 = 2 bytes per word.

Step 3: Calculate the number of words.

Number of words = 8,192 ÷ 2 = 4,096.

Answer: 4,096 words.

### Example 7: Word-addressable Capacity

A memory has 2¹² words, with 32 bits per word.

Number of words = 2¹² = 4,096.

Bytes per word = 32 ÷ 8 = 4 bytes.

Memory capacity = 4,096 × 4 = 16,384 bytes = 16 KiB.

Answer: 16 KiB.

### Address Bus vs Data Bus vs Word Size

|Term|Meaning|
|---|---|
|Address bus width|Number of address bits; determines the number of representable addresses|
|Data bus width|Number of data bits transferable per full-width bus operation|
|Word size|Natural data size for the processor's architecture|

These quantities can be related, but they are not necessarily equal.

## 4. Cache Memory Calculations

Cache is a small, fast memory that keeps copies of data from lower levels of the memory hierarchy. Numerical questions commonly involve cache size, cache lines, hit ratio, miss ratio, and average memory access time.

### A. Number of Cache Lines

A cache is divided into blocks called cache lines. Each line stores a block of data along with metadata such as a tag and status bits.

Number of cache lines = Cache data capacity ÷ Block size

Example: A 16 KiB cache has a block size of 64 bytes.

16 KiB = 16 × 1,024 = 16,384 bytes.

Number of cache lines = 16,384 ÷ 64 = 256.

Answer: 256 cache lines.

This assumes 16 KiB refers to data capacity, excluding metadata.

### B. Hit Ratio and Miss Ratio

- Cache hit: Requested data is found in the cache.
    
- Cache miss: Requested data is not found in the cache.
    
- Hit ratio: Fraction of accesses that are hits.
    
- Miss ratio: Fraction of accesses that are misses.
    

Hit ratio = Number of hits ÷ Total accesses

Miss ratio = 1 − Hit ratio

Example: Out of 1,000 memory accesses, 900 are cache hits.

Hit ratio = 900 ÷ 1,000 = 0.9 = 90%.

Miss ratio = 100% − 90% = 10%.

Answer: Hit ratio = 90%; miss ratio = 10%.

### C. Average Memory Access Time (AMAT)

A common simplified formula is:

AMAT = Hit time + (Miss rate × Miss penalty)

Definitions:

- Hit time: Time needed to check and access the cache on a hit.
    
- Miss rate: Fraction of accesses that miss.
    
- Miss penalty: Additional time required to service a miss, under this formula's convention.
    

Example:

- Hit time = 2 ns
    
- Miss rate = 5% = 0.05
    
- Miss penalty = 40 ns
    

AMAT = 2 + (0.05 × 40)

AMAT = 2 + 2 = 4 ns.

Answer: 4 ns.

Exam tip: Convert percentages into decimals before using the formula. Also check whether the question defines miss penalty as additional time or total miss access time.

### D. Cache Address Fields — Direct Mapping

In a byte-addressed system, a memory address can be divided into three fields:

- Tag: Identifies which memory block is stored.
    
- Index: Selects the cache line or set.
    
- Block offset: Selects a byte within the cache block.
    

For a cache with 2ⁱ lines and a block size of 2ᵇ bytes:

Index bits = i

Block offset bits = b

For an m-bit address in a direct-mapped cache:

Tag bits = m − i − b

### Example 8: Calculate Tag, Index, and Offset Bits

Given:

- Address size = 16 bits
    
- Number of cache lines = 64
    
- Block size = 16 bytes
    

Step 1: Find index bits.

64 = 2⁶.

Index bits = 6.

Step 2: Find block offset bits.

16 bytes = 2⁴ bytes.

Offset bits = 4.

Step 3: Find tag bits.

Tag bits = 16 − 6 − 4 = 6.

Answer:

- Tag = 6 bits
    
- Index = 6 bits
    
- Offset = 4 bits
    
- Total = 16 bits
    

For set-associative caches, the index selects a set rather than an individual line. Fully associative caches have no index field.

## 5. Quick Formula Revision

|Calculation|Formula|
|---|---|
|Number of addresses|2ⁿ|
|Byte-addressable capacity|2ⁿ bytes|
|Word-addressable capacity|2ⁿ × bytes per word|
|Bytes per word|Word bits ÷ 8|
|Number of words|Memory bytes ÷ bytes per word|
|Cache lines|Cache data bytes ÷ block bytes|
|Hit ratio|Hits ÷ total accesses|
|Miss ratio|1 − hit ratio|
|Average access time|Hit time + (miss rate × miss penalty)|
|Direct-mapped tag bits|Address bits − index bits − offset bits|

Most important exam technique: Before calculating, identify whether the question gives bits, bytes, words, addresses, or cache blocks. Many calculation mistakes happen because these quantities are confused.