---
title: "Operating Systems"
author: "Andrew Ross-Sermons"
lang: "en"
toc: true
summary: "Class notes for CS-310, Operating Systems"
relationships:
    parent: "class.md"
tags:
    - "dense-note"
---
## Chapter 1
### Operating System Basics
**Operating System** - An operating system (OS) uses system resources to provide services to the user.
**Computer Resources** - Components in a computer.
- Processor (CPU) - Computational unit for moving and manipulating data
- Main Memory - Volatile storage for immediate access
- I/O Modules - Used to move data between computer and the outside world
- System Bus - Facilitates communication between the components above
### Processor History
==Ch 01 Unfinished==
## Chapter 5
### Concurrency
**What is Concurrency?** - Design issues that arise primarily when multiple processors or processes are active at once.
- Includes: Communication between processes, resource sharing/competition, process synchronization, and process time allocation
**Concurrency Vocabulary**
- Atomic Operation - An operation that appears to be indivisible/cannot be broken down even though it may consist of multiple steps. A sequence of instructions that is guranteed to execute as a group or not at all
- Critical Section - A section of code that requires shared resources and may not be executed while another section is using those resources
- Deadlock - When two or more processes can't continue because they are waiting for the others to do something
- Livelock - When two or more processes are stuck in an infinite loop that doesn't accomplish anything
- Mutual Exclusion - The requirement that when one process is in a critical section, no other process may access shared resources being used by that critical section
- Race Condition - A situation in which multiple threads or processes read and write shared data and the final result depends on the timing of their execution
- Starvation - A situation in which a runnable process is never chosen to execute
**Three Contexts for Concurrency**
- Multiple Applications - Multiprogramming, or the sharing of processing time across multiple applications
- Structured Applications - Applications designed as a set of concurrent processes
- Operating System Structure - Structures application principles applied to operating systems
**OS Responsibilities** - Under concurrency, the operating system must...
- Be able to keep track of various processes
- Allocate and de-allocate resources for each process
- Protect the data and physical resources of each process against interference by other processes
- Ensure that processes and outputs operate independent of processing speed
## Chapter 6
**Contents**
- Concurrency
- Deadlock
- Starvation
### Deadlock
**What is Deadlock?** - The permanent blocking of a set of processes that rely on each other or the same resources.
- Causes
  - Shared Resources - Both processes are trying to access the same resources. Neither can complete when the resources are blocked by each other
  - Communication - Both processes wait on each other to complete
**Deadlock Examples**
- **Reusable Resources**
  - Process A uses and locks Resource F
  - Process B uses and locks Resource G
  - Process A needs Resource G to finish
  - Process B needs Resource F to finish
**Conditions for Deadlock**
1. Mutual Exclusion - Only one process may use a resource at a time
2. Hold and Wait - A process may hold allocated resources while awaiting assignment of other resources
3. No Preemption - No resource can be forcibly removed from a process holding it
- The first three conditions allow the possibility of deadlock, but for it to actually happen the fourth needs to occur
4. **Circular Wait** - A closed loop of processes holds a series of resources that the other process(es) in the loop need
### Resource Categories
**Reusable** - Can be safely used by only one process at a time and is not depleted by that use.
- Ex: Processors, I/O channels, memory, filesystems, etc.
**Consumable** - Can be created and consumed.
- Interrupts, signals, messages, I/O buffers
### Handling Deadlock
**Three Approaches**
- Prevent Deadlock - Eliminate one of the conditions for deadlock
- Avoid Deadlock - Avoid resource allocation that can lead to deadlock
- Detect Deadlock - Detect and react to deadlock conditions
### Preventing Deadlock
**Prevention Strategies**
- Indirect - Prevent the occurance of deadlock conditions
- Direct - Prevent the occurance of circular waits
**Hold and Wait** - Require that a process request all of its required resources at one time and blocking the process until all requests can be granted simultaneously.
- Problem 1 - The process may be held when it could have performed some operations without all resources
- Problem 2 - Resources allocated to a process may not be used for the entire time, what a waste
- Problem 3 - Modular programs can't predict resource usage before runtime
**No Preemption** - Don't allow processes to hold onto resources without using them
- Solves problem 2 above
- If a process requests a resource but is not using it while it waits for others, free that resource until all others are available
**Circular Wait Prevention** - Define a linear ordering of resource types
- If a process requests resource R, it can only requests more resources of the same type
- Problem - Slows doen processes by unnecessarily denying resource access
### Avoiding Deadlock
**Avoidance Strategies**
- Resource Allocation Denial - Do not grant a resource request if allocation may lead to deadlock
- Process Initiaion Denial - Do not initiate a process if its demands may lead to deadlock
==Slide 17==
## Chapter 7
### Vocabulary
**Frame** - A fixed-length block of main memory (RAM, caches).
**Page** - A fixed-length block of secondary memory (Disks, SSDs).
**Segment** - A variable-length block that resides in secondary memory.
