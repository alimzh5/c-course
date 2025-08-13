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

**Example**:
```
int add(int a, int b) {
    return a + b;
}
```

******

### Two ways to use a function call and print the result
**Method 1**: Store the function’s return value in a variable, then print it.

```
int sum = add(a, b);
printf("%d", sum);
```
**Method 2**: Call the function directly inside `printf`.

```
printf("%d", add(a, b));
```
Both produce the same output. The choice depends on whether you need to reuse the result later.

****
### Function Call in C

* When a function is called, the compiler replaces the call with code that:

  1) Copies the arguments into the function’s parameters (by value, unless pointers are used).

  2) Jumps to the function’s code.

  3) Executes the function body.

  4) Returns control (and a return value, if any) to the caller.

* In C, arguments are passed by value by default, meaning the function receives a copy of each argument, not the original variable.
*****

### Why the compiler’s generated assembly may have extra instructions

1) Not optimized yet – In non-optimized builds, the compiler generates straightforward code without removing redundancies. This often means more load/store instructions and less efficient execution.

2) Lack of future knowledge – The compiler cannot predict all later operations during early code generation, so it may store intermediate results in memory instead of keeping them in registers. For example, when adding two variables, it might first store them in memory and then add, even though it could have added them directly.
*******

![Alt Text](https://github.com/alimzh5/c-course/blob/main/repository/code_in_c.png)

******

```
#include <stdio.h>

int add(int a,int b);

int main(){
    int x=10;
    int y=11;
    int c = add(x,y);
    printf("%d",c);

}

int add(int a ,int b){
    return a+b;
}
```
result: 21
********

### Arithmetic Operators in C

* **Assignment & compound assignment**:
`=` `+=` `-=` `*=` `/=` `%=`

* **Basic arithmetic**:
`+` `-` `*` `/` `%` (modulus)

**Bitwise Operators**

* `&` (Bitwise AND)

* `|` (Bitwise OR)

* `^` (Bitwise XOR)

* `~` (Bitwise NOT)

* `>>` (Right shift)

* `<<` (Left shift)

**Precedence**:

* Multiplication (`*`), division (`/`), and modulus (`%`) have higher precedence than addition (`+`) and subtraction (`-`).

*******
**Empty statement in `if` condition**

* **Old style**:

```
if (a == 20) { ; }
printf("yes");
```
* **New style**:
```
if (a == 20) { }
printf("yes");
```
**Result**: In both cases, `"yes"` is always printed because the `if` body is empty and the `printf` is outside the `if` statement.

**Note**: The semicolon (`;`) as a statement means “do nothing” but still counts as the body of the `if`.
****

![Alt Text](https://github.com/alimzh5/c-course/blob/main/repository/if_in_c.png)

*******
```
#include <stdio.h>

int add(int a,int b){
    return a+b;
}

int main(){
    int a,b,sum;
    scanf("%d",&a);
    scanf("%d",&b);
    sum=add(a,b);
    if(sum==20) printf("yes");
    else printf("no");
}
```
result:
12

8

`yes`
*******

`else if` **and** `else`

* `else if { }` – Executes the block if the previous `if` was false and this condition is true.

* else `if (...) { ... }` – Same, but with a specific condition.

* `else if` can be chained, and a simple `else` executes if none of the previous conditions are true.

`while` **loops**

* `while (...) { }` – Executes repeatedly as long as the condition is true.

* `while (1) { }` – Infinite loop (never ends unless a `break` or `return` is used).

* `while (1);` – Infinite loop with no body, keeps the CPU fully busy doing nothing.

**Note on** `while(1);`

* On general-purpose CPUs, this wastes resources (100% CPU usage) and prevents the rest of the code from running.

* On microcontrollers, such loops are sometimes intentionally used to keep the system active and prevent entering a halt/low-power state.

******

`while` **vs** `do while`
`while` – Checks the condition first. If false initially, the loop body may run zero times.

`do while` – Executes the loop body once before checking the condition. Always runs at least once.

*******

`for` **loop syntax**
```
for (init; condition; update) {
    // loop body
}
```
Example:

```
for (a = 0; a < 10; a = a + 1) { }
```
* Any expression can be used in each part.

* `while(1);` is equivalent to `for( ; ; );`.

* Any section can be left empty and handled inside the loop body (e.g., updates done inside).

* Initialization can declare variables (`int i = 0;`) which exist only during the loop’s lifetime.

*********

**Loop control**
`continue;` – Skips the rest of the loop body and jumps to the next iteration.

`break;` – Immediately exits the loop, regardless of the condition.

**********

`switch` **statement**
```
switch (a) {
    case 1:
        ...
    default:
        ...
}
```
* The variable must be an integer type.

* Cases test discrete, constant values.

* Faster than multiple `if` statements because it uses a jump table for direct branching, while `if` needs sequential comparisons.

* Fall-through behavior: If a `break` is omitted, execution continues into the next case(s).

*******

Using `break` in `switch-case`

* A `break;` statement is used to exit the switch immediately after a case executes.

* Without `break`, execution falls through to the next case(s).

* So we put `break` to prevent the following cases from executing.

Example:

```
switch(x) {
    case 1:
        printf("One\n");
        break; // prevents case 2, 3, etc. from executing
    case 2:
        printf("Two\n");
        break;
}
```

*******

**Grouping multiple cases in** `switch`
* You can stack multiple `case` labels without `break` between them to execute the same code block.

* Example:

```
switch (x) {
    case 0:
    case 5:
    case 10:
        printf("10\n");
        break;
}
```
* Meaning: if `x` is 0, 5, or 10, the same `printf` is executed.

* `break`; ensures the program exits the `switch` after executing the shared block.

* This technique is called fall-through grouping and is useful for handling multiple discrete values in the same way.

****


