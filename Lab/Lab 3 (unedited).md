Revision on the last class:

(instructions, MUL)

logical right shift (divides by 2^n)
logical left shift (multiplies by 2^n) (for each step of the shift)

uses of the 4 memory segments (in x86)
uses of the 3 memory segments (in ARM)

variables, labels and stuff.
variables (only in the text segment) and labels (only in the data segment) and their other difference.

LDR, STR.

today's class:

the variable names in lab assessment must exactly match the question (even in its case)

logical operators:

ORR: (logical OR)
AND (logical AND)
EOR (Exclusive OR)
MVN (Logical NOT/Negation)

all logical instructions work bitwise.

OR (bitwise)
5 OR 4 (if we put decimal values around OR)
means taking the binary values of 5 (101) and 4 (100) and performing a bitwise or operation on them.

eg,

 101
+100
-----
 101  <-- answer

AND (bitwise)
5 AND 4 (same as OR, if we put decimals around the instruction, and this happens bitwise as well)

eg,

 101
+100
-----
 100 <-- answer

AND masking:
(we start counting bits from the right)
let's say we want to check if the 3rd bit in a value is '1'. how do we do that?

x -> _ _ _ _ _ _ (<- this one) _ _

now, in the third bit, if it's 1, we're gonna get this value:
00000100 (which means 4)

now, if we do a logical AND on the variable x AND 4, and we get 4 as a result, the value has 1 in the 3rd bit
(why?)
x -> 00100100
     00000100
          ^ this part here, if x has 1 here, the result will be:
     --------
     00000100 <- the result will still be 4.

so in summary, if we AND with a value, and get the same value, then it means there are 1's present at the bits that represent that value.

so, if we want to check the 5th bit, we'll have to AND with 16: (10000)
if we want to check if the 5th AND 3rd bit is 1, we'll have to AND with 20: (10100)

EOR (XOR)
EOR will return 1 for an odd number of 1s.
another important operation of EOR is to clear the content of a register, or to make a register address empty.

eg, 
5 XOR 5
101
101
---
000 <- see?

MVN:
flips the value of all the bits (1's complement).
mvn has only one operand.

all these operations work with immediate values.

CMP (compare):

we can arithmetically represent comparison with subtraction. if 5-5 is 0 (or the result of a subtraction is 0), then we can say they are equal.

so, cmp uses the sub operation, except:
compare does NOT have ANY DESTINATION REGISTER.

now, if we can't store the result, how do we check?
remember cpsr for flags?

cmp updates the flag in cpsr automatically (so we don't need CPSRs)
so after cmp, if the zero (Z) flag in cpsr is raised, then the numbers are equal.

we can use cmp with immediate (obviously provided that we load a value initially)

this means that cmp can be represented by subs (if the Z flag is turned on)
the only difference is that subs has a destination register, but cmp doesn't.

cmp is always used in branch (conditional branch).

LSL (logical shift left):
left shift acts like multiplication, each step 2^n, so 1 step left = *2, 2 steps left = *2^2 = *4

in left shift, the immediate value represents the positions we will shift left.
LSL r0, r1, #2 (left shift by 2 spaces).
so in reality, this left shift represents multiplication by 2^that value.
so, if we are asked to multiply a value by 16,
lsl r0, r1, #4.
(we may put a register in place of immediate with that value in it)

same goes for LSR:
in lsr, everything is exactly the same as LSR, and this represents division by 2^that immediate value.
so division by 8, for example:
lsr, r0, r1, #3

in lsr and lsl, the new bits if needed are filled with 0.

ROR (rotate right)
values rotate around the register if they go out of scope by shifting right
so, in a 4 bit register (let's say 4 bit reg, but in arm it's 32)
1001
ROR 2
step 1: 1100
step 2: 0110

there is NO ROL. we can just do ROR 32-(number of times we want to rotate left

array:
yk arrays, in arm, it's represented the same way as initialized variables, just with commas.
eg,
Lab2: .word 1, 2, 3
now, if we grab the address of Lab2 (=Lab2), we'll actually get the Base address, which is basically the address of the value 1.
so,
ldr r0, =Lab2
ldr r1, [r0] (stores 1)
now, if we want to load the value at the next address (+4, remember last class), we have to increment the value of the address by +4.

ldr r1, [r0]
add r0, r0, #4 (so we move to the next address).
now, to load it, we'll have to loop back.
how do we loop?
we use labels and branch (repsresented with just 'B')
eg,

label:
ldr r1, [r0]
add r0, r0, #4
B label (so it loops back to that line, so on the second loop, it takes the address +4 value, so it loads up 2 into the array. then, it loads up 3 [since we do address +4 +4].

but how do we stop the loop?
next class mf.