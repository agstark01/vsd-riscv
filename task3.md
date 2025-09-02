# RISC-V Instruction  

Here i have used O0 to see more instruction because o1 is optimizing the code too much...!
---
<img width="351" height="183" alt="image" src="https://github.com/user-attachments/assets/3ee76a31-53b1-4d6f-9b0f-a7ce35a23434" />

<img width="960" height="510" alt="image" src="https://github.com/user-attachments/assets/e5576502-d7c9-49d3-b680-06e72a2e77b8" />

## addi sp, sp, -32
- **Type**: I-type  
- **Binary**: `111111111100 00010 000 00010 0010011`  
- **Hex**: `0xfe010113`  
- **Meaning**: sp = sp - 32  
- **Use**: Allocate stack frame  

---
## sd ra, 24(sp)
- **Type**: S-type  
- **Binary**: `0000000 00001 00010 011 11000 0100011`  
- **Hex**: `0x00113c23`  
- **Meaning**: [sp+24] = ra  
- **Use**: Save return address  

---
## lw a5, -24(s0)
- **Type**: I-type  
- **Binary**: `111111101000 01000 010 01111 0000011`  
- **Hex**: `0xfef42683`  
- **Meaning**: a5 = *(int*)(s0-24)  
- **Use**: Load i  

---
## sw a5, -20(s0)
- **Type**: S-type  
- **Binary**: `111111101100 01111 01000 010 01100 0100011`  
- **Hex**: `0xfef42423`  
- **Meaning**: *(int*)(s0-20) = a5  
- **Use**: Store sum  

---
## li a5, 10 (addi a5, x0, 10)
- **Type**: I-type  
- **Binary**: `000000001010 00000 000 01111 0010011`  
- **Hex**: `0x00a00793`  
- **Meaning**: a5 = 10  
- **Use**: Set n=10  

---
## mv a1, a4 (addi a1, a4, 0)
- **Type**: I-type  
- **Binary**: `000000000000 01000 000 01001 0010011`  
- **Hex**: `0x00048593`  
- **Meaning**: a1 = a4  
- **Use**: Move register  

---
## jal ra, 10208 <__muldi3>
- **Type**: J-type  
- **Binary**: `imm[20|10:1|11|19:12] | rd=00001 | opcode=1101111`  
- **Hex**: `0x00000517 (example depends on offset)`  
- **Meaning**: Jump and link to function  
- **Use**: Call __muldi3  

---
## sext.w a5, a5 (addiw a5, a5, 0)
- **Type**: I-type  
- **Binary**: `000000000000 01111 000 01111 0011011`  
- **Hex**: `0x0007879b`  
- **Meaning**: Sign-extend word  
- **Use**: 32-bit to 64-bit extend  

---
## addw a5, a4, a5
- **Type**: R-type  
- **Binary**: `0000000 01111 01000 000 01111 0111011`  
- **Hex**: `0x00f707bb`  
- **Meaning**: a5 = (int)(a4 + a5)  
- **Use**: sum += i*i  

---
## addiw a5, a5, 1
- **Type**: I-type  
- **Binary**: `000000000001 01111 000 01111 0011011`  
- **Hex**: `0x0017879b`  
- **Meaning**: a5 = (int)(a5+1)  
- **Use**: i++  

---
## bge a5, a4, 101a8
- **Type**: B-type  
- **Binary**: `imm[12|10:5]=... rs2=01000 rs1=01111 funct3=101 imm[4:1|11] ... opcode=1100011`  
- **Hex**: `0xfea7dee3`  
- **Meaning**: if (a5 >= a4) branch  
- **Use**: Loop condition  

---
## ld ra, 24(sp)
- **Type**: I-type (load double)  
- **Binary**: `000000011000 00010 011 00001 0000011`  
- **Hex**: `0x01813083`  
- **Meaning**: ra = *(long*)(sp+24)  
- **Use**: Restore return address  

---
## ret (jalr x0, ra, 0)
- **Type**: I-type (JALR)  
- **Binary**: `000000000000 00001 000 00000 1100111`  
- **Hex**: `0x00008067`  
- **Meaning**: Jump to ra  
- **Use**: Return  

---
## auipc gp, 0x2
- **Type**: U-type  
- **Binary**: `00000000000000000010 00100 0010111`  
- **Hex**: `0x00002197`  
- **Meaning**: gp = pc + (0x2 << 12)  
- **Use**: Set global pointer  

---
## add a0, a0, a2
- **Type**: R-type  
- **Binary**: `0000000 00110 01010 000 01010 0110011`  
- **Hex**: `0x00c50533`  
- **Meaning**: a0 = a0 + a2  
- **Use**: Register addition  

---

# Summary
- **R-type**: `addw`, `add`, … (register-register arithmetic).  
- **I-type**: `addi`, `addiw`, `lw`, `ld`, `sext.w`, `jalr`.  
- **S-type**: `sw`, `sd` (store instructions).  
- **B-type**: `bge` (branches).  
- **U-type**: `auipc`.  
- **J-type**: `jal`.  


