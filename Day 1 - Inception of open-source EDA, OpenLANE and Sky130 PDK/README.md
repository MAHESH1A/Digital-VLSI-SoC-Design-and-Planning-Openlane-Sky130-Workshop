# Day 1 - Inception of Open-Source EDA, OpenLANE and Sky130 PDK

## SKY130_D1_SK1 - How to Talk to Computers

### L1 - Introduction to QFN-48 Package, Chip, Pads, Core, Die and IPs

When we talk about a chip on a board, what we actually see is the **Package** (e.g., QFN-48). The real silicon die sits at the centre of this package, connected to the outside world through tiny wires.

Key terms to understand:

| Term | Description |
|------|-------------|
| **Package** | Protective casing (e.g., QFN-48) that holds the die and exposes pins |
| **Die** | The actual silicon chip — everything inside the package boundary |
| **Core** | The region inside the die where all digital logic is placed |
| **Pads** | Interface cells on the boundary of the die that connect core signals to package pins |
| **Foundry IPs** | Pre-designed analog/mixed-signal blocks from the foundry (PLL, ADC, DAC, SRAM) |
| **Macros** | Reusable digital RTL blocks (GPIO bank, SPI, RISC-V SoC core) |

<div align="center">
<img src="Day1/screenshots/die_pads_core.png" width="800">
</div>
<p align="center">
<b>Figure 1:</b> QFN-48 Package showing Die, Pads and Core
</p>

> The image above shows a RISC-V SoC die with GPIO pads on all four sides, a central core area (shown empty/black), and the distinction between Die, PADS and Core labelled clearly.

![Macros and Foundry IPs](./Day1/screenshots/macros_foundry_ips.png)

> Inside the core: the RISC-V SoC (blue), GPIO bank, SRAM (Foundry IP), PLL, ADC/DAC blocks — Macros are pure digital; Foundry IPs require foundry-specific knowledge to build.

---

### L2 - Introduction to RISC-V

**RISC-V** is an open-source Instruction Set Architecture (ISA). It acts as the abstract interface between software and hardware.

Flow:
```
C/C++ Program  →  Compiler  →  RISC-V Assembly  →  Assembler  →  Binary (0s and 1s)  →  Hardware (RTL + Layout)
```

The hardware that physically executes these binary instructions is described in RTL (Verilog/VHDL) and eventually implemented as a silicon layout.

---

### L3 - From Software Applications to Hardware

![Software to Hardware](./Day1/screenshots/software_to_hardware.png)

The full stack from app to chip:

- **Application Software** (Firefox, Word, VLC) runs on an **OS**
- The OS talks to the hardware via **System Software** — it compiles high-level code using a **Compiler** into ISA instructions (e.g., RISC-V `add x6, x10, x6`)
- An **Assembler** converts those instructions into **binary machine code**
- That binary drives the actual **Hardware** (the chip layout)

![RISC-V to RTL to Layout](./Day1/screenshots/riscv_rtl_layout.png)

> Three layers shown: RISC-V ISA (assembly), RTL implementation (`picorv32`), and the resulting physical layout (qflow view) — all three represent the same design at different levels of abstraction.

---

## SKY130_D1_SK2 - SoC Design and OpenLANE

### L1 - Introduction to All Components of Open-Source Digital ASIC Design

![Open Source ASIC](./Day1/screenshots/open_source_asic.png)

A complete open-source ASIC design needs three things:

| Component | Open-Source Options |
|-----------|-------------------|
| **RTL Designs** | librecores.org, opencores.org, github.com |
| **EDA Tools** | Qflow, OpenROAD, OpenLANE |
| **PDK Data** | Google + SkyWater SKY130 (FOSS 130nm Production PDK) |

The **SKY130 PDK** (released by Google + SkyWater in 2020) was a landmark moment — the first open, manufacturable, production-quality PDK available to everyone.

---

### L2 - Simplified RTL2GDS Flow

![RTL to GDSII Flow](./Day1/screenshots/rtl2gds_flow.png)

The RTL-to-GDSII flow has 6 major stages:

```
RTL  →  Synthesis  →  Floorplan + Power Planning  →  Placement  →  CTS  →  Routing  →  Sign Off  →  GDSII
```

| Stage | What happens |
|-------|-------------|
| **Synthesis** | Converts RTL (Verilog) to a gate-level netlist using standard cells |
| **Floorplan + Power Planning (FP+PP)** | Defines core area, I/O placement, and power mesh (VDD/GND grid) |
| **Placement** | Places standard cells inside the core — Global then Detailed |
| **CTS** | Clock Tree Synthesis — builds a balanced clock distribution network |
| **Routing** | Connects all cells using metal layers — Global then Detailed routing |
| **Sign Off** | STA (timing), DRC (design rules), LVS (layout vs schematic) checks |

