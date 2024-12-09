# Why???

- Share resources and improve responsiveness
- Using parallel hardware and speeding executions up
- Scaling to do more of the same.

## Today's Hardware

Today, computer architecture is largely standardized, at a high level of abstraction, on the von Neumann Architecture:

![[Pasted image 20241209141516.png]]

### The Processor

- Often also referred to as the Central Processing Unit (CPU) 
- ALU + Control Unit 
- CPU-internal and high-speed cache memory

![[Pasted image 20241209141552.png]]

### Multi-Core Processors
We see a renewed interest in parallel architectures

Faster, although 
- They complicate system software 
- Not always possible to hide the complexity from application software (esp. to take full advantage of hardware)

![[Pasted image 20241209141641.png]]

## Another Multi-Core Architecture

![[Pasted image 20241209141714.png]]

## Coarser-Grained Parallelism: Clusters
We can also increase performance by linking computers using high-speed networks.

Idea of servers 
- They don't all need screens, etc. 

Applications run across the cluster (ideally) 
- Again: some applications cannot easily be decomposed in this way

# Concurrency? Parallelism? Our Terminology!

… when people hear the word concurrency they often think of parallelism, a related but quite distinct concept.

In programming, **concurrency** is the composition of independently executing processes, while parallelism is the simultaneous execution of (possibly related) computations.

**Concurrency is about dealing with lots of things at once. Parallelism is about doing lots of things at once.**

## Concurrency Vs Parallelism

- **Concurrency**
	- **Key Idea**: These actions can overlap in time but do not necessarily execute simultaneously.
	
	- Supports to have two or more actions in progress at the same time.
	- Demands **scheduling** and **synchronization**
	- Classical operating system responsibility (resource sharing for better utilization of CPU, memory, network)
	
- **Parnellism**
	- **Key Idea**: These actions are performed literally at the same time, often leveraging multiple processing units.

	- Supports to have two or more actions executing simultaneously 
	- Demands **parallel hardware**, **concurrency support**, (and **communication**) 
	- Programming model relates to available hardware and communication

# Classes of Concurrent Programs
There are many different methods to enable concurrent programs

We distinguish two main classes: 

- **Shared memory** locations are read and modified to communicate between concurrent components. Requires **synchronization** to ensure that communication happens safely. **We will mainly look at explicit concurrent systems programming with threads and use shared memory communication.** 

- **Message passing** tends to be far easier to reason about than sharedmemory concurrency, and is typically considered a more robust form of concurrent programming. Examples of message-passing systems are the actor model implemented in Erlang or CSP-style communication in Go. **Covered in the Distributed and Parallel Technologies H/M course**

## Communication Models
Two models of Inter Process Communication (IPC)

- Message Passing
- Shared Memory

![[Pasted image 20241209143733.png]]

# Processes and Threads

- A process is a program in execution that needs resources 
	- A program is a passive entity (executable file) 
	- A program becomes a process when its executable is loaded into memory 
	- Each process has its own memory address space 

- Multiple processes can be executed simultaneously 
- One program can involve several processes 
- One program can be started multiple times, each time in one or more additional processes

## Threads of Processes

![[Pasted image 20241209143848.png]]

## Processes Vs Threads

**Threads**:
- A thread of execution is an independent sequence of program instructions 
- Multiple threads can be executed simultaneously 
- A process can have multiple threads sharing the same address space of the process, giving all threads access to the memory of the process (both heap and stacks, actually – but you should not access another thread's stack) 
- We will use threads to implement concurrent programs 

**There is a program counter, specifying the location of the next instruction to execute, per thread:** 
- A single-threaded process has one thread with a program counter 
- A multi-threaded process has multiple program counters (one program counter per thread)

Threads of a process share memory and resources by default 
- Processes require specific communication mechanisms (shared memory, message passing) to be set up 

Threads are faster/more economical to create 
- Each process has its own copy of the in-memory data, hence process creation means data duplication (at least of page tables) 

Can have different schedulers for processes and threads 
- Depends on how threads are implemented (user threads vs kernel threads) 

If a single thread in a process crashes, the whole process crashes as well 
- If a process dies, other processes are unaffected