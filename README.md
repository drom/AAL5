# AAL5
Algebraic Assembly Language for RISC-V

## RV32I

```js
    rd = imm20 << 12                        // lui     rd imm20 6..2=0x0D 1..0=3
    pc = pc + (imm20 << 12)                 // auipc   rd imm20 6..2=0x05 1..0=3

    rd = pc + 4; goto (rs1 + imm12)         // jalr    rd rs1 imm12              14..12=0 6..2=0x19 1..0=3
    rd = pc + 4; goto (pc + imm20)          // jal     rd jimm20                          6..2=0x1b 1..0=3

    if (rs1 ==  rs2) goto (pc + bimm12hi)   // beq     bimm12hi rs1 rs2 bimm12lo 14..12=0 6..2=0x18 1..0=3
    if (rs1 !=  rs2) goto (pc + bimm12hi)   // bne     bimm12hi rs1 rs2 bimm12lo 14..12=1 6..2=0x18 1..0=3
    if (rs1  <  rs2) goto (pc + bimm12hi)   // blt     bimm12hi rs1 rs2 bimm12lo 14..12=4 6..2=0x18 1..0=3
    if (rs1 >=  rs2) goto (pc + bimm12hi)   // bge     bimm12hi rs1 rs2 bimm12lo 14..12=5 6..2=0x18 1..0=3
    if (rs1  <u rs2) goto (pc + bimm12hi)   // bltu    bimm12hi rs1 rs2 bimm12lo 14..12=6 6..2=0x18 1..0=3
    if (rs1 >=u rs2) goto (pc + bimm12hi)   // bgeu    bimm12hi rs1 rs2 bimm12lo 14..12=7 6..2=0x18 1..0=3

    rd =  i8[rs1 + imm12]  // lb      rd rs1       imm12 14..12=0 6..2=0x00 1..0=3
    rd = i16[rs1 + imm12]  // lh      rd rs1       imm12 14..12=1 6..2=0x00 1..0=3
    rd = i32[rs1 + imm12]  // lw      rd rs1       imm12 14..12=2 6..2=0x00 1..0=3
    rd =  u8[rs1 + imm12]  // lbu     rd rs1       imm12 14..12=4 6..2=0x00 1..0=3
    rd = u16[rs1 + imm12]  // lhu     rd rs1       imm12 14..12=5 6..2=0x00 1..0=3

     i8[rs1 + imm12lo] = rs2  // sb     imm12hi rs1 rs2 imm12lo 14..12=0 6..2=0x08 1..0=3
    i16[rs1 + imm12lo] = rs2  // sh     imm12hi rs1 rs2 imm12lo 14..12=1 6..2=0x08 1..0=3
    i32[rs1 + imm12lo] = rs2  // sw     imm12hi rs1 rs2 imm12lo 14..12=2 6..2=0x08 1..0=3

    rd = rs1  +  imm12    // addi    rd, rs1, imm12           14..12=0 6..2=0x04 1..0=3
    rd = rs1  <  imm12    // slti    rd, rs1, imm12           14..12=2 6..2=0x04 1..0=3
    rd = rs1 <u  imm12    // sltiu   rd, rs1, imm12           14..12=3 6..2=0x04 1..0=3
    rd = rs1  ^  imm12    // xori    rd, rs1, imm12           14..12=4 6..2=0x04 1..0=3
    rd = rs1  |  imm12    // ori     rd, rs1, imm12           14..12=6 6..2=0x04 1..0=3
    rd = rs1  &  imm12    // andi    rd, rs1, imm12           14..12=7 6..2=0x04 1..0=3
    rs = rs1 <<< shamt    // slli    rd, rs1, 31..26=0  shamt 14..12=1 6..2=0x04 1..0=3
    rd = rs1 >>> shamt    // srli    rd, rs1, 31..26=0  shamt 14..12=5 6..2=0x04 1..0=3
    rd = rs1 >>  shamt    // srai    rd, rs1, 31..26=16 shamt 14..12=5 6..2=0x04 1..0=3
    
    rd = rs1  +  rs2      // add     rd rs1 rs2 31..25=0  14..12=0 6..2=0x0C 1..0=3
    rd = rs1  -  rs2      // sub     rd rs1 rs2 31..25=32 14..12=0 6..2=0x0C 1..0=3
    rd = rs1 <<< rs2      // sll     rd rs1 rs2 31..25=0  14..12=1 6..2=0x0C 1..0=3
    rd = rs1  <  rs2      // slt     rd rs1 rs2 31..25=0  14..12=2 6..2=0x0C 1..0=3
    rd = rs1  <u rs2      // sltu    rd rs1 rs2 31..25=0  14..12=3 6..2=0x0C 1..0=3
    rd = rs1  ^  rs2      // xor     rd rs1 rs2 31..25=0  14..12=4 6..2=0x0C 1..0=3
    rd = rs1 >>> rs2      // srl     rd rs1 rs2 31..25=0  14..12=5 6..2=0x0C 1..0=3
    rd = rs1  >> rs2      // sra     rd rs1 rs2 31..25=32 14..12=5 6..2=0x0C 1..0=3
    rd = rs1  |  rs2      // or      rd rs1 rs2 31..25=0  14..12=6 6..2=0x0C 1..0=3
    rd = rs1  &  rs2      // and     rd rs1 rs2 31..25=0  14..12=7 6..2=0x0C 1..0=3

    rd = fence(fm, pred, succ, sr1)
    ecall()
    ebreak()
    
```

