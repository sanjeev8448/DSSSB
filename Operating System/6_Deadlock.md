# 1. What is deadlock?

A deadlock is a situation in which a group of processes becomes permanently blocked because each process is waiting for a resource or event that can only be provided by another blocked process in the group.

### Example

Suppose there are two processes, P1 and P2, and two resources, R1 and R2. Each resource has one instance.

- P1 holds R1 and requests R2.
    
- P2 holds R2 and requests R1.
    

### Deadlock example

### P1

Holds R1

Waits for R2

### P2

Holds R2

Waits for R1

P1 cannot proceed until R2 is released. P2 cannot proceed until R1 is released.

### Deadlock

Neither process can proceed without intervention.

This is deadlock because each process holds a resource and waits indefinitely for the resource held by the other.

Important distinction: Deadlock is not the same as starvation. In deadlock, a set of processes is stuck because of dependencies. In starvation, a process may wait indefinitely because the system repeatedly favors other processes.

# 2. Four necessary conditions for deadlock

All four classical conditions must hold simultaneously for deadlock to occur.

A useful memory trick is M-H-N-C:

- M — Mutual exclusion
    
- H — Hold and wait
    
- N — No preemption
    
- C — Circular wait
    

## A. Mutual exclusion

At least one resource must be non-shareable: only one process can use that resource instance at a time.

Example: A printer that can serve only one print job at a time.

If a required resource can be shared without conflict, mutual exclusion may not apply to that resource.

## B. Hold and wait

A process holds one or more resources while waiting to acquire additional resources held by others.

Example: P1 holds R1 while waiting for R2.

## C. No preemption

Resources cannot be forcibly taken away from a process; they must be released voluntarily or through an appropriate recovery action.

Example: A process holds a resource that the operating system cannot safely take away immediately.

This is a condition of the classical deadlock model, not a claim that operating systems can never recover resources forcibly.

## D. Circular wait

A circular chain of processes exists, with each process waiting for a resource held by the next process in the chain.

For example:

\[ P_1\rightarrow P_2\rightarrow P_3\rightarrow P_1 \]

Each process waits for another process in the cycle.

### Four conditions — comparison table

|Condition|Meaning|Example|
|---|---|---|
|Mutual exclusion|A resource cannot be shared simultaneously|Exclusive access to a printer|
|Hold and wait|Hold one resource while requesting another|P1 holds R1 and requests R2|
|No preemption|Resources cannot be forcibly taken away under the model|P2 must release R2|
|Circular wait|Processes form a waiting cycle|P1 → P2 → P3 → P1|

Exam trap: All four conditions are necessary in the classical model, but the presence of only one or two conditions does not prove deadlock.

# 3. Deadlock prevention

Deadlock prevention designs the system so that at least one of the four necessary deadlock conditions cannot hold.

The key idea is to break a necessary condition before a deadlock happens.

## Method 1: Prevent mutual exclusion

Make resources shareable wherever possible.

Example: Allow multiple processes to read a shared file concurrently when the file's access rules permit it.

Limitation: Some resources are inherently non-shareable, such as an exclusive device operation.

## Method 2: Prevent hold and wait

Require a process to request all needed resources before it starts, or require it to release its currently held resources before requesting new ones.

Example: A process needing R1 and R2 must obtain both before proceeding.

Disadvantage: Resources may remain allocated but unused, reducing utilization. A process may also wait longer before starting.

## Method 3: Prevent no preemption

Allow the system to take back resources under appropriate conditions.

Example: If a process holding some resources requests another unavailable resource, the system could require it to release its held resources and retry later.

Limitation: Preemption is not suitable for every resource. Some operations cannot be safely interrupted or rolled back without additional mechanisms.

## Method 4: Prevent circular wait

Impose a fixed ordering on resource types. Processes must request resources in the prescribed order.

Example: If resources have an ordering \(R_1<R_2<R_3\), every process must acquire them in increasing order.

This prevents circular wait because the system cannot form a cycle in which every process waits for a resource earlier in the ordering.

### Prevention summary

|Method|Condition broken|Main drawback|
|---|---|---|
|Make resources shareable where possible|Mutual exclusion|Not feasible for all resources|
|Request all resources together|Hold and wait|Lower utilization and reduced flexibility|
|Permit suitable resource preemption|No preemption|Not feasible for all resources|
|Enforce resource ordering|Circular wait|Can restrict resource-request order|

