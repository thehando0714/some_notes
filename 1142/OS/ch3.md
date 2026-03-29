# Process
## Process concept and memory structure  
- **Definition of a process**: A process is a program in execution. A program  is passive stored on disk as an executable file. A program becomes a process when the executable file is loaded into memory.
- **Memory layout(配置)** of a process  
     1. **Text section**: Contains the program code
     2. **Data section**: Contains global variables
     3. **Heap section**: Contains memory dynamically allocated during run time
     4. **Stack section**: Contains temporay data such as function parameters return addresses and local variables
## Process control block and process state
- **PCB**: Each process is represent in the OS by a PCB. It is also called a task control block. The PCB contains a lot info such as process state , program counter, CPU register, CPU scheduling info, memory management info,accounting info, I/O status
- **Process state change**: As a process execute it changes state:
    - **New**:Process is being created
    - **Ready**: Process is waiting to be assigned to a processor
    - **Running**: Instruction are being executed
    - **Waiting**: Process is waiting for some event to occur
    - **Terminated**: Process has finished execution
- **Execution cycle**: Process execution is a cycle of CPU execution(CPU burst) and I/O wait(I/O burst). Process alternate between two condition
## Context switch and threads(執行緒)
- **Context switch**: When the CPU switches to another process, the system must save the state of the old process and load the saved stated for the new process 
- **Switching overhead(負擔)**: The context of a process is stored in its PCB. Context switch time is a necessary overhead, as the system does no useful work while switching
- **Thread**: Traditionally, each process has a single thread of execution. However, having multiple program counters per process allows multiple location to execute at once, leading multiple threads of control. PCB is extended to include info for each thread 
## Process schelduling and queue
- **Scheduling objective**: The objective of multiprogramming is to have some process running at all time so  as to maximize CPU utilization. The goal of time sharing is to switch a CPU core among processes frequently that users can interact with each program while it is running
- **Scheduling queue**: The OS kernel has queue to keep track of the waiting process:
    1. **Ready queue**: A set of all process stay in main memory,ready and waiting to execute
    2. **Device queue**: A set of all process waiting for an I/O device
    3. **Job queue**: A set of all process in the system
## Scheduler in the system
- **Long term scheduler(or job schedular)**: Select which process should be into ready queue. It controls **degree of multiprogramming(the number of process in currently in memory)**. It is important that this scheduler selects a good process mix of I/O bound(密集型) and CPU bound process
- **Short term schedular(or CPU scheduler)**: Select which process should be executed next and allocates(分配) the CPU. It is invoke(執行) very frequently and must be fast.
- **Intermediate scheduling(swapping)**: Its key idea is that sometimes it can be advantage to remove a process from memory and reduce the degree of multiprogramming
## Process creation
- **Tree of process**: During the course of execution, a process may create many new process , forming a tree of process. Each process is identified and managed via(通過) process identifier(pid). In Linux system, systemd(or init in traditional UNIX) is the root of all child processes and is assigned a pid of 1
- **Creation methods(fork and exec)**: A new process created by fork() system call. The child process consists of a copy of the address space of the original parent process. To run a new program, the exec() (or execlp()) system call is used after a fork() to replace the process's memory space with a new program.
- **Execution and address space**: When a new process is created , the parent can either continue to execute concurrently(同時) with its children, or wait until some or all of its children have terminated. The child process can either be a duplicate of the parent process, or it can have a new program loaded into it.
## Process termination
- **Normal termination**: A process executes its last statement and ask the OS to delete it using the exit system call. The OS then deallocate(回收) the process's resourse
- **Forced termination(abort)**: A parent may terminate the execution if its **child has exceeded allocated resources(超出使用資源)** or task assigned to the child is no longer required. Some OS do not allow a child to continue if its parent has terminated, forcing all children to also be terminated, which is known as Cascading termination(連鎖終止)
- **Zombie and orphans**:
    1. **Zombie process** : if the parent hasn't yet called wait(), terminated child process become zombie.
    2. **Orphan process**: if parent is terminated without calling wait(), its children processes become orphans, In traditional UNIX systems, the init process becomes their new parent.
## Interprocess communication(IPC)
- **Cooperating process**: Processes executing concurrently may be either independent or cooperating. A cooperating process can affect or be affected by other processes executing in the system. They require an interprocess communication (IPC) mechanism to exchange data
- **Two fundamental model**: Shared memory and message passing.
## IPC in shared memory system 
- **Mechanism**: Communicating processes establish a region of shared memory. The form and location of the data are determined by these processes and are not under the OS's control. The processes are also responsible for ensuring that they are not writing to the same location simultaneously
- **Producer consumer problem** : A producer process produces information that is consumed by a consumer process. To run concurrently, they need a buffer (which can be an unbounded-buffer(無界限) or a bounded-buffer(有界限)) of items. The producer and consumer must be synchronized so that the consumer does not try to consume an item that has not yet been produced
## IPC in message passing system
- **Basic operation**:The OS provides a message-passing facility that includes at least two operations: send(message) and receive(message)
- **Communication method**:
    1. **Direct communication**: Each process that want to communicate must explicitly(明確的) name the recipient or sender, such as send(P, message)
    2. **Indirect communication**: Message are directed to and received from mailboxes (also referred to as ports). Each mailbox has a unique id, and processes can communicate only if they share a mailbox.
- **Synchronization**: Message passing can be designed as blocking (阻塞式)(considered synchronous) or non-blocking (considered asynchronous). When both send() and receive() are blocking, it is called a rendezvous(會合) between the sender and the receiver
- **Buffering**: Message queues can be implemented(分為) in three ways: Zero capacity (the sender must wait for the receiver, achieving a rendezvous), Bounded (有限)capacity (the sender must wait if the link is full), and Unbounded capacity (the sender never waits).