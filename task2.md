# Sum of Squares in RISC-V

This project demonstrates a simple RISC-V program that computes the
**sum of squares from 1 to 10**.\
The final result should be:

[ $1^2$ + 2^2 + $`\cdots `{=tex}$+ $10^2$ = 385 \]

------------------------------------------------------------------------
<img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/b10ef06a-ffe8-416f-ab4c-57a490e8eabf" />

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
<img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/a150109c-38a8-4fdc-bdb9-9e2c183adc64" />

<img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/2a8fc0fc-5a2d-493b-a08e-15ac3bacedab" />

## Debugging Walkthrough

### 1. Initial Register State

``` asm
(spike) reg 0 a0
0x0000000000000001
```

-   Register **a0** (x10) is initialized with `1`.
-   This will be used to accumulate the final result.

------------------------------------------------------------------------

### 2. Load Immediate Instruction

``` asm
0x00000000000100b0 li a0, 0x21
```

-   Loads the constant `0x21` (decimal **33**) into `a0`.
-   At this point, `a0 = 33`.

------------------------------------------------------------------------

### 3. Stack Setup

``` asm
0x00000000000100b4 addi sp, sp, -16
```

-   Stack pointer (**sp**) is moved down by 16 bytes.
-   This allocates space for temporary storage (function call
    convention).

------------------------------------------------------------------------

### 4. Load Loop Bound

``` asm
0x00000000000100b9 li a1, 385
```

-   Register **a1** is loaded with **385** (the expected result of the
    sum of squares).
-   This serves as a comparison or reference value.

------------------------------------------------------------------------

### 5. Accumulate Final Result

``` asm
0x00000000000100bc addi a0, a0, 368
```

-   Adds **368** to the previous value in `a0`.

**385** as the final result!
------------------------------------------------------------------------
