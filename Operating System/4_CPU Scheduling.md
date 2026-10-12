# 1. What is CPU scheduling?

CPU scheduling is the operating-system activity of selecting a process from the ready queue to execute on a CPU.

When several processes are ready to run, the OS scheduler decides which one gets CPU time next.

### Why is CPU scheduling necessary?

- To keep the CPU busy.
    
- To improve system throughput.
    
- To reduce waiting and response times.
    
- To provide fair access to the CPU.
    
- To improve responsiveness for interactive tasks.
    

## 2. Important terms and formulas

Before learning the algorithms, memorize these terms.

|Term|Meaning|
|---|---|
|AT — Arrival Time|Time when a process enters the ready queue|
|BT — Burst Time|Total CPU time required by a process|
|CT — Completion Time|Time when a process finishes execution|
|TAT — Turnaround Time|Total elapsed time from arrival to completion|
|WT — Waiting Time|Total time spent waiting in the ready queue|
|RT — Response Time|Time between arrival and the first time the process gets CPU service|

### The three most important formulas

1. Turnaround Time (TAT)

\[ \boxed{TAT=CT-AT} \]

2. Waiting Time (WT)

\[ \boxed{WT=TAT-BT} \]

3. Response Time (RT)

\[ \boxed{RT=\text{First CPU Start Time}-AT} \]

These formulas assume the usual CPU-scheduling model in which BT is the total CPU burst time and WT counts time spent waiting in the ready queue.

### Example

Suppose a process has:

- Arrival Time = 2
    
- Burst Time = 5
    
- Completion Time = 10
    
- First CPU start time = 4
    

Then:

\[ TAT=10-2=8 \]

\[ WT=8-5=3 \]

\[ RT=4-2=2 \]

Remember the difference:

- Turnaround time measures the entire time from arrival to completion.
    
- Waiting time measures time waiting for CPU service.
    
- Response time measures the wait until the first CPU service.
    

In a non-preemptive algorithm, once a process gets the CPU, it normally continues until its CPU burst finishes. With all processes arriving at time zero, WT and RT are equal under the standard model. In preemptive scheduling, they can differ.

# 3. First Come, First Served (FCFS)

FCFS schedules processes in the order they arrive in the ready queue.

It is analogous to a queue in which the first person to arrive is served first.

### Main characteristics

- Non-preemptive in its standard form.
    
- The process that arrives first runs first.
    
- Simple to implement.
    
- Does not require burst-time estimates to decide order.
    

### Example

Consider these processes, all arriving at time 0.

|Process|Arrival Time|Burst Time|
|---|---|---|
|P1|0|5|
|P2|0|3|
|P3|0|8|
|P4|0|6|

Assume ties in arrival time are resolved by the listed order.

### Step 1: Draw the Gantt chart

P1 requires 5 units, P2 requires 3, P3 requires 8, and P4 requires 6.

```
0       5       8               16              22
|  P1   |  P2   |      P3       |      P4       |
```

The completion times are P1 = 5, P2 = 8, P3 = 16 and P4 = 22.

### Step 2: Calculate the times

Because every process arrives at time 0:

|Process|AT|BT|CT|TAT = CT − AT|WT = TAT − BT|RT|
|---|---|---|---|---|---|---|
|P1|0|5|5|5|0|0|
|P2|0|3|8|8|5|5|
|P3|0|8|16|16|8|8|
|P4|0|6|22|22|16|16|

Average waiting time:

\[ \frac{0+5+8+16}{4}=\boxed{7.25} \]

Average turnaround time:

\[ \frac{5+8+16+22}{4}=\boxed{12.75} \]

Average response time:

\[ \frac{0+5+8+16}{4}=\boxed{7.25} \]

### Advantages

- Easy to understand and implement.
    
- Simple queue-based scheduling.
    
- No starvation caused purely by longer CPU bursts when arrivals are served in order and the queue progresses normally.
    

### Disadvantages

- Short processes can wait behind long processes.
    
- May produce high average waiting time.
    
- Can suffer from the convoy effect: a long process delays several short processes behind it.
    

Exam trap: FCFS does not necessarily minimize waiting time.

