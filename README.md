# DIGITAL_VLSI_SOC_DESIGN_AND_PLANNING
Day 1- Inception of Open Source EDA, Openlane and Sky130 PDK

SoC Design and Openlane-
We will be using RTL IP's, EDA tools, and PDK data to form an ASIC Design. All these components will be taken from open-source sites as it makes it easier to design the flow.

For the RTL IP's, we will be using librecores.org, opencores.org, github.com and many other open-source websites. For EDA tools, we will be using OpenLANE, and OpenRoad. OpenROAD will be used for static timing analysis.

For the PDKS, we will be using Skywater 130nm PDK. SkyWater 130nm PDK is an open source PDK developed by SkyWater and Google in collaboration. PDKs include Process Design Rules like DRC,LVS etc., Device models, Digital Standard Libraries, I/O Libraries and many other things.

For more information on the SkyWater PDK, you can visit github.com/google/skywater-pdk .. It was launched on June 30, 2020. 130nm PDKs are used in 6% of all PSK implementation.

Simplified RTL2GDS flow-
The flow starts with Synthesis moving on to Floorplanning/Powerplanning, Placement, Clock Tree Synthesis, Routing and then ending with Static Timing Analysis.
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

![Image](https://github.com/user-attachments/assets/8b5402e5-b0d3-451d-a894-10e8f24b96d9)

Get familiar to open-source EDA tools-

To get into OpenLANE flow we have to set our directory to
cd /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane

INVOKING OPENLANE FLOW,RUNNING SYNTHESIS,FLOP RATIO

openlane flow-
![Image](https://github.com/user-attachments/assets/d810fe92-34ca-4d27-9556-40bde7635f88)

running synthesis-
![Image](https://github.com/user-attachments/assets/ccaa7311-61b4-464f-bb32-56b4705c3613)

flop ratio-
![Image](https://github.com/user-attachments/assets/ec7ee68b-ae2a-4f11-a833-5cccdf8de50c)

dfxtp_2 - 1613

no.of.cells - 14876

ratio= 10.84296




Day 2- Good floorplan vs Bad floorplan and introduction to library cells


Chip Floor planning-

Floorplanning in the context of VLSI (Very-Large-Scale Integration) design refers to the process of determining the physical arrangement of components on a chip. It plays a critical role in ensuring the functionality, performance, and manufacturability of the integrated circuit (IC). A good floorplan optimizes key parameters like area, power, performance, and thermal management.

Key Components of Floorplanning:

-> Cells and Blocks: These are the fundamental building units of the design. Cells can be logic gates, flip-flops, or other standard cells, while blocks are groups of cells or larger functional units.

-> Macros: These are pre-designed functional units, such as memory or complex modules, which are placed on the chip during floorplanning.

-> Power and Ground Distribution: Ensuring proper routing of power and ground to all components is a key part of floorplanning to prevent power issues (usually seperately done as powerplan).

Floorplan Parameters: Aspect Ratio: The aspect ratio is the ratio of the chip's length to its width. A good aspect ratio ensures a balanced distribution of the area and helps in minimizing routing congestion. The aspect ratio should generally be kept close to 1:1 for optimal performance, but it depends on the specific design goals.

Aspect Ratio = Length / Width: If the chip’s dimensions are square-like, the aspect ratio is 1:1. A long, narrow chip would have a high aspect ratio  whereas a wider chip might have a lower aspect ratio 

utilization factor- area occupied by the netist/total area of core

Floorplan Types:

-> Row-based floorplan: Components are organized in horizontal rows. This is common for standard cell layouts.

-> Cluster-based floorplan: Groups related components (or blocks) into clusters, optimizing them together.

->Core-based floorplan: Components are arranged within a predefined core region, and peripheral components are placed around the core.

Pre-placed Cells:
Pre-placed cells refer to certain large, predefined blocks or modules in a circuit design that are placed early in the physical design flow, typically before the general placement and routing stages. These cells include complex functional units like memory blocks, PLLs (Phase-Locked Loops), or other highly specialized components that have been designed and optimized separately. They are pre-configured to meet specific performance, power, or area requirements and are intended to be reused across different designs, saving both time and effort.

These cells are crucial for several reasons:

Performance Optimization: Pre-placing certain cells can help in optimizing the overall performance of the design. For instance, memory blocks are often large and complex, and placing them early can ensure they are located in the most efficient part of the chip. This can reduce the delay and the overall wire length for connecting other components, thus improving speed.

IP Integration: Pre-placed cells often consist of Intellectual Property (IP) blocks that are already verified and validated. These blocks can be integrated into various designs without the need to redesign the modules from scratch. This accelerates the design process and ensures consistency and reliability across different designs.

Power Optimization: By pre-placing power-hungry modules such as memory, complex functional units, or processors, designers can optimize power delivery. This reduces the likelihood of power supply issues, ensuring that these critical blocks have the necessary resources to function without fluctuations in voltage or current.

Decoupling Capacitors:
Decoupling capacitors play an essential role in maintaining a stable power supply, particularly in circuits with high-speed switching elements or complex pre-placed cells. A decoupling capacitor is a type of capacitor placed strategically between the power supply and the integrated circuit (IC). Their primary purpose is to smooth out fluctuations in the power supply voltage caused by sudden current demands during switching events.

Key Functions of Decoupling Capacitors:

Voltage Stabilization: When high-speed circuits or modules like processors, memory, or pre-placed functional blocks switch between states, they can cause rapid changes in current demand. These changes can lead to voltage drops or noise that affect the reliability and stability of the design. Decoupling capacitors help mitigate these effects by providing a localized source of charge. They store electrical energy during periods of low activity and release it when there’s a surge in current demand, thereby stabilizing the power supply voltage.

Charge Reservoir: Decoupling capacitors act as charge reservoirs. When the circuit is idle or not switching, the capacitor charges up from the power supply. However, when the circuit begins to switch or experience high current demand, the capacitor discharges, providing the required current to the circuit. This ensures that the switching transients are met without causing voltage sag or power interruptions.

Noise Filtering: Besides stabilizing voltage, decoupling capacitors filter out high-frequency noise from the power supply. These fluctuations or noise spikes, which can be caused by high-frequency switching activities, can interfere with the operation of the circuit. By placing capacitors near sensitive pre-placed cells or blocks, this noise is suppressed, maintaining the integrity of the signal.

Proximity to Critical Components: The effectiveness of decoupling capacitors depends on their placement. Ideally, they should be placed as close as possible to the power supply pins of the pre-placed cells. This minimizes the impedance and resistance of the traces between the capacitor and the cell, ensuring quick and efficient charge delivery during switching events. Additionally, multiple capacitors may be used to target different frequencies, with smaller capacitors handling higher-frequency noise and larger ones addressing lower-frequency fluctuations.

Importance in Power and Performance:

Power Management: Decoupling capacitors contribute to better power management by reducing the demand on the central power supply, thereby enhancing efficiency.

Preventing Power Supply Instability: Without these capacitors, circuits would be more vulnerable to power supply instability during heavy switching activity, which could lead to system malfunctions or crashes.

Preserving Signal Integrity: By filtering out noise, these capacitors help maintain the integrity of signals and ensure the smooth operation of high-speed circuits.

Pin Placement
Pin placement in physical design is a crucial aspect that directly influences the performance, manufacturability, and reliability of a chip or circuit board. It involves strategically positioning the input/output (I/O) pins to optimize signal routing, minimize delays, and reduce interference. Proper placement ensures signal integrity by shielding sensitive signals from noisy power pins, preventing signal degradation. Moreover, it allows for the even distribution of power across the chip, avoiding voltage drops and hotspots that could affect performance. Heat management is another important consideration, as high-power components must be positioned for effective heat dissipation. Placing buffers near the I/O ports is a key technique used to improve signal driving capabilities and minimize the impact of long routing delays. Buffers act as intermediaries between the I/O pins and internal circuits, ensuring that signals are properly amplified and driving strength is maintained, especially in high-speed designs or when driving multiple load lines. Pin placement also must align with packaging constraints, ensuring compatibility with external connectors and packaging standards. Additionally, grouping related signals together helps simplify routing and improves design efficiency. By considering all these factors, including proper buffer placement, pin placement enhances the overall design’s reliability, manufacturability, and ease of testing.

Power Planning
Power planning is a vital aspect of integrated circuit (IC) design, ensuring efficient power delivery, minimizing power consumption, and maintaining the chip’s performance and reliability. It involves designing a comprehensive power distribution network (PDN) that effectively distributes power across the chip while minimizing voltage drops and noise. A key component of power distribution is the power mesh, which is a network of metal layers that form the power grid, connecting the power (VDD) and ground (VSS) pins to all parts of the chip. The power mesh ensures that power is delivered evenly to all modules, balancing the power distribution and reducing the risk of localized voltage fluctuations. In addition to the power mesh, the grid system is composed of horizontal and vertical metal layers, which create a structure for the PDN. The grid is designed to handle the current load and maintain a stable voltage level across the chip.

Steps to run floorplan-

run_floorplan

1)![Image](https://github.com/user-attachments/assets/7f901351-9690-4c61-b43c-583f8801d769)

2)![Image](https://github.com/user-attachments/assets/109a7eea-270c-4b92-9900-c67dc94b9665)

3)![Image](https://github.com/user-attachments/assets/e184a037-6f68-4261-a3c7-50c556d3d8d0)

4)![Image](https://github.com/user-attachments/assets/e23d5b93-b9ca-4d60-9407-42ad360e514f)

steps to run placements-

Change the directory to
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/29-12_09-40/results/placement/

Command to start the floorplan file in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &

1)![Image](https://github.com/user-attachments/assets/f8be3560-270e-4680-8746-d12125cf1ec6)

2)![Image](https://github.com/user-attachments/assets/c1ae07a1-83d2-4a0e-b0b0-73867e3f9072)

Placement and Routing-
1) Bind netlist with physical cells

The physical cells are rectangular in shape and not in their original shape

All blocks are present in the library where it also has additional information about the cells

The cells can come in various areas based on the resistance and speed the user wants.

2) Placement

We have a floorplane with shapes and sizzes of cells in netlist

We have to place the cells on the floorplan in the optimized manner.

To reduce the dropping of voltage, we also use multiple buffers to regenerate the signal.

![Image](https://github.com/user-attachments/assets/28fa1313-03b7-4080-ad3b-0f16ff78d7a0)


cell design flow-

Inputs For design flow to work, it should be inputted with PDKs, DRC and LVS Rules, SPICE Models, Library and user defined specifications

Design Steps

Circuit Design : Implementation of the design
Layout Design : Form the layout of the design
Characterization
Outputs CDL(Circuit Description Language), GDSII, LEF, extracted spice netlist

Characterizations
Read model file
Read extracted spice list
Recognize behaviour of cell
Read subcircuit of cell
Attach necessary power sources
Apply stimulus(input)
Provide output capacitance
Provide necessary simulation commands
Timing Characterization
** Timing Threshold Definations**

Slew low rise threshold: 20% of supply voltage in rising output
Slew high rise threshold: 80% of supply voltage in rising output
Slew low fall threshold: 20% of supply voltage in falling output
Slew high fall threshold: 80% of supply voltage in falling output
input rise threshold: 50% of input while rising
input falling threshold: 50% of input while falling
output rising threshold: 50% of output while rising
output falling threshold: 50% of output while falling


Day 3- Design library cell using Magic Layout and ngspice

IO Placer Revision in OpenLANE-

bash$ set ::env(FP_IO_MODE) 2

This command switches the IO placement to mode 2, which places the input-output pins based on a different algorithm, often stacking them one over the other rather than maintaining equidistant spacing. It utilizes a technique such as the Hungarian algorithm, which aims to optimize pin placement based on various factors like signal timing, congestion, and layout constraints.

SPICE Deck Creation for CMOS Inverter-

![Image](https://github.com/user-attachments/assets/cb837d76-92cf-41fe-9866-548c4e0fa9f6)

Threshold Voltage-

In CMOS (Complementary Metal-Oxide-Semiconductor) technology, the switching threshold (Vm) is one of the most important parameters for determining the transition point between the logical "0" and "1" in a CMOS inverter. Graphically, Vm corresponds to the point where the input voltage (Vin) is equal to the output voltage (Vout), which typically occurs at the middle of the inverter’s DC transfer characteristic curve. Understanding the Graphical Behavior of a CMOS Inverter

A CMOS inverter’s DC transfer characteristic graph is a plot of the output voltage (Vout) versus the input voltage (Vin). The typical curve for a CMOS inverter is an S-shaped curve, showing the following key features:

When Vin is low (0V):

The NMOS transistor is turned off, and the PMOS transistor is turned on.

The output voltage (Vout) is high (VDD).

When Vin is high (VDD):

The PMOS transistor is turned off, and the NMOS transistor is turned on.

The output voltage (Vout) is low (0V).

Transition Region:

In the middle of the curve, where Vin changes from low to high (0 to VDD), there is a region of transition. Here, both PMOS and NMOS transistors are partially turned on, and the output voltage (Vout) is not fully high or low. This region is crucial for defining the switching threshold (Vm).

Graphical Representation of Switching Threshold (Vm)

The switching threshold (Vm) occurs at the point on the curve where the output voltage (Vout) is equal to the input voltage (Vin). This is typically at the midpoint of the transition region. In an ideal CMOS inverter, the Vm is usually around VDD/2. However, it can vary slightly due to factors like process variation, temperature, and the specific characteristics of the PMOS and NMOS transistors.

Vm is the point on the graph where:

𝑉in=Vout=𝑉𝑚

![Image](https://github.com/user-attachments/assets/4acc421f-fe6c-43de-8da8-da2ad7dccda4)

Static and Dynamic Simulation of CMOS Inverter-
Key observations in static simulation:

Switching Threshold (Vm): The point where the inverter changes its output logic level from high to low (or vice versa). This is the critical point in the S-curve.

Noise Margin: The region around the switching threshold defines the noise margin, which is a measure of how much noise can be tolerated on the input without causing errors in the output.

Dynamic Simulation (Transient Analysis)
In dynamic simulation, we analyze the behavior of the CMOS inverter in response to time-varying inputs, typically involving pulses or square wave inputs. This simulation helps to determine propagation delay and transition times (rise and fall times) during the inverter’s switching operation.

Step-by-step simulation: The input voltage (Vin) is typically applied as a square wave or pulse signal that varies with time. In this type of simulation, we are interested in how the inverter responds to rapid changes in input, especially when the input signal is switching from low to high or vice versa.

Propagation delay: This is the time it takes for the output to transition from one logic state to another after the input has crossed a threshold (either from low to high or high to low). This is measured as the time between when the input crosses 50% of its transition and when the output reaches 50% of its corresponding transition.

Rise and fall time: These are the times it takes for the output to transition from 10% to 90% (rise) or from 90% to 10% (fall) of the supply voltage (VDD). These times are crucial for determining the speed at which the CMOS inverter can switch.

Key observations in dynamic simulation:

Rise Transition Time: The time it takes for the output to go from 10% to 90% of its final high state (VDD).

Fall Transition Time: The time it takes for the output to go from 90% to 10% of its final low state (0V).

Propagation Delay: The time delay from when the input signal reaches 50% of its final value to when the output reaches 50% of its final value.

Git cloning vsdstdcelldesign-

To clone the vsdstdcelldesign into your directory,

Go to openelane directory
cd Desktop/work/tools/openlane_working_dir/openlane

Clone the repository
git clone https://github.com/nickson-jose/vsdstdcelldesign

This repository contains all the necessary information to build and run the OpenLane flow, which performs a full ASIC implementation from RTL to GDSII.

It includes the procedure to create a custom LEF file and also contains the steps to integrate the custom LEF file into the OpenLANE flow

Next, we have to open the inverter layout thriugh the Magic Tool

Go to the vsdstdcelldesign directory
cd vsdstdcelldesign

copy the magic tech file
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .

Open the inverter layout
magic -T sky130A.tech sky130_inv.mag &

![Image](https://github.com/user-attachments/assets/f2d7cb90-50d0-47fb-af40-61bb2d6232b3)

![Image](https://github.com/user-attachments/assets/e7d728b1-b7b7-4e06-a2a5-8c909af18f17)

![Image](https://github.com/user-attachments/assets/8fb075fd-656c-4ae1-b780-177e942c12aa)

![Image](https://github.com/user-attachments/assets/85420762-da76-4901-ad00-c782bb61354a)

![Image](https://github.com/user-attachments/assets/05ed2f30-18f2-4c22-a2af-2edb46b7f68b)

Spice Extraction of Inverter in magic -

Use the following commands to extract the spice file of the custom inverter layout

extract all

ext2spice cthresh 0 rthresh 0

ext2spice

![Image](https://github.com/user-attachments/assets/01e1dab0-98a3-479f-9bde-27e11ba28e2c)

![Image](https://github.com/user-attachments/assets/526d8ddb-4774-4708-8816-a1b4c617f69a)


Using the Magic tool for Sky130 Tech File-

To invoke the magic tool, follow the following steps:

Change the directory to home directory
cd

Command to download the lab files
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

tar xfz drc_tests.tgz

Change to the drc_tests directory
cd drc_tests

Command to list the contents of directory
ls -al

Command to view .magicrc file
gvim .magicrc

Command to invoke the magic tool
magic -d XR &

![Image](https://github.com/user-attachments/assets/df73028a-7521-4250-9976-0b4fa4b0b511)

In the Tckon gui, type the command: "load poly"

![Image](https://github.com/user-attachments/assets/3a725e8b-3d41-4deb-999a-ade0f786589c)

Identify the poly.9 components and the box dimensions which are violating the rules

![Image](https://github.com/user-attachments/assets/097d03c7-6573-439a-94a2-c0a4dd2ea065)

Change the sky130A.tech file using the command gvim sky130A.tech in the following places

![Image](https://github.com/user-attachments/assets/18ccee8f-529f-4d27-934f-37bc741e91e5)

![Image](https://github.com/user-attachments/assets/f2993cf0-523c-4296-b990-c19dc8b50a7d)


Day4 - Pre-Layout timing analysis and importance of good clock tree synthesis


Converting grid info to track info-

We use this process for ease in the process of physical design

Follow the steps to convert the grid info to track info:

#Change directory to vsdstdcelldesign
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

#Open the layout of inverter through magic
magic -T sky130A.tech sky130_inv.mag &

To find the grid info,

help grid

grid 0.46um 0.34um 0.23um 0.17um

![Image](https://github.com/user-attachments/assets/ad5b8664-7c6d-4d8e-9122-51104bab7597)

![Image](https://github.com/user-attachments/assets/ebfc4502-957e-415d-ac00-aa6fd6c636ad)

Next, we will generate a lef file from the layout

lef write

![Image](https://github.com/user-attachments/assets/fd52b1be-777f-4a66-8659-debe5994225f)

Make the following changes to reduce the wns(worst net slack) which is coming negative

Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 24-03_10-03 -overwrite

Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

Command to display current value of variable SYNTH_STRATEGY
echo $::env(SYNTH_STRATEGY)

Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled
echo $::env(SYNTH_BUFFERING)

Command to display current value of variable SYNTH_SIZING
echo $::env(SYNTH_SIZING)

Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

![Image](https://github.com/user-attachments/assets/838b6731-4579-4364-af76-d253bf926e91)



we have to perform the OpenROAD timing analysis using the following commands-

Checking the current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

Removing 'sky130_fd_sc_hd__clkbuf_1' from the list
set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]

Checking the updated value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

Checking the current value of 'CURRENT_DEF'
echo $::env(CURRENT_DEF)

Setting the DEF file as the placement definition
set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/05-01_04-30/results/placement/picorv32a.placement.def

Run Clock Tree Synthesis (CTS) again with the updated settings
run_cts

Checking the updated value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

Launch OpenROAD for timing analysis
openroad

Read the LEF file for the design
read_lef /openLANE_flow/designs/picorv32a/runs/05-01_04-30/tmp/merged.lef

Read the DEF file after CTS
read_def /openLANE_flow/designs/picorv32a/runs/05-01_04-30/results/cts/picorv32a.cts.def

Create an OpenROAD database for the design
write_db pico_cts1.db

Load the created database in OpenROAD
read_db pico_cts.db

Read the netlist after CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/05-01_04-30/results/synthesis/picorv32a.synthesis_cts.v

Read the Liberty file for the design
read_liberty $::env(LIB_SYNTH_COMPLETE)

Link the design with the Liberty file
link_design picorv32a

Read the custom SDC file for timing constraints
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

Set all clocks as propagated clocks
set_propagated_clock [all_clocks]

Generate a custom timing report with min and max path delays
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

Report hold skew for the design
report_clock_skew -hold

Report setup skew for the design
report_clock_skew -setup

Exit OpenROAD and return to OpenLane flow
exit



Day 5- Final steps for RTL2GDS using triton route and openSTA

Routing-

Routing is a crucial step in the design process of VLSI circuits, responsible for creating the physical interconnections between various components (e.g., logic gates, flip-flops, and memory cells). The objective of routing is to establish a valid and efficient path for signals to travel between these components while adhering to design rules and avoiding obstacles. Routing algorithms take the source and target pins, typically located on the chip, and aim to find the most optimal path for the connection.

Maze Routing and the Lee Algorithm
Maze routing is one of the most fundamental methods for routing in VLSI design. The Lee algorithm is a widely used maze routing algorithm that efficiently solves the problem of finding the shortest path between two points in a grid-like structure, which is typical in VLSI layout design. The algorithm works well for both global and detailed routing, ensuring that the routing process adheres to constraints like spacing rules and layer restrictions.

Working of Lee's Algorithm:
Grid Setup:
A grid, similar to the layout created during cell customization, is established where each point corresponds to a potential location for routing.

Obstacles, such as existing metal layers or other components, are identified on the grid as "blocked" regions where routing cannot pass.

Start and Target Points:
The source (starting point) and target (destination point) are marked on the grid. The goal is to find the shortest possible path between these two points.

Labeling:
Lee's algorithm works by labeling the neighboring cells around the source point. Initially, the source point is labeled as 0 (starting point), and its immediate neighbors are assigned the value 1. The algorithm then propagates through the grid, incrementing the values of neighboring cells (e.g., 2, 3, 4, etc.) as it moves further away from the source.

The algorithm continues this process until it reaches the target, incrementing the distance labels along the way.

Pathfinding:
Once the algorithm reaches the target, it traces the path from the target back to the source by following the cells with the lowest labels.

This path is the shortest possible route between the source and target.

Path Shape:
The algorithm can produce different types of paths, such as L-shaped or zigzag-shaped routes. Lee's algorithm tends to prioritize L-shaped paths when they are available, as they typically represent more efficient routing with fewer turns.

If L-shaped paths are unavailable due to obstacles or other constraints, the algorithm may resort to zigzag paths.

Termination:
The algorithm terminates once the target is reached, and the optimal routing path is identified. If no path exists (due to obstacles blocking all possible routes), the algorithm will indicate that no solution is found.

![Image](https://github.com/user-attachments/assets/1414dd9e-525c-409e-b612-37286316c79f)

![Image](https://github.com/user-attachments/assets/2745d955-0826-4532-834f-053bcbecdb67)

Design Rule Check-

Design Rules for Physical Wires:

Minimum Width of the Wire: Ensures that the width of a wire (or metal line) does not fall below a specified minimum value. If the wire is too thin, it may not be able to carry the required current, leading to reliability issues.

Minimum Spacing Between Wires: This rule ensures that there is enough space between two adjacent wires to prevent short-circuiting. If wires are placed too close together, they may overlap, causing an electrical short.

Minimum Pitch of the Wire: The pitch is the center-to-center distance between two consecutive wires. A smaller pitch allows more wires to be placed in the same area, increasing integration, but it also increases the chance of signal interference and crosstalk.

Via Rules:

4(a). Via Width: Defines the minimum size of the via (a metal connection between layers), ensuring that it is large enough to carry the current without resistance or reliability issues.

4(b). Via Spacing: Ensures that vias are spaced apart sufficiently to avoid the risk of electrical shorts and maintain the integrity of the routing.

Metal Layer Considerations:
Metal Layer to Upper Metal Layer: To avoid signal shorts due to adjacent metal layers, it may be necessary to route a signal from one metal layer to another using a via. The design must ensure that the via rules are followed to prevent short-circuiting between metal layers.

Signal Integrity:
6(a). Minimum Width of the Metal Layers: To avoid signal degradation and ensure proper current carrying capability, the metal lines must have a sufficient width.

6(b). Spacing Between Power and Ground Rails: Ensures that the distance between the power (VDD) and ground (VSS) rails is sufficient to prevent power grid-related failures, such as voltage droop or crosstalk.

Key DRC Violations:
Short Circuits: Occur when wires or metal layers are too close, resulting in unintended connections between signals, which can lead to malfunction.

Open Circuits: Happen when there is insufficient connection between components, causing certain parts of the circuit to remain disconnected.

Metal Overlaps: These occur when metal layers intersect inappropriately or extend too far, leading to potential shorts or manufacturing errors.

Under/Over-Sized Vias: If vias are too small, they cannot carry sufficient current, while oversized vias can cause unnecessary capacitance and delays.

PDN Generation-

In OpenLANE flow, Power Distribution Network(PDN) is crucial as it helps the chip have proper power delivery to all cells within the chip.

To execute PDN Generation, we have to use the following commands:

We should do the whole process till run_cts.

gen_pdn






















































