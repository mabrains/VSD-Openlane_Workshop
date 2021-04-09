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
> - The last part was to get familiar practically with the EDA tools and synthesize picorv32 and read the reports. 

### Commands Used:
> - Flow.tcl -interactive
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


## 2nd day:

### Firstly:
> - Theoritically, It was a revision on some basic concepts:
Utilization Factor 
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

