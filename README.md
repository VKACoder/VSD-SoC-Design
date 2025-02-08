This repository culminates all my learning from the course "Digital VLSI SoC Design and Planning" offered by VLSI System Design (VSD).
---------------------------------------------------------------------------------------------------------------------------------------
The course is about introducing to open source EDA tools (openLANE flow), and Skywater 130nm open pdk and it also includes floorplanning, standard cell design, pre-layout timing analysis and CTS.

---------------------------------------------------------------------------------------------------------------------------------------
**DAY 1:
INCEPTION OF OPEN SOURCE EDA, OPENLANE, AND SKY130 PDK**

The day started with the introduction to RISC-V ISA, openLANE and concluded with synthesizing the PICORV32 design and analysis the results and reports.

**1. First, what is a RISC-V ISA:**
  An ISA descirbes the the set of instructions that the processor can execute, supported registers and data type. It is basically the programmer's manual as it is used by compiler designers and assembly language programmers.
  Now there are a sequence of steps followed to produce the final instruction for a particular application (Firefox) to run as shown in fig 1.1.1.
  
  ![image](https://github.com/user-attachments/assets/88630de8-490a-419a-9600-cfb59c02ac60)
                                                                                Fig 1.1.1: From software application to hardware - steps

**2. OpenLANE:**
   OpenLANE is actually a flow rather than tool and it includes all EDA tools such as:
     a. yosys & abc: For netlist generation,
     b. openSTA: For Static Timing Analysis,
     c. Fault: Design for Testability,
     d. openROAD: For floorplanning, placement, CTS, optimization and global routing,
     e. magic & netgen: For DRC (Design Rule Check) & LVS (Layout Vs. Schematic) and gds2 streaming.
  It uses Skywater 130nm open pdk. PDK stands for Process Design Kit, which is a collection of files used to model a fabrication process for the EDA tools used to design an IC. It include design rules (DRC, LVS, PEX), Standard Cells, etc..

  ![Screenshot from 2025-02-08 18-07-32](https://github.com/user-attachments/assets/2ff45b3d-e852-4c0c-b529-fb11cb4ef975)
                                                                                          Fig 1.2.1: OpenLANE ASIC flow

**3. OpenLANE setup:**
#TODO
