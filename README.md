# Description
- In this project, we implemented a basic interpreter with a text file that represents a program.
- When the program read that text file and start executing it, it becomes a process.
- We have 3 program files each representing a program.
- We created an interpreter that reads the txt files and executes their code. 
- We implemented a memory and save the processes in it.
- We also implemented mutexes that ensure mutual exclusion over the critical resources. 
- And finally, we implemented a scheduler that schedules the processes that we have in our system.

# System Calls
- System calls are the process’s way of requesting a service from the OS. 
- In order for a process to be able to use any of the available hardware, it makes a request, system call, to the operating system.


Types of system calls required:
1. Read the data of any file from the disk. 
2. Write text output to a file in the disk. 
3. Print data on the screen.
4. Take text input from the user. 
5. Reading data from memory. 
6. Writing data to memory.


# Memory
- One of the steps the OS does in order to create a new process is allocating a space for it in the main memory. 


- The OS is responsible for managing the memory and its allocation.


- The memory is of a fixed size. 


- It is made up of 40 memory words.

- The memory is large enough to hold the un-parsed lines of code, variables and PCB for any of the processes. 

- The memory is divided into memory words, each word can store 1 variable and it’s corresponding data.

- Processes should not access any data outside their allocated memory block.


- A process should only be created at it’s arrival time.


- A process is considered created when it’s program file is read into lines and it gets assigned a part of the memory for instructions, variables and it’s PCB. Assume that each process needs enough space for 3 variables.


- The memory is not large enough to run all the processes. When a new process is created, the system checks if there is enough space, if not the system will unload one of the existing processes and store it’s data on the disk. However while unloaded, the process remains in the scheduler, thus when it is time for the unloaded process to run again, the process memory is swapped back into the memory from the disk.


# Process Control Block
A process control block is a data structure used by computer operating systems to store all the information about a process in order to schedule processes.

The PCB should contains: 


1. Process ID (The process is given an ID when is being created) 

2. Process State


3. Program Counter


4. Memory Boundaries


# Programs
We have 3 main Programs:


- Program 1: Given 2 numbers, the program prints the numbers between the 2 given numbers on the screen.


- Program 2: Given a filename and data, the program writes the data to the file. Assume that the file doesn’t exist and should always be created.

- Program 3: Given a filename, the program prints the contents of the file on the screen.

# Program Syntax
For the programs, the following syntax is used:


• print: to print the output on the screen. Example: print x


• assign: to initialize a new variable and assign a value to it. Example: assign x y, where x is the variable and y is the value assigned. The value could be an integer number, or a string. If y is input, it first prints to the screen "Please enter a value", then the value is taken as an input from the user.


• writeFile: to write data to a file. Example: writeFile x y, where x is the filename and y is the data.


• readFile: to read data from a file. Example: readFile x, where x is the filename.


• printFromTo: to print all numbers between 2 numbers. Example: printFromTo x y, where x is the first number, and y is the second number.


• semWait: to acquire a resource. Example: semWait x, where x is the re- source name. For more details refer to section Mutual Exclusion.


• semSignal: to release a resource. Example: semSignal x, where x is the resource name. For more details refer to section Mutual Exclusion.
# Mutual Exclusion
- A mutex is a directive provided by the OS used to control access to a shared resource between processes in a concurrent system such as a multi-programming operating system by using two atomic operations, semwait and semsignal. 

- Mutexes are used to ensure mutual exclusion over the critical section.
We implemented 3 mutexes, one for each resource we have:


1. Accessing a file, to read or to write.

2. Taking user input.


3. Outputting on the screen.


Whenever a mutex is used, either a semWait or semSignal instruction is followed by the name of the resource, userInput, userOutput or file.

 For an illustration, to print on the screen:-
1. semWait userOutput: any process calls it whenever it wants to print something on the screen to acquire the key of the resource.


2. semSignal userInput: any process calls it whenever it finishes printing to release the key of the resource.


Note: ONLY ONE process is allowed to use the resource at a time. If a process requests the use of a resource while it is being used by another process, it should be blocked and added to the blocked queue of this resource and the general blocked queue.
# Scheduler
- A scheduler is responsible for scheduling between the processes in the Ready Queue. 


- It ensures that all processes get a chance to execute.


- A scheduling Algorithm is an algorithm that chooses the process that gets to execute.

- In this project, We implemented the Round Robin algorithm. Round robin is a scheduling algorithm where each process is assigned a fixed time slice. For this project, each process executes 2 instructions in its time slice.


- Processes arrive in this order: Process 1 arrives at time 0, Process 2 arrives at time 1, and Process 3 arrives at time 4.
# Queues
• Ready Queue: For the processes currently waiting to be chosen to execute on the processor


• Blocked Queue: For the processes currently waiting for resources to be available


# Output
The Simulated OS should be able to read the provided programs and execute them. 


We have the following outputs read to show:


• Queues should be printed after every scheduling event, i.e. when a process is chosen, blocked, or finished.


• Which process is currently executing.


• The instruction that is currently executing


• Time slice is subject to change, i.e. able to change it to x instructions per time slice.


• Order in which the processes are scheduled are subject to change.


• The timings in which processes arrive are subject to change


• The memory shown every clock cycle in a human readable format.


• The ID of any process whenever it is swapped in or out of disk.


• The format of the memory stored on Disk.
