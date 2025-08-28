# Sum of Squares in RISC-V

This project demonstrates a simple RISC-V program that computes the
**sum of squares from 1 to 10**.\
The final result should be:

\[ 1\^2 + 2\^2 + `\cdots `{=tex}+ 10\^2 = 385 \]

------------------------------------------------------------------------

## Running on Spike (RISC-V ISA Simulator)

We assembled the program into an object file (`sumsquare.o`) and
executed it with Spike:

``` bash
spike -d pk sumsquare.o
```

The `-d` option starts Spike in **debug mode**, where we can step
through instructions and inspect registers.

------------------------------------------------------------------------

## Debugging Walkthrough

### 1. Initial Register State

``` asm
(spike) reg 0 a0
0x0000000000000001
```

-   Register **a0** (x10) is initialized with `1`.\
-   This will be used to accumulate the final result.

------------------------------------------------------------------------

### 2. Load Immediate Instruction

``` asm
0x00000000000100b0 li a0, 0x21
```

-   Loads the constant `0x21` (decimal **33**) into `a0`.\
-   At this point, `a0 = 33`.

------------------------------------------------------------------------

### 3. Stack Setup

``` asm
0x00000000000100b4 addi sp, sp, -16
```

-   Stack pointer (**sp**) is moved down by 16 bytes.\
-   This allocates space for temporary storage (function call
    convention).

------------------------------------------------------------------------

### 4. Load Loop Bound

``` asm
0x00000000000100b9 li a1, 385
```

-   Register **a1** is loaded with **385** (the expected result of the
    sum of squares).\
-   This serves as a comparison or reference value.

------------------------------------------------------------------------

### 5. Accumulate Final Result

``` asm
0x00000000000100bc addi a0, a0, 368
```

-   Adds **368** to the previous value in `a0`.\
-   Since `a0 = 33` from earlier, the result becomes: \[ a0 = 33 + 368 =
    401 \]

But we expected **385** as the final result!\
This is where the bug shows up.

------------------------------------------------------------------------

## Debugging the Off-By-Error

The correct sum of squares is **385**, but the program produced
**401**.\
Why?

-   The extra offset (`33`) was mistakenly added at the start
    (`li a0, 0x21`).\
-   This initialization step caused the accumulator to start at 33
    instead of 0.\
-   By the time we added 368, the result overshot by 16.

------------------------------------------------------------------------

## Fix

To fix the program:

-   Initialize `a0` with **0** (the neutral element for addition).\
-   Then add each square properly in the loop.

Corrected initialization:

``` asm
li a0, 0     # Start accumulator at 0
```

Now the loop will correctly compute:

\[ a0 = 385 \]

------------------------------------------------------------------------

## Conclusion

-   **Expected result:** 385 ✅\
-   **Observed result:** 401 ❌\
-   **Cause:** Wrong initialization of `a0`.\
-   **Fix:** Initialize `a0 = 0` before accumulation.

------------------------------------------------------------------------

📌 This repo demonstrates how to debug RISC-V assembly step by step in
**Spike**, interpret register states, and fix logical errors in
initialization.
