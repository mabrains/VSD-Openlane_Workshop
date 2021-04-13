# VSD-Openlane_Workshop

## 1st day:

>### It was an introduction to:

### Firstly:
> - The flow from the Software Applications to Hardware and some basic terminologies.
###  Secondly:
> - A brief explanation to all components of openlane.
> - A simplified explanation for RTL2GDS flow.
> - Strive Family SoCs by Dr. Mohamed Shaalan.
###  Thirdly:
> - The last part was to get familiar practically with the EDA tools and synthesize picorv32a and read the reports. 

### Commands Used:
> - Flow.tcl -interactive
> - package require openlane 0.9
> - Prep -design picorv32
> - run_synthesis

To open openlane in an the interactive mode ***flow.tcl -interactive*** :

![Screenshot from 2021-04-07 11-10-47](https://user-images.githubusercontent.com/36249257/113893460-57aa5980-97c7-11eb-8edb-4734cc9b4d3d.png)

Some Dependincies: 

![Screenshot from 2021-04-07 11-11-17](https://user-images.githubusercontent.com/36249257/113894802-a5739180-97c8-11eb-9779-f4d542351637.png)

For design prepration and setup, ***prep -design picorv32*** :

![Screenshot from 2021-04-07 11-12-18](https://user-images.githubusercontent.com/36249257/113894844-ae646300-97c8-11eb-9d57-ac2d92482daa.png)

Running Synthesis: run_synthesis

![Screenshot from 2021-04-08 15-06-35](https://user-images.githubusercontent.com/36249257/114031898-1a53d380-987c-11eb-9810-9fc1b16a186e.png)

### A Brief about the ASIC Flow: 
> - 1- Floor Planning: In chip floorplanning Firstly; we need to determine the core area, the die area and the margin between them which is supposed to be placed in it the inputus, outputs and power pads.
Then we need to make partitons for whatever Macros and IPs we have to place on our chip.
In floor planning stage, Macros, tap cells and decapping cells have to be placed.
Macros & Ips have a user-defined locations and hence are placed on the chip before automated placement engine is called.
Also in floorplanning, if you open your layout you'll find even your cells are preplaced in the bottom of your design waiting for the placement stage.

![Screenshot from 2021-04-12 23-42-40](https://user-images.githubusercontent.com/36249257/114466528-e4e71700-9be8-11eb-859f-708208906e59.png)



> - 2- Power Planning: In power planning; we determine the power ring, power rails, number of power straps and our power pads.
The power distribution network is done in this way to decrease the resistance hence, decrease the IR drop and to address the electromigration problem.
Conceptually this is done to support every cell in the design with the amount of power it needs to operate at certain region, in order not to lose it's functionality and to operate in it's defined and specified regions not in the undefined region.

![Screenshot from 2021-04-12 23-54-37](https://user-images.githubusercontent.com/36249257/114467621-799e4480-9bea-11eb-8752-f3e1b88435c3.png)

> - 3-Placement: placement stage usually done in two steps; global placement followed by detailed placement.
Placement Optimization, is the stage where we estimate wire length and capacitance, based on this we insert repeaters(buffers).
> - 4-Clock Tree Synthesis-CTS-: This stage creates a clock distribution network to provide clock for all the sequential elements in the design with minimum skew(hard to achieve).
Usually for sensitive signals as clock and power distribution network we specify the higher metal layers for them, where the metal layers of higher thichkness consequently low IR drop. 
> - 4-Routing: Routing is usually done in two stages, global routing, where our route engine provides a routing guides followed by detailed routing.
The routing strategy between our blocks prefers the routes that provide the minimum number of wires' bends for low resistance values for the wires, hence low delay for the signals.
> - Lastly the physical verification step, where which we need to check that our design meet certain rules.
Checks we need to make: Design Rule Check-DRC- , Layout vs Schematic-LVS- , Timing Verification by a Static Timing Analysis Engine-STA-.

### Skywater supports:
> - hd: High Density Library
> - hdll: High Density Low Leakage Library
> - hvl: High Voltage Library
> - hs: High Speed Library
> - ms: Medium Speed Library
> - lp: Low Power Library

Those Libraries are offered at only three corners: Slow, Fast and Typical

## 2nd day:

### Firstly:
> - Theoritically, It was a revision on some basic concepts:
Utilization Factor= Area occupied by the netlist/ The total core area
Aspect Ratio= Height/ Width
Concept of Pre-Placed Cells(ex.:decoupling cells, tap-cells, macros) 
Why we use decoupling cells & tap cells?
Power Planning(Why it takes this structure? power straps and power ring)
Ground Bouncing & Voltage Drop
Pin Placement
Clock Pads and their big sizes(As they are a sensitive signals and their pad resistance has to be a very small value)
Cell Placement Blockage
For Printing an environmental variables "echo $env(CLOCK_PERIOD)"
For setting the environmental variable "set env(CLOCK_PERIOD) 15.00
###  Secondly:
> - Browsing in some important directories:
openlane/configuration/README: There you'll find the environmental variables and all the commands needed for completing the whole flow
Scripts/floorplan.tcl,
logs/floorplan/ioplacer.log
floorplan.def
###  Thirdly:
> - Cell Design Flow
Inputs:
PDKs: DRC, LVS, SPICE Models
Library & User defined specifications:
Cell’s height, Cell’s width, Supply Voltage, Pin Location  
Design Steps: 
Circuit Design
Layout Design
Characterization (Timing, Noise, Power)
Outputs(Written in CDL(Circuit Design Language) 

### Commands Used:
> - run_floorplan
> - run_placement
> - For opening magic: we need the tech file, the def file specific for the stage we’re in and the lef file:
magic  -T   xxx/pdks/sky130A/libs.tech/magic/sky130A.tech lef read xxx/designs/design_name/runs/tag_name/tmp/merged.lef def read xxx/designs/design_name/runs/tag_name/results/floorplan.def

For floorplanning: run_floorplan

![Screenshot from 2021-04-08 15-08-32](https://user-images.githubusercontent.com/36249257/114032156-55560700-987c-11eb-8e9b-c0714521f2f6.png)

For opening magic: magic  -T   xxx/pdks/sky130A/libs.tech/magic/sky130A.tech lef read xxx/designs/design_name/runs/tag_name/tmp/merged.lef def read xxx/designs/design_name/runs/tag_name/results/floorplan.def

![Screenshot from 2021-04-08 15-11-26](https://user-images.githubusercontent.com/36249257/114032549-b41b8080-987c-11eb-8432-7e789160b138.png)

The layout after floor_planning stage:

![Screenshot from 2021-04-08 15-01-34](https://user-images.githubusercontent.com/36249257/114032213-643cb980-987c-11eb-9b16-5166fef96729.png)

Tap_Cells:

![Screenshot from 2021-04-08 14-55-59](https://user-images.githubusercontent.com/36249257/114032269-7159a880-987c-11eb-8e29-c7c181f293b6.png)

Decapping_Cells:

![Screenshot from 2021-04-08 14-43-51](https://user-images.githubusercontent.com/36249257/114032312-7d456a80-987c-11eb-9d54-70b677e06c00.png)

For Placement: run_placement

![Screenshot from 2021-04-08 16-25-25](https://user-images.githubusercontent.com/36249257/114043988-12e5f780-9887-11eb-9e87-529e5272c39f.png)

The layout after placement stage:

![Screenshot from 2021-04-08 16-32-19](https://user-images.githubusercontent.com/36249257/114045085-0ca44b00-9888-11eb-8306-85822edc43b8.png)

### Decoupling Cells:
Conceptually; the problem occurs when we have a high resistance paths, there we find our loads or cells are not supported with the sufficient power they needed to operate correctly.
Imagine the load or cells are capacitances, in circuit switching from low to high for example, if the load or cells are not supported with the voltage required to charge the capacitor cells then the following load or cells or circuit will not deatermine this switching activity from 0 to 1 hence the functionality of the whole circuit will highly be affected.
For any signal to be considered as logic 0 or logic 1, it should be placed in NML(Noise Margin Low) or NMH(Noise Margin High) respictively.
The solution is to place a decoupling cell in parallel to our load or cells.
The decoupling cells are precharged to charge our loaad or cells by the sufficient amount of voltage needed for them to operate correctly.
As the name tells these cells decouple the our logic from the whole circuit.
Everytime the circuit switches, it draws current from the pre-charged parallel capacitor that we had placed.
We can't use them in all of our design, as they consume large amount of space.

### Ground Bouncing:
When switching from logic 1 to logic 0, this means all the capacitors that were charged to V volts will have to discharge to 0 volts through a single ground.
This will cause a bump in the ground point.

### Voltage Drop:
When switching from logic 0 to logic 1, this means all the capacitors will charge from 0 V to V volts from Vdd tap point.
This will cause lowering of voltage at Vdd tap point.

### The solution for Voltage Drop & The Ground Bouncing:
Simply is to support multiple Vdd & multiple ground.
This is the reason behind the importance of making an excellent power distribution network in our designs.

### Signal Integrity:
The signal propgates through our whole design through wires that can be represented by R-C circuit.
This results in a drop in our signal's voltage.
This drop may make the consequtive cell reads the signal's value incorrectly, and this will consequently affects our whole design's functionality.
So, the placement engine estimate the wire's RC values and based on this, the placement engine place repeaters or buffers to maintain the value of the signal.

![Screenshot from 2021-04-13 00-37-40](https://user-images.githubusercontent.com/36249257/114471203-80c85100-9bf0-11eb-9fc5-fce3829c2e5d.png)


# 3rd day:

### Firstly:
> - Writing a spice netlist for a CMOS inverter, by describing it's component connectivity, component values, identify nodes and naming them.
> - varying in (Wp/ Lp) and tracking the switching threshold voltage and tr(rising time), tf(falling time) following this variation.
###  Secondly:
> - git clone https://github.com/nickson-jose/vsdstdcelldesign
> - cd vsdstd_cell
> - cp sky130A.tech vsdstdceldesign
> - magic -T sky130A.tech sky130_inv.mag
> - Here we clone a CMOS layout and copy the technology file in order to be able to open it on magic
###  Thirdly:
> - Theoritically we were introduced to the CMOS fabrication process
> - 1- Selecting a substrate
> - 2- Create active region for transistor 
> - 3- N-well & P-well formation
> - 4- Gate formation
> - 5- LDD(Lightly Doped Drain) formation
> - 6- Source & Drain formation
> - 7- Steps to form contacts & local interconnects
> - 8- Higher level metal formation 
### Fourthly:
> - we extract the parasitics of the fabricated CMOS inverter on magic: extract all
> - To create a spice netlist that include the parasitics: ext2spice cthresh 0 rthresh 0
> - ext2spice
> - This will create the spice netlist needed to be plugged into ngspice to perform simulations on to get important parameters for our design 
> - Importing to ngspice done by: ngspice sky130_inv.spice
> - The parameters needed to be calculated: tr(rising time), tf(falling time) , tp(propgation delay)= tpHL(propgation delay from high to low) + tpLH(propgation delay from low to high)
### Commands Used:
> - extract all (used on magic for parasitic extraction)
> - ext2spice cthresh 0 rthresh 0 (for spice netlist generation)
> - ex2spice (for spice netlist file writing)
> - ngspice sky130_inv.spice

magic -T sky130A.tech sky130_inv.mag:

![Screenshot from 2021-04-09 20-38-58](https://user-images.githubusercontent.com/36249257/114244385-a524f300-998e-11eb-94f7-14a70d6ee43b.png)

NMOS Transistor: press 's' , write 'what' on magic terminal: 

![Screenshot from 2021-04-09 23-01-17](https://user-images.githubusercontent.com/36249257/114244407-ae15c480-998e-11eb-8b7a-9c33fea0a92f.png)

PMOS Transistor: press 's' , write 'what' on magic terminal: 

![Screenshot from 2021-04-09 23-04-30](https://user-images.githubusercontent.com/36249257/114244420-b7069600-998e-11eb-9288-39b21ee7a1e2.png)

Press double 's' , for getting the connected parts:

![Screenshot from 2021-04-09 23-05-50](https://user-images.githubusercontent.com/36249257/114244446-bec63a80-998e-11eb-9c2d-8ae1cf745cf1.png)

sky130_inv.ext file generation:

![Screenshot from 2021-04-09 23-36-57](https://user-images.githubusercontent.com/36249257/114244465-cbe32980-998e-11eb-8c51-4bf7263abad4.png)

sky130_inv.spice file generation:
![Screenshot from 2021-04-10 00-58-26](https://user-images.githubusercontent.com/36249257/114266424-9a05ad80-99f6-11eb-8034-050015d528d2.png)

sky130_inv.spice generated

![Screenshot from 2021-04-10 12-34-21](https://user-images.githubusercontent.com/36249257/114266900-49dc1a80-99f9-11eb-922b-518a374086f5.png)

To plug the spice netlist generated by magic into ngspice:

![Screenshot from 2021-04-10 12-34-49](https://user-images.githubusercontent.com/36249257/114266925-6ed08d80-99f9-11eb-93b2-92c3cadfd4c9.png)

![Screenshot from 2021-04-10 12-35-18](https://user-images.githubusercontent.com/36249257/114266931-76903200-99f9-11eb-96d7-90e93f3c2413.png)

plot y vs time a
![Screenshot from 2021-04-10 01-50-43](https://user-images.githubusercontent.com/36249257/114267712-91fd3c00-99fd-11eb-82a3-ebc876dacb71.png)

20% of the maximum output value at the output rising edge:
![Screenshot from 2021-04-10 13-04-37](https://user-images.githubusercontent.com/36249257/114267781-00da9500-99fe-11eb-94ff-1074cc3352a5.png)

look at the terminal window:

![Screenshot from 2021-04-10 13-00-25](https://user-images.githubusercontent.com/36249257/114267783-0cc65700-99fe-11eb-8d99-af645877e4e2.png)

80% of the maximum output value at the output rising edge & by looking at the terminal window:

![Screenshot from 2021-04-10 13-04-37](https://user-images.githubusercontent.com/36249257/114267829-4d25d500-99fe-11eb-8278-db3afeb40b16.png)

> - from the previous two values we can calculate tr(rising time): 6.24547 - 6.18169= 0.06378ns 
> - And by the same criteria we can calculate tf(falling time)
> - And the prpgation delay which is defined as (the time taken by the output to reach 50% of its maximum value - the time taken b y the input to reach it's maximum value) 



# 4th day:

### Firstly:
> - Timing Modeling Using Delay Tables, as the delay is function of (input transition and output load capacitance)
> - Every cell with certain functionallity with a certain size has it's own lookup table where we can extract it's cell delay.
> - If the value we're searching is not found but lies within the table's values, we calculate it using interpolation.
> - If the value we're searching is not found and lies outside the table's values, we calculate it using extrapolation.
###  Secondly:
> - Setup Timing Analysis(STA)
> - The setup time is the delay time of the launch flip-flop
###  Thirdly:
> - Clock Tree Synthesis(CTS) and Signal Integrity
> - Buffering usng H-Tree algorithm
> - Clock Shielding and Crosstalk 
### Fourthly:
> - Hold Timing Analysis
### Commands Used:
> - run_cts

Conditions for our CMOS layout:
> - The input and output ports or pins must lie on the intersection of the horizontal and vertical tracks.
> - The hieght and width parameters should be multiples of the track pitch
On magic:
press g on magic's terminal window
grid [x-spacing] [y-spacing] [x-origin] [y-origin]
This information: x-spacing, y-spacing, [x-origin]  and [y-origin], you can find it under the pdks directory: pdks/sky130A/libs.tech/openlane/sky130_fd_sc_hd >>v i tracks          ...to be edited
Also we've to define pins names:
in magic:
selact a certain pin: press 's'
edit>>text>> Text string A
             Size(um) 0.15
             enable 0 
Also for every pin we have to defins it's class(input or output and it's use)
on magic's terminal window:
port class input
port use signal 
save file_name.mag
lef write sky130_vsdinv.lef
![Screenshot from 2021-04-10 19-25-52](https://user-images.githubusercontent.com/36249257/114290104-55712500-9a7d-11eb-9bc6-a2476533f7df.png)

![Screenshot from 2021-04-10 19-27-20](https://user-images.githubusercontent.com/36249257/114290113-66219b00-9a7d-11eb-9dc2-1098de386aad.png)

![Screenshot from 2021-04-10 20-09-54](https://user-images.githubusercontent.com/36249257/114290124-789bd480-9a7d-11eb-83c2-ac6e34518db6.png)


![Screenshot from 2021-04-10 20-10-51](https://user-images.githubusercontent.com/36249257/114290127-7df91f00-9a7d-11eb-87b2-d2dc35ff3496.png)


![Screenshot from 2021-04-10 20-18-19](https://user-images.githubusercontent.com/36249257/114290131-86e9f080-9a7d-11eb-85f8-a055d4fb31fe.png)

Negative sLack!!
i.e. This happens after adding the CMOS inverter


![Screenshot from 2021-04-10 21-37-02](https://user-images.githubusercontent.com/36249257/114290164-c6b0d800-9a7d-11eb-8bc9-713db6f92267.png)

![Screenshot from 2021-04-10 21-37-44](https://user-images.githubusercontent.com/36249257/114290169-d2040380-9a7d-11eb-9a13-fb9703233552.png)

![Screenshot from 2021-04-10 21-47-10](https://user-images.githubusercontent.com/36249257/114290179-e21be300-9a7d-11eb-8408-87e75b88326e.png)

![Screenshot from 2021-04-10 21-41-50](https://user-images.githubusercontent.com/36249257/114290173-d92b1180-9a7d-11eb-9d8a-c8166b7f0dd5.png)

![Screenshot from 2021-04-10 21-49-16](https://user-images.githubusercontent.com/36249257/114290194-01b30b80-9a7e-11eb-85b0-6214858456b0.png)

![Screenshot from 2021-04-10 21-55-44](https://user-images.githubusercontent.com/36249257/114290200-0c6da080-9a7e-11eb-9dcd-9112470d76ec.png)

![Screenshot from 2021-04-10 23-57-17](https://user-images.githubusercontent.com/36249257/114290211-198a8f80-9a7e-11eb-8097-d3438a933cc2.png)

![Screenshot from 2021-04-11 03-37-34](https://user-images.githubusercontent.com/36249257/114290228-3aeb7b80-9a7e-11eb-9287-517a108d0bfe.png)

### Static Timing Analysis-STA:

![Screenshot from 2021-04-13 01-39-05](https://user-images.githubusercontent.com/36249257/114475791-3ac3bb00-9bf9-11eb-8322-3d8159c75ae5.png)

As the previous figure shows:
This is the internal structure of the flip flop:
When the clock is high '1', the first mux reads the input 'D' and the second mux retains it's it's previous value.
when the clock turns low '0', the first mux retains it's previos value while the second mux reads the output of the first mux.
The time taken by the first mux to propgate the input inside it's logic is called the setup time.
The time taken by the second mux to read the value of the first mux and propgate it to it's output is called the hold time.

![Screenshot from 2021-04-13 01-54-36](https://user-images.githubusercontent.com/36249257/114476824-44e6b900-9bfb-11eb-8d4a-cc595f9aa86e.png)

This figure shows the setup anlaysis or the maximum delay anlysis

![Screenshot from 2021-04-13 02-00-14](https://user-images.githubusercontent.com/36249257/114477158-056c9c80-9bfc-11eb-88e7-e2f9da8d1b37.png)

This figure shows the hold anlaysis or the minimum delay anlysis
