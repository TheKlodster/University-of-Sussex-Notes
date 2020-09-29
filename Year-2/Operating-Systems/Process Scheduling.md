*Lecture 6 Thursday 11th, 7 Monday 18th February*
# Process Scheduling
If you are running multiple threads concurrently, we face a **decision problem** - what to do first, second, third and what to switch back to?


This **determines** the execution order of processes.

<center>

<img src="https://thezeroalpha.github.io/os-notes/Scheduling.resources/09C0D52D-0C2A-4E90-BF83-3EA6ACFC8CAC.png">

</center>

**CPU-Bound process** - process that uses CPU for prolonged time. <br> 
**I/O-bound process** - short CPU burst/process e.g. a key press 

<center>

#### CPU Burst - an I/O bound process visualised.
<img src="https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/images/Chapter6/6_02_CPU_Histogram.jpg">

A key press ^
</center>


#### Long-term Scheduling
General admission of a process to be scheduled by the process of execution. <br>
Allow or prevent a process to be admitted for scheduling. <br>

### Short-term Scheduling
**Scheduler** : selects process from *Ready* queue. <br>
**Dispatcher** : performs the context switch. <br>
**Non-preemptive** : the current process retains a hold over the CPU until returning control. The burst will not be interrupted. <br>
**Preemptive** : scheduler takes control of the CPU even though the current process should continue executing. <br>

When is scheduling happening?
- after process creation.
- after ISR completion.
- a process blocks (I/O request, synchronisation, ...)
- at end of time slice - length of time accessing the CPU.
- after process termination.
- on a yield system call (voluntary release of CPU).

<center>

<b>utilisation = 1 - p<sup>n</sup></b>

</center>

- **p** is the fraction of time provesses spend waiting for I/O.
- <sup>**n**</sup> is the number of processes.
- This model assumes independent processes.

### Scheduling Criteria
--------------------------------------------------
- **CPU Utilisation** - % of time the CPU is busy.
- **Throughput** - processes per second handled.
- **Turnaround Time** - time from submission completion.
- **Waiting Time** - time processes spend in the *Ready* queue.
- **Response Time** - time from submission to the first response (interactive systems).
- **Meeting Deadlines** - operating within the required time constraints (real-time systems).
- **Predictability** - avoiding erratic behaviour that needs frequent correction.
- **Fairness** - every process gets a turn.
- **Balance** - all system components well-used, not just the CPU.
- **Policy Enforcement** - some things are more important than others (e.g. make sure critical processes can run when needed).

Which criteria is most important depends on what system you are talking about.

### Scheduling Algorithms
--------------------------------------------------
#### First-Come First-Served (FCFS)
Literally first process to arrive, is the first to get served. <br>

Simple Implementation technique + <br>
Long average waiting times -

#### Shortest Job First (SJF)
The shortest CPU burst first.

It is optimal : minimal average waiting time + <br>
CPU burst time information necessary, scheduler doesn't know this - (will need a good mechanism for predicting!)<br> 

<center>

Prediction by Exponential Averaging

<b>T<sub>n + 1</sub> = a * t<sub>n</sub> + (1 - a) * T<sub>n - 1</sub></b>

</center>

#### Shortest Remaining Time First (SRT)
Preemptive version of SJF.

#### Priority Scheduling (PS)
Lowest number is the highest priority. <br>
Processes with the same priority scheduled FCFS. <br>
Implementation : *priority queue*.

Starvation is possible!! i.e. indefinite waiting - <br>
To avoid through **aging** procedure : gradually increasing priority as their waiting time increases.

#### Round Robin (RR)
FCFS & preemption at the end of time splice (time quantum). <br>
Implementation : FIFO queue + Timer Interrupt

Can choose a good time quantum by looking at the **turnaround time**. If it yields a low turnaround time, it qualifies as a better time quantum.

---
Scheduling algorithm needs to be fair to **avoid starvation**.

---
### Performance of Scheduling Policies

|  | First-Come-First-Served | Shortest Job First | Shortest Remaining Time | Round Robin |
|------------------------|----------------------------|---------------------------|-----------------------------------|--------------------------|
| **Selection Function** | Maximum waiting time. | Minimum execution time. | Minimum remaining execution time. | Maximum waiting time. |
| **Decision Mode** | Non-preemptive. | Non-preemptive. | Preemptive. | Time-Quantum-preemptive. |
| **Overhead** | Very small. | Can be high. | Can be high. | Very small / small. |
| **Fairness** | Penalises short processes. | Penalises long processes. | Penalises long processes. | Fair. |
| **Starvation** | No. | Possible. | Possible. | No. |
| **Throughput** | Variable. | High. | High. | Depends on time quantum. |
| **Waiting Time** | Can be high. | Good for short processes. | Better than SJF. | Depends on time quantum. |

#### Round Robin - Another Look
**Quantum too large** : scheduling degenerates and works like FCFS. <br>
**Quantum too short** : too many context switches. <br>
**Rule of thumb** 80% of CPU burst <= time quantum.

Problem of Round Robin :
- I/O bound processes use only a small fraction of their time slice &rarr; spend a long time in the Ready queue.

Solution : **Virtual Round Robin**
- Auxiliary queue &rarr; high priority.

