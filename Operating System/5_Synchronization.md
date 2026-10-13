## 1. What is synchronization?

Process synchronization is the coordination of concurrent processes or threads to ensure that shared resources are accessed safely and operations occur in an appropriate order.

Synchronization is important when multiple execution flows access shared resources, such as:

- Shared variables in memory.
    
- Bank-account balances.
    
- Shared files.
    
- Buffers used by producer and consumer threads.
    
- Database records.
    

### Example: Shared counter

Suppose two threads access a shared variable:

```
int counter = 0;
```

Both threads execute:

```
counter = counter + 1;
```

You might expect the final value to be `2`. However, incrementing a counter usually involves multiple steps: reading the value, calculating a new value, and writing it back.

One possible interleaving is:

|Step|Thread T1|Thread T2|Counter|
|---|---|---|---|
|1|Reads 0||0|
|2||Reads 0|0|
|3|Calculates 1||0|
|4||Calculates 1|0|
|5|Writes 1||1|
|6||Writes 1|1|

The final counter is `1`, rather than `2`.

This is an example of a race condition.

# 2. Critical section

A critical section is the part of a program in which shared data or a shared resource is accessed in a way that requires coordinated access.

For example, the following operation may need protection if `counter` is shared across threads:

```
counter = counter + 1;
```

Without appropriate synchronization, concurrent executions may interfere with one another.

## Structure of a process with a critical section

A process can be represented conceptually as four sections:

1. Entry section

Requests permission to enter

2. Critical section

Accesses shared data or resources

3. Exit section

Releases access permission

4. Remainder section

Performs other work

### Requirements of a correct critical-section solution

Three classical requirements are especially important.

1. Mutual exclusion

At most one process or thread can execute the protected critical section for a particular shared resource at a time.

2. Progress

If no one is executing the critical section and some processes want to enter, the decision about who enters next should not be postponed indefinitely by processes that are not competing to enter.

3. Bounded waiting

After a process requests entry, there must be a bound on how many times other processes can enter before it gets its turn.

These are the classical requirements used in operating-system synchronization theory.

### Exam memory table

|Requirement|Key idea|
|---|---|
|Mutual exclusion|Only one at a time|
|Progress|Do not postpone a valid entry decision indefinitely|
|Bounded waiting|Prevent indefinite overtaking|

Exam trap: Mutual exclusion alone does not guarantee fairness. A process could still wait indefinitely if the synchronization method permits starvation.

# 3. Race condition

A race condition occurs when the result of concurrent operations depends on the timing or interleaving of those operations, and that dependence can produce an incorrect or unintended outcome.

It often occurs when multiple threads access shared mutable data without adequate synchronization.

### Example: Bank balance

Suppose the balance is ₹1,000. Two operations happen concurrently:

- T1 withdraws ₹200.
    
- T2 withdraws ₹300.
    

If each operation reads the old balance before either writes its updated balance, both may calculate from ₹1,000.

|Operation|T1|T2|
|---|---|---|
|Read balance|₹1,000|₹1,000|
|Calculate new balance|₹800|₹700|
|Write balance|₹800|₹700|

If T2 writes last, the final balance becomes ₹700, even though the two withdrawals total ₹500 and the expected balance is ₹500.

The correct final balance should be:

\[ 1000-200-300=\boxed{500} \]

This is a lost update caused by an unsafe interleaving.

### How can a race condition be prevented?

Use an appropriate synchronization mechanism, such as:

- A mutex to protect a shared counter or balance.
    
- A semaphore to control access to shared resources.
    
- Atomic operations for suitable simple operations.
    
- Other concurrency-control mechanisms appropriate to the problem.
    

Important distinction: A race condition is the problem; a mutex or semaphore may be part of the solution.

# 4. Semaphore

A semaphore is a synchronization mechanism that uses a counter and atomic operations to control access to resources or coordinate processes and threads.

The two classical operations are:

- Wait (P / down): Attempts to acquire a resource or decrease the semaphore count.
    
- Signal (V / up): Releases a resource or increases the count, potentially waking a waiting process.
    

The operations must be implemented atomically so that concurrent callers cannot corrupt the semaphore's state.

## Types of semaphores

### A. Binary semaphore

A binary semaphore has two logical values, commonly `0` and `1`.

It can be used for signaling or for controlling access to a single resource.

Example: A binary semaphore initialized to `1` can allow one execution flow at a time to acquire the associated permission.

