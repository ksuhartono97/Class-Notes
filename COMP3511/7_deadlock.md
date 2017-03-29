# Deadlock

## Deadlock Characterization

A deadlock can arise if the following four conditions hold simultaneously (necessary but not sufficient):

- Mutual exclusion
- Hold and wait: A process holds a resource and waits to acquire additional resource. If the process holds but doesn't request more then it cannot be included in a deadlock.
- No preemption: resources can only be released voluntarily
- Circular wait: processes waiting circularly for each others resources.

A cyclical resource allocation (Circular) doesn't always imply the existence of a deadlock.

## Methods for handling deadlocks

Note: probability that deadlock will happen is very small. It isn't something that commonly occurs.

### Protocols

Use a protocol to prevent or avoid deadlocks to ensure system will never enter deadlock.

#### Deadlock prevention

Basically provide a set of methods to ensure at least one of the necessary conditions cannot hold. Thus ensuring that deadlock cannot happen.

Restraining ways request can be made:

- Mutual exclusion: must hold for non-sharable resources. If it can be shared, not required.
- Hold and wait: No holding, either process has all resource that it needs or none at all. Will lead to terrible utilization and significant reduction to degree of multiprogramming.
- No preemption: when a process requests for more resources and it isn't available, then drop all that is being held and let others use it. That process can be restarted when it can regain the old resources as well as obtain the new resources it requests. Only applies to resources whose state can be easily saved and restored.
- Circular wait: impose a total ordering of all resource types, and require that each process request resources in an increasing order of enumeration. Very difficult to implement, we can't always know what resources are going to be used. (sometimes even impossible)

#### Deadlock avoidance

> Unrealistic to do

Requires additional information on how much resources is a process going to use and request during its lifetime. Then the OS will decide whether there is a potential for deadlock or not.

Terminologies:
- Resource allocation state: number of available and allocated resources, and the maximum demands of the processes
- Safe state: System is in a safe state if there exists s sequence of all processes in the system such that for each process, the following equation holds
> (max_resource_requested_by_process) - (resources_allocated_to process) < available_resources_in_the_system

Note that said sequence doesn't have to be unique.

The idea behind avoidance is that if system is in safe state, there cannot be any deadlocks. But if it is unsafe, there is a **possibility** of a deadlock happening (necessary but not sufficient). Therefore, ensure that system will never enter unsafe state.

>TLDR summary: Avoidance is to ensure that system will never enter unsafe state

Algorithms:
- Resource allocation graph algorithm
- Banker's algorithm: multiple instances of a resource type, each process must declare a prior maximum usage (declare when it will finish and return the resource).

#### Banker's Algorithm
Variables:
- `available`
- `max` : maximum that can be requested
- `allocation` : amount that is already allocated
- `need` : how much the process needs to complete task

`need = max - allocation`

#### Safety Algorithm
See lecture notes for full algorithm.

Work = Work + Allocation (for an i). Basically means that since process i can finish eventually then the allocated amount can also be returned to allocation eventually.

##### Resource-Request Algorithm for Process P<sub>i</sub>

Used to check whether or not a process can get the resources it requested. With flags:
- Error flag if request < need, since process has exceeded maximum claim
- Wait flag if request < available, since resources are currently not available so process must wait.

#### Example on Banker's Algorithm
Work = (3,3,2)

Check which process can complete based on its need value. Then add it work with **alloc** value, NOT THE NEED VALUE

Work = (3,3,2) + Alloc(P1) = (5,3,2)

Work = (5,3,2) + Alloc(P3) = (7,4,3)

..... and so on

Upon inquiry if request can be granted or not, first check if the request passes through the banker's algorithm first. After that if it passes, then check if it is safe or not. If not then do not grant.

### Detection and recovery

Allow system to enter deadlock states, detect it and recover.

### Ignore

Don't care about deadlocks, pretend it never occur in the system. Used by most OSes like UNIX.

This happens because solving deadlocks can be extremely costly.
