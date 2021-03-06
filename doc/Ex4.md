# HPC exercise 4
###### tags `uni-rostock` `HPC`

## Table of Contents
<!-- ts -->
* [Task4.1](#t1)
* [Task4.2](#t2)
* [Task4.3](#t3)
* [Task4.4](#t4)
* [Task4.5](#t5)
* [Task4.6](#t6)
* [Task4.7](#t7)
* [Task4.8](#t8)
<!-- te -->


<a name="t1">
  
## Task 4.1: Introduction to operating systems
**Question**\
Give the definition of operating systems according to DIN 44300 and explain the duties of an operating systems.

**Answer**\
The programs of a digital computer system which, together with the properties of the computer system, form the basis of the possible operating modes of the digital computer system and, in particular, control and monitor the execution of programs.

<a name="t2">
  
# Task 4.2: Multiprogramming
**Question**\
What do you understand by multiprogramming?

**Answer**\
Multiprogramming is a computer running more than one program at a time. It's done by process scheduling which is handled by an operating system. The OS is constantly doing context switch, storing state of running process in PCB, and dispatches other process. ALthough, there's small overhead doing context switch, it is a way to hide (I/O) latency and utilize the computer more efficiently.

<a name="t3">

## Task 4.3: Virtual memory
**Question**\
A machine has a 32-bit byte-addressable virtual address space. The page size is 4 KB. How many pages of virtual address space exist?

**Answer**\
4 KB = <img src="https://render.githubusercontent.com/render/math?math=2^{12}">bit

<img src="https://render.githubusercontent.com/render/math?math=2^{32} / 2^{12} = 2^{20} = 1"> million

<a name="t4">

## Task 4.4: File systems
**Question**\
Compare the bit-map with the free-list methods for keeping track of free space on a disk with 800 cylinders, each one having 5 tracks of 32 sectors. How many holes would it take before the hole list would be larger than the bit map? Assume that the allocation unit is the sector and that a hole requires a 32-bit table entry.

**Answer**\
schematic of the hard drive geometry:\
<img alt="schematic of the hard drive geometry" src="https://upload.wikimedia.org/wikipedia/commons/4/41/Hard_drive_geometry_-_English_-_2019-05-30.svg" width="500">
> source: [Wikipedia](https://en.wikipedia.org/wiki/Cylinder-head-sector)
 
(a) bit map method\
Size of bit map equals to the number of blocks. In this case, no. of blocks equals to no. of sectors, which is cylinders x track x sectors = 800 x 5 x 32 = 128000 (bit)

(b)free list method (linked list method)\
A hole requires 32-bit table entry. 128000 / 32 = 4000.

Ans: 4000 holes

<a name="t5">

## Task 4.5: Scheduling
**Question**\
Which scheduling strategies do you know? Give the scheduling strategy that is used in practice.

**Answer**\
(1) Preemptive v.s. Non-preemptive
* Preemptive\
  - A running process can be suspended in order to schedule another process
* Non-preemptive
  - Processes run until they become blocked by issuing a system call

(2) Priority-based\
Each process is assigned with a priority. CPU executes the process with the highest priority. Priority-based method can be preemptive or non-preemptive. The problem of priority-based method is that the process with lower priorty could be postponed by indefined time.
* Static priority
  - The priority of a process is fixed over time.
* Dynamic priority
  - The priority of a process changes over time, e.g. priority is increased for process that are ready for a long time.

(3) FIFO: first-in-first-out, non-preemptive

(4) Round-robin (RR): dynamic proirties with round-robin in each priority\
RR is a preemptive algorithm without priority. RR give every process an equal share of time. RR allows each process to be executed for a limit time slice, and then the scheduler suspends the process and dispatchs another process.

In practice: dynamic priorities with round-robin in each priority.

<a name="t6">

## Task 4.6: Process interaction
**Question**\
Explain the process of connection-oriented client-server communication.

**Answer**\
Connection-oriented: Before two devices sending any data to each other, they first establish a connection.\

TCP (a connection-oriented client-server communication protocol)\
* Establish a connection (3-way handshake)
  1. client send "SYN"(synchronize) message to server
  2. server send "SYN ACK"(synchronize acknowledgement) to client
  3. client send "ACK" to server
* Connection Termination
  1. client send "FIN"(finish) to server
  2. server send "ACK" to cient
  3. server runs termination process, after the process finish, server send "FIN" to client
  4. client send "ACK" to server

Socket: An endpoint of a two-way communication link between two programs running on the network. A socket is identified with ip address and port number.

<a name="t7">
  
## Task 4.7: Synchronization in shared-memory environments
**Question**\
The producer-consumer problem can be extended to a system with multiple producers and consumers that write (or read) to (from) one shared buffer. Assume that each producer and consumer runs in its own thread. Will the solution presented in the lecture using semaphores, work for this system?

**Answer**\
Yes. With 1 mutex for critical section "buffer access", and 2 semaphores as empty and full respectively.

<a name="t8">

## Task 4.8: Virtualization
**Question**\
What is virtualization? What is a virtual machine? Please explain the differences between a VMM Type I and a VMM Type II!

**Answer**\
“Virtualization is the simulation of the software and/or hardware upon which other software runs. This simulated environment is called a virtual machine (VM). The front-end of a virtual machine is a lot like a regular computer, but in the back-end, they're different.\
Virtual machines on the same computer are managed by a hypervisor.

* TypeI
  - Hosted directly on the hardware of a computer
* Type II
  - Run as an application on the top of an operating system installed on the host computer


|  |Type I|Type II|
|--|--|--|
|Executing Application|faster|slower|
|I/O Speed|faster|slower|
|Example|VMWare ESXi,<br> Hyper-V,<br> KVM(open source)|VMWare workstation,<br> VirtualBox|