```
Semaphore S = 1

wait(S)
    critical section
signal(S)
```

In this simplified pseudocode, `wait()` acquires the permission and `signal()` releases it.

### B. Counting semaphore

A counting semaphore tracks multiple available resource instances.

Suppose there are three identical printers available. A counting semaphore initialized to 3 can represent their availability.

```
Semaphore printers = 3

wait(printers)
    use one printer
signal(printers)
```

At most three successful acquisitions can be outstanding at once, assuming each user correctly releases its permit.

### Example: Counting semaphore values

Start with:

\[ S=3 \]

Three processes acquire permits:

\[ 3\rightarrow2\rightarrow1\rightarrow0 \]

At this point, no free permits remain. An additional `wait(S)` must block or otherwise wait according to the semaphore implementation.

When one process signals the semaphore, a permit becomes available and a waiting process may proceed.

### Semaphore vs critical section

A semaphore is a mechanism used to coordinate access; a critical section is the protected part of the program.

|Term|Meaning|
|---|---|
|Critical section|Code accessing shared state or a resource|
|Semaphore|Synchronization primitive that can control entry or coordinate events|
|`wait()`|Acquires a permit or waits|
|`signal()`|Releases a permit or signals availability|

Exam trap: A semaphore is not limited to 0 and 1. A counting semaphore can represent multiple identical resources.

# 5. Mutex

A mutex (mutual exclusion lock) is a synchronization primitive used to ensure that only one thread at a time holds a particular lock and enters the associated protected section.

A typical mutex has two main operations:

- Lock / acquire: Obtain the lock, waiting if another thread owns it.
    
- Unlock / release: Release the lock so another waiting thread can acquire it.
    

### Example: Protect a shared counter

```
lock(mutex);

counter = counter + 1;

unlock(mutex);
```

Conceptually, this ensures that the shared counter update is protected from competing threads, assuming all accesses that require protection use the same mutex and the operations are correctly implemented.

### How does a mutex solve the race condition?

Without a mutex, two threads may both read the same old value before either writes an update.

With a mutex:

1. T1 acquires the mutex.
    
2. T1 reads and updates the counter.
    
3. T1 releases the mutex.
    
4. T2 acquires the mutex.
    
5. T2 performs its update based on the current counter value.
    
6. T2 releases the mutex.
    

Now, the protected read-modify-write operations cannot overlap.

### Important mutex properties

- A mutex is intended primarily for mutual exclusion.
    
- It commonly has an ownership rule: the thread that locks it is the one expected to unlock it.
    
- A thread may block when it attempts to acquire an already-held mutex.
    
- Incorrect locking can cause deadlocks or starvation.
    
- All relevant access paths must be synchronized; a mutex does not automatically protect data that other code accesses without it.
    

Exam trap: A mutex is not simply another name for every kind of semaphore. Mutex ownership and the intended locking protocol distinguish it from a general semaphore.

# 6. Mutex vs semaphore — very important comparison

This is one of the most common synchronization comparison questions.

|Feature|Mutex|Semaphore|
|---|---|---|
|Main purpose|Mutual exclusion|Resource counting or event coordination|
|State|Typically locked or unlocked|Counter representing permits or state|
|Ownership|Usually owned by the thread that locks it|General semaphore signaling typically has no mutex-style ownership rule|
|Operations|Lock and unlock|Wait and signal|
|Resource count|Usually protects one critical section at a time|Counting semaphore can represent multiple available resources|
|Common example|Protect a shared variable|Manage a pool of three printers|
|Typical misuse|Forgetting to unlock or using the wrong ownership protocol|Incorrect wait/signal count or signaling at the wrong time|

### Can a binary semaphore act like a mutex?

A binary semaphore initialized to 1 can be used to restrict access to one resource at a time. This gives it similar mutual-exclusion behavior, but it is not identical to a mutex in every implementation.

Remember for MCQs:

- Mutex → ownership-based locking in typical designs.
    
- Binary semaphore → a semaphore whose state has two logical values.
    
- Counting semaphore → represents multiple available permits.
    
- Semaphore → can also be used for signaling and coordination between execution flows.
    

# 7. Synchronization and the producer-consumer problem

The producer-consumer problem is a classic synchronization problem.

- A producer generates data and places it into a shared buffer.
    
- A consumer removes data from that buffer.
    
- The producer must not insert data when the buffer is full.
    
- The consumer must not remove data when the buffer is empty.
    
