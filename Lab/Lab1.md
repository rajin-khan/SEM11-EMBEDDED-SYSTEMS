**CSE331 Lab Lecture 1: Introduction to ARM Assembly Programming**
============================================================

**Microprocessors**
-----------------

A microprocessor is a tiny computer chip with a central processing unit (CPU) responsible for executing computer programs. In this course, we will focus on the architecture of ARM microprocessors, and discuss famous ones like Intel architecture and ARM architecture.

**Block Diagram of a Microprocessor**
--------------------------------

Input Device -> Microprocessor -> Output Device
Microprocessor contains:
	+ Register Array
	+ Registers
    + Control Unit

**Memory Hierarchy**
---------------------

Top -> Bottom:
	+ Registers
	+ Cache Memory
	+ Main Memory (RAM)
	+ USB/Flash Memory
	+ Magnetic Disk/Hard Disk
	+ Magnetic Tapes/Tape Drives (Highest Level)

**Registers**
-------------

In ARM V7 32-bit, each space/digit is a hex value. So, 8 spaces (8*4=32)

### Types of Registers

* General Purpose Registers (GPR): Names start with R (e.g., R0, R1, R2...). We can use all other registers for our purpose, except for R7, which is dedicated for system calls (or interrupts). There are 13 general-purpose registers.
* Special Purpose Registers (SPR): Names start with SP, LR, CPSR (Current Program Status Register/Flag Register), used when making decisions, for example, storing 0, negative numbers with 2's complement, etc.

Within GPR, we have two types of registers: High and Low Registers.

**Instruction Set Architecture (ISA)**
-------------------------------------------------

If we want to control the CPU, for example, via the OS, we have an intermediate interface (between hardware and software). That is called the ISA.

ISA is of two types:

* RISC (Reduced ISA -> ARM)
* CISC (Complex ISA -> x86)

**ARM Assembly Coding**
---------------------

We will be using a simulator website named CPulator: https://cpulator.01xz.net/
Specifically, ARM V7, Altera DE1 Board, DE1SOC (V16.1): https://cpulator.01xz.net/?sys=arm-de1soc&d_audio=48000

**ARM Assembly Snippet Example**
--------------------------------

```
_start:
	mov r0, #7
	mov r7, #1
	add r8, r7, r0
	sub r9, r0, r7
	swi 0
```

* `mov`: moves values into a register
* `mov r0, #7`: move the immediate value 7 into register 0
* `add r8, r7, r0`: adds r0 and r7, and stores it in r8
* `sub r9, r0, r1`: subtracts r7 from r0, and stores it in r9
* `swi 0`: sends a software interrupt and ends the program

**ARM Assembly Instructions**
-------------------------------

* `mov`: moves values into a register
* `add`: adds two registers and stores the result in a register
* `sub`: subtracts one register from another and stores the result in a register

**ARM Assembly Instruction Format**
-----------------------------------------

* Label: every label is followed by a colon (e.g., `_start:`)
* Opcode: the action to be performed (e.g., `mov`, `add`, `sub`)
* Operand/Immediate: the value to be used (e.g., `#7`, `r0`, `r1`)
* Destination: the register where the result will be (e.g., `r0`, `r8`)

**ARM Assembly Instruction Examples**
-----------------------------------

* `mov r0, #7`: move the immediate value 7 into register 0
* `add r6, r1, r2`: adds r1 and r2, and stores the result in r6
* `swi 0`: sends a software interrupt and ends the program

**MOV Instruction**
-----------------

* Can copy the value from one register to another
* `mov r0, #7` and `mov r1, r0` are two types of MOV instructions
* ARM instructions are of two types:
	+ Normal instructions (e.g., `mov r1, r0`)
	+ Immediate instructions (e.g., `mov r0, #7`)

**ADD and SUB Instructions**
-----------------------------

* `add r0, r1, #7`: adds r1 and the immediate value 7, and stores the result in r0
* `sub r0, r1, #7`: subtracts the immediate value 7 from r1, and stores the result in r0

**Immediate Operands**
---------------------

* Can only have one immediate value
* Immediate operands can only be on the outside, not on the inside (e.g., `add r0, r1, #7` is possible, but `add r0, #7, r1` is not possible)

**Set Flag Register (S)**
-------------------------

* With every opcode, we can add an "s". It turns on the "set flag register" (turns on the CPSR)
* Example: `adds r0, r1, r2`