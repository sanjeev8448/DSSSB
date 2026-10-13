# CPU Scheduling — DSSSB TGT Computer Science

## 1. What Is CPU Scheduling?

CPU scheduling is the operating-system activity of selecting a process from the ready queue to execute on the CPU.

When several processes are ready to run, the OS scheduler decides which process receives CPU time next.

### Why Is CPU Scheduling Necessary?

- To keep the CPU busy.
    
- To improve system throughput.
    
- To reduce waiting and response times.
    
- To provide fair access to the CPU.
    
- To improve responsiveness for interactive tasks.
    

---

## 2. Important Terms and Formulas

|Term|Meaning|
|---|---|
|AT — Arrival Time|Time when a process enters the ready queue|
|BT — Burst Time|Total CPU time required by a process|
|CT — Completion Time|Time when a process finishes execution|
|TAT — Turnaround Time|Total elapsed time from arrival to completion|
|WT — Waiting Time|Total time spent waiting in the ready queue|
|RT — Response Time|Time between arrival and the first CPU service|

### Three Most Important Formulas

**1. Turnaround Time**

```
TAT = CT − AT
```

**2. Waiting Time**

```
WT = TAT − BT
```

**3. Response Time**

```
RT = First CPU Start Time − AT
```

These formulas assume the standard CPU-scheduling model, where BT is the total CPU burst time.

### Example

Suppose a process has:

- Arrival Time = 2
    
- Burst Time = 5
    
- Completion Time = 10
    
- First CPU start time = 4
    

Then:

```
TAT = CT − AT
    = 10 − 2
    = 8

WT = TAT − BT
   = 8 − 5
   = 3

RT = First CPU Start Time − AT
   = 4 − 2
   = 2
```

Remember the difference:

- **Turnaround time:** Entire time from arrival to completion.
    
- **Waiting time:** Total time spent waiting for CPU service.
    
- **Response time:** Time spent waiting until the first CPU service.
    

For a non-preemptive algorithm, response time equals the initial ready-queue wait. In preemptive scheduling, response time can be smaller than total waiting time.

---

## 3. First Come, First Served (FCFS)

FCFS schedules processes in the order they arrive in the ready queue.

It works like a normal queue: the first person to arrive is served first.

### Main Characteristics

- Non-preemptive in its standard form.
    
- The process that arrives first runs first.
    
- Simple to implement.
    
- Does not require CPU burst-time estimates to determine the order.
    

### Example

All processes arrive at time 0.

|Process|Arrival Time|Burst Time|
|---|---|---|
|P1|0|5|
|P2|0|3|
|P3|0|8|
|P4|0|6|

Assume ties in arrival time are resolved by the listed order.

### Step 1: Draw the Gantt Chart

```
0       5       8               16              22
|  P1   |  P2   |      P3       |      P4       |
```

Completion times:

- P1 = 5
    
- P2 = 8
    
- P3 = 16
    
- P4 = 22
    

### Step 2: Calculate the Times

|Process|AT|BT|CT|TAT = CT − AT|WT = TAT − BT|RT|
|---|---|---|---|---|---|---|
|P1|0|5|5|5|0|0|
|P2|0|3|8|8|5|5|
|P3|0|8|16|16|8|8|
|P4|0|6|22|22|16|16|

Average waiting time:

```
(0 + 5 + 8 + 16) / 4 = 7.25
```

Average turnaround time:

```
(5 + 8 + 16 + 22) / 4 = 12.75
```

Average response time:

```
(0 + 5 + 8 + 16) / 4 = 7.25
```

### Advantages

- Easy to understand and implement.
    
- Uses a simple queue-based approach.
    
- Does not cause starvation purely because a process has a long CPU burst, provided the queue progresses normally.
    

### Disadvantages

- Short processes can wait behind long processes.
    
- Can produce high average waiting time.
    
- Can suffer from the **convoy effect**, where one long process delays several shorter processes.
    

**Exam trap:** FCFS does not necessarily minimize average waiting time.

