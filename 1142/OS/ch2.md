## Operating system architecture and interfaces  
- **The overall architecture of an OS**,from top to bottom:**user interface,system call, service, the operating system itself, and hardware** at the bottom
- The user's view of the computer different according to interfac  
- **User interface include**: Graphical User Interfaces (GUI), Command Line Interfaces (CLI), Touchscreen Interfaces and Batch
## OS service
- OS service can be divided into two main categories
1. **Function to help users**: Include UI,program execution(loading and running code),I/O operations, file system manipulation ,communications(message passing and shared memory), and erro detection
2. **Function for ensuring efficient operations**: include resource allocation , logging, and protection and security
## System call
- **Definiton**:system calls provide interface to the service made available by an OS
- **Implementation and Execution:** These calls written in C and C++, some low level task have to be written by assembly language instruction. When system call is invoke, execution mode changed to kernel mode
- **Mechanism**: a number is associated with each system call in the OS (for example, the number for the write() system call is 1). The invocation steps are: find the system call from the table → invoke the functions → return the status of the system call and any return values
## Application Program Interface (API)
- Developer usually design programs a high level Application Program Interface (API), such as the standard C library, rather than using direct system calls.
- **Benefits** One major benefit concerns program **portability**; an application programmer designing a program using an API can expect their program to compile and run on any system that supports the same API. Additionally, actual system calls can often be more detailed and difficult to work with than the API
## **Parameter(參數) Passing in System Calls**
- There are three general method used to pass parameter to the OS  
1. **Registers**: Parameters are stored in registers, but this is constrained by the limited number of registers available
2. **Block or Table**: Parameters are stored in a block, or table, in memory, and the address of the block is passed as a parameter in a register (Linux uses this approach)
3. **Stack**:Parameters are placed, or pushed, onto the stack by the program and popped off the stack by the OS
## Program execution
- A program usually as a binary executable file. To run on a CPU, the code must be brought into memory and placed in the context of a process. The process of running a program involves:
1. **Compilation**: Convert source files into relocatable object file
2. **Linking**: Combine relocatable object file and libraries to generate an executable file ,resolving external reference(解析外部參考)
3. **Loading and Relocation**Loads the executable file into memory , assigns final addresses to the program parts, and adjusts code and data to match those addresses
## Why Applications are OS-specific?
- Applications compiled on one operating system are generally not executable on other operating systems because each operating system provides a unique set of system calls.
- Three ways to run code on multiple operating systems:
1. The application can be written in an interpreted language (such as Python or Ruby).
2. The application can be written in a language that includes a virtual machine containing a run-time environment (RTE)
3. The application developer can use a standard language or API, but the application must be ported and compiled for each specific operating system.
## OS Design and Implementation
- **Design Goals**: "User goals" state that the operating system should be convenient to use, easy to learn, reliable, safe, and fast. "System goals" state that the operating system should be easy to design, implement, and maintain, as well as flexible, reliable, error-free, and efficient.
- **Important Design Principle**: It is crucial to separate "Policy" (What will be done?) from "Mechanism" (How to do it?). This separation allows maximum flexibility if policy decisions need to be changed later.
- **Implementation Languages:** The lowest levels of the kernel are typically written in Assembly and C , while higher-level routines use C and C++. The advantages of using a higher-level language include faster development, more compact code, easier understanding and debugging, and easier porting to other hardware
## OS structure
- **Simple structure**: Such as MS-DOS , which was written to provide the most functionality in the least space but is not divided into modules, and its interfaces are not well separated.
- **Monolithic structure:** Such as the original UNIX , where all functionality is placed into a single, static binary file running in a single address space. Despite its apparent simplicity, it is difficult to implement and extend.
- **Layered approach:** The OS is divided into layers, with the bottom layer (layer 0) being the hardware and the highest (layer N) being the user interface. Each layer uses functions and services of only lower-level layers
- **Microkernels**: Such as Mach , which moves as much from the kernel into user space as possible. Communication takes place using message passing. Pros: Easier to extend, port, and offers more security and reliability. Cons: Performance can suffer due to the overhead of message copying and process switching
- **Modules**: Uses loadable kernel modules (LKMs). The kernel has core components and can link in additional services via modules, providing similar structure to layers but with more flexibility
- **Hybrid systems:** In practice, systems combine different structures to address performance, security, and usability issues. Linux is monolithic but also modular. Windows is mostly monolithic but retains microkernel behavior and supports dynamically loadable modules . macOS, iOS, and Android use a layered stack of frameworks over a kernel environment.
## Building and Booting
- Booting the system is the process of starting a computer by loading the kernel.
- **Boot process**: A small piece of code known as the bootstrap program or boot loader locates the kernel. The kernel is then loaded into memory and started. After that, the kernel initializes the hardware and the root file system is mounted.
## OS Debugging and Performance Monitoring
- Debugging is finding and fixing errors, or bugs
- **Ways to get error information:** Operating systems generate log files. An application failure can generate a core dump file capturing the memory of the process , while an operating system failure can generate a crash dump file containing kernel memory.
- **Performance Monitoring:** Operating systems keep track of system activity through a series of counters , such as top in Linux. Performance tuning can also involve profiling, which is the periodic sampling of the instruction pointer to look for statistical trends