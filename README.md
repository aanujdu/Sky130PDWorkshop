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

Third set of videos described the directory structure and the commands to invoke the OpenLANE tool and synthesis our first design called picorv32. The working directory contains two folders named openlane and pdks. We will be invoking the openLANE flow from the openlane directory. pdks folder as the name suggests contains the PDK files that are used by the openLANE tool during the various steps of the backend flow.

The subdirectory designs contains all the RTL design and the respective configuration files for each design. Following is the hierarchy for the picorv32a design:

 |-sky130A_sky130_fd_sc_ls_config.tcl
 |-sky130A_sky130_fd_sc_hdll_config.tcl
 |-src
 | |-picorv32a.sdc
 | |-picorv32a.v
 |-config.tcl
 |-sky130A_sky130_fd_sc_ms_config.tcl
 |-runs
 | |-27-10_07-14
 | | |-logs
 | | | |-cts
 | | | |-klayout
 | | | |-synthesis
 | | | | |-2-opensta
 | | | | |-1-yosys.log
 | | | | |-1-yosys_runtime.txt
 | | | | |-2-opensta_runtime.txt
 | | | |-magic
 | | | |-lvs
 | | | |-flow_summary.log
 | | | |-cvc
 | | | |-0-prep_runtime.txt
 | | | |-placement
 | | | |-routing
 | | | |-floorplan
 | | |-results
 | | | |-cts
 | | | | |-merged_unpadded.lef
 | | | |-klayout
 | | | | |-merged_unpadded.lef
 | | | |-synthesis
 | | | | |-merged_unpadded.lef
 | | | | |-picorv32a.synthesis.v
 | | | |-magic
 | | | | |-merged_unpadded.lef
 | | | |-lvs
 | | | | |-merged_unpadded.lef
 | | | |-cvc
 | | | | |-merged_unpadded.lef
 | | | |-placement
 | | | | |-merged_unpadded.lef
 | | | |-routing
 | | | | |-merged_unpadded.lef
 | | | |-floorplan
 | | | | |-merged_unpadded.lef
 | | |-config.tcl
 | | |-PDK_SOURCES
 | | |-tmp
 | | | |-cts
 | | | | |-merged_unpadded.lef
 | | | |-trimmed.lib.exclude.list
 | | | |-klayout
 | | | | |-merged_unpadded.lef
 | | | |-synthesis
 | | | | |-yosys.sdc
 | | | | |-hierarchy.dot
 | | | | |-merged_unpadded.lef
 | | | |-magic
 | | | | |-merged_unpadded.lef
 | | | |-lvs
 | | | | |-merged_unpadded.lef
 | | | |-merged_unpadded.lef
 | | | |-met_layers_list.txt
 | | | |-trimmed.lib
 | | | |-cvc
 | | | | |-merged_unpadded.lef
 | | | |-tracks_copy.info
 | | | |-sky130_fd_sc_hd__tt_025C_1v80.no_pg.lib
 | | | |-placement
 | | | | |-merged_unpadded.lef
 | | | |-merged.lef
 | | | |-routing
 | | | | |-merged_unpadded.lef
 | | | |-floorplan
 | | | | |-merged_unpadded.lef
 | | |-cmds.log
 | | |-OPENLANE_VERSION
 | | |-reports
 | | | |-cts
 | | | |-klayout
 | | | |-synthesis
 | | | | |-2-opensta_tns.rpt
 | | | | |-1-yosys_pre.stat
 | | | | |-1-yosys_4.chk.rpt
 | | | | |-2-opensta.rpt
 | | | | |-1-yosys_4.stat.rpt
 | | | | |-2-opensta_wns.rpt
 | | | | |-2-opensta.min_max.rpt
 | | | | |-2-opensta.timing.rpt
 | | | | |-2-opensta.slew.rpt
 | | | | |-1-yosys_dff.stat
 | | | |-magic
 | | | |-lvs
 | | | |-cvc
 | | | |-placement
 | | | |-routing
 | | | |-floorplan
 |-sky130A_sky130_fd_sc_hd_config.tcl
 |-sky130A_sky130_fd_sc_hs_config.tcl

For now, the important items in this list are the runs directory, the src directory and the \*.tcl files. src contains the sdc and verilog code. runs directory contains the configuration and reports of the various steps executed during the backend flow such as synthesis, STA, floorplanning, etc. The .tcl files set various variables such as the clock frequency, RTL location, core utilization, etc. The precedence is *sky130A_sky130_fd_sc_hd_config.tcl* > *config.tcl*.

Run the following commands to start the openLANE flow:
`docker run -it -v $(pwd):/openLANE-flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) openlane:rc2`

This invokes the docker where we shall execute the openLANE flow.

## Day 2
## Day 3
## Day 4
## Day 5
