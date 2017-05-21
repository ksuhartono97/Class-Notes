# Concurrency Control

## Lock Based Control

Ultimate purpose of this is to generate a schedule that is conflict serializable without having to be checked first (there is a certainty or guarantee of safety).

### From the example

Data manager assumes that there is nothing else requesting B so the lock manager is able to grant the X lock for B. After finish, since there is nothing else using X lock for B, just release.

Repeat the same system for A, lock manager issues the lock only if there is nothing else requesting A.

The protocol that needs to be ensured when designing a lock manager, is how do we **grant** and **release** locks when requested.

> Note that the example is incorrect currently because the lock and unlock process causes a different result than what should be the answer.

The locking and unlocking mechanism is correct, but why does this issue still happen? Because we can see from the processes, there is still some computation that needs to be done in A, but we already let the T2 transaction do what it wants. Causing the displayed value to be wrong because we haven't done an operation on A's value.

So this shows that when making these transaction rules, we can't simply arbitrarily grant locks. We have a need for **locking protocols**, which are sets of rules that needs to be obeyed by all transactions in the process of granting and releasing locks. This is to ensure the result of the process is conflict serializable.

### The 2PL (Two Phase Locking) protocols

A Protocol that ensures conflict serializable schedules:

- Growing Phase : may obtain locks, **should not** release locks
- Shrinking Phase : may release locks, **should not** obtain locks

A schedule is executed by 2PL implies that the generated schedule would be conflict serializable, but the opposite is not true.

#### Deadlocks

Neither transactions can progress because a requested lock is being held by the other transaction, and the other transaction is requesting a lock from the first transaction.

#### Starvation

A transaction kept on getting rolled back because multiple transactions keep on coming requesting the S lock (while the original transaction requests for an X lock). Causing this one transaction to keep getting rolled back and being unable to progress.

### Lock Conversions

Allows upgrading of locks from shared locks to exclusive locks, and also downgrading locks from exclusive locks to shared locks.

### Strict 2PL

To prevent cascading rollback, by saying that a transaction must hold all its exclusive locks till it commits/aborts.

Theres even **rigorous** 2PL, that forces **all** locks that are held to be held till commit/abort.

## Deadlock recovery

Choose a victim to roll back that will incur minimum cost. But it can cause starvation if a certain victim is always chosen. A solution to this is to keep a number of maximum rollbacks.
