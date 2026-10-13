Memory is the part of a computer system that stores data, instructions, and results. For the exam, focus on the differences between RAM and ROM, cache memory, primary and secondary memory, and the order of the memory hierarchy.

## 1. RAM — Random Access Memory

RAM is the computer’s main working memory. It temporarily stores programs and data that the CPU is currently using.

- Volatile: data is lost when power is switched off.
    
- Read/write memory.
    
- Faster than secondary storage.
    
- The CPU can access locations in RAM directly through the memory system.
    

![Memory (RAM) Kingston #2](https://images.openai.com/static-rsc-4/cy9c6C2E6h-40vOxpZFSW8Ym0xBRArEnFdAYYpZmmZHPKGEUlqtVvx6AccF0eMhyPcL52d-YFXub-n8bYeSUsjVLEdx2YmKtS9M9Yg5-R-BEoDo1zzvRvfzV3fTbND3N2Rw5nmPInPmVJnBCNLrDwUW9zL2FBwiXuYJBgyzLt-0?purpose=inline)

### Types of RAM

SRAM — Static RAM

- Stores bits using flip-flop circuits.
    
- Does not need periodic refreshing while powered.
    
- Faster and more expensive.
    
- Commonly used for CPU cache.
    

Faster

DRAM — Dynamic RAM

- Stores bits using capacitors.
    
- Requires periodic refreshing.
    
- Generally slower and cheaper than SRAM.
    
- Commonly used as main memory.
    

Cheaper

Exam trick: SRAM is generally used for cache; DRAM is generally used for main memory.

## 2. ROM — Read-Only Memory

ROM stores instructions or firmware needed for specific device operations, such as starting up a computer.

- Non-volatile: retains data without power.
    
- Retains its contents when the system shuts down.
    
- Traditionally read-only, although modern ROM-family technologies can be reprogrammed.
    

![Cómo arreglar un PC que entra en la BIOS cada vez que enciende](https://images.openai.com/static-rsc-4/Gp5nRrXn7SH-zgP5jgUCjqx18vp90cZmMz5BYnM_ax0MkVrfp7WHxYUOQgixD6qdM3ebCb4_s40Cb2iqAnrkvi_IRpx4_7ZxFiMKcmze7m7ogqtFeMY36CagFD6aItcPXWwvxgicWqbkkus3xiHxL7NJxeG_iHw44JfECtxwtpc?purpose=inline)

### Types of ROM

|Type|Full form / key feature|
|---|---|
|MROM|Mask ROM — programmed during manufacturing|
|PROM|Programmable ROM — normally programmed once|
|EPROM|Erasable Programmable ROM — erased using ultraviolet light|
|EEPROM|Electrically Erasable Programmable ROM|
|Flash memory|A type of electrically erasable non-volatile memory, typically erased in blocks|

Important MCQ facts

- UV light → EPROM
    
- Electrical erasure → EEPROM
    
- USB pen drives and SSDs use flash memory.
    
- Firmware is stored in non-volatile memory, commonly flash memory in modern systems.
    

## 3. RAM vs ROM

|Feature|RAM|ROM|
|---|---|---|
|Volatility|Volatile|Non-volatile|
|Typical purpose|Working data and programs|Firmware and persistent instructions|
|Normal operation|Read and write|Primarily read|
|Power off|Data is lost|Data is retained|
|Common technology|DRAM, SRAM|Flash, EEPROM and other ROM-family technologies|

Remember: RAM and ROM are not distinguished simply by speed. Their most important distinction is volatility and typical use.

## 4. Cache Memory

Cache memory is a small, high-speed memory that stores frequently or recently used instructions and data so the CPU can access them faster.

- Usually built using SRAM.
    
- Faster than main RAM.
    
- Smaller and more expensive per bit than RAM.
    
- Reduces average memory access time.
    

![CPU level cache — L1, L2, L3, RAM(in-memory) | by Umesh Kumar Yadav | Medium](https://images.openai.com/static-rsc-4/VjSSBO4LLx_iYItApFsGHA2NBG20Q-PGmv1Aaft_sLCw9cojSUh2GT41UcCsJbZgFmAYjEwGOj8It4ie14o02MyfSH2Djv49O0xKJS5CdgypOpc7Ui8Gh909sH3Z_zC2_T48pb8f4eZgGsjqwDIHi0n4ghvSshaB1PoUKfuXQLs?purpose=inline)

### Levels of cache

|Cache|General characteristics|
|---|---|
|L1|Smallest and usually fastest; often private to a CPU core|
|L2|Usually larger and slower than L1|
|L3|Usually larger and slower than L2; often shared across CPU cores|

Actual sizes and sharing arrangements depend on the processor.

### Cache hit and cache miss

- Cache hit: requested data is found in cache.
    
- Cache miss: requested data is not found in cache, so the system fetches it from a lower level of the memory hierarchy.
    
- Hit ratio: proportion of memory accesses that result in cache hits.
    

\[ \text{Hit Ratio}=\frac{\text{Cache Hits}}{\text{Total Memory Accesses}} \]

Example: If there are 80 cache hits out of 100 accesses, the hit ratio is 80%.

### Locality of reference

Cache works effectively because programs often exhibit locality:

- Temporal locality: recently accessed data is likely to be accessed again.
    
- Spatial locality: data near a recently accessed memory location is likely to be accessed soon.
    
- Sequential locality: instructions or data are often accessed in sequence; this is closely related to spatial locality.
    

For example, repeatedly accessing the same loop variable demonstrates temporal locality, while reading consecutive array elements demonstrates spatial locality.

## 5. Primary Memory vs Secondary Memory

### Primary memory

Primary memory is the memory used directly by the CPU's memory system during processing.

Examples:

- RAM
    
- ROM
    
- Cache memory is commonly included in broad primary-memory classifications, though textbooks may classify it separately.
    

### Secondary memory

Secondary memory provides long-term storage for programs, files, and other data.

![Solid state drive (SSD)](https://images.openai.com/static-rsc-4/7j9ggsGx-JpP8SJmYLeYaqiMM0nPhcT1UDOEB4hXHB8myiSr6iFqn5Ix2QTSjCNLlcmcQmKV3D4yhGWSY6m9-5JdiayagqaRrSzAftFru6wmOXFzkiQP4a43qLTsNiPFAVrn3lZqowE6_vkydUEjbS4p_JnwewCBtBa-utpmu8E9kdT_ffPAdKoryBUEocsl?purpose=inline)

SSD

Flash-based, non-volatile storage; no moving parts.

![Computer Hard Disk Drive PNG Image -  PurePNG | Free transparent CC0 PNG Image Library](https://images.openai.com/static-rsc-4/1xlocxRG1rEEapjiCRv5w_GOzkbvKf-HKtwTtpTZtTYxJUP6cdZxZdmqXFGa68bdZmfz0YZ8OPYQ3ALto0rHdI9RN604SQXNMRQyGPfsJLWde6pRAWytEwfGJm2GAPHc2GzdDBdOho46saS5bKqFPoGJ7GlI_0L1zWUdVtDlLJo?purpose=inline)

HDD

Magnetic storage using rotating platters.

![USB 3.0 Flash Drive without cap isolated on white background](https://images.openai.com/static-rsc-4/rGchvRqBhKy_puJJsSKU3oS6ohRt3Xk6a_wpg9TVCSkxHzvYoK57SAzThuy2a4CBT1pCU1Oj6ewVc9ZtU4J4TfbG0etsynGERzqBNwpl37UUUte8fsgA3u_Qygy8EGIV4HcFXJSiK-omMV55rQup__uDu73Fv1ftZMl3cxy5dFTElrxD7qfm_4h0N11cdCOu?purpose=inline)

Pen drive

Portable flash-based storage.

![DVD on white background - High resolution.](https://images.openai.com/static-rsc-4/RdPTb5Dv9DdxPu90lgJU9Zhz0YeKsHCEEsXaorR41ghPq9mbWcftn-k-x2i5RCeCqzONZpygHf2cA1Atrhu5PylUIeJXjwPIkh1ajFcVTs7_IgCvC6_7MrkzeUQZzIQuZRwFavlp87eqbnXvcHQRXsp2UFTH1mmNKatwNBcb7lh7wYOSkicjeuqDCZ07dGUj?purpose=inline)

Optical disc

Uses laser technology to read or write data.

|Feature|Primary memory|Secondary memory|
|---|---|---|
|Main purpose|Active processing and immediate access|Long-term data storage|
|Speed|Generally faster|Generally slower|
|Capacity|Usually smaller|Usually larger|
|Cost per bit|Generally higher|Generally lower|
|Volatility|Depends on type: RAM is volatile, ROM is not|Usually non-volatile|
|Examples|RAM, ROM, cache (broad classification)|SSD, HDD, pen drive, DVD|

Important: Do not assume all primary memory is volatile—ROM is non-volatile. Also, an SSD is generally slower than RAM but faster than an HDD for many workloads.

## 6. Memory Hierarchy

Memory hierarchy arranges storage levels according to factors such as speed, capacity, cost per bit, and proximity to the CPU.

CPUNext 6

A₀A₁A₂A₃A₄A₅

Fast · costly / bit ↑Capacity · latency ↓

Registers

L1 cache

L2 cache

L3 cache

Main memory

Storage (SSD/HDD)

Spatial: nearby values copied up · 4 L1 hits

1 cache miss before L2 cache supplies the value

Found at

RegistersL1L2L3DRAMStorage

Pattern

RepeatedNearbyScattered

Give feedback

The typical order from fastest to slowest is:

CPU Registers

Fastest • Very small

L1 Cache

L2 Cache

L3 Cache

Main Memory (RAM)

Secondary Storage (SSD/HDD)

Largest capacity in the typical hierarchy • Persistent

Moving downward generally means greater capacity, lower cost per bit, and higher access latency.

|Property|Toward registers/cache|Toward secondary storage|
|---|---|---|
|Access speed|Increases|Decreases|
|Access latency|Decreases|Increases|
|Capacity|Decreases|Increases|
|Cost per bit|Increases|Decreases|
|Persistence|Mostly volatile working storage|Usually non-volatile storage|

Why do we need a hierarchy? Very fast memory is expensive and limited in capacity. The hierarchy balances performance, capacity, and cost by keeping frequently needed data closer to the CPU.

### Virtual memory — an extra exam point

Virtual memory allows the operating system to use secondary storage to extend the apparent address space available to programs. When required pages are not in RAM, a page fault can cause the OS to load them from storage.

- Virtual memory is not the same as cache.
    
- RAM is physical main memory.
    
- SSD/HDD can back virtual memory, but they are much slower than RAM.
    

## 7. Quick revision for DSSSB

|Concept|One-line fact to remember|
|---|---|
|RAM|Volatile working memory|
|ROM|Non-volatile memory traditionally used for firmware|
|SRAM|Fast; commonly used in cache|
|DRAM|Requires refreshing; commonly used in main memory|
|EPROM|Erased using ultraviolet light|
|EEPROM|Electrically erasable|
|Cache hit|Data is found in cache|
|Cache miss|Data is not found in cache|
|Temporal locality|Recently used data may be reused|
|Spatial locality|Nearby data may be used soon|
|SSD|Non-volatile flash-based storage|
|HDD|Magnetic storage with moving parts|
|Registers|Small, fastest CPU storage|
|Memory hierarchy|Balances speed, capacity, and cost|