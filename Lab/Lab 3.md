Revision on the Last Class
==========================

### Memory Segments

In x86 architecture, there are 4 memory segments:

* Code segment (instructions)
* Data segment (initialized variables)
* Stack segment (runtime memory allocation)
* Extra segment (additional memory for specific purposes)

In ARM architecture, there are 3 memory segments:

* Code segment (instructions)
* Data segment (initialized variables)
* Stack segment (runtime memory allocation)

### Variables, Labels, and Instructions

* Variables are stored in the data segment and can be accessed using labels.
* Labels are used to mark locations in the code and can be used to jump to specific locations.
* Instructions are stored in the code segment and are executed by the processor.

### Load and Store Instructions

* LDR (Load Register) is used to load a value from memory into a register.
* STR (Store Register) is used to store a value from a register into memory.

Today's Class
=============

### Logical Operators

Logical operators perform bitwise operations on the operands.

#### ORR (Logical OR)

* ORR performs a logical OR operation on the operands.
* Example: `5 ORR 4` performs a bitwise OR operation on the binary representations of 5 and 4.

```
  101 (5)
+ 100 (4)
-----
  101 (result)
```

#### AND (Logical AND)

* AND performs a logical AND operation on the operands.
* Example: `5 AND 4` performs a bitwise AND operation on the binary representations of 5 and 4.

```
  101 (5)
+ 100 (4)
-----
  100 (result)
```

#### AND Masking

* AND masking is used to check if a specific bit is set in a value.
* Example: To check if the 3rd bit is set in a value x, we can perform an AND operation with the value 4 (00000100).
* If the result is 4, then the 3rd bit is set in the value x.

#### EOR (Exclusive OR)

* EOR performs a logical Exclusive OR operation on the operands.
* EOR returns 1 if an odd number of bits are set in the operands.
* Example: `5 EOR 5` performs a bitwise EOR operation on the binary representations of 5 and 5.

```
  101 (5)
  101 (5)
-----
  000 (result)
```

* EOR can be used to clear the contents of a register or to make a register address empty.

#### MVN (Logical NOT/Negation)

* MVN performs a logical NOT operation on the operand.
* MVN flips the value of all the bits in the operand (1's complement).
* MVN has only one operand.

### CMP (Compare)

* CMP performs a comparison operation on the operands.
* CMP uses the subtraction operation to compare the operands.
* If the result of the subtraction is 0, then the operands are equal.
* CMP updates the flags in the CPSR (Current Program Status Register) automatically.
* The Z (Zero) flag in the CPSR is set if the result of the comparison is 0.

### Shift Instructions

#### LSL (Logical Shift Left)

* LSL performs a logical shift left operation on the operand.
* LSL multiplies the operand by 2^n, where n is the shift amount.
* Example: `LSL r0, r1, #2` shifts the value in register r1 left by 2 positions and stores the result in register r0.

#### LSR (Logical Shift Right)

* LSR performs a logical shift right operation on the operand.
* LSR divides the operand by 2^n, where n is the shift amount.
* Example: `LSR r0, r1, #3` shifts the value in register r1 right by 3 positions and stores the result in register r0.

#### ROR (Rotate Right)

* ROR performs a rotate right operation on the operand.
* ROR rotates the bits in the operand to the right by the specified amount.
* Example: `ROR r0, r1, #2` rotates the value in register r1 right by 2 positions and stores the result in register r0.

### Arrays

* In ARM, arrays are represented the same way as initialized variables, with commas separating the elements.
* Example: `Lab2: .word 1, 2, 3` defines an array Lab2 with elements 1, 2, and 3.
* To access the elements of the array, we can use the load and store instructions.
* Example: `ldr r0, =Lab2` loads the base address of the array Lab2 into register r0.
* `ldr r1, [r0]` loads the first element of the array into register r1.
* To access the next element, we can increment the base address by 4 (the size of a word) using `add r0, r0, #4`.
* We can use a loop to access all the elements of the array.

```
label:
    ldr r1, [r0]
    add r0, r0, #4
    B label
```

This loop will continue until we manually stop it.