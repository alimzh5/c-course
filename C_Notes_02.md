### CPU and Task Scheduling
* The operating system runs on hardware and manages scheduling so that multiple programs can share the CPU.

* On a single-core CPU, parallel execution is an illusion created by rapidly switching tasks (time slicing).

* If too many tasks are running, the system slows down, and high CPU usage can reach 100%.

* CPU-intensive tasks (e.g., infinite loops) keep the CPU busy and block other work.

* A single program can use only one core unless it is multi-threaded or parallelized.

* Some code is dependent (sequential) and cannot be split across cores.

### CPU Frequency
* CPUs have a clock frequency (e.g., 2.4 GHz) meaning 2.4 billion cycles per second.

* Frequency can be fixed or variable (e.g., 2.4–2.9 GHz).

* Each instruction may require multiple cycles to complete.

* Higher frequency → faster execution, but more power usage and heat.

* CPUs can boost frequency temporarily under high load (dynamic frequency scaling).
****

**/proc Folder**
* A virtual filesystem where the kernel shares reports, status, and information with user space.

**Syscalls**
* Functions that allow user programs to request services from the kernel.

* Involve context switching, so they are slower than pure CPU operations.

**CPU-Intensive vs I/O-Intensive**
* CPU-Intensive: Tasks that require heavy computation (e.g., math loops).

* I/O-Intensive: Tasks that mainly wait for input/output (disk, network, sleep, etc.) and use little CPU.

* Mixed workloads may still be called CPU-intensive if computation dominates.

**OS Scheduling**
* In time-sharing systems, too many tasks can cause delays and missed deadlines.

**RTOS (Real-Time Operating System)**
* Guarantees that a task will run at a specific time, unlike general time-sharing OS where delays are possible.

****

**FreeRTOS** – A lightweight, open-source real-time operating system widely used in embedded and IoT devices.

**Zephyr** – A scalable, open-source real-time operating system designed for embedded devices, supporting multiple architectures.
****
### Async & Non-blocking Programming
* In non-blocking programming, you don’t wait for a task to finish before moving on; instead, you check later if it’s ready.

* Example: read from a network — if data exists, take it; if not, move to the next task and check again later.

* You can also set timeouts to avoid waiting too long for one task.

* This allows multiple tasks to progress in parallel, similar to software-level time-sharing.

### Detecting Changes
* **Polling** – Regularly check if something changed (CPU intensive and inefficient).

* **Polling with Sleep** – Pause between checks to reduce CPU load (still inefficient if changes are rare).

* **Interrupts** – Hardware notifies you when an event happens (efficient).

* **Inotify** – Software mechanism to notify on file changes.

* **Signals** – OS interrupts the normal flow to handle a specific event.

### Select
* A system call that monitors multiple file descriptors (e.g., sockets or files) and tells you when one is ready for reading/writing.

****
### `movl` in Assembly
In x86 assembly, `movl` means move 32-bit (long) data from one place to another.

Example: `movl %eax, %ebx` → copy value from EAX register to EBX register.
****
### GCC Compilation Steps
```
# Generate assembly code from C
gcc -S test.c -o test.s

# Compile with debug info for GDB
gcc -g test.c -o test
```
****
### Debugging with GDB (TUI mode)
```
# Open in GDB with Text User Interface
gdb -tui ./test

# Split view: source code + assembly
layout split
```
***
### GDB Common Commands
`ni` (next instruction) → Executes the next assembly instruction.

`b <line>` → Set breakpoint at the given source line (e.g., `b 4` → start debugging at line 4).

`step` → Go inside function calls, execute line by line (source level).

`next` → Execute the current source line but skip inside functions.
****
### Code Modification & Security Risk
If code is modified between instructions (e.g., between line 3 and 4), the binary’s hash changes.

In security, this can be exploited — malicious code (virus) could be injected at runtime via such modifications.

Example: Interrupting execution, editing instructions in memory, and resuming.
*******
## GDB Basic Workflow
### Compile with debug info

`gcc -g test.c -o test`
### Start GDB

`gdb ./test`
### (Optional) Set breakpoints

`b 4`        # Break at line 4
### Run the program

`run`
### Debug commands

**Command**-------**Description**

  `step`------------Execute next line, enter functions
  
  `next`------------Execute next line, skip over functions
  
  `ni`--------------Execute next assembly instruction
  
  `si`--------------Step into assembly call
  
  `continue`--------Resume until next breakpoint
  
  `layout split`----Show source + assembly side by side

****
### C Data Types & Memory Representation
* `int` – 4 bytes (commonly), stored in 2’s complement for signed integers.

* `float` – Single precision floating point (IEEE 754, 4 bytes).

* `char` – 1 byte, stores a single character or small integer.

* `double` – Double precision floating point (8 bytes).

* `struct` – Group of variables under one name, stored in contiguous memory with possible padding.

* `union` – Variables share the same memory location, size equals the largest member.

* `array` – Sequential elements of the same type in memory.

* `enum` – Named integer constants.

