### GCC `-g` Option
* Enables debug information to be included in the executable, allowing source-level debugging with tools like GDB.

* Also disables optimization by default, making debugging easier because the generated code closely matches the source.

* Without `-g`, debugging info is missing, and optimizations may rearrange or remove code, complicating debugging.
*****
### GDB `layout` Command
* The `layout` command in GDB controls the TUI (Text User Interface) display.

* `layout split` shows both the source code and the corresponding assembly instructions side by side.

* Useful for debugging at both high-level code and low-level machine instructions simultaneously.
******
### Debugging View: Source and Assembly Code

![Alt Text](https://github.com/alimzh5/c-course/blob/main/repository/Debugging%20View%20Source%20and%20Assembly%20Code.png)

****
### Process, Thread, and Core Explained
* **Process**:
A process is an independent program running in its own memory space.
Each process has its own separate memory (code, data, stack, heap).
For example, if you run 4 processes, the OS allocates 4 separate memory spaces for them.

* **Thread**:
A thread is a lightweight unit of execution within a process.
Multiple threads inside the same process share the same memory space (code, data, heap).
This makes communication and context switching between threads faster and easier.
For example, 4 threads in one process share one memory space.

* **Core**:
A core is a physical processing unit inside the CPU.
Each core can execute one or more threads concurrently.
For example, a CPU with 4 cores can run 4 threads truly in parallel.

**Summary**:

* Processes are isolated and have separate memory, so heavier and slower to switch between.

* Threads share memory inside the same process, lighter and faster to switch.

* Cores are hardware units that run threads.

****

### Data Types and Portability in C

* C is not object-oriented, and you cannot perform operations like addition directly on structs.

* Except for struct, union, enum, and array, all other types represent numbers.

* Even char is a number type occupying 1 byte in memory.

* Everything in memory is stored as numbers (bits and bytes).
  
****

### Writing Portable Code for 32-bit and 64-bit Systems

* Standard integer types like `int8_t`, `uint8_t`, `int64_t` are not part of the original C standard, but come from libraries (e.g., `<stdint.h>`).

* Using these types ensures fixed size but creates a dependency on those libraries.

* Another method is using macros to detect the platform (32-bit or 64-bit) and change data types accordingly.

* The macro can call the proper library functions or typedefs based on the detected system.

* Modifiers like `short`, `long`, `signed` change size or sign of the type.

* Example: On a 64-bit system, `int` might be equivalent to `signed long int`.
  
****

### C Has No Runtime Overhead

* C does not have a runtime system that adds extra code during program execution.

* No automatic checks or protections are added by the compiler or runtime.

* Example: If you store the number 300 in a 1-byte variable, it wraps around and stores 44 (300 mod 256 = 44).

* This wrap-around (overflow) behavior can sometimes be used intentionally in programs.

* However, it can also lead to bugs if not handled carefully.

****

### Runtime and Writing Operating Systems

* Languages like C, C++, and Rust do not require a runtime system by default (or have minimal runtime).

* Because they lack heavy runtime overhead, they are well-suited for writing operating systems and low-level system software.

* This gives programmers full control over memory, hardware, and execution without hidden layers interfering.

* Many OS kernels and embedded systems are written in these languages for this reason.

****

### No Runtime Means Direct CPU Execution

* When a language has no runtime, the compiled code runs directly on the CPU without extra layers or virtual machines.

* This allows maximum control and efficiency, since no additional code runs behind the scenes.

* Languages like C produce such code that interacts closely with hardware and OS.

****
**Declaration**

* Tells the compiler what exists (name, return type, parameters) but not how it works.

* No memory allocation for code or variables (except for extern variables).

* Example:
```
int sum(int a, int b); // Declaration only
```

**Definition**

* Provides the actual implementation or allocates memory.

* Contains the body of the function or initializes variables.

* Example:

```
int sum(int a, int b) { // Definition
    return a + b;
}
```

**In functions**:

Writing the function body is both a declaration and a definition.

The compiler needs declarations to know the interface, but needs the definition to actually generate code.

****
```
#include <stdio.h>

int main(){
    unsigned char a;
    scanf("%d",&a);
    printf("%d\n",a);
    a+=200;
    printf("%d\n",a);
    return 0;
}
```
result:
```
100
100
44
*** stack smashing detected ***: terminated
Aborted (core dumped)
```
****
```
// Declaration only
void test(int, int);
```
* Here, you only tell the compiler that a function named test exists, takes two int parameters, and returns nothing.

* No body → no implementation → no actual code generated for test.

Definition example (with implementation):

```
// Definition
void test(int a, int b) {
    // function body
}
```
* Here you really implement the body, so the compiler generates machine code for it.

****
```
gcc -c -g 01.c -o 01
````
The `-c` option tells GCC to compile only and stop before the linking stage.

This produces an object file (`01` in this case) without creating an executable.

**Compile-time vs. Runtime warnings/errors**

Compile-time: The compiler can give errors or warnings if it detects issues from the source code (e.g., type mismatch, unused variables).

Runtime: Errors or crashes that happen while the program is running. These are not caught by the compiler.
****
### Order of declaration and definition in functions

* A declaration of a function must appear before it is used, because the compiler reads the code from top to bottom and needs to know the function’s interface in advance.

* A definition (implementation) can appear after the function is used, as long as a declaration was provided earlier.

* Example:

```
// Declaration
void test(int, int);

int main() {
    test(3, 4); // OK, compiler already knows test()
}

// Definition
void test(int a, int b) {
    // function body
}
```
****
The crash is caused by using the wrong `scanf` format specifier. `%d` expects an `int` (4 bytes) but the variable is `unsigned char` (1 byte). This causes `scanf` to overwrite memory on the stack (stack buffer overflow), triggering stack smashing detected when the function returns.

The `\n` in `printf` does not fix the bug — it only forces the output buffer to flush immediately, changing when you see printed values and the error message. The actual detection happens at the end of the function, not at the moment of the overflow.
****
### Variable definition in C

* A variable definition allocates memory for the variable and optionally initializes it.

* Examples:

  * `int data;` → defines `data` without initialization (contains garbage value).

  * `int data2;` → same as above.

  * `int a, b, c;` → defines three uninitialized integers.

  * `int d = 1, e = 0, f;` → defines three integers, initializes `d` to 1, `e` to 0, and leaves `f` uninitialized.

Uninitialized variables have indeterminate values and should not be used before assignment.
*****

### Storage Class in C
Specifies where data is stored, its initial value, scope (where it can be accessed), and lifetime (how long it exists).

**1. auto (default for local variables)**

  * **Storage**: Stack.

  * **Initial value**: Garbage (indeterminate).

  * **Scope**: Block {} where it is defined.

  * **Lifetime**: Until the block ends.

  * **Note**: Most local variables are auto by default.

**2. extern**

  * **Storage**: Data segment (initialized) or BSS segment (uninitialized).

  * **Initial value**: 0 if not explicitly initialized.

  * **Scope**: Global.

  * **Lifetime**: Entire program run.

  * **Purpose**: Access global variables defined in another file or location.

**3. static**
   
  * **Storage**: Data segment (if initialized) or BSS (if uninitialized).

  * **Initial value**: 0 if not initialized.

  * **Scope**:

    * **Global static**: visible only within the file.

    * **Local static**: visible only in the block, but retains value between calls.

  * **Lifetime**: Entire program run.

**4. register**
  * **Storage**: CPU register (if available).

  * **Initial value**: Garbage.

  * **Scope**: Block.

  * **Lifetime**: Block.

  * **Note**: Similar to auto, but stored in registers for faster access.
****

`main` **Function Signatures in C**
* `int main(int argc, char* argv[], char **envp)`

* `int main(int argc, char* argv[])`

* `int main()`

All are valid forms, with the first providing access to command-line arguments and environment variables.

*****

**Function Basics in C**
* Syntax:

```
return_type function_name(parameter_type parameter_name, ...);
```
* C does not support optional parameters—all arguments must be provided explicitly when calling the function.

* C does not support function overloading—you cannot have multiple functions with the same name but different parameters.

* Function names must be unique at the global scope. No spaces allowed in names.

*****

Example:
```
int add(int a, int b) {
    return a + b;
}
```

******
