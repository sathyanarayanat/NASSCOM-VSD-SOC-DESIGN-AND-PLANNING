# NASSCOM-VSD-SOC-DESIGN-AND-PLANNING

# Table of Contents
- **Introduction**
- **Day 1 - Synthesis of RTL**
- **Day 2 - Good floorplan and vs Bad floorplan and Itroduction to library cells**
- **Day 3 - Design library cell using Magic Layout and ngspice characterization**

## Introduction
OpenLane is an open-source ASIC (Application-Specific Integrated Circuit) flow that facilitates the design and implementation of digital integrated circuits. It provides a complete RTL-to-GDSII (Register Transfer Level to Graphic Data System II) flow, leveraging various open-source EDA (Electronic Design Automation) tools. Developed by Efabless Corporation, OpenLane aims to lower the barrier to entry for ASIC design by providing accessible, high-quality tools and resources.

Key Features of OpenLane
- *Open-Source Tools Integration:*

OpenLane integrates a variety of open-source EDA tools, creating a cohesive flow for ASIC design. These tools include Yosys for synthesis, OpenROAD for place and route, Magic and KLayout for layout, and Netgen for LVS (Layout vs. Schematic) verification.

- *Customization and Flexibility:*

The flow is highly customizable, allowing designers to tweak parameters and configurations to suit their specific design needs. This flexibility is essential for handling different design constraints and requirements.

- *Community and Collaboration:*

OpenLane benefits from a strong open-source community, providing extensive documentation, support, and continuous improvements. This collaborative approach ensures that the flow stays up-to-date with the latest advancements and best practices in ASIC design.

- *Educational and Research Use:*

OpenLane is widely used in academic and research settings, providing a valuable platform for teaching and experimenting with digital design concepts. Its open nature makes it an excellent tool for learning and innovation.

### Components and Tools in OpenLane

OpenLane integrates several key open-source tools to provide a comprehensive ASIC design flow:

- *Yosys:*

Function: Synthesis

Description: Converts RTL (Verilog) code into a gate-level netlist.

- *OpenROAD:*

Function: Place and Route

Description: Handles the physical placement of cells and the routing of interconnections.

- *Magic:*

Function: Layout Editor

Description: An interactive layout tool used for designing and viewing chip layouts.

- *KLayout:*

Function: Layout Viewer and Editor

Description: Another layout tool, often used for viewing and editing GDSII files.

- *Netgen:*

Function: LVS (Layout vs. Schematic)

Description: Compares the layout netlist against the schematic netlist to ensure they match.

- *OpenSTA:*

Function: Static Timing Analysis

Description: Performs timing analysis to verify that the design meets timing constraints.

- *Fault:*

Function: Formal Verification

Description: Used for formal verification of designs.

### The OpenLane Flow
The typical flow in OpenLane consists of several stages, each corresponding to a specific phase in the ASIC design process:

- *Synthesis:*

Convert RTL designs into gate-level netlists using Yosys.

- *Floorplanning:*

Define the placement of different blocks and establish the power grid.

- *Placement:*

Place the standard cells in the predefined floorplan using OpenROAD.

- *Clock Tree Synthesis (CTS):*

Design and insert the clock tree to ensure clock signals are distributed efficiently.

- *Routing:*

Route the interconnections between cells and blocks using OpenROAD.

- *Signoff:*

Perform final checks and verifications, including DRC (Design Rule Check) and LVS.

- *GDSII Generation:*

Generate the final GDSII file, which is used for manufacturing the chip.

Below is the representation of the RTL to GDSII flow

![flowchart](images/openlane-flow.png)

## Day 1 - Synthesis of RTL

Aim: we are going to calculate the Flop ratio after the systhesis of RTL of Picorv32a.

### Step 1 - Setting up openlane environment
![OpenLane setup](images/openlane_setup.png)

### Step 2 - Run Synthesis of the RTL
![Run synthesis](images/run_synthesis.png)

### Step 3 - Calculate the flop ratio
![Usage report](images/usage_report.png)

Flop ratio = number of d-flipflops / Total number of cells = 1613/14876 = 0.10842969 .

## Day 2 - Good floorplan and vs Bad floorplan and Itroduction to library cells

### Chip floor planning considerations

1. Height and width of core and die

   **core**: The "core" refers to the central part of an integrated circuit (IC) that contains the primary functional elements of the chip, such as the central processing 
  unit (CPU), graphics processing unit (GPU), digital signal processor (DSP), or other specialized processing units.

   **Die**: The "die" is the actual piece of silicon wafer that is cut from the larger wafer during the manufacturing process. It contains the complete integrated circuit, 
  including the core and all peripheral components.

- Utilization factor = Area of the netlist blocks/ total area of core .
- Aspect ratio = Height/width. (of core)

2. Define location of pre-placed cells

   Some of the IPs are placed by the user before automated placement and routing and placement. Hence they are called pre-placed cells.

