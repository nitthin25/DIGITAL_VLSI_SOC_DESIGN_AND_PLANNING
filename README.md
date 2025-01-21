# DIGITAL_VLSI_SOC_DESIGN_AND_PLANNING
Day 1- Inception of Open Source EDA, Openlane and Sky130 PDK

SoC Design and Openlane-
We will be using RTL IP's, EDA tools, and PDK data to form an ASIC Design. All these components will be taken from open-source sites as it makes it easier to design the flow.

For the RTL IP's, we will be using librecores.org, opencores.org, github.com and many other open-source websites. For EDA tools, we will be using OpenLANE, and OpenRoad. OpenROAD will be used for static timing analysis.

For the PDKS, we will be using Skywater 130nm PDK. SkyWater 130nm PDK is an open source PDK developed by SkyWater and Google in collaboration. PDKs include Process Design Rules like DRC,LVS etc., Device models, Digital Standard Libraries, I/O Libraries and many other things.

For more information on the SkyWater PDK, you can visit github.com/google/skywater-pdk .. It was launched on June 30, 2020. 130nm PDKs are used in 6% of all PSK implementation.

Simplified RTL2GDS flow-
The flow starts with Synthesis moving on to Floorplanning/Powerplanning, Placement, Clock Tree Synthesis, Routing and then ending with Static Timing Analysis.
![Image](https://github.com/user-attachments/assets/3790c1c2-4e92-45be-add7-f30632cc6a1a)
Synthesis The synthesis converts the RTL to a circuit out of components from the standard cell library. There are multiple different standard cells. Standard cells of the same component can have different areas based on the use case.

Floorplanning/PowerPlanning There are 2 types of Floorplanning namely Chip Foorplanning and Macro Floorplanning. Power planning works on the placement of power sources such as Vdd and ground.

Placement Placement is used to place the cells on the floorplan rows, alogned with the sites. It is done in 2 steps.

The first step is Global placement in which the flow places the standard cells in optimal position even when they overlap with each other.
Clock Tree Synthesis It is done to create a clock distribution network used to deliver the clock to all sequential elements with minimum skew.

Routing It is used to implement interconnect using available metal layers. Metal tracks form a routing grid which is huge as it covers the entire chip.

Sign Off The Sign Off contains the Physical Verifications like Design Rule Check(DRC) and Layout Vs. Schematic(LVS).

It also does the timing verification using Static Timing Analysis.

OpenLANE-
OpenLANE started as an Open-Source Flow for true Open Source Tape-Out Experiment. They use the striVe family of open everythings.

The ASIC flow's main goal is to produce a clean GDSII with no human intervention. The operation has 2 modes namely autonomous and interactive.
