# Introduction  
## What is an operating system  
- It is a program that acts as an intermediary between a **user of a computer** and the **computer hardware**  
## Why do we need  an OS
### Two goals  
- **Primary goal**:make the computer system convenient to use  
- **Secondary goal**: use the computer hardware in an efficient manner  
## Early batch systems 
1. Because computer time was very expensive , we want to maximize its usage. Operator group similar job together into batches  
2. In early batch systems, the CPU usually sit idle while operator noticed a job stopped. To overcome this idle time we need automatic job sequencing  
## Computer interrupts  
- Interrupt-Driven Operations: CPU very fast , I/O device slow.  
- To deal with it , A device controller informs the CPU that it has finished its specific operation by generating a hardware interrupt
## Operating system operations
1. **Multiprogramming**
    1. **Prevent CPU idle time**
    2. **Processes in memory**: OS keeps multiple processes in the computer's memory at the same time
    3. **Processes switch**: when a process has to **wait for a I/O or system operation** , OS will **find other process to run** , and CPU switch to that process
    4. **Job scheduling**: Because there are many processes in the system, the OS requires a scheduling policy to decide which process will be picked next
2. **Multitasking**
    1. **Frequent switch**: a logical extension of multiprogramming. CPU executes multiple processes by switching among them , but **switch very frequently**  
    2. **Fast response time** : frequent switch provide user a fast response time and **prevent a small process from waiting for a big process** for a long time.
    3. **Virtual memory** : to ensure reasonable response times, OS uses virtual memory , allows execution of a process that is not completely in memory
3. **Dual mode operation**
    1. **System protection**: Because the **OS kernel and multiple user processes exist in memory at the same time**, the OS must ensure that **an incorrect or malicious(惡意的) program** cannot cause other programs or the OS to **execute incorrectly**
    2. **Two operation modes**: System use a **hardware mode bit** to distinguish between **user mode (mode bit=1) and Kernel mode (mode bit=0)**, some instructions can only be executed in kernel mode
    3. **Mode transition**:When user processes call OS services or encounter software errors, they generate a **trap (a software-generated interrupt)**. This causes the hardware to switch from user mode to kernel mode to execute the system call, and it returns to user mode once finished
4. **Timer control**
    1. **Prevent resourse hogging**: Timer can prevent processes from entering infinite loops or hogging system resourses 
    2. **Hardware interrupt**: OS set a counter that decrease every clock ticks. When counter reaches 0 interupt occurs
## Define OS
- **Definition of an OS**: There is no universally accepted definition. A good approximation is "everything a vendor ships when you order an operating system". More precisely, the kernel is "the one program running at all times on the computer". Everything else is either a system program or an application program
- **User view**: The user's view of the computer varies according to the interface being used. A personal computing system is designed for one user to monopolize its resources to maximize work or play. Shared systems aim to maximize system throughput for many users. Embedded computers in home devices and automobiles have little or no user view
- **System view**: The OS plays two important roles. First, it acts as a resource allocator that manages all resources and decides between conflicting requests for efficient and fair use. Second, it acts as a control program that controls the execution of programs to prevent errors and improper use of the computer.