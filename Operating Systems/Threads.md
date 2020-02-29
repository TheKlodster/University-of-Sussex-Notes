*Lecture 4 & 5 Thursday 6th, Tuesday 11th*
# Threads
Many processes can be disadvantageous due to process management and resource allocation overheads. A thread is a unit for **scheduling only**.
- Thread Control Block : Thread ID, state, context.

Threads are more likght-weight than processes. They can access process resources. We can have multiple threads at a relatively low expense! :)

#### Single & Multi-Threaded Processes
Threads enable processes to maintain multiple threads of control, whilst maintaining information - registers, stack memory.

**Multiple Threads on Multiple Cores** :
- benefits of multi-threading are amplified.
	- single-threaded processes can only run on a single CPU core, even if 15 others are available.
- thread can run in parallel on different cores.
- multi-threading on multi-core computers increases concurrency.
	- single-core CPUs effectively switch between threads as if they were processes.


### Advantages of Threads
- Lightweight Management
	- creation.
	- context-switching.
	- termination.
- Lightweight Communication
	- shared resources within the same address space.
	- direct communication within the process.
- Application Responsiveness
	- user requests have less impact on execution performance.
	- expensive computation can run separately.
		- e.g. a web server: a popular software is getting an update, and everyone wants this update now. The owners could assign a thread to those requesting that update so they don't have other threads interfering with eachother about this issue.

### Thread States
1. **Ready** - waiting for execution.
1. **Running** - executing code.
1. **Blocked** - waiting for something to happen, I/O.

What happens to a thread when a process is suspended / terminates? <br>
The thread is effected, it is usually also suspended.

## Thread Implementations
#### User-Level Threads
Implemented as a user-space threading library. It handles :
- creation and termination of threads.
- thread communication.
- thread scheduling.
	- OS cannot interfer with the scheduling, so if something goes wrong, uh-oh.
- saving and restoring thread contexts.
- invisible to the kernel, and OS-agnostic.
- thread switching happens in user mode.
- when a thread is blocked, the entire process is blocked.
- multi-core execution is not possible.

#### Kernel-Level Threads
- provided by kernel.
- thread switching.
- thread-wise scheduling.
- thread-wise blocking.
- threads of the same process can execute on different cores.
- but: more management effort, any thread switch requires mode switching.

#### Example Threading Libraries
- POSIX Pthreads extension (user- or kernel-level)
- Windows thread lib (kernel-level)
- Java lib/ JVM -> mapping to native threading model through virtual machine.

#### Implicit Threading
Resources are not infinite! So Implicit Threading is key! Better management with *thread* pools.

1. Threads are created in advance - *job consumers*.
1. Incoming requests - *job providers* - are scheduled - *job queue*.
1. If a request arrives, a worker is activated.
1. Once a request has been serviced, the worker goes back to waiting.

##### Advantages
1. Less overhead
	- threads do not need to be created and terminated on the fly, leading to  overall faster response times.
1. Risk of Exhausting the system is low.
	- number of workers is predetermined.
1. Job Consumers can be flexible.
1. Small overhead = more flexibility in how jobs are serviced.

