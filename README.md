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
  Starting the openLANE environment is simple. Just go to the respective directory, which is work/tools/openlane_working_dir/openlane in my case and run docker by just typing "docker". To run the flow execute flow.tcl with interactive switch (Fig 1.3.1).

  ![Screenshot from 2025-02-08 22-04-36](https://github.com/user-attachments/assets/5f6a293e-c4c5-4ac8-8db5-2d3ab69a6300)
  Fig 1.3.1: Starting openLANE environment.

Just as starting the environment is simple, so is preparing the design -> "prep -design picorv32a", where picorv32a is te design that we want to prepare to synthesize (Fig 1.3.2)!
The picorv32a directory consists of the source file (verilog) and config.tcl. The config.tcl file consist of clock period which overrides the default clock period (Fig. 1.3.3).
  
  ![design](https://github.com/user-attachments/assets/30df520c-6779-4d79-8ed5-5e8325b3f0ed)
  Fig 1.3.2: Preparing the picorv32a design.

  ![config](https://github.com/user-attachments/assets/50b1f01f-0471-43a7-915f-bb87f81cd57e)
  Fig 1.3.3: config.tcl file with clock period = 5ns.

To synthesize the design, type "run_synthesis". It may take 2-3 minutes to complete the synthesis. 

  ![syn_success](https://github.com/user-attachments/assets/5fc19ebd-10bc-40ad-8d16-975cbd98cc1d)
  Fig 1.3.4: Synthesis completed.

To view the results and reports of the synthesis, direct to work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/<date_time>/ (Fig 1.3.5).

  ![runs](https://github.com/user-attachments/assets/803dca51-0e5a-4748-94cc-de4f7e3e600c)
  Fig 1.3.5: 'Runs' directory to view the results and reports.

  To view the yosys report, navigate to reports/synthesis/ directory, and open "1-yosys_4.stat.rpt" as shown in Fig 1.3.6. It will include the no. of cells, D-Flip flops, etc. used (Fig 1.3.7).

  ![rep](https://github.com/user-attachments/assets/a2aa58ef-af8f-4361-bd2f-73b22e78d908)
  Fig 1.3.6: Reports directory.
  
  ![syn_stat](https://github.com/user-attachments/assets/a2b44492-b157-44cf-9d6e-a9fcec64efb8)
  Fig 1.3.7: Yosys synthesis report.

  From Fig 1.3.7, it can be inferred that the flip flop ratio which is defined as the ratio of no. of flip flops/total no. of cells, is 0.1084 or 10.84% (1613/14876).

--------------------------------------------------------------------------------------------------------------------------------------------------
