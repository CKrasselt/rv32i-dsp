# rv32i-dsp

A custom RISC-V (RV32I) processor implemented in SystemVerilog, extended with a hardware DSP coprocessor, targeting the Digilent Basys 3 (Xilinx Artix-7) FPGA. Developed as a personal project to deepen practical experience with RTL design, FPGA implementation, and algorithm-to-hardware deployment using the Vivado toolchain.

---

## Project Goals

- Implement a complete, functional RV32I in-order pipeline in SystemVerilog from scratch
- Extend the core with a custom DSP peripheral (FIR filter) connected via a memory-mapped interface
- Synthesize, implement, and achieve timing closure on the Basys 3 using Vivado WebPACK
- Document architecture decisions, resource utilization, and timing results throughout

---

## Architecture Overview

> *To be updated as implementation progresses*

### Processor Core (RV32I)
- 5-stage in-order pipeline: Fetch → Decode → Execute → Memory → Writeback
- Full RV32I base integer instruction set support
- Hazard detection and data forwarding
- Static branch prediction (branch-not-taken)

### DSP Coprocessor
- Pipelined FIR filter
- Memory-mapped interface (planned: AXI4-Lite)
- Configurable filter coefficients

### Memory
- Instruction and data memory (on-chip BRAM)

---

## Repository Structure

```
rv32i-dsp/
├── rtl/                  # SystemVerilog source files
│   ├── core/             # RV32I pipeline stages
│   └── dsp/              # DSP coprocessor
├── tb/                   # Testbenches
├── constraints/          # Vivado XDC constraints (Basys 3)
├── sim/                  # Simulation scripts and waveform configs
└── docs/                 # Architecture notes and design log
```

---

## Tools

| Tool | Version |
|------|---------|
| Vivado WebPACK | 2024.x |
| Target Device | XC7A35T-1CPG236C (Basys 3) |
| HDL | SystemVerilog |

---

## Status

| Module | Status |
|--------|--------|
| RV32I Core | 🔲 In progress |
| Hazard Detection | 🔲 Not started |
| FIR Filter | 🔲 Not started |
| Memory Interface | 🔲 Not started |
| AXI4-Lite Peripheral | 🔲 Not started |
| Top-level Integration | 🔲 Not started |
| Timing Closure (Basys 3) | 🔲 Not started |

---

## References

- [RISC-V ISA Specification (RV32I)](https://riscv.org/technical/specifications/)
- [PicoRV32 — Reference RISC-V Implementation](https://github.com/YosysHQ/picorv32)
- [Basys 3 Reference Manual](https://digilent.com/reference/programmable-logic/basys-3/reference-manual)
- [Vivado Design Suite User Guide](https://docs.amd.com/r/en-US/ug910-vivado-getting-started)
- *Modern VLSI Design*, W. Wolf (4th ed.)
