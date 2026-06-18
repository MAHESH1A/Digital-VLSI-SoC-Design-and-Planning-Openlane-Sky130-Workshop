# Digital-VLSI-SoC-Design-and-Planning-Openlane-Sky130-Workshop
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
## Overview

This repository documents my learning journey through the **5-Day Digital VLSI SoC Design and Planning** workshop organized by **VSD (VLSI System Design)**. The workshop covers the complete RTL-to-GDSII flow using the open-source EDA tool **OpenLANE** with **SkyWater 130nm PDK (Sky130)**.

The workshop provides hands-on experience with:
- Open-source VLSI design tools
- SkyWater 130nm Process Design Kit (PDK)
- Full chip design flow from RTL to GDSII
- Standard cell characterization
- Physical design and timing closure

### Design Used: `picorv32a` (RISC-V based SoC)

---

## Tools & Technologies

| Tool | Purpose |
|------|---------|
| **OpenLANE** | RTL-to-GDSII flow automation |
| **Magic** | Layout editor and DRC/LVS |
| **ngspice** | SPICE simulation |
| **OpenSTA** | Static Timing Analysis |
| **TritonRoute** | Detailed router |
| **Yosys** | RTL synthesis |
| **OpenROAD** | Placement, CTS, optimization |
| **Sky130 PDK** | SkyWater 130nm Process Design Kit |

---
## Course Agenda

In this 5-day workshop we cover:

1. [Inception of Open Source EDA, OpenLANE and Sky130 PDK](./Day1-Inception-of-OpenSource-EDA-OpenLANE-Sky130PDK.md)
2. [Good Floorplan vs Bad Floorplan and Introduction to Library Cells](./Day2-Floorplan-and-Introduction-to-LibraryCells.md)
3. [Design Library Cell using Magic Layout and ngspice Characterization](./Day3-Magic-Layout-ngspice-Characterization.md)
4. [Pre-Layout Timing Analysis and Importance of Good Clock Tree](./Day4-PreLayout-Timing-Analysis-ClockTree.md)
5. [Final Steps for RTL2GDS using TritonRoute and OpenSTA](./Day5-RTL2GDS-TritonRoute-OpenSTA.md)

To conclude the workshop, we learnt how to use, plan, floorplan, place, synthesize clock trees, route and sign-off a complete digital SoC using **open-source RTL-to-GDSII flow**.


