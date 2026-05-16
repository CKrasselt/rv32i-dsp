# rv32i-dsp

A custom RISC-V (RV32I) processor implemented in SystemVerilog and extended with a hardware DSP coprocessor, targeting the Digilent Basys 3 (Xilinx Artix-7) FPGA. The project focuses on FPGA-based processor design, hardware acceleration, and practical RTL development using the Vivado toolchain.

---

## Project Goals

- Implement a complete, functional RV32I pipeline in SystemVerilog
- Extend the core with a custom FIR filter DSP peripheral connected via a memory-mapped interface
- Demonstrate hardware acceleration through an end-to-end audio filtering pipeline
- Synthesize, implement, and achieve timing closure on the Basys 3
- Document architecture decisions, resource utilization, and timing results throughout

---

## Architecture Overview

> *To be updated as implementation progresses*

### Processor Core (RV32I)
- 5-stage in-order pipeline: Fetch → Decode → Execute → Memory → Writeback
- Full RV32I base integer instruction set support
- Hazard detection and data forwarding
- Fixed not-taken control flow behavior

### DSP Coprocessor
- Pipelined FIR filter for audio signal processing
- Memory-mapped interface (MMIO)
- Configurable filter coefficients
- Fixed-point arithmetic (Q1.15)

### Memory
- Instruction and data memory (on-chip BRAM)
- Program loaded via memory initialization file at bitstream generation

---

## Demo: Audio Filtering Pipeline

The Phase 1 demo sends audio samples from a PC to the FPGA over UART, filters them using the hardware FIR accelerator, and returns the filtered output to be reconstructed as a WAV file.

```
PC (Python)
    |
    | WAV samples over UART
    v
RV32I Core (FPGA)
    |
    | MMIO writes
    v
FIR DSP Accelerator
    |
    | Filtered samples over UART
    v
PC (Python)
    |
    v
Filtered WAV output
```

The demo benchmarks software-only FIR on the RV32I core against hardware-accelerated FIR to measure speedup, cycles, and FPGA DSP resource utilization.

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
├── sw/                   # Bare-metal firmware and host Python scripts
└── docs/                 # Architecture notes and design log
```

---

## Tools

| Tool | Version |
|------|---------|
| Vivado WebPACK | 2025.2.1 |
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
| DSP Peripheral Interface | 🔲 Not started |
| UART Peripheral | 🔲 Not started |
| Top-level Integration | 🔲 Not started |
| Timing Closure (Basys 3) | 🔲 Not started |

---

## Roadmap

### Phase 1 — RV32I + FIR Accelerator
Audio noise reduction and tone filtering demo. RV32I core handles UART communication and MMIO, FIR accelerator performs hardware-accelerated filtering. Benchmarks software vs. hardware FIR execution.

### Phase 2 — Custom DSP ISA Extensions
Extend the RV32I ISA with custom MAC and saturating arithmetic instructions. Modify decode, ALU, and control logic to accelerate DSP workloads natively in the pipeline. Benchmark cycles-per-tap against baseline.

### Phase 3 — Caches and Performance Counters
Add instruction and data caches with performance counter CSRs tracking cycles, instructions retired, cache misses, and branch behavior. Use the CPU as a benchmarking platform for embedded workloads.

### Phase 4 — Hardware Accelerator
Add a matrix multiply or FFT accelerator. Target application is either tiny neural network inference (MLP/CNN layer) or a real-time frequency spectrum analyzer, depending on direction.

---

## References

- [RISC-V ISA Specification (RV32I)](https://riscv.org/technical/specifications/)
- [PicoRV32 — Reference RISC-V Implementation](https://github.com/YosysHQ/picorv32)
- [Basys 3 Reference Manual](https://digilent.com/reference/programmable-logic/basys-3/reference-manual)
- [Vivado Design Suite User Guide](https://docs.amd.com/r/en-US/ug910-vivado-getting-started)
- *Modern VLSI Design*, W. Wolf (4th ed.)
