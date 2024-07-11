# NASSCOM-VSD-SOC-DESIGN-AND-PLANNING

# Table of Contents
- **Introduction**
- **Day 1 - Synthesis of RTL**

## Introduction
OpenLane is an open-source ASIC (Application-Specific Integrated Circuit) flow that facilitates the design and implementation of digital integrated circuits. It provides a complete RTL-to-GDSII (Register Transfer Level to Graphic Data System II) flow, leveraging various open-source EDA (Electronic Design Automation) tools. Developed by Efabless Corporation, OpenLane aims to lower the barrier to entry for ASIC design by providing accessible, high-quality tools and resources.

Key Features of OpenLane
*Open-Source Tools Integration:*

OpenLane integrates a variety of open-source EDA tools, creating a cohesive flow for ASIC design. These tools include Yosys for synthesis, OpenROAD for place and route, Magic and KLayout for layout, and Netgen for LVS (Layout vs. Schematic) verification.

*Customization and Flexibility:*

The flow is highly customizable, allowing designers to tweak parameters and configurations to suit their specific design needs. This flexibility is essential for handling different design constraints and requirements.

*Community and Collaboration:*

OpenLane benefits from a strong open-source community, providing extensive documentation, support, and continuous improvements. This collaborative approach ensures that the flow stays up-to-date with the latest advancements and best practices in ASIC design.

*Educational and Research Use:*

OpenLane is widely used in academic and research settings, providing a valuable platform for teaching and experimenting with digital design concepts. Its open nature makes it an excellent tool for learning and innovation.

###Components and Tools in OpenLane
OpenLane integrates several key open-source tools to provide a comprehensive ASIC design flow:

*Yosys:*

Function: Synthesis
Description: Converts RTL (Verilog) code into a gate-level netlist.

*OpenROAD:*

Function: Place and Route
Description: Handles the physical placement of cells and the routing of interconnections.

*Magic:*

Function: Layout Editor
Description: An interactive layout tool used for designing and viewing chip layouts.

*KLayout:*

Function: Layout Viewer and Editor
Description: Another layout tool, often used for viewing and editing GDSII files.

*Netgen:*

Function: LVS (Layout vs. Schematic)
Description: Compares the layout netlist against the schematic netlist to ensure they match.

*OpenSTA:*

Function: Static Timing Analysis
Description: Performs timing analysis to verify that the design meets timing constraints.

*Fault:*

Function: Formal Verification
Description: Used for formal verification of designs.

###The OpenLane Flow
The typical flow in OpenLane consists of several stages, each corresponding to a specific phase in the ASIC design process:

*Synthesis:*

Convert RTL designs into gate-level netlists using Yosys.

*Floorplanning:*

Define the placement of different blocks and establish the power grid.

*Placement:*

Place the standard cells in the predefined floorplan using OpenROAD.

*Clock Tree Synthesis (CTS):*

Design and insert the clock tree to ensure clock signals are distributed efficiently.

*Routing:*

Route the interconnections between cells and blocks using OpenROAD.

*Signoff:*

Perform final checks and verifications, including DRC (Design Rule Check) and LVS.

*GDSII Generation:*

Generate the final GDSII file, which is used for manufacturing the chip.

## Day 1 - Synthesis of RTL

Aim: we are going to calculate the Flop ratio after the systhesis of RTL of Picorv32a.

### Step 1 - Setting up openlane environment
![OpenLane setup](images/openlane_setup.png)

### Step 2 - Run Synthesis of the RTL
![Run synthesis](images/run_synthesis.png)

### Step 3 - Calculate the flop ratio
![Usage report](images/usage_report.png)

Flop ratio = number of d-flipflops / Total number of cells = 1613/14876 = 0.10842969 .


