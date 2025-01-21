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