---

## 4. Shortest Job First (SJF)

SJF selects the ready process with the shortest next CPU burst.

In its standard form, SJF is **non-preemptive**: once a process starts, it continues until its CPU burst finishes.

### Example

Use the same burst times, with every process arriving at time 0.

|Process|Burst Time|
|---|---|
|P1|5|
|P2|3|
|P3|8|
|P4|6|

### Step 1: Arrange by Shortest Burst Time

Execution order:

```
P2 → P1 → P4 → P3
```

Burst times: 3, 5, 6, 8.

### Step 2: Gantt Chart

```
0       3           8              14               22
|  P2   |    P1     |      P4      |       P3       |
```

### Step 3: Calculate the Times

|Process|AT|BT|CT|TAT|WT|RT|
|---|---|---|---|---|---|---|
|P1|0|5|8|8|3|3|
|P2|0|3|3|3|0|0|
|P3|0|8|22|22|14|14|
|P4|0|6|14|14|8|8|

Average waiting time:

```
(3 + 0 + 14 + 8) / 4 = 6.25
```

Average turnaround time:

```
(8 + 3 + 22 + 14) / 4 = 11.75
```

Average response time:

```
6.25
```

### Why Is SJF Important?

Under the classic assumptions of known CPU burst lengths, a single CPU, and independent jobs that are all available together, non-preemptive SJF minimizes average waiting time.

In real operating systems, future CPU burst lengths generally have to be estimated.

### Advantages

- Can reduce average waiting time.
    
- Short jobs finish quickly.
    
- Useful when CPU burst estimates are available.
    

### Disadvantages

- Requires knowledge or estimates of CPU burst lengths.
    
- Long processes can experience starvation if shorter processes repeatedly arrive.
    
- Less practical when burst lengths are unpredictable.
    

**Exam trap:** SJF and SRTF are not the same algorithm. Standard SJF is non-preemptive; SRTF is its preemptive counterpart.

---

## 5. Shortest Remaining Time First (SRTF)

SRTF selects the ready process with the shortest remaining CPU burst.

It is the **preemptive version of SJF**.

If a new process arrives with a shorter remaining time than the currently running process, the current process can be interrupted.

### Example With Different Arrival Times

|Process|Arrival Time|Burst Time|
|---|---|---|
|P1|0|8|
|P2|1|4|
|P3|2|2|
|P4|3|1|

Assume that if two processes have equal remaining time, the running process continues.

### Step 1: Schedule the Processes

- **Time 0:** Only P1 is available, so P1 starts.
    
- **Time 1:** P2 arrives. P1 has 7 units remaining, while P2 needs 4. P2 preempts P1.
    
- **Time 2:** P3 arrives. P2 has 3 units remaining, while P3 needs 2. P3 preempts P2.
    
- **Time 3:** P4 arrives. P3 and P4 each need 1 unit. Under our tie rule, P3 continues and finishes at time 4.
    
- **Time 4:** P4 runs and finishes at time 5.
    
- **Time 5:** P2 runs its remaining 3 units and finishes at time 8.
    
- **Time 8:** P1 runs its remaining 7 units and finishes at time 15.
    

### Step 2: Gantt Chart

```
0   1   2       4   5       8               15
| P1| P2|  P3   | P4|  P2   |       P1      |
```

### Step 3: Calculate the Times

|Process|AT|BT|CT|TAT = CT − AT|WT = TAT − BT|RT|
|---|---|---|---|---|---|---|
|P1|0|8|15|15|7|0|
|P2|1|4|8|7|3|0|
|P3|2|2|4|2|0|0|
|P4|3|1|5|2|1|1|

Average waiting time:

```
(7 + 3 + 0 + 1) / 4 = 2.75
```

Average turnaround time:

```
(15 + 7 + 2 + 2) / 4 = 6.5
```

Average response time:

```
(0 + 0 + 0 + 1) / 4 = 0.25
```

### Advantages

- Short jobs can complete quickly.
    
- Can provide low average waiting time.
    
