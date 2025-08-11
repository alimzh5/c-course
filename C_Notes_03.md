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
