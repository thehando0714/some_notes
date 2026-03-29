# Thread
## Thread concept and structure
- A thread is a basic unit of CPU utilization
- Each thread include its own thread ID, program counter (PC), register set, and stack
- In a multithreaded process, although each thread has its own registers and stack, they share the process's code, data, and files
## Why multithreading and its benefits
- In the early days, a thread was sometimes called a lightweight process (LWP輕量級處理程序). If a thread is blocked, the CPU can switch to another thread to continue executing tasks
- Using a web server as an example, creating a new process to service a client request is time-consuming and resource-intensive(耗時又耗費資源), whereas(而) creating a thread is much more efficient.
- **Four major benefits of multithreading:**
    1. **Responsiveness(回應性)**: Multithreading an interactive application may allow a program to continue running even if part of it is blocked or performing a lengthy operation, thereby increasing responsiveness to the user(互動式應用程式即使部分被阻塞或正在執行冗長操作，程式仍能繼續執行，提高對使用者的回應速度)
    2. **Resourse sharing(資源共享)**: While processes usually share resources through techniques like shared memory and message passing, threads can directly share the resources of the process they belong to
    3. **Economy(經濟性)**: Allocating memory and resources for process creation is costly(成本高), making it more economical to create and context-switch threads
    4. **Scalability(可擴展性)**: In a multiprocessor architecture, the benefits are even greater as threads may run in parallel on different processing cores.
## Pthreads library(函式庫)
- A thread library provides the programmer with an API for creating and managing threads. There are two primary implementation approaches: a library entirely in user space, or a kernel-level library supported directly by the operating system.
- POSIX Pthreads (IEEE 1003.1c) is an API specification standard for thread creation and synchronization, rather than an implementation
- Any data declared globally are shared among all threads belonging to the same process.
## Concurrency(並行) vs. Parallelism
- **Concurrency:** A concurrent system supports more than one task by allowing all the tasks to make progress . This can be achieved even on a single-core system through interleaved execution(快速交錯執行).
- **Parallelism:** A parallel system can perform more than one task **simultaneously** across multiple cores
- Any data declared globally are shared among all threads belonging to the same process.
## Multicore Programming Challenges and Amdahl's Law
- Programmers face five key challenges when developing for multicore systems: Identifying tasks(識別任務), Balance, Data splitting, Data dependency, and Testing and debugging
- **Amdahl's Law:** This is a formula that identifies potential performance gains (speedup) from adding additional computing cores to an application that has both serial (nonparallel串列) and parallel components
- The formula is: $Speedup\le\frac{1}{S+\frac{1-S}{N}}$ , where $S$ is the portion of the application that must be performed serially(S是須串列執行的應用程式比例), and $N$ is the number of processing cores.
## 1. How do threads communicate with the OS? (Multithreading Models)
- **What is the problem?**: Support for threads may be provided either at the user level, for user threads, or by the kernel, for kernel threads. The issue is establishing a relationship(對應與溝通) between user threads and kernel threads.
- **Solution 1: Many-to-One Model**. This model maps many user-level threads to one kernel thread. The benefit is that thread management is efficient.
    - **The New Problem:** The entire process will block if a thread makes a blocking system call. Furthermore, multiple user threads cannot run in parallel on multicore systems.
- **Solution 2: One-to-One Model.** This model maps each user thread to a kernel thread. This provides more concurrency. Multiple threads can run in parallel on multiprocessors
    - **The New Problem**: Thread creation is very costly. The overhead of creating kernel threads can burden (拖垮)the performance of an application. Number of threads per process is sometimes restricted due to overhead
- **Solution 3: Many-to-Many Model.** This model multiplexes many user-level threads to a smaller or equal number of kernel threads. It allows the operating system to create a sufficient(足夠的) number of kernel threads. However, although flexible, in practice it is difficult to implement(難以實作).
## 2. What if there are too many threads? (Implicit Threading (隱式執行緒)& Thread Pools)
- **What is the problem?**:  Creating a separate thread requires a certain amount of time. Unlimited threads could exhaust system resources, such as CPU time or memory. Applications containing hundreds or even thousands of threads are looming on the horizon. Designing such applications is hard
- **Proposed Solutions:**
    - **Implicit Threading:** Transfer the creation and management of threading from application developers to compilers and run-time libraries. This is called implicit threading
    - **Thread Pools:**Create a number of threads at start-up and place them into a pool, where they sit and wait for work. When a server receives a request, it submits the request to the thread pool instead of creating a new thread.
- **The Benefits**: Servicing a request with an existing thread is often faster than waiting to create a thread. A thread pool limits the number of threads that exist at any one point.
## 3. Various challenges in a multithreaded environment (Threading Issues)
- **Semantics of fork() and exec()(系統呼叫的問題)**: Does fork() duplicate only the calling thread or all threads? Some UNIX systems have chosen to have two versions of fork(): one that duplicates all threads, and another that duplicates only the thread that invoked the fork() system call. The exec() system call typically works by replacing the entire process—including all threads—with the specified program.
- **Signal Handling:** A signal is used in UNIX systems to notify a process that a particular event has occurred. Where should a signal be delivered for multi-threaded? The 4 options are: deliver the signal to the thread to which the signal applies , to every thread in the process , to certain threads in the process , or assign a specific thread to receive all signals for the process
- **Thread Cancellation:** Thread cancellation involves terminating a thread before it has completed.   
    1. Asynchronous(非同步) cancellation means one thread immediately terminates the target thread. 
    2. Deferred (延遲)cancellation allows the target thread to periodically check whether it should terminate in an orderly fashion. **The default cancellation type is deferred cancellation**
- **Thread-Local Storage (TLS)(專屬資料的儲存)**: In some circumstances, each thread might need its own copy of certain data. For example, each transaction might be assigned a unique identifier, and to associate each thread with its unique transaction identifier, we could use thread-local storage. TLS data are visible across function invocations. TLS data are similar to static data. The difference is that TLS data are unique to each thread.