# Operating Systems: Page Replacement Algorithms

## 1. What Is Page Replacement?

When a process references a virtual-memory page that is not currently in RAM, a page fault occurs. If the reference is valid but no free frame is available, the OS may need to select a resident page to evict.

This selection is called **page replacement**.

The page that is removed is the **victim page**.

### Example

Suppose RAM has three frames:

|Frame|Page|
|---|---|
|F1|2|
|F2|5|
|F3|7|

The process requests page 4. If page 4 is not resident and all frames are occupied, a replacement algorithm chooses one of pages 2, 5 or 7 to remove and loads page 4.

The result depends on the replacement policy.

## 2. Important Terms

|Term|Meaning|
|---|---|
|Page|Fixed-size block of virtual memory|
|Frame|Fixed-size block of physical memory|
|Reference string|Sequence of page numbers requested by a process|
|Page hit|Requested page is already resident in a frame|
|Page fault|Requested page is not resident and requires handling|
|Victim page|Resident page selected for replacement|
|Page-fault count|Number of page faults for a given reference string and starting condition|

For the examples below, assume all frames are initially empty. A hit means the page is already loaded; a fault means the requested page must be loaded.

---

## 3. FIFO — First In, First Out

FIFO replaces the page that has been in memory the longest since it was loaded.

It follows a queue-like rule: the page loaded earliest is the first candidate for replacement, regardless of how recently it was used.

### How FIFO Works

1. If the requested page is already in a frame, it is a hit.
    
2. If a free frame exists, load the page into it.
    
3. Otherwise, remove the page that entered memory earliest.
    
4. Load the new page in its place.
    

**Important:** FIFO does not choose the page that was least recently accessed. It chooses the page that has been resident the longest.

### Example

Reference string: `1, 2, 3, 1, 4, 2`

Number of page frames: 3

Initially, all frames are empty.

|Step|Requested page|Frame 1|Frame 2|Frame 3|Result|
|---|---|---|---|---|---|
|1|1|1|–|–|Fault|
|2|2|1|2|–|Fault|
|3|3|1|2|3|Fault|
|4|1|1|2|3|Hit|
|5|4|4|2|3|Fault|
|6|2|4|2|3|Hit|

At step 5, the frames contained pages 1, 2 and 3. Page 1 was loaded first, so FIFO removes page 1 and loads page 4.

**Total page faults = 4**

### Advantages of FIFO

- Simple to implement.
    
- Requires tracking the order in which pages were loaded.
    
- Has relatively low policy-management overhead.
    

### Disadvantages of FIFO

- Ignores how frequently or recently a page is used.
    
- A frequently accessed page can be replaced merely because it is old.
    
- Can suffer from Belady's anomaly.
    

**Exam memory trick:** FIFO = replace the page loaded earliest.

---

## 4. LRU — Least Recently Used

LRU replaces the page that has not been used for the longest time in the past.

Unlike FIFO, LRU considers the most recent access to each page.

### How LRU Works

1. If the requested page is already loaded, it is a hit and becomes the most recently used page.
    
2. If a free frame exists, load the requested page.
    
3. Otherwise, evict the page whose last use was farthest in the past.
    
4. Load the new page.
    

### Example

Reference string:

`7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2`

Number of page frames: 3

|Step|Page requested|Frame 1|Frame 2|Frame 3|Result|
|---|---|---|---|---|---|
|1|7|7|–|–|Fault|
|2|0|7|0|–|Fault|
|3|1|7|0|1|Fault|
|4|2|2|0|1|Fault|
|5|0|2|0|1|Hit|
|6|3|2|0|3|Fault|
|7|0|2|0|3|Hit|
|8|4|4|0|3|Fault|
|9|2|4|0|2|Fault|
|10|3|4|3|2|Fault|
|11|0|0|3|2|Fault|
|12|3|0|3|2|Hit|
|13|2|0|3|2|Hit|

**Total page faults = 9**

### Understanding the Replacements

