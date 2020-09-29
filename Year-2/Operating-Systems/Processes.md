*Lecture 3, Tuesday 4th February*
# Processes
Bootstrapping
--------------------------------------------------
In ROM, there is a program called **Bootstrapping**. It loads the OS files from persistent storage into Main Memory.

<center>BIOS -> Master Boot Record (MBR) -> Bootsector -> Bootloader</center>

1. PC is turned on, and the BIOS initliases the hardware.
1. BIOS calls code stored in the MBR at the start of the disk 0.
1. MBR loads code from the bootsector of the active partition.
1. Bootsector loads & runs the bootloader from its file system.

BIOS is now largely replaced by the **UEFI** (Unified Extensible Firmware Interface).

Processes
--------------------------------------------------
A process is created whenever some kind of program is started, e.g :
- OS startup.
- User login.
- Opening an application, etc...

#### Process Creation
- A process becomes a **parent** when it creates other processes - *children*.
- Child processes receive resources from their parent or independently from the OS.
- Flexible Execution
	- parents and child can run concurrently.
- Flexible use of address space
	- child can be derived from the parent or run a completely different program.

#### Process Management
- OS maintains a **process table** to keep track of active programs.
	- cannot delete files, programs if they are running in the **process table**.
- For each process, a **process image** is stored in virtual memory, containing all the information regarding its state.

Process Image Contents :
1. Process Control Block.
	- Process ID, Parent Process ID, User ID.
	- Process State (e.g. current activity, register contents, program counter).
	- CPU scheduling information (e.g. priority).
	- Memory management information, process priviledges.
	- Accounting information (e.g. resource use statistics, time limits).
	- I/O status information (e.g. devices & files allocated to the process).
1. User Program.
1. User Data.
1. Stack.
1. Heap.

#### Process Execution

1. **Control Flow** - the order in which individual instructions or function calls are executed. 
	- **Exceptional Control Flow** : exists at all levels of a computer system. The change in control flow in response to a system event.
1. **Exception Handling** - an exception triggers a sudden transfer of control from the program to OS. Each exception has a unique number, and the OS looks up the correct exception handler from an *exception table*.
	- **Interrupt Exception** : occur at the same time as a result of signals from I/O devices that are external to the processor. They are not caused by the program execution. E.g. user presses a mouse button.
	- **Trap Exception** : occur as a result of executing an instruction that triggers control transfer to the OS, usually a **system call**.
	- **Fault Exception** : result from error conditions that a handler might be able to fix. If the handler is able to correct the error condition, it returns control to the current instruction for re-execution. Else, the handler terminates the process. E.g. memory page mission.
	- **Abort Exception** : results from unrecoverable fatal errors, typically hardware errors such as parity errors that occur when memory bits are corrupted. These handlers **do not** return control back to the application program. E.g. fatal hardware error or division by 0 (UNIX).
1. **Flow of Control for Concurrent Processes**
	- **Process Switching** : exception-like activity that the OS kernel uses to assign particular processes to the CPU to work on. It has four steps :
		1. save current process.
		1. pre-empty that process
		1. restore another process/open new process.
		1. pass control onto it.

#### Process Memory Management
##### Swapping!
Virtual Memory can make use of secondary stroage in order to temporarily suspend certain processes. Possible reasons :
- insufficient memory.
- process suspected of causing a problem.
- user request, e.g. debugging.
- timing, e.g. periodic process.
- parent process request.

#### Process Termination
Execution stops indefinitely.
- program finished
- program error routine, e.g. exception handling.
- unexpected fatal error, e.g. division by 0, illegal memory reference etc...
- killed by another process - requires authorisation, e.g. superior process getting rid of its helper.
- related system calls, ```exit```, ```kill```.

What if a parent process dies whilst the child process is still running? The child becomes an '*orphan*' process, and may be assigned to another process; in **linux**, they are assigned to the *init* process.
