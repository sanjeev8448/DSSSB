## 1. What is a transaction?

A transaction is a logical unit of work consisting of one or more database operations that should be executed as a single unit.

For example, transferring ₹1,000 from Account A to Account B requires two operations:

1. Deduct ₹1,000 from Account A.
    
2. Add ₹1,000 to Account B.
    

If the money is deducted from A but not credited to B, the database becomes inconsistent. A transaction helps ensure that both operations succeed together or the transfer is undone.

### Example: Bank transfer

Initial balances

Account A

### ₹5,000

Account B

### ₹2,000

Transfer ₹1,000 from A to B

Final balances after successful COMMIT

Account A

### ₹4,000

Account B

### ₹3,000

Example SQL transaction:

```

START TRANSACTION;

UPDATE Accounts
SET Balance = Balance - 1000
WHERE AccountID = 'A';

UPDATE Accounts
SET Balance = Balance + 1000
WHERE AccountID = 'B';

COMMIT;
```

The example assumes both accounts exist and the transaction completes successfully. If an error occurs before commitment, the application or DBMS can roll back the transaction as appropriate.

## 2. ACID properties — extremely important

ACID stands for:

- A — Atomicity
    
- C — Consistency
    
- I — Isolation
    
- D — Durability
    

These properties help ensure reliable transaction processing.

# A

Atomicity — All or nothing

A transaction's operations succeed as a unit, or its effects are rolled back when the transaction fails.

Example: Money must not be permanently deducted without being credited to the recipient.

# C

Consistency — Valid state to valid state

A committed transaction must preserve the database's defined integrity constraints.

Example: A transfer preserves the total balance if there are no fees or other adjustments.

# I

Isolation — Concurrent transactions behave appropriately

Concurrent transactions should be isolated according to the selected isolation level, preventing unwanted interference.

Example: Two users updating the same account should not cause a lost update.

# D

Durability — Committed changes persist

Once a transaction is committed, its changes should survive system failures, subject to the DBMS's durability guarantees.

Example: A successfully completed bank transfer is not lost merely because the database server restarts.

### ACID memory trick

|Property|Ask yourself|
|---|---|
|Atomicity|Did everything succeed, or was it undone?|
|Consistency|Were database rules preserved?|
|Isolation|Did concurrent transactions interfere improperly?|
|Durability|Will committed changes persist?|

Common exam traps:

- All-or-nothing = Atomicity.
    
- Integrity constraints = Consistency.
    
- Concurrent execution = Isolation.
    
- Permanent committed changes = Durability.
    

## 3. COMMIT

`COMMIT` completes a transaction successfully and makes its changes permanent according to the DBMS's transaction guarantees.

Example:

```

START TRANSACTION;

UPDATE Accounts
SET Balance = Balance - 500
WHERE AccountID = 'A';

COMMIT;
```

After a successful `COMMIT`, the transaction cannot ordinarily be undone using a simple `ROLLBACK` of that completed transaction. Reversing it generally requires another transaction or a recovery mechanism.

Remember: COMMIT = Accept and finalize the transaction's changes.

## 4. ROLLBACK

`ROLLBACK` undoes uncommitted changes made by the current transaction, returning the database state to an appropriate earlier transaction state.

Example:

```

START TRANSACTION;

UPDATE Accounts
SET Balance = Balance - 500
WHERE AccountID = 'A';

ROLLBACK;
```

The deduction is undone if it was part of the current uncommitted transaction and the DBMS supports the expected transaction behavior.

Remember: ROLLBACK = Undo uncommitted transaction changes.

### COMMIT vs ROLLBACK

|Feature|COMMIT|ROLLBACK|
|---|---|---|
|Purpose|Finalizes changes|Undoes uncommitted changes|
|Effect|Changes persist|Changes are reverted|
|Typical use|Successful operation|Error or cancellation|
|After completion|Simple rollback of that transaction is no longer available|Transaction returns to an earlier state|

Note: Exact SQL transaction behavior, including implicit commits, savepoints, and DDL handling, varies by DBMS.

## 5. Transaction states

A transaction may pass through several states.

Active

Operations are executing

Partially Committed

Last operation executed

Committed

Successful completion

Active / Failed

Aborted

Effects undone

Other important terms:

- Failed: The transaction cannot continue, perhaps due to an error or system failure.
    
- Aborted: Its effects have been undone.
    
- Terminated: The transaction has finished and leaves the transaction processing lifecycle.
    

Exam point: A transaction that has executed its final statement is not necessarily committed yet.

## 6. Concurrency in DBMS

Concurrency means multiple transactions execute during overlapping periods of time.

For example, two users try to book the last available seat at nearly the same time. Without proper control, both may see the seat as available and attempt to book it.

Concurrency improves throughput and resource utilization, but it can create problems if transactions interfere with each other.

### Common concurrency problems

A. Lost update

Two transactions read the same old value and update it. One transaction's update overwrites the other's.

Suppose the balance is ₹1,000.

|Step|Transaction T1|Transaction T2|
|---|---|---|
|1|Reads ₹1,000||
|2||Reads ₹1,000|
|3|Adds ₹200, calculates ₹1,200||
|4||Subtracts ₹100, calculates ₹900|
|5|Writes ₹1,200||
|6||Writes ₹900|