---

### L3 - Introduction to OpenLANE and Strive Chipsets

**OpenLANE** is an open-source, automated RTL-to-GDSII flow built around the SkyWater 130nm PDK.

- Developed at **efabless** as part of the **Strive** chipset family
- Integrates multiple open-source tools into a single push-button flow
- Supports both **autonomous** (fully automated) and **interactive** modes
- Design target: produce a **clean GDSII with zero DRC/LVS violations**

---

### L4 - Introduction to OpenLANE Detailed ASIC Design Flow

![OpenLANE ASIC Flow](./Day1/screenshots/openlane_asic_flow.png)

The detailed OpenLANE flow:

| Step | Tool Used |
|------|-----------|
| RTL Synthesis | Yosys + ABC |
| STA (post-synth) | OpenSTA |
| DFT | Fault |
| Floorplanning | OpenROAD App |
| Placement | OpenROAD App |
| CTS | OpenROAD App (TritonCTS) |
| Global Routing | OpenROAD App (FastRoute) |
| Fake antenna diode insertion | Custom script |
| Detailed Routing | TritonRoute |
| RC Extraction | SPEF-Extractor |
| STA (post-route) | OpenSTA |
| Physical Verification (DRC+LVS) | Magic + Netgen |
| GDSII Streaming | Magic |

---

## SKY130_D1_SK3 - Get Familiar with Open-Source EDA Tools

### L1 - OpenLANE Directory Structure in Detail

```
~/Desktop/work/tools/openlane_working_dir/
├── openlane/                        ← OpenLANE flow scripts
│   └── designs/
│       └── picorv32a/
│           ├── config.tcl           ← Design-level configuration
│           ├── sky130A_sky130_fd_sc_hd_config.tcl
│           └── src/
│               ├── picorv32a.v      ← RTL source
│               └── *.lib            ← Timing libraries (slow/fast/typical)
└── pdks/
    └── sky130A/
        ├── libs.ref/                ← Technology files (LEF, LIB, SPICE)
        └── libs.tech/               ← Tool-specific files (Magic, ngspice, etc.)
```

**PDK used:** `sky130A` → Cell library: `sky130_fd_sc_hd` (High Density standard cell library)

---

### L2 - Design Preparation Step

```bash
# Go to OpenLANE working directory
cd ~/Desktop/work/tools/openlane_working_dir/openlane

# Launch OpenLANE in Docker
docker

# Start interactive flow
./flow.tcl -interactive

# Load OpenLANE package
package require openlane 0.9

# Prepare the design — merges LEFs, sets up run directory
prep -design picorv32a
```

After `prep`, a `runs/` directory is created under `picorv32a/` with a timestamped folder containing all config and log files for this run.

---

### L3 - Review Files After Design Prep and Run Synthesis

```bash
# Run synthesis (Yosys + ABC)
run_synthesis
```

Synthesis output is saved to:
```
designs/picorv32a/runs/<tag>/results/synthesis/picorv32a.synthesis.v
```

---

### L4 - OpenLANE Project Git Link Description

OpenLANE source and documentation:
- [https://github.com/The-OpenROAD-Project/OpenLane](https://github.com/The-OpenROAD-Project/OpenLane)

---

### L5 - Steps to Characterize Synthesis Results

After synthesis, check the statistics report at:
```
designs/picorv32a/runs/<tag>/reports/synthesis/
```

**Key metric — Flop Ratio:**

```
Flop Ratio = Number of D Flip-Flops / Total Number of Cells
           = 1613 / 14876
           = 0.1084
           ≈ 10.84%
```

| Parameter | Value |
|-----------|-------|
| Total cells | 14876 |
| D Flip-Flops (`sky130_fd_sc_hd__dfxtp_2`) | 1613 |
| **Flop Ratio** | **10.84%** |
| Chip area | ~147712 µm² |

A higher flop ratio generally indicates a more sequential (register-heavy) design.

---

## Summary

By the end of Day 1 we understood:
- The anatomy of a chip: Package → Die → Core → Pads, Macros, Foundry IPs
- How software flows down to hardware through ISA, RTL, and physical layout
- The three pillars of open-source ASIC design: RTL + EDA Tools + PDK
- The complete OpenLANE RTL-to-GDSII flow and its tool chain
- How to invoke OpenLANE, prepare a design, run synthesis, and read flop ratio from synthesis reports

---

> Next: [Day 2 - Good Floorplan vs Bad Floorplan and Introduction to Library Cells](../Day2-Floorplan-and-Introduction-to-LibraryCells.md)
