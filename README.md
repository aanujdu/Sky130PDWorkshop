# Advanced Physical Design using OpenLANE/Sky130
![image](https://user-images.githubusercontent.com/37201355/139192423-67926cc7-0039-4c41-b41f-f6b45ff19408.png)

## Introduction
Manufacturing an ASIC is an sophisticated process involving multiple steps. First, we write the design specification using a hardware description language (HDL) such as Verilog or VHDL. The written code is commonly also called register transfer language (RTL). Next, the RTL is synthesized into a netlist; netlist should be functionally equivalent to RTL with the only difference that it only uses standard cell instantiations.
TODO

The aim of this workshop is to familiarize the participants with the OpenLANE flow. OpenLANE is a flow that can be used to generate the GDSII file from any given RTL using only open source tools. 

## Day 1
The first set of videos called "How to talk to computers" discussed three topics. First, how does a die look like and its various components. 
![image](https://user-images.githubusercontent.com/37201355/139192837-43934b63-eb5e-4236-b9ca-2e231c73ada9.png)

Second, a brief introduction of the RISC V instruction set architecture and an implementation called picorv32. Third, how do applications actually make the hardware run, i.e., the compilation, assembly and eventual generation of the executable.
![image](https://user-images.githubusercontent.com/37201355/139193051-fd9c6ba5-2f1c-4aed-8e31-cd84a5abafd0.png)

Second set of videos discussed the details of a typical RTL2GDSII flow and how it is mapped in the OpenLANE flow. 
![image](https://user-images.githubusercontent.com/37201355/139193300-874e10d5-83aa-4ee4-948b-c1e72df44def.png)
![image](https://user-images.githubusercontent.com/37201355/139193527-38f3222b-25f2-4e93-9234-201a82b80680.png)

Third set of videos described the directory structure and the commands to invoke the OpenLANE tool and synthesis our first design called picorv32.

## Day 2
## Day 3
## Day 4
## Day 5