- **Step 4:** Page 2 arrives while pages 7, 0 and 1 occupy memory. Page 7 is least recently used, so it is replaced.
    
- **Step 6:** Page 3 arrives. Among pages 2, 0 and 1, page 1 was used least recently, so page 1 is replaced.
    
- **Step 8:** Page 4 arrives. Page 2 is the least recently used among the resident pages, so page 2 is replaced.
    

This differs from FIFO because a page loaded earliest might have been used recently. LRU cares about the most recent access, not the load time.

### Advantages

- Uses recent access history.
    
- Often performs well because programs tend to exhibit locality of reference.
    
- Does not suffer from Belady's anomaly under the standard page-replacement model.
    

### Disadvantages

- Exact LRU requires maintaining or approximating recency information.
    
- Timestamp or ordering-based implementations can add overhead.
    
- Many real systems use approximations rather than exact LRU.
    

**Exam memory trick:** LRU = replace the page least recently accessed.

---

## 5. Optimal Page Replacement (OPT)

Optimal page replacement replaces the page whose next use is farthest in the future.

If a resident page will never be used again, it is an ideal candidate for replacement.

OPT is also called **Optimal**, **MIN**, or **Belady's optimal page-replacement algorithm** in many textbooks.

### How OPT Works

1. If the requested page is already in memory, it is a hit.
    
2. If a free frame exists, load the page.
    
3. Otherwise, examine the future reference string.
    
4. Replace the page whose next use occurs farthest in the future, or that will never be used again.
    

### Example

Use the same reference string and three frames:

`7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2`

|Step|Page requested|Frame 1|Frame 2|Frame 3|Result|
|---|---|---|---|---|---|
|1|7|7|–|–|Fault|
|2|0|7|0|–|Fault|
|3|1|7|0|1|Fault|
|4|2|2|0|1|Fault|
|5|0|2|0|1|Hit|
|6|3|2|0|3|Fault|
|7|0|2|0|3|Hit|
|8|4|2|4|3|Fault|
|9|2|2|4|3|Hit|
|10|3|2|4|3|Hit|
|11|0|2|0|3|Fault|
|12|3|2|0|3|Hit|
|13|2|2|0|3|Hit|

**Total page faults = 7**

### Why Is OPT Considered Optimal?

It uses knowledge of future page references to make the best replacement choice for the known reference string. Under the standard model, it produces the minimum possible number of page faults for that string and number of frames.

### Can Real Operating Systems Implement Exact OPT?

Generally, no. The system cannot know the future sequence of all page references exactly. OPT is mainly a theoretical benchmark for comparing practical replacement algorithms.

### Advantages

- Produces the minimum possible page-fault count for a given reference string under the model.
    
- Useful for comparing FIFO, LRU and other practical approaches.
    
- Does not suffer from Belady's anomaly.
    

### Disadvantages

- Requires knowledge of future page references.
    
- Exact future knowledge is generally unavailable at runtime.
    
- Primarily useful for theoretical analysis and benchmarking.
    

**Exam memory trick:** OPT = replace the page whose next use is farthest away.

---

## 6. FIFO vs LRU vs Optimal

This comparison is extremely important for conceptual MCQs.

|Feature|FIFO|LRU|Optimal|
|---|---|---|---|
|Full form|First In, First Out|Least Recently Used|Optimal page replacement|
|Replaces|Page loaded earliest|Page least recently used in the past|Page whose next use is farthest in the future|
|Uses load order?|Yes|No|No|
|Uses past access history?|No, beyond load order|Yes|No|
|Requires future knowledge?|No|No|Yes|
|Can show Belady's anomaly?|Yes|No|No|
|Exact practical implementation|Simple queue|Requires recency tracking|Generally impossible without future knowledge|
|Role in studies|Simple baseline|Practical locality-based policy|Theoretical benchmark|

### Page-Fault Counts for the Worked Example

Reference string:

`7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2`

With three frames, initially empty:

|Algorithm|Page faults|
|---|---|
|FIFO|10|
|LRU|9|
|Optimal|7|