Exam memory trick: Prevention means breaking at least one of the four conditions.

# 4. Deadlock avoidance

Deadlock avoidance examines resource-allocation decisions and grants a request only if doing so keeps the system in a safe state.

Unlike prevention, avoidance does not necessarily eliminate one of the four conditions. Instead, it uses information about resource needs and current allocations to avoid unsafe allocations.

The classic algorithm associated with avoidance is the Banker's algorithm.

## Safe state

A system is in a safe state if there is at least one sequence of all processes such that each process can obtain its remaining required resources, finish, and release its allocated resources for the next process.

That sequence is called a safe sequence.

For example:

\[ P_2\rightarrow P_1\rightarrow P_3 \]

If P2 can finish using the currently available resources, it can release its resources when finished. Those resources can then help P1 finish, followed by P3.

## Unsafe state

An unsafe state is a state in which no safe sequence is demonstrated by the current allocation and maximum-claim model.

Important:

- Safe state: At least one safe sequence exists.
    
- Unsafe state: No safe sequence exists under the model.
    
- Deadlocked state: A deadlock actually exists.
    

An unsafe state is not necessarily already deadlocked, but it means the system cannot guarantee safe completion based on the declared maximum resource needs.

### Prevention vs avoidance

|Deadlock prevention|Deadlock avoidance|
|---|---|
|Breaks at least one necessary condition|Grants requests only when safety is preserved|
|Does not require maximum future resource claims in every approach|Classic avoidance algorithms require relevant future resource-need information|
|Restricts possible system behavior|Evaluates resource allocation dynamically|
|Example: Resource ordering|Example: Banker's algorithm|

Exam trap: Prevention breaks a condition; avoidance checks whether resource allocation is safe.

# 5. Banker's algorithm — very important

The Banker's algorithm is a deadlock-avoidance algorithm. It checks whether a resource request can be granted while keeping the system in a safe state.

It is traditionally explained using multiple resource types, each with a limited number of instances.

The analogy is a bank: the system grants a request only when it can still satisfy all customers in some safe order.

## A. Important terms

|Term|Meaning|
|---|---|
|Available|Number of currently available instances of each resource|
|Max|Maximum resources a process may need in total|
|Allocation|Resources currently allocated to a process|
|Need|Resources the process still requires to reach its declared maximum|

The most important formula is:

\[ \boxed{Need=Max-Allocation} \]

This subtraction is performed element by element for every resource type.

## B. Banker's algorithm example

Suppose there are five processes, P0 through P4, and three resource types, A, B and C.

### Allocation matrix

Resources already allocated to each process:

|Process|A|B|C|
|---|---|---|---|
|P0|0|1|0|
|P1|2|0|0|
|P2|3|0|2|
|P3|2|1|1|
|P4|0|0|2|

### Maximum-claim matrix

Maximum total resources each process may need:

|Process|A|B|C|
|---|---|---|---|
|P0|7|5|3|
|P1|3|2|2|
|P2|9|0|2|
|P3|2|2|2|
|P4|4|3|3|

### Available resources

\[ Available=(3,3,2) \]

This means 3 instances of A, 3 of B and 2 of C are currently available.

### Step 1: Calculate Need

Use:

\[ Need=Max-Allocation \]

For P0:

\[ Need_0=(7,5,3)-(0,1,0) \]

\[ Need_0=(7,4,3) \]

For P1:

\[ Need_1=(3,2,2)-(2,0,0)=(1,2,2) \]

Apply the same formula to all five processes.

### Need matrix

|Process|A|B|C|
|---|---|---|---|
|P0|7|4|3|
|P1|1|2|2|
|P2|6|0|0|
|P3|0|1|1|
|P4|4|3|1|

The Need matrix is essential for performing the safety check.

## C. Safety algorithm: find a safe sequence

Start with:

\[ Work=Available=(3,3,2) \]

`Work` is a temporary vector used to track resources available during the safety check.

A process can finish if its remaining need is no greater than Work in every resource type:

\[ Need_i\leq Work \]

