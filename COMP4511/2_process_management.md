# Process Management

A process is not necessarily the whole program nor is it just the program code.

Linux doesn't do a distinction between a process and a thread, it just creates a task. The only difference is when creating a process, it copies resources from the parent. While when you create a thread, it will share the resources with its parents.

In Linux, the list (linked list) is embedded into a data structure. That is the list is part of the data structure. Such that a list pointer will point to a `list_head` data structure rather than to the struct itself. This is done so that when traversing through the list, we don't have to care what type of list it is.

`thread_info`:
- cpu: may have several processors in a computer, process can run in any one, this is an identifier for which processor is it running in.
- preempt_count: kernel preemption (higher priority processes that can stop a process from using the cpu and take the cpu). That is for when there is a higher priority process that arrives, kick this low priority process out.

Macros: something that will be replaced with actual long code, done during compilation time. Is different from function call as function calls will take a longer time due to the function call overhead. Macros are much faster and more efficient.

`task_struct` members:
- In interrupt context: there is no `mm` field as there is no memory map. But as we only need to do something quick and so that we are able to go back to the user space, we will borrow a memory map from the last process.

Process genesis:
- Bootloader will find your OS, then it will load OS into kernel, and when it is finished it will run the `init` process.
- Copy-on-write: delay the copying of information from parent until there is a write operation.
- vfork: for when you don't need resources from the parent, so that there is no need to copy the resources.

Process termination:
- Voluntarily: through exit
- Involuntarily:
  - Kill signal on the process
  - Unhandled exception (causes crash)
- Cleanup is done on termination:
  - Decrement reference counters for resources.
  - EXIT_ZOMBIE state only has the process data structure. All resources are returned to system already. When the init process sees processes in this state, init will reap these processes.