- Access to the buffer's shared state must be coordinated.
    

Consider a buffer with three available slots.

A conventional semaphore solution uses:

- `mutex = 1` to protect buffer access.
    
- `empty = 3` to count empty slots.
    
- `full = 0` to count occupied slots.
    

### Producer pseudocode

```
produce(item)

wait(empty)
wait(mutex)

insert item into buffer

signal(mutex)
signal(full)
```

### Consumer pseudocode

```
wait(full)
wait(mutex)

remove item from buffer

signal(mutex)
signal(empty)

consume(item)
```

### What does each semaphore do?

|Semaphore|Initial value|Purpose|
|---|---|---|
|`mutex`|1|Protects shared buffer operations|
|`empty`|Buffer capacity|Counts available slots|
|`full`|0|Counts occupied slots|

The order is important: the producer obtains an empty-slot permit before entering the protected buffer section, while the consumer obtains an occupied-slot permit.

This is classical pseudocode. A real implementation also needs careful handling of errors, interruption and shutdown.

Exam trap: The producer-consumer problem involves both mutual exclusion and condition synchronization. A mutex alone does not tell the producer whether a buffer slot is available.

# 8. Other synchronization problems and hazards

## A. Deadlock

A deadlock occurs when processes or threads are stuck waiting for resources or events that cannot become available because of their mutual dependencies.

Example:

- T1 locks resource A and waits for B.
    
- T2 locks resource B and waits for A.
    

Neither can continue until the situation is resolved.

## B. Starvation

Starvation occurs when a process or thread waits indefinitely because the system repeatedly favors other execution flows.

For example, a thread might repeatedly fail to acquire a lock because other threads acquire it first.

## C. Busy waiting

Busy waiting occurs when an execution flow repeatedly checks whether a condition or lock is available instead of sleeping or blocking.

Busy waiting can waste CPU time, though spinlocks can be useful when critical sections are very short and blocking would cost more.

## D. Priority inversion

Priority inversion occurs when a high-priority task is delayed because a lower-priority task holds a resource it needs. The issue can become worse if medium-priority tasks prevent the lower-priority owner from running and releasing the resource.

A common mitigation is priority inheritance, where the resource owner temporarily inherits a higher priority.

### Quick comparison

|Problem|Meaning|
|---|---|
|Race condition|Outcome depends on unsafe interleaving|
|Deadlock|Execution flows wait in a circular or otherwise unresolvable dependency|
|Starvation|A process waits indefinitely due to unfair access|
|Busy waiting|Repeatedly checking a condition consumes CPU time|
|Priority inversion|A high-priority task is delayed by resource ownership involving lower-priority work|

# 9. Final exam revision sheet

|Topic|One-line definition|
|---|---|
|Synchronization|Coordinates concurrent access and execution|
|Critical section|Code accessing shared data that requires coordinated access|
|Mutual exclusion|At most one execution flow in a protected section|
|Race condition|An unsafe timing-dependent outcome|
|Semaphore|Counter-based coordination mechanism|
|Binary semaphore|Semaphore with two logical states|
|Counting semaphore|Semaphore representing multiple permits|
|Mutex|Ownership-based mutual-exclusion lock in typical designs|
|`wait()` / P|Acquires a permit or waits|
|`signal()` / V|Releases a permit or signals|
|Producer-consumer|Coordinates buffer access and availability|
|Deadlock|Unresolvable waiting dependencies|
|Starvation|Indefinite or excessive waiting due to unfair allocation|
|Busy waiting|Repeated checking rather than blocking|
|Priority inversion|High-priority work is delayed by lower-priority resource ownership|
## Last-minute memory trick

- Critical section: Protected shared-resource code.
    
- Race condition: Wrong outcome due to unsafe timing/interleaving.
    
- Semaphore: Coordinates through permits and wait/signal operations.
    
- Mutex: Mutual-exclusion lock, usually with ownership.
    
- Mutual exclusion: One at a time.
    
- Progress: Do not postpone a valid entry decision indefinitely.
    
- Bounded waiting: Prevent indefinite overtaking.
    
- Deadlock: Waiting dependencies prevent progress.
    
- Starvation: A thread keeps getting denied a chance to proceed.
    
- Producer-consumer: Coordinate both access to the buffer and available/occupied slots.
    

The most important distinction to remember for DSSSB is: a critical section is the code being protected, a race condition is the problem, and a mutex or semaphore is a possible synchronization mechanism.