When a process is assumed to finish, release its allocated resources back into Work:

\[ Work=Work+Allocation_i \]

We now check the processes one by one.

### Step 1: Can P1 finish?

\[ Need_1=(1,2,2) \]

\[ Work=(3,3,2) \]

Since P1's need is no greater than Work for every resource, P1 can finish.

After P1 finishes, release its allocation:

\[ Work=(3,3,2)+(2,0,0) \]

\[ Work=(5,3,2) \]

### Step 2: Can P3 finish?

\[ Need_3=(0,1,1) \]

This is no greater than \((5,3,2)\), so P3 can finish.

Release its allocation:

\[ Work=(5,3,2)+(2,1,1) \]

\[ Work=(7,4,3) \]

### Step 3: Can P4 finish?

\[ Need_4=(4,3,1) \]

This is no greater than \((7,4,3)\), so P4 can finish.

Release its allocation:

\[ Work=(7,4,3)+(0,0,2) \]

\[ Work=(7,4,5) \]

### Step 4: Can P0 finish?

\[ Need_0=(7,4,3) \]

This is no greater than \((7,4,5)\), so P0 can finish.

Release its allocation:

\[ Work=(7,4,5)+(0,1,0) \]

\[ Work=(7,5,5) \]

### Step 5: Can P2 finish?

\[ Need_2=(6,0,0) \]

This is no greater than \((7,5,5)\), so P2 can finish.

Release its allocation:

\[ Work=(7,5,5)+(3,0,2) \]

\[ Work=(10,5,7) \]

All five processes can finish.

### Final result

The system is in a safe state.

One safe sequence is:

\[ \boxed{P1\rightarrow P3\rightarrow P4\rightarrow P0\rightarrow P2} \]

A safe sequence need not be unique. Another valid order can also demonstrate safety.

Exam tip: If you can repeatedly find a process whose remaining Need is less than or equal to Work, finish it in the safety check, add its Allocation back to Work, and continue. If every process can finish, the state is safe.

## D. Banker's algorithm when a new request arrives

Suppose process \(P_i\) requests resource vector \(Request_i\).

The standard resource-request procedure is:

1. Check whether \(Request_i\leq Need_i\). If not, the request exceeds the declared maximum and must be rejected as invalid under the model.
    
2. Check whether \(Request_i\leq Available\). If not, the process must wait.
    
3. Temporarily allocate the requested resources:
    
    - \(Available=Available-Request_i\)
        
    - \(Allocation_i=Allocation_i+Request_i\)
        
    - \(Need_i=Need_i-Request_i\)
        
    
4. Run the safety algorithm on this tentative state.
    
5. If the state remains safe, grant the request. Otherwise, restore the previous state and make the process wait.
    

Most important rule: Banker's algorithm grants a request only when the resulting allocation is safe.

# 6. Deadlock detection

Deadlock detection allows resource requests to be granted without necessarily preventing every unsafe state in advance. The system then checks whether a deadlock has actually occurred.

There are two common textbook approaches.

## A. Resource Allocation Graph (RAG)

A resource allocation graph represents processes, resource types and their allocation or request relationships.

- Circle: Process.
    
- Rectangle: Resource type.
    
- Process → Resource: Request edge.
    
- Resource → Process: Assignment edge.
    

### Detecting cycles

For a resource allocation graph in which each resource type has exactly one instance:

- A cycle exists if and only if there is deadlock.

When resource types have multiple instances, a cycle alone is generally a necessary but not sufficient condition for deadlock.

Exam trap: Do not apply the single-instance cycle rule blindly to resources with multiple instances.

## B. Detection algorithm for multiple resource instances

For systems with multiple instances of resource types, textbook detection algorithms use information such as:

- `Available`: Resources currently available.
    
- `Allocation`: Resources allocated to each process.
    
- `Request`: Resources each process is currently waiting to obtain.
    

The algorithm conceptually searches for a process whose current Request can be satisfied by Work. It then assumes the process finishes, releases its Allocation into Work, and repeats.

If a process still cannot be marked finished after the algorithm has made all possible progress, that process may be deadlocked under the algorithm's assumptions.

### Detection vs Banker's safety algorithm

