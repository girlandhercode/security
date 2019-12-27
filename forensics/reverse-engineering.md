# Reverse Engineering



### Reverse \(WIP\) <a id="reverse-wip"></a>

Determine type of file

```text
file filename
```

High Level Overview of process

```text
strings
```

To view plaintext \(potentially passwords and text printing to screen\)

Try simple buffers to input functions:

```text
python -c 'print "A"*2000'
```

to view library calls

```text
ltrace
```

to view system calls

```text
strace
```

Break down and disassemble

```text
gdb

set disassembly-flavor intel

disass main
```

review the calls and any cmp and jne functions. May lead to potential passwords which are used in the compare function or jump if not equal.

view functions may be an easy win

```text
gdb

info fucntions

call <name of interesting function>
```

### **Radare2** <a id="radare2"></a>

to start

```text
r2 -d filename
```

start code analysis

```text
> aaa
```

to print all functions

```text
>afl
```

to move location to main function \(seek to location of function main\)

```text
>s [name of main function from previous command]
```

to view the dissassembyl of current function

```text
>pdf
```

To enter visual mode helpful for stepping thorugh and debugging

```text
V
then 
pp
```

to see visual mode like IDA

```text
>VV

# you can hit ? to view all options within this mode
```

to see visual mode that also shows registers, stack and dissassembly

```text
>V!
```

to enter command mode

```text
:     #colon enters the command mode
```

to exit command mode

```text
[enter key]   #enter key exits command mode
```

to run the application with parameters in debug

```text
>:ood [parameter]  #initiate
>:dc #execute
```

set a breakpoint

```text
>:db 0x00460649

then above two commands to rerun
```

to view registers

```text
:dr
```

to view hex dump of bytes

```text
:pxq    #how hexadecimal quad-words dump (64bit)

:pxw    #show hexadecimal words dump (32bit)
```

to step once

```text
s
```

to enter cursoe mode \(to manuall set break points

```text
c

use arrows to move around and tab to switch panes

to set breakpoint in cursor mode use

b
```

Remember to view help at anytime in radare it's simply "?". Also when in visual mode, use ":" to enter cmd mode and &lt;enter&gt; to exit cmd mode.

### GDB <a id="gdb"></a>

to start

```text
gdb filename
```

disassemble main function

```text
disassemble main
```

start with inspecting functions \(**note: gets and strcpy** are vulnerable to buffer overflows\)

```text
> info functions
```

to find the value of the vulnerable buffer in the instance of a gets or strcpy:

```text
Look for a something similarly to right before the call

lea eax,[esp+0x1e]

in the preceding case the buffer is 30 bytes (decimal version of the hex value 1e)
```

if looking for a flag and find a flag type function

```text
(gdb) break main

(gdb) r

(gdb) call <nameofflagfunction)

#If the program required input and thus the call function you can input with the following syntax
#in this case 1234

(gdb) call <nameofflagfunction)(1234)
```

### Ghidra <a id="ghidra"></a>

```text
download ghidra from website (ghidra-sre.org)

./ghirdaRun

create new project
click dragon(code browser)
file->import file-> target app
analyze it->select all->go
To start off looking at main function: functions->main (on the left hand side under symbol tree)
```

