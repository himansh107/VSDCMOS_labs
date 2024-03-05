# VSDCMOS_labs
this repository consists of labs done in ngspice 

**File descriptions :**
- sky130.lib.spice file contains all the include commands for including the libraries for nfet and pfet <br>
  ![](cmos_circuit.png)
- The design folder in the lab repository contains the two folders : "cells" and "models"
- The "cells" folder contains library files for nfet and pfet. The library files for different corners for a nfet is shown below <br>
  [image of nfet corner files]
    - contents of a spice library file for a tt nfet is shown below. It contains different parameters for describing the nfet. <br>
      [image]
- The models folder contains the sky130.lib.spice (explaine above).

## Lab 1 - nfet characteristics 

Plotting the graph between Ids and Vds we need to write the following SPICE code: <br>
```bash
  *Model Description
.param temp=27

*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt

*Netlist Description

XM1 Vdd n1 0 0 sky130_fd_pr__nfet_01v8 w=0.39 l=0.15
R1 n1 in 55

Vdd vdd 0 1.8V
Vin in 0 1.8V

*simulation commands

.op
.dc Vdd 0 1.8 0.1 Vin 0 1.8 0.2

.control

run
display
setplot dc1
.endc

.end
```
[image for launching and plotting ngspice] <br><br>

 The snap shot of plot between Ids and Vds:<br> 
 [image for lab1 plot] <br>

 - To observe any point on the graph, left click on the point
 - The corresponding (x,y) values would be reflected in the terminal
 - The peak current was found out to be 210 micro Ampere.

   
 
 ## Lab 2 - nfet characteristics for lower nodes

 For plotting the graph between Ids and Vds for short channel devices we need to write the following SPICE code:
```bash
*Model Description
.param temp=27

*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt

*Netlist Description

XM1 Vdd n1 0 0 sky130_fd_pr__nfet_01v8 w=0.39 l=0.15
R1 n1 in 55

Vdd vdd 0 1.8V
Vin in 0 1.8V

*simulation commands

.op
.dc Vdd 0 1.8 0.1 Vin 0 1.8 0.2

.control

run
display
setplot dc1
.endc

.end
```
<br>

The snap shot of plot between Ids and Vds for lower nodes: <br> 
[image] <br>

The plot for Id vs Vgs for Vds = 1.8 V at lower nodes is shown below: <br>
[image]

- this graph is usually quadratic but we see that it becomes linear for lower nodes.
- This linearization of Id vs Vgs curve is due to **velocity saturation** and this is one of the effects under **short channel effect**.
- The threshold voltage is the voltage at which the drain current shoots up exponentially
- Move the cursor along the linear part of the graph and keep moving linearly till you cut the x axis. That will give Vt

### Effect of velocity saturation in Lower nodes vs Higher nodes
[image] <br>

In velocity saturation the current Id saturates early. As a result peak current for same W/L ratio decreases. 

## Lab 3 - Voltage transfer characteristics of a CMOS

To plot the VTC for a CMOS we need the following code:

```bash
*Model Description
.param temp=27

*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt

*Netlist Description

XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=0.84 l=0.15
XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.36 l=0.15

Cload out 0 50fF

Vdd vdd 0 1.8V
Vin in 0 1.8V

*simulation commands

.op

.dc Vin 0 1.8 0.01

.control
run
setplot dc1
display
.endc

.end
```
[image of ngspice opening] <br>

### Switching threshold of CMOS

- Switching threshold is a voltage at which the device switches.
- At switching threshold Vin = Vout.
- To calculate the switching threshold of CMOS. We zoomed in the exact middle of the metastability region of the VTC <br>

[image]

### Transient analysis of CMOS <br>

The following code was needed for transient analysis <br> 

[image]

The snapshot of the graph of transient analysis is found as below <br>

[image]

- Rise delay = time lag between 50% of output rise and 50% of input fall.
- From the graph the following points were noted for rise delay <br>
[image of rise delay] <br>

Rise delay = 2.48 - 2.15 = 0.33ns <br>

- Fall delay = time lag between 50% of output fall and 50% of input rise.
[image of fall delay] <br>

Fall delay = 4.33 - 4.04 = 0.29ns <br>

## Lab 4 - Noise margin of CMOS

- Noise margin means the tolerance of a cmos circuit for logic 1 or logic 0 <br>
  [image of noise margin] <br>

The transfer characteristics from which noise margin is calculated is given below: <br>
 [image of vtc]

 The plot values for noise margin calculation: <br>
  [image of plot values] <br>

  Method to calculate noise margin: <br>

 - Noise margin high = Voh - Vih = 1.689 - 0.970 = 0.7184
 - Noise margin low = Vil - Vol = 0.7836 - 0.1253 = 0.658.
   




