---
title: "MIPS Assembly language"
math: false
toc: true
tags:
- WIP
---

## Operands and operations
### MIPS Operands
- **Registers**(2^5 = 32):  `$s0-$s7, $t0-$t9, $zero, $a0-$a3, $v0-$v1, $gp, $fp, $sp, $ra, $at`
- **Memory words** (2^30): `Memory[X]`

### MIPS assembly language
| **Category**  | **Instruction**       | **Example**         | **Meaning**              |
| ------------- | --------------------- | ------------------- | ------------------------ |
| Arithmetic    | Add                   | `add $s1, $s2, $s3` | `$s1 = $s2 + $s3`        |
|               | Subtraction           | `sub $s1, $s2, $s3` | `$s1 = $s2 - $s3`        |
|               | Add immediate         | `addi $s1, $s2, 20` | `$s1 = $s2 + 20`         |
| Data Transfer | Load word             | `lw $s1, 20($s2)`   | `$s1 = Memory[$s2 + 20]` |
|               | Store word            | `sw $s1, 20($s2)`   | `Memory[$s2 + 20] = $s1` |
|               | Load half             | `lh`                |                          |
|               | Load half unsigned    | `lhu`               |                          |
|               | Store half            | `sh`                |                          |
|               | Load byte             | `lb`                |                          |
|               | Load byte unsigned    | `lbu`               |                          |
|               | Store byte            | `sb`                |                          |
|               | Load linked word      | `ll`                |                          |
|               | Store condition. word | `sc`                |                          |
|               | Load upper immediate  | `lui $s1, 20`       | `$s1 = 20<<16`           |
| Logical       | AND                   | `and $s1, $s2, $s3` | `$s1 = $s2 & $s3`        |
|               | OR                    | `or $s1, $s2, $s3`  | `$s1 = $s2 | $s3`        |
|               | NOR                   | `nor $s1, $s2, $s3` | `$s1 = ~($s2 | $s3)`     |
|               |                       |                     |                          |