The same reference string and initial condition are used for all three algorithms, so these counts can be compared directly.

**Exam trap:** FIFO may remove a frequently used page simply because it entered memory earlier. LRU uses past accesses, while Optimal uses future accesses.

---

## 7. Belady's Anomaly — Very Important

Belady's anomaly is the phenomenon in which **increasing the number of page frames causes FIFO to produce more page faults** for the same reference string.

Normally, more frames might be expected to reduce page faults. FIFO can violate that expectation.

### Classic Reference String

`1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5`

Assume all frames are initially empty.

### A. FIFO with 3 Frames

|Requested page|Result|
|---|---|
|1|Fault|
|2|Fault|
|3|Fault|
|4|Fault|
|1|Fault|
|2|Fault|
|5|Fault|
|1|Hit|
|2|Hit|
|3|Fault|
|4|Fault|
|5|Hit|

**Total = 9 page faults**

### B. FIFO with 4 Frames

|Requested page|Result|
|---|---|
|1|Fault|
|2|Fault|
|3|Fault|
|4|Fault|
|1|Hit|
|2|Hit|
|5|Fault|
|1|Fault|
|2|Fault|
|3|Fault|
|4|Fault|
|5|Fault|

**Total = 10 page faults**

### Compare the Results

|Number of frames|FIFO page faults|
|---|---|
|3|9|
|4|10|

More frames produce more page faults in this FIFO example.

This is **Belady's anomaly**: increasing the number of frames from 3 to 4 increases the fault count from 9 to 10 for the same reference string.

### Which Algorithms Suffer from Belady's Anomaly?

- **FIFO:** Can suffer from Belady's anomaly.
    
- **LRU:** Does not suffer from Belady's anomaly under the standard model.
    
- **Optimal:** Does not suffer from Belady's anomaly under the standard model.
    

LRU and Optimal are examples of **stack algorithms**: increasing the number of frames preserves the pages that would have been resident with fewer frames, under the standard assumptions. This prevents the page-fault count from increasing merely because another frame is added.

**Exam memory trick:** Belady's anomaly is classically associated with FIFO, not LRU or Optimal.

---

## 8. How to Solve Page-Replacement Numerical Questions

Use this procedure every time:

1. Write the reference string in the exact order provided.
    
2. Draw the specified number of frames, initially empty unless stated otherwise.
    
3. For each page reference, mark a **Hit** if the page is already in memory; otherwise mark a **Fault**.
    
4. If a fault occurs and a frame is empty, load the page without replacing another page.
    
5. If a fault occurs and all frames are full, apply the given policy: FIFO, LRU or Optimal.
    
6. Count all faults, including the faults needed to fill initially empty frames.
    

### Quick Decision Table

|Question asks you to replace…|Algorithm|
|---|---|
|The page loaded earliest|FIFO|
|The page unused for the longest time in the past|LRU|
|The page that will be used farthest in the future|Optimal|
|Whether faults can increase with more frames under FIFO|Belady's anomaly|

### Page Faults vs Page Hits

For the 13-reference example with three frames:

|Algorithm|Faults|Hits|
|---|---|---|
|FIFO|10|3|
|LRU|9|4|
|Optimal|7|6|
|Total references|13|13|

Check the arithmetic:

**Faults + Hits = Total references**

For FIFO:

10 + 3 = 13

This is a useful way to verify your numerical answer.

---

## Last-Minute Revision

- **FIFO:** Evict the page loaded earliest.
    
- **LRU:** Evict the page least recently used in the past.
    
- **Optimal:** Evict the page whose next use is farthest in the future.
    
- **Page hit:** Requested page is already in a frame.
    
- **Page fault:** Requested page is not resident and needs handling.
    
- **Belady's anomaly:** FIFO can produce more page faults when more frames are added.
    
- **LRU and Optimal:** Do not exhibit Belady's anomaly in the standard model.
    

### DSSSB Practice Priority

Solve several complete reference-string tables by hand. For each request, mark hit or fault, update the frames according to the algorithm, and only then count the faults.