# 4. Shortest Job First (SJF)

SJF selects the ready process with the shortest next CPU burst.

In its standard form, SJF is non-preemptive: once a process starts executing, it continues until its CPU burst finishes.

### Example

Use the same burst times, with every process arriving at time 0.

|Process|Burst Time|
|---|---|
|P1|5|
|P2|3|
|P3|8|
|P4|6|

### Step 1: Arrange by shortest burst time

Order:

\[ P2 \rightarrow P1 \rightarrow P4 \rightarrow P3 \]

Burst times: \(3,5,6,8\).

### Step 2: Draw the Gantt chart

```
0       3           8              14               22
|  P2   |    P1     |      P4      |       P3       |
```

### Step 3: Calculate the times

|Process|AT|BT|CT|TAT|WT|RT|
|---|---|---|---|---|---|---|
|P1|0|5|8|8|3|3|
|P2|0|3|3|3|0|0|
|P3|0|8|22|22|14|14|
|P4|0|6|14|14|8|8|

Average waiting time:

\[ \frac{3+0+14+8}{4}=\boxed{6.25} \]

Average turnaround time:

\[ \frac{8+3+22+14}{4}=\boxed{11.75} \]

Average response time:

\[ \boxed{6.25} \]

### Why is SJF important?

For a known set of independent processes that are all available together, non-preemptive SJF minimizes average waiting time. More broadly, SJF is optimal for average waiting time under the classic assumptions of known CPU burst lengths and a single CPU burst per job.

In real systems, future CPU burst lengths generally must be estimated.

### Advantages

- Can reduce average waiting time.
    
- Short jobs finish quickly.
    
- Useful when CPU burst estimates are available.
    

### Disadvantages

- Requires knowledge or estimates of CPU burst lengths.
    
- Long processes can experience starvation if shorter processes repeatedly arrive.
    
- The algorithm is less practical when burst lengths are unpredictable.
    

Exam trap: SJF and SRTF are not the same algorithm. Standard SJF is non-preemptive; SRTF is the preemptive counterpart.

# 5. Shortest Remaining Time First (SRTF)

SRTF selects the process with the shortest remaining CPU burst among the processes currently ready.

SRTF is the preemptive version of SJF.

If a new process arrives with a shorter remaining time than the currently running process, the current process can be interrupted and the new one can run.

## Example with different arrival times

Consider the following processes.

|Process|Arrival Time|Burst Time|
|---|---|---|
|P1|0|8|
|P2|1|4|
|P3|2|2|
|P4|3|1|

Assume that on a tie in remaining time, the running process continues. Other tie-breaking rules can produce different schedules.

### Step 1: Schedule the processes

Time 0: Only P1 is available, so P1 starts.

Time 1: P2 arrives. P1 has 7 units remaining, while P2 needs 4, so P2 preempts P1.

Time 2: P3 arrives. P2 has 3 units remaining, while P3 needs 2, so P3 preempts P2.

Time 3: P4 arrives. P3 has 1 unit remaining and P4 needs 1 unit. With our tie rule, P3 continues and finishes at time 4.

Time 4: P4 has 1 unit remaining, less than the remaining times of P1 and P2, so P4 runs and finishes at time 5.

Time 5: P2 has 3 units remaining, so it runs and finishes at time 8.

Time 8: P1 runs its final 7 units and finishes at time 15.

### Step 2: Gantt chart

```
0   1   2       4   5       8               15
| P1| P2|  P3   | P4|  P2   |       P1      |
```

### Step 3: Calculate the times

|Process|AT|BT|CT|TAT = CT − AT|WT = TAT − BT|RT|
|---|---|---|---|---|---|---|
|P1|0|8|15|15|7|0|
|P2|1|4|8|7|3|0|
|P3|2|2|4|2|0|0|
|P4|3|1|5|2|1|1|

Average waiting time:

\[ \frac{7+3+0+1}{4}=\boxed{2.75} \]

Average turnaround time:

\[ \frac{15+7+2+2}{4}=\boxed{6.5} \]

Average response time:

\[ \frac{0+0+0+1}{4}=\boxed{0.25} \]

