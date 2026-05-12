# 2-Bit ALU Design in Verilog

A fully functional 2-bit Arithmetic Logic Unit (ALU) implemented in Verilog HDL, supporting core arithmetic and logical operations with a clean modular design.

---

## Overview

This project implements a 2-bit ALU capable of performing arithmetic and logical operations on two 2-bit input operands. It is designed for simulation and synthesis on FPGA platforms, and serves as a foundational digital design exercise in hardware description using Verilog.

---

## Features

- 2-bit input operands (`A[1:0]` and `B[1:0]`)
- Multiple ALU operations selectable via opcode
- 2-bit result output with carry/overflow flag
- Modular, synthesizable Verilog HDL
- Testbench included for simulation

---

## Supported Operations

| Opcode | Operation     | Description                        |
|--------|---------------|------------------------------------|
| `00`   | ADD           | A + B (arithmetic addition)        |
| `01`   | SUB           | A - B (arithmetic subtraction)     |
| `10`   | AND           | A AND B (bitwise logical AND)      |
| `11`   | OR            | A OR B (bitwise logical OR)        |

> Additional operations such as XOR, NOT, and comparators can be added by extending the opcode width.

---

## Port Description

| Port      | Direction | Width  | Description                          |
|-----------|-----------|--------|--------------------------------------|
| `A`       | Input     | [1:0]  | First 2-bit operand                  |
| `B`       | Input     | [1:0]  | Second 2-bit operand                 |
| `opcode`  | Input     | [1:0]  | Operation selector (2-bit)           |
| `result`  | Output    | [1:0]  | 2-bit ALU output                     |
| `carry`   | Output    | 1-bit  | Carry/overflow flag                  |

---

## File Structure

```
2-bit-Alu-Design-in-Verilog/
├── alu_2bit.v          # Top-level ALU module
├── alu_tb.v            # Testbench for simulation
└── README.md           # Project documentation
```

---

## Block Diagram

See the visual block diagram below for a full overview of the ALU architecture.

---

## Getting Started

### Prerequisites

- [Icarus Verilog](http://iverilog.icarus.com/) (`iverilog`) for simulation
- [GTKWave](http://gtkwave.sourceforge.net/) for waveform viewing
- Or any FPGA toolchain (Xilinx Vivado, Intel Quartus, etc.)

### Simulation with Icarus Verilog

```bash
# Compile the design and testbench
iverilog -o alu_sim alu_2bit.v alu_tb.v

# Run the simulation
vvp alu_sim

# View the waveform (if .vcd dump is enabled in testbench)
gtkwave alu_dump.vcd
```

---

## Sample Verilog Code

```verilog
module alu_2bit (
    input  [1:0] A,
    input  [1:0] B,
    input  [1:0] opcode,
    output reg [1:0] result,
    output reg carry
);

always @(*) begin
    carry = 0;
    case (opcode)
        2'b00: {carry, result} = A + B;  // ADD
        2'b01: {carry, result} = A - B;  // SUB
        2'b10: result = A & B;           // AND
        2'b11: result = A | B;           // OR
        default: result = 2'b00;
    endcase
end

endmodule
```

---

## Simulation Results

The testbench exercises all four opcodes across multiple input combinations. Verified outputs:

| A    | B    | Opcode | Result | Carry |
|------|------|--------|--------|-------|
| `01` | `01` | `00`   | `10`   | `0`   |
| `11` | `01` | `00`   | `00`   | `1`   |
| `10` | `01` | `01`   | `01`   | `0`   |
| `11` | `10` | `10`   | `10`   | `0`   |
| `01` | `10` | `11`   | `11`   | `0`   |

---

## Applications

- Learning and teaching digital logic design
- Building blocks for more complex ALU or CPU designs
- FPGA prototyping and synthesis exercises
- Introduction to Verilog HDL for hardware engineers

---

## License

This project is open-source and available for educational and personal use.

---

## Author

**Naveen** — [GitHub Profile](https://github.com/Naveen5356220)