|Banker's safety algorithm|Deadlock detection algorithm|
|---|---|
|Uses remaining Need based on maximum claims|Uses current outstanding Request|
|Tests whether a safe sequence exists|Tests which processes can complete under the current state|
|Used for avoidance|Used to detect existing deadlocks|
|Requires maximum-claim information|Does not require the same maximum-claim model|

Exam trap: The two algorithms are related, but they do not answer the same question.

# 7. Deadlock recovery

After detecting a deadlock, the system needs a way to break it.

## A. Process termination

The OS can terminate processes involved in the deadlock.

Two common strategies are:

- Terminate all deadlocked processes: Simple but can discard substantial work.
    
- Terminate one process at a time: Continue until the deadlock cycle is broken.
    

Choosing a victim involves trade-offs, such as how much work will be lost, which resources it holds, and the process's priority.

## B. Resource preemption

The OS forcibly takes a resource from one process and reallocates it to another where this is safe and feasible.

Issues include:

- Selecting a victim.
    
- Rolling back the affected process if necessary.
    
- Avoiding starvation by repeatedly preempting the same process.
    

Not all resources can safely be preempted.

## C. Rollback

If the system has suitable checkpoints, it can roll a process back to an earlier state and restart it later.

Rollback may allow resources to be released and the deadlock to be broken without discarding all the work completed by every process.

### Recovery comparison

|Method|How it works|Main drawback|
|---|---|---|
|Terminate all affected processes|Removes all involved processes|High loss of work|
|Terminate one process at a time|Breaks the deadlock incrementally|Repeated checking and possible work loss|
|Resource preemption|Takes resources away from a victim|Not always feasible; rollback may be needed|
|Rollback|Restores a process to an earlier checkpoint|Requires checkpointing and may lose recent progress|

# 8. Prevention vs avoidance vs detection vs recovery

This comparison is particularly useful for DSSSB multiple-choice questions.

|Technique|Main question|Approach|
|---|---|---|
|Prevention|How can deadlock be made impossible?|Break at least one necessary condition|
|Avoidance|Is this allocation safe?|Grant requests only when safety is preserved|
|Detection|Has deadlock occurred?|Examine allocations, requests or resource graphs|
|Recovery|How do we resolve the deadlock?|Termination, preemption or rollback|

### A simple scenario

Suppose a system has two processes and two resources.

- Prevention: Make all processes request resources in one fixed global order.
    
- Avoidance: Check whether granting a request leaves a safe sequence.
    
- Detection: Examine the current requests and allocations to determine whether a deadlock exists.
    
- Recovery: Terminate a process or reclaim a suitable resource to break the deadlock.
    

Memory trick: Prevention = break a condition; avoidance = stay safe; detection = find the deadlock; recovery = break the deadlock.

# 9. Banker’s algorithm — quick numerical checklist

When solving a numerical question, work in this order:

1. Write the `Allocation`, `Max` and `Available` data.
    
2. Calculate the `Need` matrix using `Need = Max − Allocation`.
    
3. Initialize `Work = Available` and mark all processes unfinished.
    
4. Find an unfinished process whose `Need ≤ Work` for every resource type.
    
5. Assume it finishes, mark it finished, and add its Allocation to Work.
    
6. Repeat until all processes finish or no additional process can be selected.
    

If all processes finish, the state is safe and the selected order is a safe sequence. If not, no safe sequence has been found from the current state.

Important distinction: A safe state guarantees a safe completion sequence under the declared maximum claims. An unsafe state does not necessarily mean that a deadlock already exists.

## Last-minute memory trick

- Four conditions: Mutual exclusion, Hold and wait, No preemption, Circular wait.
    
- Prevention: Break at least one necessary condition.
    
- Avoidance: Keep the system in a safe state.
    
- Detection: Identify processes currently deadlocked.
    
- Recovery: Use termination, resource preemption or rollback.
    
- Banker's algorithm: Calculate `Need = Max − Allocation`, then search for a safe sequence.
    
- Safe sequence: An order in which every process can finish using currently available resources plus resources released by earlier finished processes.
    

For DSSSB, practise at least a few full Banker's algorithm numerical problems. Recognizing the definitions is useful, but being able to calculate the `Need` matrix and verify a safe sequence is the skill most likely to separate a strong answer from a guess.