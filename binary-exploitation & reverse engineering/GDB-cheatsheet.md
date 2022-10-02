# Running

```bash
gdb <program> <core dump>
	- start GDB with core dump

gdb --args <program> <args...>
	- start GDB and pass arguments

gdb --pid <process_id>
	- start GDB with an attached process

set args <args...>
	- set arguments to pass to program to be debugged

run
	- run the program

kill
	- kill the running program
```


# Breakpoints

```bash
break 
	- Set a new breakpoint
	- break *main
	- break *0x00000000

delete 
	- Remove a breakpoint
	- delete *main
	- delete *0x00000000
clear 
	- Delete all breakpoints

enable
	- Enable a disabled breakpoint
	- enable *0x00000000

disable
	- Disable a breakpoint
	- disable 0x00000000
```

# Watchpoints
```bash
watch <where>
	- Set a new watchpoint.
delete/enable/disable <watchpoint number>
	- like breakpoints
```


# Stepping

```bash
step
	- go to next instruction

next 
	- Go to next instruction (source line) but donʻt dive into functions

finish
	- Continue until the current function returns

continue 
	- Continue normal execution
```

# Variables & Memory
```bash
print/format <what>
	- Print content of variable/memory location/register.

display/format <what>
	- Like print, but print the information after each stepping instruction.

undisplay <display_number> 
	- Remove the display with the given number.

enable display <display_number>
disable display <display_number>
	- Enanble or disable the display with the given number.

x/nfu
example-one: x/15i *main # this will print out 15 instructions from the start of main
example-two: x/10i $RIP # this will print out 10 instructions from the start of RIP

	- Print memory.
		- n: How many units to print (default 1). 
		- f: Format character (like print). 
		- u: Unit. Unit is one of: 
		- unit is one of:
			- b: Byte, 
			- h: Half-word (two bytes) 
			- w: Word (four bytes) 
			- g: Giant word (eight bytes)).
```

# Examining the stack
```bash
backtrace 
where 
	- Show call stack.

backtrace full 
where full 
	- Show call stack, also print the local variables in each frame.

frame <frame number>
	- Select the stack frame to operate on.
```


# Format
```
a  : Pointer.
c  : Read as integer, print as character.
d  : Integer, signed decimal.
f  : Floating point number.
o  : Integer, print as octal.
s  : Try to treat as C string.
t  : Integer, print as binary (t = two).
u  : Integer, unsigned decimal.
x  : Integer, print as hexadecimal.
```


# what is what
```bash
expression 
	- Almost any C expression, including function calls (must be prefixed with 
	a cast to tell GDB the return value type).

file_name::variable_name
	- Content of the variable defined in the named file (static variables).

function::variable_name 
	- Content of the variable defined in the named function (if on the stack).

{type}address
	- Content at address, interpreted as being of the C type type. 

$register 
	- Content of named register. 
	- Interesting registers are $esp (stack pointer), $ebp (frame pointer) and $eip (instruction pointer).
```

# Manipulating the program
```bash
set var <variable_name>=<value>
	- Change the content of a variable to the given value.

return <expression>
	- Force the current function to return immediately, passing the given value.
```

# Sources
```bash
directory 
Add directory to the list of directories that is searched for sources. 


list 
list <filename>:<function>
list <filename>:<line_number>
list <first>,<last>
	- Shows the current or given source context. The filename may be omitted.
	If last is omitted the context starting at start is printed instead of
	centered around it.

set listsize <count>
	- Set how many lines to show in list.
```

# Information

```bash
disassemble <where>
	- Disassemble the current function or given location.

info args
	 - Print the arguments to the function of the current stack frame.

info breakpoints
	- Print informations about the break- and watchpoints.

info display 
	- Print informations about the „displays“.

info locals
	- Print the local variables in the currently selected stack frame.

info sharedlibrary
	- List loaded shared libraries.

info signals
	- List all signals and how they are currently handled.

info threads 
	- List all threads.

show directories 
	- Print all directories in which GDB searches for source files.

show listsize
	- Print how many are shown in the list command.

whatis <variable_name>
	- Print type of named variable.

```