### Multi-Level Queue Scheduling
--------------------------------------------------
Separate processes according to their expected behaviour.
<center>

<img src="https://www.codingalpha.com/wp-content/uploads/2016/11/Multi-Level-Scheduling-Program-in-C.jpg">

</center>

### Multi-Level Feedback Queue Scheduling
--------------------------------------------------
Processes may change their behaviour, so they might require different priorities.
- Dynamically adapt to process behaviour.
	- move processes between queues as they change.
- Example :
	- I/O bound processes get served quickly.
	- CPU-bound processes get demoted.

Generally used on Windows 10 PCs.
<center>

<img src="https://i.pinimg.com/originals/9e/56/96/9e5696a52f10453be9717470b28a44c7.jpg">

</center>

### Parameterised Scheduling Algorithms
--------------------------------------------------
Scheduling policies can be flexibly designed and highly configurable. <br>
E.g. Multi-level Feedback Queues :
- Number of levels in the scheduling system.
- Methods for determining at which level a process is admitted.
- Methods for upgrading and demoting processes between queues.
- Choice of scheduling algorithm at every level.
	- e.g. Round Robin.
		- time quantum parameter.

### Real-Time Scheduling
--------------------------------------------------
- Processes with periodic arrival times.
- Deadlines!!!
- **Hard Real-Time** : guarantee that there are no deadlines missed.
- **Soft Real-Time** : minimise the number of deadlines missed.
- Preemptive scheduling with static or dynamic priorities.

<center>

<img src="https://walkccc.github.io/CS/assets/os/6.19.png">

<img src="https://i.stack.imgur.com/kk7kg.png">

</center>

A set of tasks is scheduled if and only if :

<center>

Σ Ci/Ti <= 1

where:
- Worst-Case Execution Time = Ci
- Task Deadline - Period Ti

</center>

### Java Thread Scheduling
--------------------------------------------------
Scheduling policy :
- Early Java Versions : user threads map to **ONE** kernel thread.
	- FCFS + priorities, preemptive.
- Depends on OS, user threads map 1:1 to kernel-threads.
	- a java thread can be preempted by the OS.

Scheduler is run when :
- A thread terminates.
- A higher priority thread becomes runnable (Ready).
- A thread calls yield().
--------------------------------------------------

### Selecting a CPU Scheduling Algorithm - Performance Evaluation
--------------------------------------------------
Factors to Consider :
- Type of System.
- Expected process characteristics.
- Expected workload.
- Scheduling criteria/goals &rarr; metrics.

Evaluation Methods :
1. Deterministic.
1. Probabilistic.
1. Stochastic.
1. Testing the Implementation.

#### Deterministic Evaluation
Given a predefined workload.

- FCFS.
	- executed in the order of the processes' creation.
- SJF.
	- executed in the order of the shorted process first.
- RR.
	- executed through time quantums (time sharing), and the process is interrupted and resumed later if it has not completed within it's allocated time slot.


Average waiting time : calculate the waiting time of all the processes and divide by how many processes there are!

CPU Utilisation could go down :
- if a process goes down, or it is waiting.
- throughput.

### Probabilistic Evaluation
--------------------------------------------------
Analytical models.
- Mathematical representations of computer systems.
- E.g. *Markov Chains* (below is an example of a non-related situation, but the same applies to operating systems too!).

<center>

<img src="https://revolution-computing.typepad.com/.a/6a010534b1db25970b01bb08a7df31970d-pi">

</center>

| Pros | Cons |
|---------------------------------|----------------------------------------------------------|
| Large body of existing work. | Probabilities are only approximations of real behaviour. |
| Can be applied to new problems. | Systems can be too complex to model everything. |
| Relatively fast and accurate. | Must use other techniques to <b>validate</b> results. |

#### Queueing Models
Computer System : a network of servers, each with a queue of waiting processes.
- Knowing arrival rates and services rates.
- Computes throughput, average queue length, average wait time etc...
- Arrival of processes & CPU and I/O bursts can be determined probabilistically.
- Typically, these are exponentionally distributed and described by their mean value.

#### Little's Law - Conservation of Flow
Assuming a system in a steady state, processes that are leaving the queue must equal processes arriving at the queue.

<center>

#### L = &lambda; * W

</center>

where
- **L** : average queue length.
- **&lambda;** : average arrival rate into queue.
- **W** : average waiting time in queue.

Valid for any sceduling algorithm and arrival distribution. <br>
For example :
- If 7 processes arrive per second on average, and there are 14 processes in queue on average, then the average wait time per process = 2 seconds.

### Stochastic Evaluation
--------------------------------------------------
Simulation
- Gather statistics indicating algorithm performance.
- Data to drive simulation gathered via :
	- random generation informed by probability distributions.
	- data record from real systems (trace tape of sequence of events).

| Pros | Cons |
|----------------|--------------------------------------------|
| More accurate. | Bugs in the simulation. |
|  | Imprecise Modelling. |
|  | Results of a simulation must be validated. |

### Implementation and Testing
--------------------------------------------------
The real thing.
- Even the best simulations have limited accuracy.
- We could also implement our own scheduler and :
	- test it with hand-crafted / random-generated data.
	- test it in real systems.
- Parameterisation of scheduler important for compatibility & fine tuning.
- High cost, high risk.
