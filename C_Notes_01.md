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

****
### PE and ELF File Formats
**PE (Portable Executable)**:

The standard executable file format used in Windows.

Contains headers, sections for code, data, resources, and information needed by the Windows loader to run the program.

**ELF (Executable and Linkable Format)**:

The standard executable file format used in Unix/Linux systems.

Stores program instructions, data, symbol tables, and sections that help the OS loader manage the program.

**How OS Loads Executable Files**
The OS reads the executable’s header to understand its structure (e.g., code size, data size, entry point).

It loads the necessary sections (code, data) into memory.

It sets up the process environment (stack, heap, registers).

Finally, it jumps to the program’s entry point to start execution.
****
****
![Alt Text](https://github.com/alimzh5/c-course/blob/main/repository/C%D9%80Program%D9%80Compilation%D9%80Process.png)
Caption: The process of converting a C program into an executable: from source code through preprocessor, compiler, assembly, object file, linker, and finally to the executable.
****
****
### Assemblers
**NASM** – Netwide Assembler, popular for x86 architecture.

**MASM** – Microsoft Macro Assembler, assembler for Windows/x86.

### Compilers
**GCC** – GNU Compiler Collection, supports C, C++, and more.

**Clang** – Compiler frontend for C/C++/Objective-C, part of LLVM.

**Xcode** – Apple’s IDE with built-in LLVM/Clang compiler for macOS/iOS.

**Visual Studio** – Microsoft IDE with MSVC compiler.

**Intel C Compiler (ICC)** – Optimized C/C++ compiler from Intel.

**AMD Compiler** – AMD’s optimized compiler tools.

**Borland C** – Older C/C++ compiler and IDE for DOS/Windows.
***

****
### Macros in Preprocessing
Macro: A preprocessor directive that defines a name or expression to be replaced before compilation, often used for constants or simple code snippets.

### Metaprogramming
Writing code that generates or modifies other code at compile-time or runtime, allowing automation, code reuse, and dynamic behavior.
****

****
**Compiler**: Translates C source code into assembly, checks for errors, and may optimize the code for better performance.

**Assembler**: Converts assembly code line-by-line into equivalent machine code (object file).

**Linker**: Combines object files and libraries into a final executable format that the OS can run.
****

****
### Example GCC Compilation Command:
```
gcc test.c -o test
```
**gcc** – GNU Compiler Collection.

**test.c** – Source file written in C.

**-o test** – Output option, names the compiled executable test.
****

****
### File Paths in Linux
**Absolute Path**: Full directory path starting from / (root).

**Relative Path**: Path relative to the current working directory.

**Special directories**:

./ – Current directory.

../ – Parent directory.

**Command search path**:

If a command (e.g., ls) is run without specifying a path, the shell searches directories listed in the $PATH environment variable and runs the first match it finds.

Example:
```
echo $PATH
```
Shows the list of directories searched for executables.

****

****
**Statement**
An independent instruction in a program, usually ending with a semicolon ;.

Can stand alone and perform an action.

Example:
```
x = 5;
```
**Expression**
A combination of variables, values, and operators that produces a value.

Cannot do anything by itself unless part of a statement.

Example:
```
x + 3
```
****

****
## Data Type
Defines the storage format of data: includes size and structure (layout).

Specifies the valid operations that can be performed on the data.

## Basic Types:

**Integer** – Whole numbers.

**Float** – Numbers with fractional parts.

**Character** – Single characters.

## Note:
The compiler determines the data type of each value (e.g., whether it’s an integer, float, or character) during compilation.
****

****
### Addressing in 32-bit and 64-bit Systems

**32-bit system**:

Uses 32-bit addresses.

Can address up to 2^32 = 4,294,967,296 unique memory locations (~4 GB).

**64-bit system**:

Uses 64-bit addresses.

Can theoretically address up to 2^64 ≈ 1.84×10^19 memory locations (very large).

Note: Actual usable memory is usually less due to hardware and OS limitations.
****
