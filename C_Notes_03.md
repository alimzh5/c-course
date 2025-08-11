### GCC `-g` Option
* Enables debug information to be included in the executable, allowing source-level debugging with tools like GDB.

* Also disables optimization by default, making debugging easier because the generated code closely matches the source.

* Without `-g`, debugging info is missing, and optimizations may rearrange or remove code, complicating debugging.
*****
### GDB `layout` Command
* The `layout` command in GDB controls the TUI (Text User Interface) display.

* `layout split` shows both the source code and the corresponding assembly instructions side by side.

* Useful for debugging at both high-level code and low-level machine instructions simultaneously.