3. Surround pre-placed cell with decoupling capacitor.

     The state change from a logic '0' to logic '1' requires charge from a voltage source. But, due to the connecting wires
  from the voltage source to the filpflops, there might be voltage drop because of resistance of the wires. If the voltage drop is less than the noise margin, there will no 
  state change. To mitigate this issuse , we make use of decoupling capacitors. These decoupling capacitors are placed near all the sub-blocks.

4. Power planning

     Power planning is a critical aspect of integrated circuit (IC) and system-on-chip (SoC) design that involves creating an efficient power distribution network (PDN) to 
   ensure reliable power delivery to all components of the chip. 

5. Pin placement

    The I/O pins are placed between the boundaries of die and core. The pins are placed in such a way that they are close to the blocks that they feed as input to. The 
  clocks pins are bigger than the normal pins as to provide least resistance path since clocks provide continuous signals throughout the chip function.

6. Logical cells placement blockage

   we make sure to block the pin placement region as to avoid the automated place and route from accessing this region. This is called Logical cells placement blockage.

### Running floorplan

![run_floorplan](images/run_floorplan_1.png)

![run_floorplan](/images/run_floorplan__2.png)

### Io log

![io log](/images/ioplaner_log.png)

### Magic layout view

![io log](/images/floorplan_magic.png)

### Library binding and placement

1. Netlist binding

  - We make use of library files to convert our design components to actual blocks. This library file contains a detailed description of the standard cells or components that can be used to design and implement digital circuits.

2. Inital placement
  - we start with initial placement of cells. we make sure that the blocks are placed close to thier respective inputs and outputs.

    ![initial placement diagram](images/intial_place.png)
    (Image courtesy: [vlsisystemdesign](https://www.vlsisystemdesign.com/))
    
3. Optimizing placement

 - In some scenarios, the distance between the IO pin and the sub-blocks might be large enough such that it may encounter signal integrity loss. In such secaniors, we place buffers between them . These buffers act as repeaters ensuring that signal integrity is maintained till the signal reaches the sub-blocks from the IO pins. Refer to the below diagram.

  ![optimized placement diagram](images/opt_place.png)
  (Image courtesy: [vlsisystemdesign](https://www.vlsisystemdesign.com/)) 
   
### Run placement

![run_placement](images/run_placement.png)

### Magic tool view after placement

![placement view 1](images/magic_place_1.png)

### Zoomed in view

![placement view 1](images/magic_place_2.png)

### Cell design and characterization flows

- **Inputs for cell design flow**: Process design kits (PDKs), DRC nad LVS , SPICE models, library and user defined specs.
  
- **Circuit design step**: We design the p-mos--n-mos diagram as per the specifications. we take into consideration sveral 
                       paramters during this step.
  
- **Layout design step**: With help of eular's path devired from the p-mos and n-mos network paths, we draw stick diagrams.
                          We make use of this stick diagram to come up with the layout diagram of the system.

- **Characterization**: We feed parameters obtained from SPICE list of circuits into a Characterization software called GUNA. This software tool provides us with timing characterization, power characterization and noise characterization.

  ![GUNA](images/guna.png)

  ## Day 3 - Design library cell using Magic Layout and ngspice characterization

  ### IO placer revision

   IO placement can be chnaged by making chnages in the floorplan parameters. This is available in the "floorplan.tcl" file.
  
 - command to view the floorplan.tcl file  
  
```
  cd /Desktop/work/tools/openlane_working_dir/openlane/configuratons/

  cd less floorplan.tcl
  ```

![floorplan.tcl](images/flr_tcl.png)

We now change the IO parameter and run floorplan again.

![change_parameter](images/change_io.png)

The below picture shows the change in the IO placement

![changed_io](images/chng_io_place.png)

### SPICE deck creation for CMOS inverter

A SPICE deck refers to a file containing the input netlist and commands used by the SPICE simulation program. 

Below is an example of a CMOS invertr spice deck.

![spice deck](images/spice_deck.png)
(Image courtesy [vlsisystemdesign](https://www.vlsisystemdesign.com))

### Cloning vsdstdcelldesign repository

```
git clone https://github.com/nickson-jose/vsdstdcelldesign.git
```
![cloning git repo](images/git_vsd.png)

- The next step is to copy the sky130A.tech from magic tool folder to the newly clones directory.

```
cp /Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech /Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign/
```
- This cloned repository contains the library files for a CMOS inverter. We can view the layout using MAGIC tool.

```
magic -T sky130A.tech sky130_inv.mag &
```
![Layout of cmos inverter](images/magic_inv_1.png)

### Extracting SPICE list

The next step is to extract the SPICE list of the inverter. By extracting a SPICE netlist from the layout and performing post-layout simulations, designers can ensure that the physical implementation of the circuit meets the required specifications and functions correctly in the real world.

- Use the below commands to extract the spice list.(In tkcon tab)
```
extract all
ext2spice cthresh 0 rthresh 0
ext2spice
```
![tkcon commands](images/tkcon_cmnd.png)
![spice file creation](images/spice_crt.png)