- Responds to newly arrived processes with shorter remaining bursts.
    

### Disadvantages

- Long processes may starve.
    
- Requires knowledge or estimates of remaining burst times.
    
- Frequent preemption can increase context-switching overhead.
    

**Exam memory trick:**

- SJF compares total burst time before making a non-preemptive choice.
    
- SRTF compares remaining time as the schedule evolves.
    

---

## 6. Priority Scheduling

Priority Scheduling allocates the CPU to the ready process with the highest priority.

A common convention is that a smaller priority number means higher priority. However, some questions use the opposite convention, so always read the question carefully.

Priority Scheduling can be:

- **Non-preemptive:** The running process continues until its CPU burst finishes.
    
- **Preemptive:** A newly arrived higher-priority process can interrupt the running process.
    

### Example: Non-Preemptive Priority Scheduling

Assume every process arrives at time 0 and a smaller number means higher priority.

|Process|Burst Time|Priority|
|---|---|---|
|P1|5|3|
|P2|3|4|
|P3|8|1|
|P4|6|2|

### Step 1: Arrange by Priority

Execution order:

```
P3 → P4 → P1 → P2
```

P3 has priority 1, P4 has priority 2, P1 has priority 3, and P2 has priority 4.

### Step 2: Gantt Chart

```
0               8              14          19      22
|      P3       |      P4      |    P1     |  P2  |
```

### Step 3: Calculate the Times

|Process|AT|BT|Priority|CT|TAT|WT|RT|
|---|---|---|---|---|---|---|---|
|P1|0|5|3|19|19|14|14|
|P2|0|3|4|22|22|19|19|
|P3|0|8|1|8|8|0|0|
|P4|0|6|2|14|14|8|8|

Average waiting time:

```
(14 + 19 + 0 + 8) / 4 = 10.25
```

Average turnaround time:

```
(19 + 22 + 8 + 14) / 4 = 15.75
```

Average response time:

```
10.25
```

### What Is Starvation?

Starvation occurs when a process waits indefinitely or excessively because other processes keep receiving preference.

In Priority Scheduling, low-priority processes can starve if higher-priority processes continually arrive.

### What Is Aging?

Aging gradually increases the priority of a waiting process so that it becomes more likely to receive CPU time.

|Concept|Meaning|
|---|---|
|Starvation|A process waits indefinitely or excessively|
|Aging|Gradually improves a waiting process's priority|
|Priority Scheduling|Selects processes based on priority|
|Preemptive Priority|A newly arrived higher-priority process can preempt the current one|

**Exam traps:**

- A smaller priority number is not a universal rule.
    
- Priority Scheduling can be preemptive or non-preemptive.
    
- Aging is a common remedy for starvation.
    

---

## 7. Round Robin (RR)

Round Robin is a preemptive scheduling algorithm in which each ready process receives CPU time for a fixed maximum interval called the **time quantum**.

If the process does not finish within its quantum, it is preempted and placed at the back of the ready queue, assuming it remains runnable.

Round Robin is commonly associated with time-sharing systems.

### Example

All processes arrive at time 0. The time quantum is 3 units.

|Process|Arrival Time|Burst Time|
|---|---|---|
|P1|0|5|
|P2|0|3|
|P3|0|8|
|P4|0|6|

Initial ready queue:

```
P1 → P2 → P3 → P4
```

### Step 1: Execute One Quantum at a Time

- P1: Runs from 0 to 3. Remaining burst time = 2.
    
- P2: Runs from 3 to 6 and finishes.
    
- P3: Runs from 6 to 9. Remaining = 5.
    
- P4: Runs from 9 to 12. Remaining = 3.
    
- P1: Runs from 12 to 14 and finishes.
    
- P3: Runs from 14 to 17. Remaining = 2.
    
- P4: Runs from 17 to 20 and finishes.
    
- P3: Runs from 20 to 22 and finishes.
    

### Step 2: Gantt Chart

