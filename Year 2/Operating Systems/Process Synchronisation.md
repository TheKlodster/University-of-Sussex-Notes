*Lectures 9 & 10, Tuesday 25th February*
# Process Synchronisation

### Inter-Process Communication
--------------------------------------------------
- Processes :
	- share data and resources.
	- cooperate to work on common tasks.
- There is a need to **synchronise** activities, i.e. coordinate.
	- access to shared data and resources.
	- sequences of operations of different processes.

**Problem** : *Race Conditions* lead to inconsistent results because of how the execution of instructions may **interleave** (run concurrently). E.g. x++ or x--.

**Race Condition** : undesirable situation when a device/system attempts to performs two tasks at once - but because of the nature of the device/system, the operations must be performed one at a time to function properly.

### Communication Models
--------------------------------------------------
#### Shared Memory
- Commonly accessible memory region.
- Requires synchronisation.
- Problems : We can run into performance problems, or race conditions this way however.

#### Message Passing (MP)
- <code>send</code> and <code>receive</code> messages.
- Synchronisation is implicit!

Support by OS kernel e.g. POSIX SHM, pipes <code>|</code>, RPC, sockets, MPI...

### Critical Section
--------------------------------------------------
Any solution must ensure one of the following :
- **Mutual Exclusion** - if a process is executing in its critical section, then other processes must not execute in their critical section.
- **Progress** (prevent *deadlock*) - if no process is executing in its critical section and some processes wish to enter their critical sections, then the selection of which process may enter cannot be postponed indefinitely.
- **Bounded Waiting** (prevent *starvation*) -iIf a process wishes to enter the critical section then only a bounded number of processes may enter the critical section before it.

Running <code>x++</code> and <code>x--</code> simultaenously is bad.

**Busy Waiting** : a process in a loop running, doing actively nothing.
- Can be found in deadlock or livelock situations.

**Deadlock** : a state in which each member of a group of actions is waiting for some other member to release a lock. <br>
**Livelock** : states of the processes involved in the livelock constantly change with regard to one another, none progressing - a special case of resource starvation.
### Solutions
--------------------------------------------------
- Software.
	- assume atomicty of read and write operations.
- Hardware-supported.
	- more powerful instructions (e.g. test-and-set).
- Higher-level APIs.
	- wrap low-level primitives into library :
		- semaphores, monitors, condition variables etc...
	- thread-safe data structures :
		- blocking queues, synchronised maps etc...

#### Software Solutions
- **Busy Waiting** :
```
while(condition) {
	/* do nothing */
}
```

#### Hardware-Supported Solutions
**Interrupt Disabling**
- Protect low-level instruction sequences in kernel.
- Suitable for user processes?
- Suitable in multi-core processes?

**Test-and-Set** <br>
**Compare-and-Swap** <br>
**Compare-and-Exchange** <br>

### Condition Synchronisation
--------------------------------------------------
Ensure processes perform actions in desired order. <br>
- Example : data transfer from prcess P<sub>1</sub> to P<sub>2</sub>.
	- P<sub>1</sub> writes to shared memory, P<sub>2</sub> reads it.
	- **Goal** : avoid duplication or loss of data.
- E.g. using <code>wait()</code> and <code>notify</code> in java.

#### Bakery Algorithm
How it works :
1. Customers draw a ticket as they arrive.
1. Ticket has a number that indicates your priority as a customer.
1. In OS, the processes are the customers.

### Synchronisation Primitives
--------------------------------------------------
Synchronisation algorithms tend to be tricky to implement.
- Do not re-implement them in a user program.
- Use the synchronisation primitives provided by the OS.
- Usually better performance : *blocking* instead of *busy waiting*.

#### Mutex
- Data Structure : boolean <code> m</code>
- Operations :
	- <code>aquire(m)</code> : process blocks until <code>m</code> is false, then sets to true.
	- <code>release(m)</code> : sets <code>m</code> to false.

E.g. PThreads :
- <code> int pthread mutex lock(pthread mutex t * mutex);</code>

#### Semaphore
- Generalisation of a mutex : allows <code>n</code> processes to access a resource.
- Data structure : <code>int c</code> (intialised to <code>n</code>), <code>queue q</code>.
- Operations :
	- <code>aquire()</code> : process blocks if <code>c = 0</code> and is added to <code>q</code>, other decrement <code>c</code>.
	- <code>release()</code> : remove a process from <code>q</code> and unblock it if <code>q</code> is non-empty, otherwise increment <code>c</code>

Application example : license server for software applications. <br>
Java :
- <code>Semaphore(int permits, boolean fair)</code>
- <code>void aquire(int permits)</code>
- <code>void release(int permits)</code>

#### Producer-Consumer Problem
Synchronisation algorithms tend to be tricky to implement.

- *Producer* : generates data.
- *Consumer* : reads data.

Bounded Buffer (Ring buffer) :
- Producer waits for consumer to read data if buffer is full.
- Consumer waits until data is available if buffer is empty.

#### Memory Passage
Data Structure : queue.

Operations :
- <code>send</code> : blocks until the message has been received by the receiver.
- <code>receive</code> : blocks until a message has been received.

#### Transactional Memory
Data Structure : undo logs.

- <code>start transaction</code> : starts a transaction.
- <code>commit transaction</code> : returns true if the transaction succeeded, otherwise rolls back the changes.

Important for scenarios like bank transfers.

#### Condition Variable, Monitor
Condition Variable :
- <code>await(c, v)</code> : blocks until <code>c = v</code>
- <code>signal(c, v)</code> : sets <code>c</code> to value <code>v</code>

Monitor : abstract data type that provides mutual exclusion.
- Encapsulates variables : only access from monitor functions.
- Monitor functions only executed by one process at a time.

Java :
- Monitor function qualified <code>synchronized</code>
- Boolean condition variable : <code>wait</code>,<code>notify</code>

#### Event Count
Useful if you a process relies on periodic behaviour.

#### Sequencer
Solves the bakery algorithm issue. Nobody can draw the same number.
- Data structure : <code>int s</code>
- <code>ticket(s)</code> : returns <code>s</code> and increments <code>s</code>
