previous class revision

when do we use cpsr?

if we're moving a negative value, directly, we know its already negative, so we don't need to use cpsr

but, say in add or sub, we don't know what the result might be
so just in case, we use the s flag

let's start with multiplication today.

MUL:

R1 = R2 * R3
mov r1, r2, r3

2 exceptions for multiplication:

when multiplying, the digits may be more in the answer than in the question. in arm, we cannot show the carry bits as it is a value larger 32 bits (this is an exception)

MUL (multiplication) instructions have no immediate form. only regular instructions.

multiplication differs from the other 2 basic operations.

there is no divide operation in ARM assembly.
because division produces quotient and remainder. we can't store these two values.
we can't set 2 destinations in arm, only 1.
instead, we binary shift right to divide in half wherever possible.

memory segments:

8086 vs arm

in 8086, memory segments have 4 parts.
1: cs (code segment)
2: ds (data segment)
3: ss (stack segment)
4: es (extra segment)

now, arm instructions have 4 parts, right?
so, we start with the opcode (let's ignore the label for now).

1: cs (code segments) - the memory part that has stored the equivalent machine code for each opcode.

2: ds (data segments) - stores variables, string, array, etc.

3: ss (stack segments) - line by line function calls/call by stack (allows it to read line by line and track which line comes after which).

4: es (extra segments) - extra stuff, we don't study this that much. but, it may be used for: (storing dummy values of variables until it's initialized maybe and moved to the data segment).

arm, however has 3 segments, they correspond to the 8086 segments:

1: ts (text segment) -> corresponding to cs
2: ds (data segment) -> corresponding to ds
3: bss (b stack segment, no one knows what the fuck bss means) -> corresponding to ss + es

in cpulator, when we're coding, we put in .text (to let it know we're using ts) before the opcodes section.

declaring variables:

we need to start with .data

labels and variables both end with colon.

however, label is in the .text segment, and we don't need to declare a data type
but variable is in the .data segment, and we need to declare a data type (.word [size: 32b/4bytes], .hword [16b/2bytes]).

in the data segment, we can declare immediate values without using #.

e.g,

.data
CSE331L: .word 0xf

if no data type stated, assume it uses .word, because most systems are 32 bit, .hword causes issues.

to send values from the data segment to the text segment (for operations), we use the "ldr" load register command.
to send values from the text segment to the segment we use "str" (store).

load (ldr) must have 2 steps.
1: address load (notation: "=")
2. value load (notation: "[ ]")
e.g, 
```bash

.text
_start:

ldr r0, =a (load the address of a into r0, similar to &a in c programming)
ldr r1, [r0] (load the value that is at an address into r1, in this case r0)

```
e.g,

```bash

.data
CSE331L: .word 0xf

.text
_start:

ldr r0, =CSE331L
ldr r1, [r0]

```
for storing, "str", we also have 2 steps:

1: address load (ldr)
2: store the actual value. but store has an exception. DO NOT FORGET THIS.
STR IS THE ONLY INSTRUCTION WHERE THE DESTINATION COMES LATER.

e.g,

```bash

ldr r0, =a
str r1, [r0] (assuming r1 already has something stored)

```

so, (storing the value 7 for cse331l)

mov r1, #7
ldr r0, =CSE331L
str r1, [r0]

addresses (always in hexadecimal):
since 32 bits, in groups of 4.
so address goes like this:
0-3 (one section) | 4-7 | 8-b | c-f
then,
10-13 (in hex) | 14-17 | 18-(3 later) | 1c-(3 later) |  (here, 3l/3later means add 3, i just made this up, it should not be like this)
20-(3l) | 24- | 28- | 2c |
30- | 34- | 38- | 3c |
...
90000 | 9004- | 9008- | 900c |
(you get it)

immediate addressing, offset addressing (in lab manual)