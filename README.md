# SAP-1-Architecture-Logisim
## Table of Contents
Click on the Table of Contents below to directly go to the sections:
- [Video Tutorials](#video-tutorials)
- [Project Overview](#project-overview)
- [Objectives](#objectives)
- [Key Features](#key-features)

- [Architecture and Functional Block Analysis](#architecture-and-functional-block-analysis)
  - [System Architecture Overview](#system-architecture-overview)
  - [Register Implementation (A, B)](#register-implementation-a-b)
  - [Program Counter (PC) Implementation](#program-counter-pc-implementation)
  - [Memory System and Address Register](#memory-system-and-address-register)
  - [Instruction Register and Opcode Decoder](#instruction-register-and-opcode-decoder)
  - [Arithmetic Logic Unit (ALU) Implementation](#arithmetic-logic-unit-alu-implementation)
  - [Boot/Loader Counter and Phase Generation](#bootloader-counter-and-phase-generation)

- [Control System Design](#control-system-design)
  - [Timing Control Generator](#timing-control-generator)
  - [Automatic Operation Control Logic](#automatic-operation-control-logic)
  - [Manual/Loader Operation Control](#manualloader-operation-control)

- [Instruction Set Architecture](#instruction-set-architecture)
  - [Instruction Encoding Scheme](#instruction-encoding-scheme)
  - [Assembler](#assembler)

- [Operation](#operation)
  - [Fetch–Decode–Execute Cycle](#fetchdecodeexecute-cycle)
  - [Running the CPU in Manual Mode](#running-the-cpu-in-manual-mode)
  - [Running the CPU in Automatic Mode (JMP + ADD Program)](#running-the-cpu-in-automatic-mode-jmp--add-program)

- [Future Improvement](#future-improvement)
- [Conclusion](#conclusion)
## Instruction Set Architecture

### Instruction Encoding Scheme
The instruction encoding system utilizes **upper nibble = IR[7:4]** for opcode specification and **lower nibble** for 4-bit operand/address when required.

---

#### Table 1: Instruction Set & Program

| Address   | Instruction | Hex | Mnemonic & Explanation        |
|-----------|-------------|-----|--------------------------------|
| 00001101  | 00011101    | 1D  | LDA 13 (Load A from M[13])     |
| 00001110  | 00101110    | 2E  | LDB 14 (Load B from M[14])     |
| 00010001  | 01100101    | 65  | JMP 5 (PC ← 5)                 |
| 00001001  | 00110000    | 30  | ADD (A ← A + B)                |
| 00001110  | 01011111    | 5F  | STA 15 (M[15] ← A)             |
| 00001001  | 11110000    | F0  | HLT (Stop execution)           |

---

#### Table 2: Data Values in RAM

| Address (Binary) | Data (Binary) | Decimal | Hex |
|------------------|---------------|---------|-----|
| 0000101          | 00100011      | 35      | 23  |
| 0000110          | 00011001      | 25      | 19  |
### Assembler

The assembler translates **SAP-1 assembly language programs** into **machine code (hexadecimal)** suitable for execution in Logisim.  
It supports instructions such as **LDA, LDB, ADD, SUB, STA, JMP, and HLT**, along with directives like **ORG** and **DEC**.  
The tool automatically generates **Logisim-compatible v2.0 raw hex output**, avoiding manual conversion errors.  

This enables efficient program development, testing, and debugging of the SAP-1 system.

---

#### 🔗 [Open the SAP-1 Assembler Tool](PUT-YOUR-ASSEMBLER-LINK-HERE)

---

#### SAP-1 Assembler Interface

![SAP-1 Assembler](assembler_screenshot.png)

*Figure: Web-based SAP-1 assembler interface converting assembly instructions into Logisim-compatible hexadecimal code.*

---

#### Table 3: Examples of Assembly Programs and Corresponding Hex Codes

| Example         | Assembly Code                                                                                       | Hex Code                                      |
|-----------------|----------------------------------------------------------------------------------------------------|-----------------------------------------------|
| **ADD Program** | LDA 13, LDB 14, ADD, STA 15, HLT <br> (ORG 13, DEC 35, ORG 14, DEC 25)                              | 1D 2E 30 5F F0 00 00 00 00 00 00 23 19 00 00  |
| **JMP + ADD Program** | LDA 13, LDB 14, JMP 5, ADD, STA 15, HLT <br> (ORG 13, DEC 35, ORG 14, DEC 25)                 | 1D 2E 65 30 5F F0 00 00 00 00 00 00 23 19 00  |

---
