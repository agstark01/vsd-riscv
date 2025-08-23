# Sum of Squares in C and RISC-V

## 📌 Overview
This project demonstrates a simple **C program** that calculates the sum of squares of the first `n` natural numbers.  
The program is compiled with the **RISC-V GCC toolchain**, and the resulting **RISC-V assembly instructions** are analyzed to understand how high-level C constructs map to low-level machine instructions.

---

## 💻 C Program (`sumsquare.c`)
```c
#include <stdio.h>

int main() {
    int sum = 0, n = 10;
    for (int i = 1; i <= n; i++) {
        sum += i * i;   // sum of squares
    }
    printf("%d\n", sum);
    return 0;
}
```

### ✅ Output
```
385
```
This matches the mathematical formula:

\[
\sum_{i=1}^{10} i^2 = \frac{n(n+1)(2n+1)}{6} = 385
\]

---

## ⚙️ RISC-V Disassembly (`sum1.o`)
When compiled using the RISC-V GCC toolchain, we can inspect the generated object file with:

```bash
riscv64-unknown-elf-objdump -d sum1.o
```

Example output snippet (from `main` function):

```
0000000000010184 <main>:
10184:  ff010113   addi sp,sp,-16
10188:  00113423   sd   ra,8(sp)
1018c:  18100593   li   a1,385
10190:  00021537   lui  a0,0x21
10194:  17050513   addi a0,a0,368
10198:  26c000ef   jal  ra, <printf>
1019c:  00000513   li   a0,0
101a0:  00813083   ld   ra,8(sp)
101a4:  01010113   addi sp,sp,16
101a8:  00008067   ret
```

---

## 🛠️ RISC-V Instruction Types
RISC-V instructions are divided into several **types** based on their format:

- **R-type** → Register to register operations  
  Example: `add x1, x2, x3`
- **I-type** → Immediate operations and loads  
  Example: `addi sp, sp, -16`
- **S-type** → Stores to memory  
  Example: `sd ra, 8(sp)`
- **B-type** → Conditional branches  
  Example: `beq x1, x2, label`
- **U-type** → Upper immediate (used for loading large constants)  
  Example: `lui a0, 0x21`
- **J-type** → Jumps (used for function calls and returns)  
  Example: `jal ra, <printf>`

### Mapping in Our Program
- `addi sp, sp, -16` → **I-type** (adjust stack pointer)  
- `sd ra, 8(sp)` → **S-type** (store return address on stack)  
- `li a1, 385` → **Pseudo-instruction**, expands into **I-type/U-type** depending on value  
- `lui a0, 0x21` → **U-type** (load upper immediate)  
- `jal ra, <printf>` → **J-type** (function call)  
- `ret` → **Pseudo-instruction**, expands to `jalr x0, 0(ra)`  

---

## 🚀 How to Run
1. Compile with RISC-V GCC:
   ```bash
   riscv64-unknown-elf-gcc sumsquare.c -o sum1
   ```
2. Run in a RISC-V emulator (like Spike or QEMU):
   ```bash
   spike pk sum1
   ```
3. Disassemble to see instructions:
   ```bash
   riscv64-unknown-elf-objdump -d sum1 > sum1.asm
   ```

---

## 📚 Learning Outcome
- Understand how **C loops and arithmetic** translate into **RISC-V assembly**.  
- Learn about **instruction types** (R, I, S, B, U, J).  
- See how function calls (`printf`) and stack management are implemented at the machine level.  

---

👉 This project is a beginner-friendly way to explore **C programming, compilation, and RISC-V assembly**.
