# RISC-V Instruction  

Here i have used O0 to see more instruction because o1 is optimizing the code too much...!
---
<img width="351" height="183" alt="image" src="https://github.com/user-attachments/assets/3ee76a31-53b1-4d6f-9b0f-a7ce35a23434" />

<img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/e5576502-d7c9-49d3-b680-06e72a2e77b8" />

## 1. `addi sp, sp, -32`
- **Type**: I-type  
- **Meaning**: `sp = sp - 32`  
- **Use**: Allocate 32 bytes on the stack.

---

## 2. `sd ra, 24(sp)`
- **Type**: S-type  
- **Meaning**: Store doubleword → `[sp+24] = ra`  
- **Use**: Save return address.

---

## 3. `lw a5, -24(s0)`
- **Type**: I-type  
- **Meaning**: `a5 = *(int*)(s0-24)`  
- **Use**: Load variable `i`.

---

## 4. `sw a5, -20(s0)`
- **Type**: S-type  
- **Meaning**: `*(int*)(s0-20) = a5`  
- **Use**: Store variable `sum`.

---

## 5. `li a5, 10`
- **Pseudo (addi a5, x0, 10)**  
- **Type**: I-type  
- **Meaning**: `a5 = 10`  
- **Use**: Initialize `n = 10`.

---

## 6. `mv a1, a4`
- **Pseudo (addi a1, a4, 0)**  
- **Type**: I-type  
- **Meaning**: Copy register → `a1 = a4`.

---

## 7. `jal ra, 10208 <__muldi3>`
- **Type**: J-type  
- **Meaning**: Jump to function and link return address.  
- **Use**: Call `__muldi3(i, i)`.

---

## 8. `sext.w a5, a5`
- **Pseudo (addiw a5, a5, 0)**  
- **Type**: I-type  
- **Meaning**: Sign-extend 32-bit result to 64-bit.  
- **Use**: Make `i*i` behave like `int`.

---

## 9. `addw a5, a4, a5`
- **Type**: R-type  
- **Meaning**: `a5 = (int)(a4 + a5)`  
- **Use**: `sum += i*i`.

---

## 10. `addiw a5, a5, 1`
- **Type**: I-type  
- **Meaning**: `a5 = (int)(a5 + 1)`  
- **Use**: `i++`.

---

## 11. `bge a5, a4, 101a8`
- **Type**: B-type  
- **Meaning**: Branch if `a5 >= a4`.  
- **Use**: Loop condition `if (i <= n)`.

---

## 12. `ld ra, 24(sp)`
- **Type**: I-type  
- **Meaning**: `ra = *(long*)(sp+24)`  
- **Use**: Restore return address.

---

## 13. `ret`
- **Pseudo (jalr x0, ra, 0)**  
- **Type**: I-type  
- **Meaning**: Jump to `ra`.  
- **Use**: Return from function.

---

## 14. `auipc gp, 0x2`
- **Type**: U-type  
- **Meaning**: `gp = pc + (0x2 << 12)`  
- **Use**: Set up global pointer.

---

## 15. `add a0, a0, a2`
- **Type**: R-type  
- **Meaning**: `a0 = a0 + a2`  
- **Use**: Simple register add (appears in `__muldi3`).

---

# Summary
- **R-type**: `addw`, `add`, … (register-register arithmetic).  
- **I-type**: `addi`, `addiw`, `lw`, `ld`, `sext.w`, `jalr`.  
- **S-type**: `sw`, `sd` (store instructions).  
- **B-type**: `bge` (branches).  
- **U-type**: `auipc`.  
- **J-type**: `jal`.  