The final balance becomes ₹900. T1's update is lost. A properly designed concurrent transaction scheme prevents this kind of unintended overwrite.

B. Dirty read

A transaction reads a value written by another transaction that has not yet committed.

If the writer later rolls back, the reader has used a value that was never committed.

C. Non-repeatable read

A transaction reads the same row twice but gets different values because another transaction updated and committed that row between the reads.

D. Phantom read

A transaction repeats a query that returns a set of rows and sees new or missing rows because another transaction inserts, deletes, or modifies rows in a way that changes the query result.

Example: A transaction queries employees with salary above ₹50,000 twice and sees an additional qualifying employee the second time.

### Comparison table

|Problem|Main idea|
|---|---|
|Lost update|One update overwrites another|
|Dirty read|Reading uncommitted data|
|Non-repeatable read|Same row read twice, different values|
|Phantom read|Same predicate query returns a different set of rows|

Exam trap: Dirty read concerns uncommitted data. Non-repeatable read concerns the value of an existing row. Phantom read concerns rows matching a query condition.

## 7. Locks in DBMS

A lock is a concurrency-control mechanism used to restrict access to a data item while a transaction operates on it.

Locks help prevent conflicting operations and maintain isolation.

### A. Shared lock (S-lock)

A shared lock is generally used when a transaction wants to read data.

- Multiple transactions can hold shared locks on the same item at the same time.
    
- While shared locks are held, a conflicting exclusive lock cannot be granted.
    

Example: Two users can read the same account balance simultaneously.

### B. Exclusive lock (X-lock)

An exclusive lock is generally required when a transaction wants to write or update data.

- Only one transaction can hold an exclusive lock on a particular item at a time.
    
- It conflicts with both shared and exclusive locks held by other transactions.
    

Example: A transaction updating an account balance needs write access that conflicts with another transaction's read or write lock on that item.

### Shared vs exclusive lock

|Feature|Shared lock (S)|Exclusive lock (X)|
|---|---|---|
|Main purpose|Read|Write/update|
|Multiple holders on the same item|Allowed for shared locks|Not allowed concurrently|
|Compatible with another S-lock|Yes|No|
|Compatible with another X-lock|No|No|
|Compatible with another transaction's S-lock|Yes|No|

### Lock compatibility matrix

The following matrix shows whether two different transactions' locks can coexist on the same data item:

|Existing lock|Requested S-lock|Requested X-lock|
|---|---|---|
|S-lock|Compatible|Not compatible|
|X-lock|Not compatible|Not compatible|

Memory trick: S-S = allowed; S-X, X-S and X-X = conflict.

## 8. Two-Phase Locking (2PL)

Two-Phase Locking is a locking protocol used to ensure conflict serializability.

It has two phases:

1. Growing phase: The transaction can acquire locks but cannot release locks.
    
2. Shrinking phase: The transaction can release locks but cannot acquire new locks.
    

A transaction's lock point is the point at which it acquires its final lock.

Important distinctions:

- Basic 2PL guarantees conflict serializability under the usual protocol assumptions.
    
- Basic 2PL does not by itself guarantee freedom from deadlocks.
    
- Strict 2PL holds exclusive locks until commit or abort, preventing other transactions from reading or overwriting uncommitted writes.
    
- Rigorous 2PL holds both shared and exclusive locks until commit or abort.
    

These distinctions can appear in more advanced MCQs.

## 9. Deadlock

A deadlock occurs when two or more transactions wait indefinitely for locks held by one another, so none of them can proceed.

Example:

- T1 holds a lock on resource A and waits for resource B.
    
- T2 holds a lock on resource B and waits for resource A.
    

T1

Holds A

T2

Holds B

Waits for B

Waits for A

Circular wait → Deadlock

### Deadlock handling methods

- Prevention: Design the protocol to make at least one necessary deadlock condition impossible.
    
- Avoidance: Grant resources only when a safe state can be maintained.
    
- Detection and recovery: Detect deadlocks, then abort or roll back selected transactions to break the cycle.
    
- Timeout: Treat sufficiently long waiting as a potential deadlock and take corrective action, although this can sometimes abort a transaction that was merely slow.
    

A wait-for graph helps detect deadlocks: a cycle indicates a deadlock under the usual single-instance resource assumptions.

## 10. Quick revision table

| Topic          | Must remember                                        |
| -------------- | ---------------------------------------------------- |
| Transaction    | Logical unit of database work                        |
| Atomicity      | All or nothing                                       |
| Consistency    | Preserve integrity rules                             |
| Isolation      | Control interference between concurrent transactions |
| Durability     | Committed changes persist                            |
| COMMIT         | Finalize transaction changes                         |
| ROLLBACK       | Undo uncommitted changes                             |
| Concurrency    | Overlapping execution of transactions                |
| Shared lock    | Read lock; shared locks can coexist                  |
| Exclusive lock | Write lock; conflicts with other locks               |
| 2PL            | Growing phase followed by shrinking phase            |
| Deadlock       | Transactions wait in a cycle                         |
Last-minute memory trick: ACID = All-or-nothing, Consistency, Isolation, Durability. COMMIT saves; ROLLBACK undoes uncommitted changes. Shared locks allow shared reads; exclusive locks block conflicting access.