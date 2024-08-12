### Process Concept

- An operating system executes a variety of programs that run as a
process.
- `Process` – a program in execution; process execution must progress
in sequential fashion. No parallel execution of instructions of a single
process
- `Multiple parts`
    - The program code, also called `text section`
    - Current activity including `program counter`, processor registers
    - `Stack` containing temporary data
        - Function parameters, return addresses, local variables
    - `Data` section containing global variables
        - initialized and uninitialized
    - `Heap` containing memory dynamically allocated during run time

<aside>
⚠️ Program is passive entity stored on disk (executable file);
process is active

</aside>

- One program can be several processes

## Process State

- As a process executes, it changes `state`
    - New: The process is being created
    - Running: Instructions are being executed
    - Waiting: The process is waiting for some event to occur
    - Ready: The process is waiting to be assigned to a processor
    - Terminated: The process has finished execution

### Diagram of Process State

![image](https://github.com/user-attachments/assets/267d4f71-c59c-4383-949b-a5bea5aec18f)


## Process Control Block (PCB)

A **Process Control Block (PCB)** is a data structure used by the operating system to store information about a specific process. The PCB is crucial for the management of processes in a multitasking operating system, as it contains all the necessary data needed to manage a process's execution, such as its current state, priority, and resources.

## Threads

<aside>
⚠️ ไปอ่านได้ใน Chapter 4

</aside>

**Threads** are the smallest unit of execution within a process. A process can contain multiple threads, all of which share the same resources but execute independently. Threads are often referred to as "lightweight processes" because they allow concurrent execution of tasks within the same process, improving the efficiency and performance of applications.

- Consider having multiple program counters per process
    - Multiple locations can execute at once
        - Multiple threads of control -> `threads`
    - Must then have storage for thread details, multiple program
    counters in PCB

## Process Scheduling

- Process scheduler selects among available processes
for next execution on CPU core

<aside>
🔑 Goal -- Maximize CPU use, quickly switch processes onto
CPU core

</aside>

- Maintains scheduling queues of processes
    - Ready queue – set of all processes residing in main
    memory, ready and waiting to execute
    - Wait queues – set of processes waiting for an event
    (i.e., I/O)
    - Processes migrate among the various queues

### Context Switch

- When CPU switches to another process, the system must
`save the state` of the old process and load the `saved state`
for the new process via a `context switch`
- Context of a process represented in the PCB
- Context-switch time is pure overhead; the system does no
useful work while switching
    - The more complex the OS and the PCB ➔ the longer
    the context switch
- Time dependent on hardware support
    - Some hardware provides multiple sets of registers per
    CPU ➔ multiple contexts loaded at once

## Process Creation

- `Parent` process create `children` processes, which, in turn
create other processes, forming a tree of processes
- Generally, process identified and managed via a process
identifier (pid)
- Resource sharing options
    - Parent and children share all resources
    - Children share subset of parent’s resources
    - Parent and child share no resources
- Execution options
    - Parent and children execute concurrently
    - Parent waits until children terminate
- UNIX examples
    - `fork()` system call creates new process
    - `exec()` system call used after a `fork()` to replace the process’
    memory space with a new program
    - Parent process calls `wait()` waiting for the child to terminate

## Process Termination

- Process executes last statement and then asks the operating
system to delete it using the `exit()` system call.
- Parent may terminate the execution of children processes using
the abort() system call. Some reasons for doing so:
    - Child has exceeded allocated resources
    - Task assigned to child is no longer required
    - The parent is exiting, and the operating systems does not
    allow a child to continue if its parent terminates
- If no parent waiting (did not invoke wait()) process is a
`zombie`
- If parent terminated without invoking wait(), process is an
`orphan`

## Communications Models

- Shared memory
    - **Shared Memory** is an IPC mechanism where multiple processes can access a common memory space. This shared memory region is used for exchanging information directly by reading and writing data.
- Message passing
    - **Message Passing** is an IPC mechanism where processes communicate by sending and receiving messages. The messages are typically passed through the operating system’s messaging services or through network protocols.

<aside>
❓ IPC ไม่ออกหรอกมั้ง สาธุ

</aside>

## Sockets

- A socket is defined as an endpoint for communication
- Concatenation of IP address and port – a number included at start of
message packet to differentiate network services on a host

<aside>
❓ Socket ไม่ออกหรอกสาธุ

</aside>
