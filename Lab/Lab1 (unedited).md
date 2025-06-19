cse331 Lab lecture 1

we will be working with stm32 (blue pill circ)

arm processor

will have to code with assembly (arm assembly to be specific)

must be on time, within 8:15

mid and final syllabus will be same, on arm assembly.

microprocessors ::

what is a microprocessor?
microprocessor a tiny computer chup with a cpu, responsible for executing computer pgrosrams
we will be discussing the architecture of sa microprocessor mainly arm
famous ones are intel architecture, and arm arch

diag:

input device -> microprocessor -> output device
microprocessor contains:
register array, alu, control unit

primary memory is not RAM, but the memory within the CPU. (L1 L2 L3 cache, etc).
made up of registers. (this is the smallest unit of memory)

hierarchy of memory ::

top -> bottom:
(lowest level) registers -> cache memory -> main memory (ram) -> usb/flash memory -> magnetic disk/hard disk -> magnetic tapes/tape drives (highest level)

the main content of this course, let's start
registers: (we will be studying arm v7 32 bit)
in the registers of arm, each space/digit is a hex value. so 8 spaces (8*4=32)

types of registers:

gpr: general purpose registers (names start with r, eg, r0, r1, r2...)
we can use all other registers for our purpose, except for r7, which is dedicated for system calls (or interrupts). there are 13 general purpose registers

sp: special purpose registers (eg sp, lr, pc, cpsr: current program status 
register/flag register, used when making decisions, for example storing 0, negative numbers with 2's complement, etc).
registers are used to store: data, instruction (so for this purpose, we can use the gprs)
special purpose registers are reserved for specific things. we cannot use it outside its intended purpose)

within gpr, we have 2 types of registers, high and low registers.

up next we have ISA (instruction set architecture): if we want to control the cpu, for example, via the os, we have an intermediate interface (between hardware and software). that is called the isa.
isa is of two types. risc (reduced isa -> arm) and cisc (complex isa -> x86).

what is arm
a family of risc isa for computer processors.

for arm assembly coding we will be using a simulator website named cpulator.
https://cpulator.01xz.net/
specifically arm v7, altera de1 board, de1soc (v16.1)
https://cpulator.01xz.net/?sys=arm-de1soc&d_audio=48000

example of arm7 assembly snippet:
"""
.global _start
_start:
	
	mov r0, #7
	mov r7, #1
	add r8, r7, r0
	sub r9, r0, r7
	
	swi 0
"""
mov: moves values into register
if we want to directly input values, they're called immediate values, we must put # before the value (eg #7)
mov r0, #7 (so this means move the immediate value, 7 into register 0)
after compiling, in cpulator, we have to "step over"
to put in, 15 as immediate value, we'll write mov r0, #15.
but if it's hex 15, we put in #0x15 (hash zero x 15).
arm assembly is case insensitive.

what if we wrote mov r7 #1? it wouldn't work, bc r7 is reserved.

add:
add r8, r7, r0 (adds r0, and r7 and stores it in r8). but, we can't use r7 for anything, so this is wrong.
but, 
"""
mov r1, #5
	mov r2, #3
	
	add r6, r1, r2
"""

sub works the same way.

to end an assembly program (like return 0), we call the software interrupt (swi).
so, we put in "swi 0" at the end, or ".end". this sends a software interrupt and ends the program.

don't refresh cpulator without copying code, it refreshes everything.

arm instructions have 4 parts.
- label
- opcode
- operand/s (or immediate value)
- destination

let's look at examples:

label:
every label is followed by a colon, (eg, _start:)
every code starts at a label.

opcode:
mov r0, #7
here, the action to be performed is denoted by the opcode/name of the opcode
in this case, "mov"

operand/immediate: "#7"

destination: r0

let's look at another example:
mov r2, #3

label: _start
opcode: mov
immediate: 3
destination: r2

another example:
add r6, r1, r2

label: _start (default label)
opcode: add
operands (not immediate, as many operands): r1, r2 (arm instruction categories depend on the operand)
destination: r6 

another example:
swi 0

label: _start (default label)
opcode: swi
operand: 0 (as it's not an immediate value, as it's not being stored in a register and no #)
destination:~ (no destination) 

MOV: can copy the value from one register to another. 
eg, mov r0, #7
mov r1, r0
arm instructions are of two types.
normal instructions (mov r1, r0)
immediate instructions (mov r0, #7)
they differ mainly in the operand. if the operand is a register, then normal instruction. if immediate, then immediate.

arm immediate instructions can only have ONE immediate value.

add immediate
add r0, r1, #7

immediate operands can only be on the outside, not on the inside.
(eg, add r0, r1, #7 possible, but add r0, #7, r1 not possible)

with every opcode, we can add an "s". it turns on the "set flag register" (turns on the cpsr)
eg,
adds r0, r1, r2
subs r0, r1, r2