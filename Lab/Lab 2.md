**Revision Notes: Computer Organization and Assembly Language**

**When to Use CPSR (Current Program Status Register)**
=====================================================

The CPSR is used when the result of an operation is unknown, such as in addition or subtraction, to set the S flag accordingly. However, when moving a negative value directly, the S flag is not needed as the value is already known to be negative.

**Multiplication (MUL)**
=====================

The MUL instruction multiplies two registers and stores the result in a third register. The syntax is `MUL R1, R2, R3`, which is equivalent to `R1 = R2 * R3`.

There are two exceptions to note:

*   **Carry Bits**: In ARM, the result of a multiplication may have more digits than the original operands. Since ARM is a 32-bit architecture, the carry bits are not stored.
*   **No Immediate Form**: MUL instructions do not have an immediate form, unlike other arithmetic operations.

**Memory Segments**
===============

**8086 vs ARM**
--------------------

In 8086, there are four memory segments:

1.  **CS (Code Segment)**: Stores the machine code for each opcode.
2.  **DS (Data Segment)**: Stores variables, strings, arrays, etc.
3.  **SS (Stack Segment)**: Used for function calls and tracking the call stack.
4.  **ES (Extra Segment)**: Used for storing dummy values of variables until they are initialized and moved to the data segment**.

In ARM, there are three memory segments that correspond to the 8086 segments:

1.  **TS (Text Segment)**: Corresponds to CS.
2.  **(Data Segment)**: Corresponds to DS and ES.
3.  **BSS (Block Storage Segment)**: Corresponds to SS.

**Declaring Variables**
=====================

To declare variables, we need to start with the `.data` directive. Labels and variables both end with a colon. However, labels are in the `.text` segment and do not require a data type declaration, while variables are in the `.data` segment and require a data type declaration (e.g., `.word` for 32-bit or `.hword` for 16-bit).

**Loading and Storing Values**
================================

To load values from the `.data` segment to the `.text` segment, we use the `LDR` (Load Register) instruction. To store values from the `.text` segment to the `.data` segment, we use the `STR` (Store Register) instruction.

**Loading Values**
-----------------

The `LDR` instruction has two steps:
    1.  **Address Load**: Load the address of the variable into the register (notation: `=`).
    2.  **Value Load**: Load the value at the address into the register (notation: `[ ]`).

Example:
```bash
.text
_start:
    ldr r0, =CSE331L  ; load the address of CSE331L into r0
    ldr r1, [r0]      ; load the value into r1
```

**Storing Values**
----------------

The `STR` instruction also has two steps:
    1.  **Address Load**: Load the address of the variable into the register (notation: `ldr`).
    2.  **Value Store**: Store the value into the register at the address (notation: `[ ]`).

Note: The destination register comes later in the `STR` instruction**.

Example:

```bash
ldr r0, =CSE331L
str r1, [r0]      ; store the value in r1 into the address in r0
```

**Addresses**
=============

In ARM, addresses are represented in hexadecimal and are divided into groups of 4 bytes. The address format is:

`0-3) | 4-7) | 8-b | c-f`

**Immediate Addressing and Offset Addressing
-----------------------------------

These concepts will be covered in the manual.