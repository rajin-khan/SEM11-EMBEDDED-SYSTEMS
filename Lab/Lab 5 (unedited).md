Lab 4 (missed)

Branching and stuff (take notes from kabbya)

lab task 4
1. steps: load value, then compare with initial max, then update address (+4), then update counter.

.data
martyrs: .word 13, 0x19, 15, 0x48, 12, 0x17

max: .word
total: .word

.text
lads r0, =martyrs
mov r6, #6

loop:
ldr r1, [r0]
cmp r1, r5
bgt update
b skip

update: 
mov r5, r1

skip:
add r9, r9, r1
add r0, r0, #4
sub r6, r6, #1
cmp r6, #0
bne loop

ldr r10, =max
str r5, r[10]
ldr r11, =total
str r9, r[11]

new lecture:

peripherals:

main motto:
take input, or give output

we will try to learn the peripherals of arm with 4 main ones:
leds, 7 segments (both outputs), switches, pbs (both inputs)
these peripherals, when connected to an arm device, will have its own specific address. (located to the right of the thing in cpulator)

thus, in leds, for 7 segments, we use str (as we only write values to them).

eg, address of leds are ff200000

then,

ldr r0, =0xff200000
mov r5, #7
str r5, [r0]

this will turn on the leds. you will notice that since leds have 2 states, on/off, thus they are represented as binary values (the last 3 light up, 111). same goes fro switches.

for switch, we turn them on, lets say the last 3. then, we load the address of the switch, and then the value into a register, it'll load 7.

for example, 

ldr r0, =0xff200040
ldr r1, [r0]

for our purposes, switches and pbs (push buttons) are the same in cpulator. we may use it when two inputs are needed.

loading values into 7 segment displays is not the same. it loads 7 bits of binary for a single digit: (draw an ascii representation of digital number lines (represented by abcdefgh [g is the middle stick, going clockwise from top]).

thus, to print 8, every line needs to be on (01111111) added a bc hex values can be passed as groups of 4 bits (hgfedcba, it goes in this order actually).

so, to print 8, we would move and store #0x7F (0111 = 7, 1111 = F)

so, to print A, we would move and store #0x77 (0111 = 7, 0111 = 7), as hgfedcba = 01110111.


ldr r0, =0xff200020
mov r5, #0x7F
STR r5, [r0]

in 7 segment displays, b or d should be lowercase (as B = 8 and D = 0 on 7 segment display).

a table for all values in the hex system has been given in the lab manual.

let's say, we want a program to sequentially print values from 1-5 in the 7 segment display.

cmp r5, #0
beq print0


cmp r5, #1
beq print1

cmp r5, #2
beq print2

cmp r5, #3
beq print3

cmp r5, #4
beq print4

cmp r5, #5
beq print5
b end

print0:
ldr r0, =0xff20020
mov r5, #0x3F
str, r5, [r0]

print1:
ldr r0, =0xff20020
mov r5, #0x06
str, r5, [r0]

print2:
ldr r0, =0xff20020
mov r5, #0x5B
str, r5, [r0]

print3:
ldr r0, =0xff20020
mov r5, #0x4F
str, r5, [r0]

print4:
ldr r0, =0xff20020
mov r5, #0x66
str, r5, [r0]

print5:
ldr r0, =0xff20020
mov r5, #0x6D
str, r5, [r0]

we may also store really long addresses in "variables" like this:

.equ sevenseg, 0xff200020
then, we can write:
ldr r0, =sevenseg