## RV64I

```js
    rd = i64[rs1 + imm12]  // ld      rd rs1       imm12 14..12=3 6..2=0x00 1..0=3
    rd = u32[rs1 + imm12]  // lwu     rd rs1       imm12 14..12=6 6..2=0x00 1..0=3

    i64[rs1 + imm12lo] = rs2  // sd     imm12hi rs1 rs2 imm12lo 14..12=3 6..2=0x08 1..0=3
```

## F

```js
rd = rs1 + rs2      // fadd.s    rd rs1 rs2      31..27=0x00 rm       26..25=0 6..2=0x14 1..0=3
rd = rs1 - rs2      // fsub.s    rd rs1 rs2      31..27=0x01 rm       26..25=0 6..2=0x14 1..0=3
rd = rs1 * rs2      // fmul.s    rd rs1 rs2      31..27=0x02 rm       26..25=0 6..2=0x14 1..0=3
rd = rs1 / rs2      // fdiv.s    rd rs1 rs2      31..27=0x03 rm       26..25=0 6..2=0x14 1..0=3
fsgnj.s   rd rs1 rs2      31..27=0x04 14..12=0 26..25=0 6..2=0x14 1..0=3
fsgnjn.s  rd rs1 rs2      31..27=0x04 14..12=1 26..25=0 6..2=0x14 1..0=3
fsgnjx.s  rd rs1 rs2      31..27=0x04 14..12=2 26..25=0 6..2=0x14 1..0=3
rd = min(rs1, rs2)      // fmin.s    rd rs1 rs2      31..27=0x05 14..12=0 26..25=0 6..2=0x14 1..0=3
rd = max(rs1, rs2)      // fmax.s    rd rs1 rs2      31..27=0x05 14..12=1 26..25=0 6..2=0x14 1..0=3
rd = sqrt(rs1, rs2)     // fsqrt.s   rd rs1 24..20=0 31..27=0x0B rm       26..25=0 6..2=0x14 1..0=3

rd = rs1 <= rs2         // fle.s     rd rs1 rs2      31..27=0x14 14..12=0 26..25=0 6..2=0x14 1..0=3
rd = rs1 <  rs2         // flt.s     rd rs1 rs2      31..27=0x14 14..12=1 26..25=0 6..2=0x14 1..0=3
rd = rs1 == rs2         // feq.s     rd rs1 rs2      31..27=0x14 14..12=2 26..25=0 6..2=0x14 1..0=3

rd = rs1                // fcvt.w.s  rd rs1 24..20=0 31..27=0x18 rm       26..25=0 6..2=0x14 1..0=3
rd = rs1                // fcvt.wu.s rd rs1 24..20=1 31..27=0x18 rm       26..25=0 6..2=0x14 1..0=3
rd = rs1                // fcvt.l.s  rd rs1 24..20=2 31..27=0x18 rm       26..25=0 6..2=0x14 1..0=3
rd = rs1                // fcvt.lu.s rd rs1 24..20=3 31..27=0x18 rm       26..25=0 6..2=0x14 1..0=3
rd = rs1                // fmv.x.w   rd rs1 24..20=0 31..27=0x1C 14..12=0 26..25=0 6..2=0x14 1..0=3
rd = rs1                // fclass.s  rd rs1 24..20=0 31..27=0x1C 14..12=1 26..25=0 6..2=0x14 1..0=3

rd = f32[rs1 + imm12]   // flw       rd rs1 imm12 14..12=2 6..2=0x01 1..0=3

f32[rs + imm12lo] = rs2 // fsw       imm12hi rs1 rs2 imm12lo 14..12=2 6..2=0x09 1..0=3

rd = rs1 * rs2 + rs3    // fmadd.s   rd rs1 rs2 rs3 rm 26..25=0 6..2=0x10 1..0=3
rd = rs1 * rs2 - rs3    // fmsub.s   rd rs1 rs2 rs3 rm 26..25=0 6..2=0x11 1..0=3
rd = -rs1 * rs2 - rs3   // fnmsub.s  rd rs1 rs2 rs3 rm 26..25=0 6..2=0x12 1..0=3
rd = -rs1 * rs2 + rs3   // fnmadd.s  rd rs1 rs2 rs3 rm 26..25=0 6..2=0x13 1..0=3
```
