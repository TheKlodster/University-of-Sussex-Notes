*Lecture 6a, 3<sup>rd</sup> March*
# Deadlocks
A set of processes is **deadlocked** if each process in the set is waiting for an event that only another process in the set can cause.

Necessary and Sufficient conditions :
- **Mutual Exclusion** : each resource is currently assigned to eactly one process, or is available.
- **Hold-and-wait** : processes currently holding resources that were granted earlier can request new resources.
- **No-preemption** : resources previously granted cannot be taken away.
- **Circular wait** : must be a circular list of two or more processes, each of which is waiting for a resource held by the next member of the chain.

### Dealing with Deadlocks
--------------------------------------------------
No general solution.

- Deadlock prevention
	- design the system so that at least 1/4 condiitons never arise.
- Deadlock avoidance
	- do not approve resource requests that might lead to deadlock.
- Deadlock detection
	- always approve resource requests if available.
	- periodically check whether there is a deadlock.
	- if there is a deadlock, perform deadlock recovery.

#### Mutual Exclusion
System designed so that 1/4 cases never arise.

We cannot build a system with shared resource access, must prevent race conditions.

General precautions :
- make any data sources <code>read-only</code> where there is no modification.
- acquire only those resources that are really needed.

#### Hold-and-wait & No-preemption
Hold-and-wait :
- Acquire all resources at once, i.e. block until all resources are available.
	- + Process can execute one all required resources are held.
	- - Long delays.
	- - Bad resource utilisation.
	- - Advance knowledge needed about the resources required.

No-preemption :
- (a) Process releases resources when it fails to acquire a resource, and re-tries later.
- (b) Resource request forces another process to release a resource.
- only possible if the if the state of the resource can be saved and restored.

#### Circular Wait
- Enforce linear ordering of requests to resource types R<sub>1</sub>
- Process has to acquire all types of R<sub>i</sub> at once.
- After having acquired R<sub>i</sub>, it can only request resource types of R<sub>j</sub>, where O(R<sub>j</sub>) > O(R<sub>i</sub>).

Prevents deadlocks!!! :) <br>
However, there can be inefficiencies if ordering is poorly chosen. :(

### Synchronisation and Priority Scheduling
**Problem : Priority Inversion** <br>
Higher priority process has to wait because lower priority process holds the resource it wants to access.

**Solution : Priority Inheritance Protocol** <br>
Temporarily raise the priority of the lower process to the maximum priority of all processes accessing the same resource. Avoids priority inversion.


