# MEMORY UNITS — DSSSB TGT COMPUTER SCIENCE

Memory units measure the amount of data a computer can store or process.

**Important exam areas:**

- Bit and byte
    
- KB, MB, GB, TB, and PB
    
- Decimal versus binary units
    
- Memory unit conversion
    
- Solved numerical questions
    
- Common exam traps involving bits and bytes
    

## 1. Bit

A **bit** (binary digit) is the smallest unit of digital information. It can have one of two values: `0` or `1`.

Examples:

- `0` = one bit
    
- `1` = one bit
    
- `1011` = four bits
    

**Symbol:** Lowercase `b`

## 2. Byte

A **byte (B)** consists of 8 bits.

[  
1\text{ Byte}=8\text{ bits}  
]

A byte is commonly used as a basic unit for measuring file sizes and memory capacity.

Important distinction:

- `b` = bit
    
- `B` = byte
    
- `1 B = 8 b`
    

Example:

[  
16\text{ bits}\div8=2\text{ bytes}  
]

## 3. KB, MB, GB, TB, and PB

There are two common measurement conventions: decimal units and binary units. This distinction is important for computer-fundamentals MCQs.

### A. Decimal units (SI convention)

Each unit is 1,000 times the preceding unit.

|Unit|Full name|Bytes|
|---|---|---|
|KB|Kilobyte|1,000 bytes|
|MB|Megabyte|1,000,000 bytes|
|GB|Gigabyte|1,000,000,000 bytes|
|TB|Terabyte|1,000,000,000,000 bytes|
|PB|Petabyte|1,000,000,000,000,000 bytes|

### B. Binary units (IEC convention)

Each unit is 1,024 times the preceding unit.

|Unit|Full name|Conversion|
|---|---|---|
|KiB|Kibibyte|1,024 bytes|
|MiB|Mebibyte|1,024 KiB|
|GiB|Gibibyte|1,024 MiB|
|TiB|Tebibyte|1,024 GiB|
|PiB|Pebibyte|1,024 TiB|

**Exam note:** Many traditional computer-fundamentals questions use KB = 1,024 bytes, MB = 1,024 KB, and so on. Modern standards distinguish these binary units as KiB, MiB, GiB, TiB, and PiB.

Follow the convention specified in the question.

## 4. Memory Unit Conversion Ladder

The commonly used sequence is:

**Byte → KB → MB → GB → TB → PB**

Under the traditional binary convention:

[  
1\text{ KB}=1024\text{ bytes}  
]

[  
1\text{ MB}=1024\text{ KB}  
]

[  
1\text{ GB}=1024\text{ MB}  
]

[  
1\text{ TB}=1024\text{ GB}  
]

[  
1\text{ PB}=1024\text{ TB}  
]

### How to convert

- **Larger unit to smaller unit:** Multiply.
    
- **Smaller unit to larger unit:** Divide.
    

Under the decimal convention, use 1,000 per step instead of 1,024.

## 5. Solved Numerical Questions

The following examples use the traditional binary convention of 1 KB = 1,024 bytes.

### Example 1: Convert 4 KB into bytes

[  
4\times1024=4096\text{ bytes}  
]

**Answer: 4,096 bytes**

### Example 2: Convert 3 MB into KB

[  
3\times1024=3072\text{ KB}  
]

**Answer: 3,072 KB**

### Example 3: Convert 2 GB into MB

[  
2\times1024=2048\text{ MB}  
]

**Answer: 2,048 MB**

### Example 4: Convert 8,192 bytes into KB

[  
8192\div1024=8\text{ KB}  
]

**Answer: 8 KB**

### Example 5: Convert 2 TB into GB

[  
2\times1024=2048\text{ GB}  
]

**Answer: 2,048 GB**

### Example 6: Convert 3 PB into TB

[  
3\times1024=3072\text{ TB}  
]

**Answer: 3,072 TB**

### Example 7: Convert 64 bits into bytes

Since 8 bits = 1 byte:

[  
64\div8=8\text{ bytes}  
]

**Answer: 8 bytes**

## 6. Quick Revision Table

|Unit|Binary conversion|
|---|---|
|1 Byte|8 bits|
|1 KiB|1,024 bytes|
|1 MiB|1,024 KiB|
|1 GiB|1,024 MiB|
|1 TiB|1,024 GiB|
|1 PiB|1,024 TiB|

### Memory trick

Remember the sequence:

**Byte → KB → MB → GB → TB → PB**

Each step upward is larger by a factor of 1,024 under the traditional binary convention.

## 7. Important Exam Traps

1. A bit is the smallest unit of digital information.
    
2. A byte contains 8 bits.
    
3. `b` means bit, whereas `B` means byte.
    
4. Under the traditional binary convention, 1 KB = 1,024 bytes.
    
5. Under the decimal convention, 1 KB = 1,000 bytes.
    
6. KiB, MiB, GiB, TiB, and PiB are binary units.
    
7. To convert a larger unit into a smaller unit, multiply.
    
8. To convert a smaller unit into a larger unit, divide.
    
9. Always check whether a question specifies decimal or binary conversion.
    
10. Do not confuse bits per second (`b/s`) with bytes per second (`B/s`).