```
0    3    6    9    12   14   17   20   22
| P1 | P2 | P3 | P4 | P1 | P3 | P4 | P3 |
```

### Step 3: Calculate the Times

|Process|AT|BT|CT|TAT|WT|RT|
|---|---|---|---|---|---|---|
|P1|0|5|14|14|9|0|
|P2|0|3|6|6|3|3|
|P3|0|8|22|22|14|6|
|P4|0|6|20|20|14|9|

Average waiting time:

```
(9 + 3 + 14 + 14) / 4 = 10
```

Average turnaround time:

```
(14 + 6 + 22 + 20) / 4 = 15.5
```

Average response time:

```
(0 + 3 + 6 + 9) / 4 = 4.5
```

### Advantages

- Gives runnable processes repeated opportunities to execute.
    
- Usually provides good responsiveness for interactive workloads with a suitable quantum.
    
- Prevents a runnable process from monopolizing the CPU indefinitely under ordinary queue assumptions.
    

### Disadvantages

- Very small time quanta cause frequent context switches.
    
- Very large time quanta make Round Robin behave increasingly like FCFS.
    
- Average waiting time may be relatively high for some workloads.
    
- Outcomes depend on arrival order, quantum size, and how simultaneous events are handled.
    

### Effect of Time Quantum

|Quantum size|Typical effect|
|---|---|
|Very small|Fine-grained sharing, but more context-switching overhead|
|Moderate|Balances responsiveness and switching overhead|
|Very large|Approaches FCFS behavior|

**Exam trap:** Round Robin uses a time quantum. SJF chooses the shortest burst, while Priority Scheduling chooses according to priority.

---

## 8. Waiting Time, Turnaround Time and Response Time

These three metrics are essential because many CPU-scheduling questions ask you to calculate them from a Gantt chart.

### A. Turnaround Time (TAT)

Turnaround time measures the total elapsed time between process arrival and completion.

```
TAT = CT − AT
```

Example: A process arrives at time 3 and finishes at time 11.

```
TAT = 11 − 3 = 8
```

Its turnaround time is 8 units.

### B. Waiting Time (WT)

Waiting time is the total time spent waiting in the ready queue.

For the standard single-CPU scheduling exercise:

```
WT = TAT − BT
```

Example: If TAT = 8 and BT = 5:

```
WT = 8 − 5 = 3
```

For a preemptive process, waiting time includes the waits between its CPU execution intervals.

### C. Response Time (RT)

Response time measures how long a process waits before receiving CPU service for the first time.

```
RT = First CPU Start Time − AT
```

Example: A process arrives at time 2 but first runs at time 6.

```
RT = 6 − 2 = 4
```

Even if it waits several more times later, its response time remains 4.

### Comparison Table

|Metric|Measures|When is it determined?|
|---|---|---|
|Turnaround time|Arrival to completion|When the process finishes|
|Waiting time|Total ready-queue waiting|When the full scheduling history is known|
|Response time|Arrival to first CPU service|When execution first begins|

**Common exam trap:** For a non-preemptive process, response time equals its initial ready-queue wait. For a preemptive process, response time may be much smaller than total waiting time.

For example, under Round Robin, P3 first runs at time 6, completes at time 22, and has BT = 8.

```
TAT = 22 − 0 = 22
WT  = 22 − 8 = 14
RT  = 6 − 0 = 6
```

Thus, WT = 14 but RT = 6.

---

## 9. Average Metrics

To calculate an average, add the metric for all processes and divide by the number of processes.

```
Average WT  = Sum of waiting times / n

Average TAT = Sum of turnaround times / n

Average RT  = Sum of response times / n
```

For example, if four processes have waiting times 0, 5, 8, and 16:

```
Average WT = (0 + 5 + 8 + 16) / 4
           = 7.25
```

**Exam trap:** Do not divide by total burst time or by the completion time of the last process.

---

## 10. Comparison of All CPU Scheduling Algorithms

