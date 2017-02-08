#System Structures

##Operating System Services
Provides functions that are helpful to the user

Types:
- User Interface : CLI, GUI, batch interface. Not all OSes may have
UI.
- Program execution
- I/O operations : cannot be accesed by user directly. May involve file or device.
- File-system manipulation
- Communications : exchange info between processes, on the same computer, or between computers
in a network (via shared memory or message passing)
> Message passing is packets moved by OS within the same machine
- Error detection : OS should take appropriate action for each type of error.
- Resource Allocation : multiple users/jobs running concurrently, resource distribution needed
- Accounting 
- Protection and Security 

####API - Application Programming Interface
A set of functions that are available to application programmers, including the
parameters passed and return values it expects. These functions typically invoke the actual
system calls on behalf of the application programmer. 

Why are they important:
- Simplification : hides low level details
- Portability : over platforms, same API, different platforms

####System Call
System Call interface serves as a link to the system calls of the OS.

Typically there is a number associated with each system call.

Sometimes may need to pass arguments with system calls, possible ways:
- Simplest, use values in registers
- Parameters stored in block, address of block passed as a register
- Using stack

####System Programs
Provides a convenient environment for program development and execution. Some are simply
interfaces to system calls, some are more complex.

###Operating System Design and Implementation
Important principles to separate:
- Policy : what will be done / what needs to be done
- Mechanism : How to do it.

This separation is very important because it allows maximum flexibility 
if policy decisions are changed later.

Implementation:
- Mix of assembly and high level language (early on assembly only). Low level details in assembly,
Main body in a language, usually C, and system programs in other languages.

Higher level languages are easier to port to other hardware, code can be written faster, more compact, and easier to debug. 
However, performance is slower and might require more storage.

####Operating System Structure
- Simple:
    - Not very well separated
    - Not divided carefully into modules
- UNIX