### Advantages

- Short jobs can complete quickly.
    
- Can give a low average waiting time.
    
- Responds to newly arrived processes with shorter remaining bursts.
    

### Disadvantages

- Long processes may starve.
    
- Requires knowledge or estimates of remaining CPU burst times.
    
- Frequent preemption can increase context-switching overhead.
    

Exam memory trick: SJF compares total burst time before a non-preemptive choice; SRTF compares remaining time as the schedule evolves.

# 6. Priority Scheduling

In Priority Scheduling, the CPU is allocated to the ready process with the highest priority.

A common convention is that a smaller priority number means higher priority, but some questions use the opposite convention. Always read the question carefully.

Priority Scheduling can be:

- Non-preemptive: The running process continues until its CPU burst finishes.
    
- Preemptive: A newly arrived higher-priority process can interrupt the running process.
    

## Example: Non-preemptive Priority Scheduling

Assume every process arrives at time 0 and a smaller number means higher priority.

|Process|Burst Time|Priority|
|---|---|---|
|P1|5|3|
|P2|3|4|
|P3|8|1|
|P4|6|2|

### Step 1: Arrange by priority

P3 has priority 1, P4 has priority 2, P1 has priority 3, and P2 has priority 4.

The execution order is:

\[ P3 \rightarrow P4 \rightarrow P1 \rightarrow P2 \]

### Step 2: Draw the Gantt chart

```
0               8              14          19      22
|      P3       |      P4      |    P1     |  P2  |
```

### Step 3: Calculate the times

|Process|AT|BT|Priority|CT|TAT|WT|RT|
|---|---|---|---|---|---|---|---|
|P1|0|5|3|19|19|14|14|
|P2|0|3|4|22|22|19|19|
|P3|0|8|1|8|8|0|0|
|P4|0|6|2|14|14|8|8|

Average waiting time:

\[ \frac{14+19+0+8}{4}=\boxed{10.25} \]

Average turnaround time:

\[ \frac{19+22+8+14}{4}=\boxed{15.75} \]

Average response time:

\[ \boxed{10.25} \]

### What is starvation?

Starvation occurs when a process waits indefinitely or for an excessively long time because other processes keep receiving preference.

In Priority Scheduling, low-priority processes can starve if higher-priority processes continually arrive.

### What is aging?

Aging gradually increases the priority of a waiting process so that it becomes more likely to receive CPU time.

For example, a process that waits for a long time might gradually move to a higher scheduling priority.

|Concept|Meaning|
|---|---|
|Starvation|A process waits indefinitely or excessively|
|Aging|Gradually improves a waiting process's priority|
|Priority Scheduling|Selects based on priority|
|Preemptive Priority|A newly arrived higher-priority process can preempt the current one|

Exam traps:

- A smaller priority number is not universal; follow the stated convention.
    
- Priority Scheduling can be preemptive or non-preemptive.
    
- Aging is a common remedy for starvation.
    

# 7. Round Robin (RR)

Round Robin is a preemptive scheduling algorithm in which each ready process receives CPU time for a fixed maximum interval called the time quantum.

If the process does not finish within its quantum, it is preempted and placed at the back of the ready queue, assuming it remains runnable.

Round Robin is commonly associated with time-sharing systems.

## Example

Use the following processes, each arriving at time 0. Let the time quantum be 3 units.

|Process|Arrival Time|Burst Time|
|---|---|---|
|P1|0|5|
|P2|0|3|
|P3|0|8|
|P4|0|6|

Initial ready queue:

\[ P1 \rightarrow P2 \rightarrow P3 \rightarrow P4 \]

### Step 1: Execute one quantum at a time

- P1: Runs for 3 units, from 0 to 3. Remaining burst time = 2.
    
- P2: Runs from 3 to 6 and finishes.
    
- P3: Runs from 6 to 9. Remaining = 5.
    
- P4: Runs from 9 to 12. Remaining = 3.
    
- P1: Runs from 12 to 14 and finishes.
    
- P3: Runs from 14 to 17. Remaining = 2.
    
- P4: Runs from 17 to 20 and finishes.
    
