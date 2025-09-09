# Basic gdb Debugging Steps

### 1.Compile with debug info (no optimization):
```
gcc -g -O0 ccod1.c -o test46
```

### 2.Start gdb:
```
gdb ./test46
```

### 3.Set a breakpoint at main:
```
(gdb) break main
```

### 4.Enable source code view (TUI):
```
(gdb) layout src
```

### 5.Run the program:
```
(gdb) run
```

### 6.Step through the code:

`next` → execute next line (don’t enter functions)

`step` → step into functions

### 7.Inspect variables:

`print var` → show value

`print &var` → show address

`x/s var` → show string at pointer

### 8.Continue / quit:

`continue` → run until next breakpoint

`quit` → exit gdb
