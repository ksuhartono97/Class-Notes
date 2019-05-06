# Interrupts
Actions on devices attached to the computer will send interrupts to the CPU to process the events.

There are two PIC (programmable controllers), one master and slave.

IRQs can be shared by multiple devices by multiplexing the signal on the physical IRQ. This can only be done if the devices aren't using the IRQs at the same time. This is done by masking the IRQ, that is while an event arrives at IRQ, that IRQ line will reject any new events to that IRQ(untriggerable).

Several interrupts are unmaskable, that is you can't say that you won't care about them. The IRQs to handle these interrupts are reserved by the system. (Interrupt numbers 0-31)

Interrupt Service Routine is divided into the top half and bottom half. The top part is usually the masked part.

## Interrupt Handling
Interrupt Service Routine (ISR) handles interrupts. Context are the values that has to be loaded into the register. Old information (stack pointer, program counter, etc) is saved either in the new stack or the old stack (caller or callee).

Interrupts cannot have any code that sleeps or locks, as there is no way to wake up again and return to the interrupt context.

IRQ statuses:
- `IRQ_DISABLED`: disallow (no device here)
- `IRQ_INPROGRESS`: handling an event
- `IRQ_PENDING`: there is an event that needs to be handled
- `IRQ_MASKED`: ignoring

`unlikely`: directives that tells the compiler to optimize the code for the opposite option. Done to optimize branches.

Choosing irq numbers can be done statically or dynamically (pick a number, then try to register it, if it isn't shareable it will fail otherwise it will succeed) or automatically (at boot, the PCI bus registers the different devices dynamically as they come).

Kernel code footprint becomes too large due to device drivers, thus linux created kernel modules that are inserted into the kernel as they are needed. This module lies on the hard disk of the device (not in the kernel). When you plug the device in, the module is mounted to the kernel, and as you are ejecting a device, the software will have to unmount the device and deregister the IRQ handlers associated to it.

There are two points where we can mask an interrupt, on the CPU or on the chip itself.  


## Interrupt Context
No such thing as an ongoing process, as such there no `current` macro that can be accessed.

Reentrant code is code that is invariable with respect to entering the code. E.g. If you have a function, then you get interrupted in the middle, then rerun the code, then would be no problem.

> Remember interrupts are hardware triggered, exceptions are special interrupts that are common to the code.

Exceptions can be nested but only two levels deep. As they are exceptions in the code.

## Bottom Halves
In modern OSes, the philosophy of interrupt handling is to do as little as possible in the interrupt handler. That is in the interrupt handler, usually you just do interrupt masking, do a bit of work, then unmask it.

### Softirqs
A table with 32 entries that contain function pointers to softirq functions. The enumeration tells you which function corresponds to which array entry.

Creation of new IRQs are done by adding it to the enumeration in the kernel. The position in the enumeration decides the priority. To register it with the system, we need to open it on runtime, done on the part of the code that initializes the device driver.

When you plug a device, the kernel will be interrupted to find the device driver that corresponds to this device. When the device driver isn't in the kernel, it will find the driver from the USB after finding the right module for that driver, the module is inserted into the kernel. In the module there is an initialization function, which is where you register the softirq.

Softirqs are not for trivial uses.

### Tasklets
Mechanisms built on top of softirqs, works in a similar way.

Simpler and weaker locking requirement because it is by default locked so that it doesn't execute again. This is because we don't need the scalability over multiple processors. The tasklet itself is already automatically locked by the system.

There is one tasklet queue per CPU. Scheduled using a function call to raise the flag for the correct softirq.

### Work Queues
Want to defer work to threads, thus create processes that will run the functions. The work queue structure contains a list of works and a pointer to the current work. Worklist is a list that allows us to queue the works. Each CPU's work queue struct will have its own work (work struct) that contains a function to execute.