- P3: Runs from 20 to 22 and finishes.
    

### Step 2: Draw the Gantt chart

```
0    3    6    9    12   14   17   20   22
| P1 | P2 | P3 | P4 | P1 | P3 | P4 | P3 |
```

### Step 3: Calculate the times

|Process|AT|BT|CT|TAT|WT|RT|
|---|---|---|---|---|---|---|
|P1|0|5|14|14|9|0|
|P2|0|3|6|6|3|3|
|P3|0|8|22|22|14|6|
|P4|0|6|20|20|14|9|

Average waiting time:

\[ \frac{9+3+14+14}{4}=\boxed{10} \]

Average turnaround time:

\[ \frac{14+6+22+20}{4}=\boxed{15.5} \]

Average response time:

\[ \frac{0+3+6+9}{4}=\boxed{4.5} \]

### Advantages

- Gives runnable processes repeated opportunities to execute.
    
- Usually provides good responsiveness for interactive workloads with a suitable quantum.
    
- Prevents a runnable process from monopolizing the CPU indefinitely under ordinary queue assumptions.
    

### Disadvantages

- Very small time quanta cause frequent context switches.
    
- Very large time quanta make RR behave increasingly like FCFS.
    
- Average waiting time may be relatively high for some workloads.
    
- Actual scheduling outcomes depend on arrival order, the quantum and the implementation's handling of simultaneous events.
    

### Effect of the time quantum

|Quantum size|Typical effect|
|---|---|
|Very small|Better-grained sharing, but more context-switching overhead|
|Moderate|Balances responsiveness and switching overhead|
|Very large|Approaches FCFS behavior|

Exam trap: Round Robin uses a time quantum. SJF chooses the shortest burst; Priority Scheduling chooses according to priority.

# 8. Waiting Time, Turnaround Time and Response Time — Deep Revision

These three metrics are essential because many CPU-scheduling questions ask you to calculate them from a Gantt chart.

## A. Turnaround Time (TAT)

Turnaround time measures the total elapsed time between process arrival and completion.

\[ \boxed{TAT=CT-AT} \]

Example: A process arrives at time 3 and finishes at time 11.

\[ TAT=11-3=8 \]

Its turnaround time is 8 units.

## B. Waiting Time (WT)

Waiting time is the total time spent waiting in the ready queue.

For the standard single-CPU scheduling exercise, where BT represents the entire CPU burst:

\[ \boxed{WT=TAT-BT} \]

Example: If TAT = 8 and BT = 5:

\[ WT=8-5=3 \]

The process spent three time units waiting for the CPU.

For a preemptive process, waiting time includes the waits between its CPU execution intervals.

## C. Response Time (RT)

Response time measures how long a process waits before receiving CPU service for the first time.

\[ \boxed{RT=\text{First CPU Start Time}-AT} \]

Example: A process arrives at time 2 but first runs at time 6.

\[ RT=6-2=4 \]

Even if it later waits several more times, its response time stays 4.

### Waiting time vs turnaround time vs response time

|Metric|Measures|When is it complete?|
|---|---|---|
|Turnaround time|Arrival to completion|When the process finishes|
|Waiting time|Total time waiting in the ready queue|When the full scheduling history is known|
|Response time|Arrival to first CPU service|As soon as its first execution begins|

### Common exam trap

For a non-preemptive process, response time equals the initial ready-queue wait. For a preemptive process, response time may be much smaller than total waiting time.

For example, under Round Robin, P3 first runs at time 6, so RT = 6. It completes at time 22 with BT = 8:

\[ TAT=22-0=22 \]

\[ WT=22-8=14 \]

\[ RT=6-0=6 \]

Thus, `WT = 14` but `RT = 6`.

## 9. Average metrics

To calculate an average, add the metric for all processes and divide by the number of processes.

\[ \boxed{\text{Average WT}=\frac{\sum WT}{n}} \]

\[ \boxed{\text{Average TAT}=\frac{\sum TAT}{n}} \]

\[ \boxed{\text{Average RT}=\frac{\sum RT}{n}} \]

For example, if four processes have waiting times 0, 5, 8 and 16:

