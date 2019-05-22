---
layout: post
section-type: post
title: "[tech interview 4 편] Operating System"
categories: Tech_Interview
tags: [ 'interview', 'technology', 'it', 'OS' ]
comments: true
---



# 1. What is an operating system?

An operating system is a program that acts as an intermediary between the user and the computer hardware. The purpose of an OS is to provide a convenient environment in which user can execute programs in a convenient and efficient manner.


# 2. What are the different operating systems?

# 3. Batched operating systems

# 4. Multi-programmed operating systems

# 5. timesharing operating systems

# 6. Distributed operating systems

# 7. Real-time operating systems




# 8. What are the basic functions of an operating system?

Operating system controls and coordinates the use of the hardware among the various applications programs for various uses. Operating system acts as resource allocator and manager. Also operating system is control program which controls the user programs to prevent errors and improper use of the computer. It is especially concerned with the operation and control of I/O devices.



# 9. What is kernel?

Kernel is the core and essential part of computer operating system that provides basic services for all parts of OS.


# 10. What is dead lock?

Deadlock is a situation or condition where the two processes are waiting for each other to complete so that they can start. This result both the processes to hang.



# 11. What is a process?

A program in execution is called a process.

Processes are of two types:
1. Operating system processes
2. User processes



# 12. What are the states of a process?

1. New
2. Running
3. Waiting
4. Ready
5. Terminated


# 13. What is starvation and aging?

Starvation is Resource management problem where a process does not get the resources it needs for a long time because the resources are being allocated to other processes.

Aging is a technique to avoid starvation in a scheduling system.



# 14. What is semaphore?

Semaphore is a variable, whose status reports common resource, Semaphore is of two types one is Binary semaphore and other is Counting semaphore.



# 15. What is context switching?

Transferring the control from one process to other process requires saving the state of the old process and loading the saved state for new process. This task is known as context switching.



# 16. What is a thread?

A thread is a program line under execution. Thread sometimes called a light-weight process, is a basic unit of CPU utilization; it comprises a thread id, a program counter, a register set, and a stack


# 17. What is process synchronization?

A situation, where several processes access and manipulate the same data concurrently and the outcome of the execution depends on the particular order in which the access takes place, is called race condition. To guard against the race condition we need to ensure that only one process at a time can be manipulating the same data. The technique we use for this is called process synchronization.



# 18. What is virtual memory?

Virtual memory is hardware technique where the system appears to have more memory that it actually does. This is done by time-sharing, the physical memory and storage parts of the memory one disk when they are not actively being used.


17. What are necessary conditions for dead lock?

1. Mutual exclusion (where at least one resource is non-sharable)

2. Hold and wait (where a process holds one resource and waits for other resource)

3. No preemption (where the resources cant be preempted)

4. Circular wait (where p[i] is waiting for p[j] to release a resource. i= 1,2,n

j=if (i!=n) then i+1

else 1 )



18. What is cache memory?

Cache memory is random access memory (RAM) that a computer microprocessor can access more quickly than it can access regular RAM. As the microprocessor processes data, it looks first in the cache memory and if it finds the data there (from a previous reading of data), it does not have to do the more time-consuming reading of data from larger memory.



19. What is logical and physical addresses space?

Logical address space is generated from CPU; it bound to a separate physical address space is central to proper memory management. Physical address space is seen by the memory unit. Logical address space is virtual address space. Both these address space will be same at compile time but differ at execution time.


20. Differentiate between Complier and Interpreter?

An interpreter reads one instruction at a time and carries out the actions implied by that instruction. It does not perform any translation. But a compiler translates the entire instructions

28. What is a long term scheduler & short term schedulers?

Long term schedulers are the job schedulers that select processes from the job queue and load them into memory for execution. The short term schedulers are the CPU schedulers that select a process from the ready queue and allocate the CPU to one of them.



29. Explain the meaning of mutex.

Mutex is the short form for Mutual Exclusion object. A mutex allows multiple threads for sharing the same resource. The resource can be file. A mutex with a unique name is created at the time of starting a program. A mutex must be locked from other threads, when any thread that needs the resource. When the data is no longer used / needed, the mutex is set to unlock


32. What is a daemon?

Daemon is a program that runs in the background without users interaction. A daemon runs in a multitasking operating system like UNIX. A daemon is initiated and controlled by special programs known as processes.



33. What is pre-emptive and non-preemptive scheduling?

Preemptive scheduling: The preemptive scheduling is prioritized. The highest priority process should always be the process that is currently utilized.

Non-Preemptive scheduling: When a process enters the state of running, the state of that process is not deleted from the scheduler until it finishes its service time.



34. What is busy waiting?

The repeated execution of a loop of code while waiting for an event to occur is called busy-waiting. The CPU is not engaged in any real productive activity during this period, and the process does not progress toward completion.



35. What is page cannibalizing?

Page swapping or page replacements are called page cannibalizing.

37. What is process migration?

It is the transfer of sufficient amount of the state of process from one machine to the target machine.

53. What is an idle thread?

The special thread a dispatcher will execute when no ready thread is found.
