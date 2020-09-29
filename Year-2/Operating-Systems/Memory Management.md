*Lecture 7a Tuesday 10<sup>th</sup> March*
# Memory Management
- Addressing and address spaces.
- Partitioning and Segmentation.

## Memory Addressing
CPU-Memory interaction :
- Operations and data in registers.
- Data and instructions loaded from memory into CPU.
- Memory locations are accessed through addresses.
- Bit-width of addresses (e.g. 32 bits) determines the size of addressable memory (4 GiB!).

#### Dynamic Relocation
Has a :
- limit register - used for protection, so we don't use more than the limited amount of memory.
- base register.

#### Logical Addressing
Makes use of the limit and base registers.
- If the address is > limit register, it returns an addressing error.

### Address Binding
Bind instructions and data to memory addresses.
- **Compile Time**
	- if memory location known a priori.
	- must recompile code if starting address changes.
- **Load Time**
	- must generate relocatable code.
	- i.e. information allowing the loader to adapt addresses.
- **Execution Time**
	- binding delayed until run time.
	- process can be moved during its execution within memory.
	- requires hardware support (MMU).

### Static and Dynamic Linking
- **Static Linking**
	- libraries and program code combined into the executable (so they don't get into eachother's way).
- **Dynamic Linking**
	- linking postponed until execution time.
	- useful for shared libraries (.so, .dll).
	- OS support by dynamic linker.
	- dynamic linker is invoked when a library function is called.
		- loads the library (if not loaded yet).
		- maps library into the processs address space.
		- binds addresses of calls to the library functions.

### Memory Management Unit (MMU)
Hardware device that, at run time, maps logical to physical addresses.
- Performs execution-time binding of addresses.
	- Many methods possible: simplest scheme: base address + offset.
		- Implements **memory protection**.

**Logical Address Space** - addresses in the code that is being executed. <br>
**Physical Address Space** - addresses used by the system to execute the process.

## Memory Allocation
Partitioning : contiguous memory partition for each process. <br>
Segmentation : process memory subdivided into segments. <br>
Paging : process memory subdivided into pages.

### Memory Partitions
#### Fixed-size partitions :
- Memory is divided into fixed-size partitions.
- Process is assigned a free partition.
- Process image resides in memory as a single chunk.

Disadvantages :
1. Max number of processes in memory is fixed.
1. Max size of process images is limited.
1. Interal fragmentation : unused memory in the assigned partitions.

#### Variable-size partitions :
- Process image resides in memory as one single chunk.
- Process is allocated a free partition required size.
- On termination the partition is freed and combined with adjacent free partitions.
- OS maintains information on allocated and free partitions.

This is the **Dynamic Storage-Allocation Problem**.

We could use :
- **First-fit** :
	- allocate the first free section that is big enough.
- **Best-fit** :
	- allocate the smallest free section that is big enough.
	- must search entire list, unless ordered by size.
	- produces the smallest leftover tree section.
- **Worst-fit** :
	- allocate the largest free section.
	- must search entire list, unless ordered by size.
	- produces in the largest leftover free section.

Could also use **Compaction** :
- move processes to eliminate small free partitions.
- requires execution-time address binding.
- I/O problem :
	- keep job in memory while waiting for I/O.
	- use double-buffering to decouple I/O from process image.

<center> 

Summary

| Advantages | Disadvantages |
|--------------------------------------|-----------------------------------------------|
| Enables multiprogramming. | Limit maximum size of process image. |
| Memory protection between processes. | No memory protection within processes. |
| Easy to implement. | Suffers from internal/external fragmentation. |

</center>

### Memory Segmentation
Process image divided into segments.

**Segment Table** - indexed by segment number <i>s</i> :
- Segment base.
- Segment limit.
- Access bits (read, write, execute).

**Segmentation Protection** :
- Offset (d) encoded in the logical address together with the segment number (s).
- Look up allowed limit (length) for this segment in the segment table.
- Proceed addressing if offset (d) within limit bounds, else addressing error.

<center>

Summary

| Advantages | Disadvantages |
|------------------------------------------------------|-----------------------------|
| Non-contiguous memory. | Limit max size of segments. |
| Segments can be swapped in/out independently. |  |
| Memory protection within segments of process memory. |  |
| Less fragmentation. |  |

</center>
