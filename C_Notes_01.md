# CPU Architecture: RISC vs. CISC
## 1. RISC (Reduced Instruction Set Computer)

Uses a small and simple set of instructions.

Each instruction typically takes one clock cycle to execute.

Emphasizes speed and efficiency.

Easier for pipelining and parallel execution.

Examples: ARM, MIPS, RISC-V.

## 2. CISC (Complex Instruction Set Computer)

Uses a large and complex set of instructions.

A single instruction can perform multiple low-level operations.

Instructions may take multiple clock cycles.

Designed to reduce the number of instructions in a program.

Examples: x86, VAX, System/360.

## Summary:

RISC → fewer, simpler instructions → faster execution per instruction.

CISC → more complex instructions → fewer instructions per program but possibly slower per instruction.

### CISC Architectures
**8086** – Intel’s original 16-bit x86 processor, basis of modern PC architecture.

**x86** – 32-bit Intel architecture, common in PCs and laptops.

**x86_64 (x64 / AMD64)** – 64-bit extension of x86, supports more memory and registers.

**Itanium (IA-64)** – Intel’s 64-bit architecture for high-end servers (discontinued).

**Z80** – 8-bit microprocessor used in early computers and embedded devices.

### RISC Architectures
**ARM** – Widely used in mobile devices and embedded systems.

**MIPS** – Common in embedded systems, networking devices, and older game consoles.

**RISC-V** – Open-source, modular, and customizable RISC architecture.

**PowerPC** – Used in older Apple computers, game consoles, and embedded devices.

**SPARC** – Developed by Sun Microsystems, used in servers and workstations.

____
### Firmware:
**Firmware** – Software programmed into a device’s non-volatile memory that runs independently to control the device’s hardware functions.
<br><br> 
**Pluggable Firmware OS** – A type of firmware-based operating system that, unlike regular firmware, can be replaced or upgraded like a plugin.
**Use case**: Allows switching between different tasks or applications through software instead of changing hardware.
____

****
**Unix** – A multiuser, multitasking operating system originally developed in the 1970s, foundation for many modern OS.

**BSD (Berkeley Software Distribution)** – A Unix-based OS developed at UC Berkeley, known for stability and networking features.

**Minix** – A small, educational Unix-like OS designed for teaching OS concepts.

**Linux** – An open-source Unix-like OS kernel created by Linus Torvalds, inspired by Minix.
****

****
### User Space vs Kernel Space
**Kernel Space**: The memory area where the core of the operating system (kernel) runs with full access to hardware. It manages system resources and controls hardware.

**User Space**: The memory area where user applications and programs run with limited privileges, isolated from direct hardware access.

### Program vs Kernel
**Program**: A set of instructions executed in user space by the CPU, performing specific tasks for the user.

**Kernel**: The central part of the OS running in kernel space, responsible for managing hardware, processes, memory, and system calls.
****

****
### Kernel Modules / Subsystems
**Kernel Module**: A piece of code that can be loaded into the kernel to add new functionality without rebooting.

**Subsystem**: A part of the kernel that handles specific functions or hardware.

Example in Windows:

Driver: A kernel module that enables the OS to communicate and work with specific hardware or software devices.

****
