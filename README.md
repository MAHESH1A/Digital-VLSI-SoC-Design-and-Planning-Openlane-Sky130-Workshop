# Digital VLSI SoC Design and Planning

What are the Goals of a Digital VLSI SoC Design and Planning Engineer?

- A Digital VLSI SoC Design and Planning Engineer takes an RTL netlist through the complete physical design flow to generate a manufacturable GDSII layout.

- The engineer is not just running tools — they are making design decisions at every stage: floorplanning, placement, clock tree synthesis, routing, and timing closure.

### What topics do we need to cover as a [Digital VLSI SoC Design and Planning Engineer?](https://github.com/nickson-jose/vsdstdcelldesign)

This progression takes you from RTL → Synthesis → Floorplan → Placement → CTS → Routing → [GDSII](https://github.com/The-OpenROAD-Project/OpenLane) using fully open-source EDA tools on the SkyWater 130nm PDK.

## [Digital-VLSI-SoC-Design-and-Planning Workshop](https://www.vlsisystemdesign.com/digital-vlsi-soc-design-and-planning/)

This workshop is a 5-day paid cloud-based program where we synthesize, floorplan, place, perform CTS, route and sign-off a RISC-V based SoC (`picorv32a`) using OpenLANE and Sky130 PDK. Lectures and lab access are paid and private to the individual.

1. [Lecture access](https://vsdiat.vlsisystemdesign.com/sign-in)
2. [Lab access](https://www.vlsisystemdesign.com/digital-vlsi-soc-design-and-planning/)

## Course Agenda

In this 5-day workshop we cover:

1. [Inception of Open Source EDA, OpenLANE and Sky130 PDK](./Day1-Inception-of-OpenSource-EDA-OpenLANE-Sky130PDK.md)
   - QFN-48 package, die, core, pads, macros and foundry IPs
   - RISC-V ISA and the software-to-hardware abstraction stack
   - Open-source ASIC components: RTL + EDA Tools + PDK
   - The OpenLANE RTL2GDS flow and its tool chain
   - Invoking OpenLANE, design prep, running synthesis, and flop ratio calculation

2. [Good Floorplan vs Bad Floorplan and Introduction to Library Cells](./Day2-Floorplan-and-Introduction-to-LibraryCells.md)
   - Utilization factor, aspect ratio and core/die sizing
   - Pre-placed cells, decoupling capacitors and power planning
   - Pin placement and placement blockage
   - Library binding, placement optimization and congestion-aware placement (RePlAce)
   - Cell design flow and characterization (GUNA), timing threshold definitions

3. [Design Library Cell using Magic Layout and ngspice Characterization](./Day3-Magic-Layout-ngspice-Characterization.md)
   - SPICE deck creation and simulation of a CMOS inverter
   - Switching threshold (Vm) and static/dynamic characterization
   - The 16-mask CMOS fabrication process — wells, gate, LDD, source/drain, interconnects
   - Sky130 layers in Magic, layout-to-SPICE extraction
   - Sky130 tech-file DRC rules and fixing rule errors

4. [Pre-Layout Timing Analysis and Importance of Good Clock Tree](./Day4-PreLayout-Timing-Analysis-ClockTree.md)
   - Converting a custom cell layout to LEF and integrating it into OpenLANE
   - Delay tables and timing libraries
   - Setup/hold timing analysis with ideal clocks using OpenSTA
   - Clock Tree Synthesis (TritonCTS) using the H-Tree algorithm and clock net shielding
   - Setup/hold timing analysis with real (post-CTS) clocks

5. [Final Steps for RTL2GDS using TritonRoute and OpenSTA](./Day5-RTL2GDS-TritonRoute-OpenSTA.md)
   - Maze routing using Lee's Algorithm and Design Rule Check (DRC)
   - Power Distribution Network — from power pads to standard cell rails
   - Global routing (FastRoute) vs Detailed routing (TritonRoute)
   - TritonRoute features: route guides, inter-guide connectivity, routing topology optimization
   - Final sign-off: DRC, LVS, antenna check, and GDSII generation

To conclude the workshop, we learnt how to use, plan, floorplan, place, synthesize clock trees, route and sign-off a complete digital SoC using **open-source RTL-to-GDSII flow**.

## Repository Structure

```
Digital-VLSI-SoC-Design-and-Planning/
├── README.md
├── Day1-Inception-of-OpenSource-EDA-OpenLANE-Sky130PDK.md
├── Day2-Floorplan-and-Introduction-to-LibraryCells.md
├── Day3-Magic-Layout-ngspice-Characterization.md
├── Day4-PreLayout-Timing-Analysis-ClockTree.md
├── Day5-RTL2GDS-TritonRoute-OpenSTA.md

```

## Tools and PDK Used

| Tool | Purpose |
|------|---------|
| **OpenLANE** | RTL-to-GDSII flow automation |
| **Yosys + ABC** | RTL synthesis |
| **OpenROAD** | Floorplanning, placement, CTS, global routing |
| **TritonRoute** | Detailed routing |
| **Magic** | Layout editing, DRC, GDSII generation |
| **ngspice** | SPICE circuit simulation |
| **OpenSTA** | Static timing analysis |
| **Netgen** | LVS (Layout vs Schematic) |
| **Sky130 PDK** | SkyWater 130nm open-source process design kit |

**Design used:** `picorv32a` — a RISC-V based SoC core

