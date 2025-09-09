Basic gdb Debugging Steps

Compile with debug info (no optimization):

gcc -g -O0 ccod1.c -o test46


Start gdb:

gdb ./test46


Set a breakpoint at main:

(gdb) break main


Enable source code view (TUI):

(gdb) layout src


Run the program:

(gdb) run


Step through the code:

next → execute next line (don’t enter functions)

step → step into functions

Inspect variables:

print var → show value

print &var → show address

x/s var → show string at pointer

Continue / quit:

continue → run until next breakpoint

quit → exit gdb
