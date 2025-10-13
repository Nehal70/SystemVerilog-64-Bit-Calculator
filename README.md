# SystemVerilog 64-Bit Calculator Project

## About This Project
This repository contains my implementation of a 64-bit calculator system designed as part of the SiliconJackets Digital Design Team onboarding project. Through this project, I've gained hands-on experience with SystemVerilog, RTL design, FSM-based control, and digital circuit simulation/verification.

Also, you can find my Physical Design Code / Submission here : https://drive.google.com/file/d/1MV9C1cCGPoItuLDFaxNPrvWfe1FyGTSN/view?usp=sharing 

## What I've Learned

### 🎯 Core Skills Developed
- SystemVerilog programming and best practices for hardware description
- RTL design with clean combinational vs sequential separation (`always_comb`, `always_ff`)
- Finite State Machine (FSM) design for control sequencing
- Memory-mapped interfaces and SRAM read/write timing
- Digital simulation and waveform-based debugging

### 🔧 Technical Competencies
- Combinational logic: 32-bit adder using generate blocks and 1-bit full adders
- Sequential logic: synchronous resets, clocked registers, and data path control
- System integration at the top level (SRAM + controller + adder + buffer)
- Testbench architecture (driver/monitor/scoreboard/sequencer/sequence items)
- Tool proficiency: Cadence Xcelium, SimVision/Verisium, Make-based flows

## Project Architecture
The calculator system consists of core RTL modules and a DV environment.

### 📁 Core RTL (Digital Design)
- `src/verilog/adder32.sv` — 32-bit ripple-carry adder built from 1-bit adders
- `src/verilog/full_adder.sv` — 1-bit full adder cell used by `adder32.sv`
- `src/verilog/result_buffer.sv` — 64-bit buffer with upper/lower 32-bit write select
- `src/verilog/controller.sv` — FSM orchestrating reads/writes and adder operation
- `src/verilog/top_lvl.sv` — Top-level integration (SRAM + controller + adder + buffer)
- `src/verilog/calculator_pkg.sv` — Shared parameters/types package
- `src/verilog/sky130_sram_2kbyte_1rw1r_32x512_8.sv` — SRAM macro model

### 🧪 Testbench and Verification (DV)
- `src/verilog/calc_tb_top.sv` — Top-level testbench instantiating DUT and TB components
- `src/verilog/calc_tb_pkg.sv` — TB package and shared TB types
- `src/verilog/calc_if.sv` — Virtual interface connecting DUT and TB
- `src/verilog/calc_driver.svh` — Drives stimulus transactions to the DUT
- `src/verilog/calc_monitor.svh` — Observes DUT activity and publishes transactions
- `src/verilog/calc_sequencer.svh` — Coordinates sequences to the driver
- `src/verilog/calc_seq_item.svh` — Transaction object with fields/constraints
- `src/verilog/calc_sb.svh` — Scoreboard comparing DUT against golden model
- `sim/behav/Include/calculator.include` — Filelist for compilation
- `sim/behav/Makefile` — `make xrun` (simulate), `make simvision`/`make verisium` (waves)
- `sim/behav/link_files.py` — Links sources for sim workspace (`make link`)
- `sim/behav/exclusions.el` — Coverage exclusions for unreachable points

## 🏗️ System Design
The system performs 64-bit unsigned integer addition by:
1. Reading two 32-bit operands from memory
2. Computing their sum using the 32-bit adder
3. Storing intermediate results into a 64-bit result buffer
4. Writing the full 64-bit result back to memory

## Key Learning Moments

### 💡 Challenges Overcome
- Designing an FSM that correctly sequences memory operations
- Understanding SRAM interface timing and handshake behavior
- Translating software instincts to hardware (concurrency, latency, and resets)
- Setting up a reproducible DV flow with compilation, run, and waveform debug

### 🎓 Educational Value
- Hardware-software co-design thinking and dataflow reasoning
- End-to-end digital system integration and verification
- Professional EDA tool usage and Make-driven automation
- Version control workflows for hardware projects

## Project Structure
```
src/verilog/              # SystemVerilog source and TB files
├── adder32.sv            # DD
├── full_adder.sv         # DD
├── controller.sv         # DD
├── result_buffer.sv      # DD
├── top_lvl.sv            # DD
├── calculator_pkg.sv     # DD
├── sky130_sram_2kbyte_1rw1r_32x512_8.sv  # DD (macro model)
├── calc_tb_top.sv        # DV
├── calc_tb_pkg.sv        # DV
├── calc_if.sv            # DV
├── calc_driver.svh       # DV
├── calc_monitor.svh      # DV
├── calc_sequencer.svh    # DV
├── calc_seq_item.svh     # DV
└── calc_sb.svh           # DV

sim/behav/
├── Include/calculator.include  # DV filelist
├── Makefile                    # DV make targets
├── link_files.py               # DV source linking
└── exclusions.el               # DV coverage exclusions
```

## Tools & Technologies Used
- SystemVerilog — Hardware Description Language
- Cadence Xcelium — Simulation and verification
- SimVision/Verisium — Waveform viewing and debug
- Linux/Unix, Make — Development and automation
- Git — Version control

## Future Development
- Add additional corner cases and negative tests
- Expand assertions around reset/handshake timing
- Grow functional coverage toward 98%+

## Acknowledgments
Special thanks to the SiliconJackets Digital Design Team and the Georgia Tech ECE department for an excellent learning environment and access to professional EDA tools.

---
This project represents my journey into digital design and verification and serves as a portfolio piece demonstrating my growing expertise in SystemVerilog, RTL design, and DV practices.
