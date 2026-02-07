# 🧮 Custom 8-bit ALU - Verilog Implementation

A fully-functional 8-bit Arithmetic Logic Unit (ALU) designed and implemented in Verilog as part of a Computer Organization and Architecture course. This ALU supports 12 distinct operations including arithmetic, logical, shift, and rotate operations with comprehensive flag handling.

## ALU Specifications

### Inputs/Outputs
- **Inputs**: 
  - `A[7:0]`, `B[7:0]`: 8-bit operands
  - `AluOp[3:0]`      : 4-bit operation code
- **Outputs**:
  - `Result[7:0]`: 8-bit result
  - `Zero`       : Set when result equals zero
  - `Negative`   : Set when result is negative (MSB = 1)
  - `Overflow`   : Set on signed arithmetic overflow

### Supported Operations

| AluOp | Operation | Description                                   |
|-------|-----------|-----------------------------------------------|
| 0000  | A + B     | Addition                                      |
| 0001  | B - A     | Reverse subtraction                           |
| 0010  | A + 1     | Increment A by 1                              |
| 0101  | A == B    | Set on equal (returns 1 if equal, 0 otherwise)|
| 0110  | B <<< 1   | Arithmetic left shift B by 1 bit              |
| 0111  | B >>> 1   | Arithmetic right shift B by 1 bit             |
| 1100  | A ⟲ 1    | Rotate A left by 1 bit                        |
| 1101  | A ⟳ 1    | Rotate A right by 1 bit                       |
| 1000  | not A     | Bitwise NOT                                   |
| 1001  | A and B   | Bitwise AND                                   |
| 1010  | A or B    | Bitwise OR                                    |
| 1011  | A nand B  | Bitwise NAND                                  |

## Design Architecture

### Modular Structure
The ALU follows a highly modular design with separate modules for each component:
ALU_8 (Top Module)
├── adder (Shared for first 3 arithmetic ops)
├── andAB (Bitwise AND - Structural)
├── orAB (Bitwise OR - Structural)
├── notA (Bitwise NOT - Structural)
├── nandAB (Bitwise NAND - Structural)
├── shift_leftB (Arithmetic left shift)
├── shift_rightB (Arithmetic right shift)
├── rotate_leftA (Rotate left)
├── rotate_rightA (Rotate right)
├── mux (4:1 multiplexer)
├── zero_detect (Zero flag generator - Structural)
├── negative_detect (Negative flag)
└── Internal Control Logic


### Key Design Features

1. **Shared Adder Architecture**: First three arithmetic operations (A+B, B-A, A+1) share the same adder instance
2. **Hierarchical Multiplexing**: Two-level mux system groups operations logically
3. **Structural Modeling**: At least 4 components use structural Verilog (gate-level implementation)
4. **No Case/If Statements**: Operation selection done purely through multiplexers as per requirements
5. **Flag Handling**: Proper detection of Zero, Negative, and Overflow flags

## 🚀 How to Simulate

### Prerequisites
- Verilog simulator (Icarus Verilog recommended)
- Waveform viewer (GTKWave or similar)

### Steps
1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/8-bit-alu-verilog.git
   cd 8-bit-alu-verilog
2. **Compile with Icarus Verilog:**
   ```bash
   iverilog -o alu_simulation ALU_8.vl
3. **Run the simulation:**
   ```bash
   vvp alu_simulation
4. **Expected output:** The testbench will display results for all operation categories with flag values.

## Course Information
Course: Computer Organization and Architecture

University: Cairo University, Faculty of Computing and Artificial Intelligence

Department: Computer Science

Academic Year: 2025-2026