\[ \text{Average WT}=\frac{0+5+8+16}{4}=7.25 \]

Do not divide by total burst time or by the completion time of the last process.

# 10. All CPU Scheduling Algorithms — Comparison Table

|Feature|FCFS|SJF|SRTF|Priority|Round Robin|
|---|---|---|---|---|---|
|Main decision|Arrival order|Shortest CPU burst|Shortest remaining time|Priority|Circular ready queue|
|Standard form|Non-preemptive|Non-preemptive|Preemptive|Either|Preemptive|
|Needs burst estimates|No|Yes|Yes|No, but needs priority values|No|
|Can preempt a running process?|Not in standard FCFS|Not in standard SJF|Yes|Yes, in preemptive form|At quantum expiry|
|Main strength|Simple|Low average waiting time under classic assumptions|Favors short remaining jobs|Enforces priority preference|Repeated opportunities to execute|
|Main concern|Convoy effect|Starvation of long jobs|Starvation of long jobs|Starvation of low-priority jobs|Context-switching overhead|
|Common remedy|—|Aging or hybrid schemes|Aging or hybrid schemes|Aging|Choose a suitable quantum|

### Average results from our shared all-processes-arrive-at-zero example

These values use the same four processes for FCFS, SJF, non-preemptive Priority Scheduling and Round Robin.

|Algorithm|Average WT|Average TAT|Average RT|
|---|---|---|---|
|FCFS|7.25|12.75|7.25|
|SJF|6.25|11.75|6.25|
|Priority|10.25|15.75|10.25|
|Round Robin (quantum = 3)|10.00|15.50|4.50|

SRTF used a separate example with different arrival times, so its results should not be compared directly with this table.

# 11. How to solve any CPU-scheduling numerical question

Follow this method in your exam.

1. Write each process's Arrival Time (AT), Burst Time (BT) and Priority, if provided.
    
2. Identify the algorithm and check whether it is preemptive or non-preemptive.
    
3. Draw the Gantt chart. Mark every start, finish and preemption time.
    
4. Find each process's Completion Time (CT) using its final finish time.
    
5. Calculate TAT using \(CT-AT\).
    
6. Calculate WT using \(TAT-BT\), for the standard CPU-burst model.
    
7. Calculate RT using the first CPU start time minus AT.
    
8. Add each metric across processes and divide by the number of processes to get its average.
    

## 12. More important exam traps

| Question                                                                    | Correct answer                                                                   |
| --------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| Which algorithm is the preemptive version of SJF?                           | SRTF                                                                             |
| Which algorithm uses a time quantum?                                        | Round Robin                                                                      |
| Which algorithm can suffer from the convoy effect?                          | FCFS                                                                             |
| Which algorithm can starve long CPU bursts?                                 | SJF / SRTF                                                                       |
| Which algorithm can starve low-priority processes?                          | Priority Scheduling                                                              |
| What is a common solution to priority starvation?                           | Aging                                                                            |
| When does RT stop accumulating?                                             | At the process's first CPU service                                               |
| Can response time be greater than waiting time?                             | Not under the standard definitions where total waiting includes the initial wait |
| Can waiting time be greater than response time?                             | Yes, especially in preemptive scheduling                                         |
| If all processes arrive at time 0 and execute non-preemptively, what is RT? | The initial waiting time for each process                                        |
| Does a smaller priority number always mean higher priority?                 | No; follow the question's stated convention                                      |
| Does a smaller quantum always improve total performance?                    | No; switching overhead can increase                                              |
## Final revision

- FCFS: Arrival order; non-preemptive.
    
- SJF: Shortest burst; typically non-preemptive.
    
- SRTF: Shortest remaining burst; preemptive.
    
- Priority: Highest-priority ready process; can be preemptive or non-preemptive.
    
- Round Robin: Fixed time quantum; preemptive.
    
- TAT: `CT − AT`.
    
- WT: `TAT − BT`.
    
- RT: `First CPU start − AT`.
    
- Starvation remedy: Aging.
    

Most important exam skill: Given a set of processes and their arrival times, burst times and priorities, draw the correct Gantt chart first. Once the chart is right, the calculations become much easier.