* `pointer` – Stores a memory address, size depends on architecture (e.g., 8 bytes in 64-bit).

* `void` – No value, used for functions that return nothing or generic pointers (void*).

**Key idea**:
* The compiler uses type information to know:

* How many bytes to read/write.

* How to interpret (decode) the raw bits.

* Layout and ordering in memory (e.g., `A` before `B` in a struct is compiler/ABI-defined).
****
### Virtual Memory & Memory Allocation in Operating Systems
An operating system manages RAM by dividing it into small chunks (pages or segments) and assigning them to programs as needed.
When a program starts, it is given an initial block of memory. If it needs more, the OS allocates additional memory over time.

**Two main problems with direct (physical) allocation**:

1) **Non-contiguous allocation**:
A program might receive blocks like addresses 1,2,3,4 at first, but when more memory is needed, the OS may give 7,8,9,10 instead of 5,6.
This creates fragmentation and makes it harder for programs to treat memory as one continuous space.

2) **Unknown addresses at compile time**:
When compiling a program, the exact physical memory location is not yet known.
This means we cannot store real physical addresses in the generated machine code.

### Solution: Virtual Memory

* The CPU and OS provide a virtual address space for each program.

* For example, in a 32-bit system, each process can address up to 4 GB of memory, regardless of how much RAM is physically installed.

* The OS maintains a mapping (via the MMU — Memory Management Unit) between virtual addresses and physical addresses.

* The program works with virtual addresses, and the OS transparently translates them to real locations in RAM.

### Benefits:

* Programs can use contiguous virtual memory even if physical memory is scattered.

* Prevents programs from interfering with each other’s memory.

* Allows features like paging, swapping, and memory protection.
****
### Memory Layout of a Process
When a program is loaded into memory, its address space is divided into several regions, each with a specific purpose:

1) **Text Segment**

* Contains the compiled program code (machine instructions).

* Usually read-only to prevent accidental modification of code during execution.

* Shared among processes running the same program to save memory.

2) **Data Segment**

* Stores global and static variables that are initialized in the source code.

* Example:

```
int counter = 5; // goes into data segment
```
3) **BSS Segment** (Block Started by Symbol)

* Stores uninitialized global and static variables.

* Example:

```
int counter; // no initial value → goes into BSS
```
* This section is zero-initialized at program start.

4) **Heap**

* Used for dynamic memory allocation (malloc, calloc, new in C/C++).

* Grows upwards toward higher memory addresses as more memory is allocated.

5) **Stack**

* Stores function call frames, local variables, and return addresses.

* Grows downwards toward lower memory addresses.

* Managed automatically by the compiler.

6) **OS Kernel Space**

* Reserved for the operating system kernel and device drivers.

* User programs cannot directly access this space (for security and stability).
****
### Dynamic vs Static Memory
* **Static / Compile-time Memory**

  * Allocated at **program load** (before execution starts).

  * Includes:

    * **Text segment** (code)

    * **Data segment** (initialized globals/static)

    * **BSS segment** (uninitialized globals/static)

  * Size is fixed and known at compile time.

* **Dynamic Memory** (Heap & Stack)

  * Created and freed at runtime.

  * **Heap**:

    * Starts empty and grows upward as you allocate memory with malloc/new.

    * Freed explicitly by the programmer (free/delete).

  * **Stack**:

    * Starts at the top of the process memory space and grows downward as functions are called.

    * Freed automatically when the function returns.

  * If heap and stack meet → Out of memory (stack overflow or heap collision).

### Stack Overflow & Exploits
* Stack overflow happens when more data is pushed to the stack than it can hold.

* In C, this can occur if you write beyond the bounds of a local array:

```
void foo() {
    char buf[10];
    gets(buf); // if input > 10 bytes → overflow
}
```
* Attackers can overwrite the return address on the stack, making the program jump to malicious code (possibly stored in the heap or even in the stack itself).

* Firmware is especially vulnerable because:

  * Often written in C/C++ (no automatic bounds checking).

  * Sometimes lacks modern protections like ASLR or stack canaries.

****
### Modifiers and Integer Types in C
* Modifiers change how the compiler treats variables and types.

* `signed` and `unsigned` specify whether integers can be negative.

  *Signed integers use 2's complement representation.

* Integer sizes:

  * `short` (usually 2 bytes)

  * `int` (commonly 4 bytes, default integer type)

  * `long` (4 or 8 bytes depending on system)

  * `long long` (at least 8 bytes)

* Example: Number 300 stored in 2 bytes:

```
[00000001] [00101100]
```
*****
### Endianness
* **Big Endian**:

  * Stores the most significant byte first (lowest memory address).

  * CPU waits for the most significant byte before starting calculations.

  * Used in older CPUs and many network protocols by default.

* **Little Endian**:

  * Intel introduced this idea.

  * Stores the least significant byte first (lowest memory address).

  * Bytes are reversed compared to big endian, but bit order inside each byte remains the same.

  * Enables faster computation start since least significant byte arrives first.

  * Used in most modern CPUs and devices.

*****