|Feature|FCFS|SJF|SRTF|Priority|Round Robin|
|---|---|---|---|---|---|
|Main decision|Arrival order|Shortest CPU burst|Shortest remaining time|Priority|Circular ready queue|
|Standard form|Non-preemptive|Non-preemptive|Preemptive|Either|Preemptive|
|Needs burst estimates|No|Yes|Yes|No, but needs priority values|No|
|Can preempt a running process?|No, standard form|No, standard form|Yes|Yes, in preemptive form|At quantum expiry|
|Main strength|Simple|Low average waiting time under classic assumptions|Favors short remaining jobs|Enforces priority preference|Repeated opportunities to execute|
|Main concern|Convoy effect|Starvation of long jobs|Starvation of long jobs|Starvation of low-priority jobs|Context-switching overhead|
|Common remedy|—|Aging or hybrid schemes|Aging or hybrid schemes|Aging|Choose a suitable quantum|

### Average Results From the Shared Example

These values use the same four processes for FCFS, SJF, non-preemptive Priority Scheduling, and Round Robin.

|Algorithm|Average WT|Average TAT|Average RT|
|---|---|---|---|
|FCFS|7.25|12.75|7.25|
|SJF|6.25|11.75|6.25|
|Priority|10.25|15.75|10.25|
|Round Robin, quantum = 3|10.00|15.50|4.50|

SRTF used a separate example with different arrival times, so its results should not be compared directly with this table.

---

## 11. How to Solve Any CPU-Scheduling Numerical Question

Follow this method in your exam:

1. Write each process's Arrival Time (AT), Burst Time (BT), and Priority, if provided.
    
2. Identify the scheduling algorithm and check whether it is preemptive or non-preemptive.
    
3. Draw the Gantt chart. Mark every start, finish, and preemption time.
    
4. Find each process's Completion Time (CT) using its final finish time.
    
5. Calculate TAT using `CT − AT`.
    
6. Calculate WT using `TAT − BT`.
    
7. Calculate RT using `First CPU Start Time − AT`.
    
8. Add each metric across processes and divide by the number of processes to obtain its average.
    

Once the Gantt chart is correct, the calculations become much easier.

---

## 12. Important Exam Traps

|Question|Correct answer|
|---|---|
|Which algorithm is the preemptive version of SJF?|SRTF|
|Which algorithm uses a time quantum?|Round Robin|
|Which algorithm can suffer from the convoy effect?|FCFS|
|Which algorithms can starve long CPU bursts?|SJF / SRTF|
|Which algorithm can starve low-priority processes?|Priority Scheduling|
|What is a common solution to priority starvation?|Aging|
|When does response time stop accumulating?|At the process's first CPU service|
|Can response time be greater than waiting time?|Not under the standard definitions|
|Can waiting time be greater than response time?|Yes, especially in preemptive scheduling|
|If all processes arrive at time 0 and execute non-preemptively, what is RT?|The initial waiting time|
|Does a smaller priority number always mean higher priority?|No; follow the stated convention|
|Does a smaller quantum always improve performance?|No; switching overhead can increase|

---

## 13. Final Revision Sheet

- **FCFS:** Arrival order; non-preemptive.
    
- **SJF:** Shortest burst; typically non-preemptive.
    
- **SRTF:** Shortest remaining burst; preemptive.
    
- **Priority Scheduling:** Selects the highest-priority ready process; can be preemptive or non-preemptive.
    
- **Round Robin:** Fixed time quantum; preemptive.
    
- **TAT:** `CT − AT`.
    
- **WT:** `TAT − BT`.
    
- **RT:** `First CPU Start − AT`.
    
- **Starvation remedy:** Aging.
    

### Highest-Priority DSSSB Preparation Points

1. Memorize the five scheduling algorithms and their preemptive/non-preemptive forms.
    
2. Practise Gantt charts with different arrival and burst times.
    
3. Calculate CT, TAT, WT, and RT accurately.
    
4. Learn the convoy effect, starvation, and aging.
    
5. Understand how the Round Robin time quantum affects responsiveness and context-switching overhead.