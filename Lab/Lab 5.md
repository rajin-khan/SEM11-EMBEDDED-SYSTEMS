**Lab 4: Branching (Missed)**
=====================================

**Branching**
------------

### Lab Task 4

The lab task involves finding the maximum value in an array and storing it in a memory location. The array is defined as:

```arm
.data
martyrs: .word 13, 0x19, 15, 0x48, 12, 0x17
max: .word
total: .word
```

The program to find the maximum value is as follows:

```arm
.text
ladr0, =martyrs
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
str r5, [r10]
ldr r11, =total
str r9, [r11]
```

**Lab 5: Peripherals**
=====================================

### Peripherals
--------------

Peripherals are devices that interact with the ARM processor to provide input or output. The main motto of peripherals is to take input or give output. In this lab, we will focus on four main peripherals:

* LEDs (output)
* 7-Segment Displays (output)
* Switches (input)
* Push Buttons (input)

Each peripheral has its own specific address, which can be found to the right of the device in the CPulator.

### LEDs

LEDs have two states: on and off, which can be represented as binary values. To turn on the LEDs, we use the `str` instruction to write a value to the LED address. For example:

```arm
ldr r0, =0xff200000
mov r5, #7
str r5, [r0]
```

This will turn on the last three LEDs.

### Switches

Switches are similar to LEDs, but they are used as inputs. To read the value of a switch, we load the address of the switch into a register and then load the value into another register. For example:

```arm
ldr r0, =0xff200040
ldr r1, [r0]
```

This will load the value of the switch into register `r1`.

### 7-Segment Displays

7-Segment Displays are used to display digits from 0 to 9. Each digit is represented by 7 bits of binary data. To display a digit, we need to load the correct binary value into the display. For example, to display the digit 8, we need to load the value `0x7F` into the display:

```arm
ldr r0, =0xff200020
mov r5, #0x7F
str r5, [r0]
```

To display the digit A, we need to load the value `0x77` into the display:

```arm
ldr r0, =0xff200020
mov r5, #0x77
str r5, [r0]
```

Note that in 7-Segment Displays, the letters B and D should be in lowercase, as B represents the digit 8 and D represents the digit 0.

### Sequential Printing in 7-Segment Displays

To print sequential values from 1 to 5 in a 7-Segment Display, we can use a program like this:

```arm
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
    ldr r0, =0xff200020
    mov r5, #0x3F
    str r5, [r0]

print1:
    ldr r0, =0xff200020
    mov r5, #0x06
    str r5, [r0]

print2:
    ldr r0, =0xff200020
    mov r5, #0x5B
    str r5, [r0]

print3:
    ldr r0, =0xff200020
    mov r5, #0x4F
    str r5, [r0]

print4:
    ldr r0, =0xff200020
    mov r5, #0x66
    str r5, [r0]

print5:
    ldr r0, =0xff200020
    mov r5, #0x6D
    str r5, [r0]
```

We can also store long addresses in "variables" like this:

```arm
.equ sevenseg, 0xff200020
```

Then, we can use the variable `sevenseg` instead of the long address:

```arm
ldr r0, =sevenseg
```