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
FLOORPLAN:
![fp-10-2-files](https://github.com/user-attachments/assets/0dcdbc16-2eb6-4d14-9a19-c124ff205b9e)
![fparea](https://github.com/user-attachments/assets/73d49b29-a55f-4954-9bc6-dc1a19424408)
![fp-def](https://github.com/user-attachments/assets/c7daa9de-57fa-4eb6-94ce-71be43cacd78)
![fplog](https://github.com/user-attachments/assets/ef41f7eb-cc1e-40b8-8a59-9a224a1ca361)
![Screenshot from 2025-02-10 15-46-16](https://github.com/user-attachments/assets/919d2a8d-d3d9-4c33-9aea-4fb4b999cd80)
![Screenshot from 2025-02-10 15-48-22](https://github.com/user-attachments/assets/f7b54b93-1331-47b0-9ca9-3b0ef7875285)


PLACEMENT:

![Screenshot from 2025-02-11 10-33-47](https://github.com/user-attachments/assets/b91e0f43-13e8-4959-8382-63e999d942fe)
![Screenshot from 2025-02-11 10-34-17](https://github.com/user-attachments/assets/ab5af6fd-3099-4a20-be64-5347271558b6)
![Screenshot from 2025-02-15 09-38-54](https://github.com/user-attachments/assets/ba047214-cee4-4a3e-b602-85779365f8d2)

CUSTOM CELL - INVERTER:
![Screenshot from 2025-02-11 11-15-53](https://github.com/user-attachments/assets/32fe366b-7d09-4799-88bb-8781e7194d6f)
![Screenshot from 2025-02-13 21-04-13](https://github.com/user-attachments/assets/cf8cb8fc-7151-4e60-abc6-c43cef35953c)

LAYOUT:
![Screenshot from 2025-02-11 11-20-58](https://github.com/user-attachments/assets/22f01e35-9940-44af-912d-8fc2dedb8d54)

![Screenshot from 2025-02-13 20-43-56](https://github.com/user-attachments/assets/f5cfdcf8-8706-4157-9d6b-02b042e5c6d7)
![Screenshot from 2025-02-13 20-47-08](https://github.com/user-attachments/assets/6a1cac40-86b8-4636-b2b0-aa6514e4868f)
![Screenshot from 2025-02-13 20-49-07](https://github.com/user-attachments/assets/aff89e17-4169-4a79-a50d-3c7252c68054)
![Screenshot from 2025-02-13 21-01-19](https://github.com/user-attachments/assets/c8a1543c-abbd-4da8-85a1-b3fd9df8b92e)

![Screenshot from 2025-02-13 21-04-03](https://github.com/user-attachments/assets/9b31de76-4ccb-4b72-812a-52e5e49ccfd1)
![Screenshot from 2025-02-12 18-18-46](https://github.com/user-attachments/assets/bd6c9d4c-b051-4795-93fa-049261036d6d)
![Screenshot from 2025-02-12 20-38-27](https://github.com/user-attachments/assets/21288ea6-47f6-4536-afac-ce1eb69a6724)

![Screenshot from 2025-02-12 20-36-36](https://github.com/user-attachments/assets/e64057f4-817c-40d6-84ba-63c18987d4a6)
![Screenshot from 2025-02-12 20-40-32](https://github.com/user-attachments/assets/78bb0fc1-4bbb-4821-a944-2432acd5479d)
![Screenshot from 2025-02-13 21-06-22](https://github.com/user-attachments/assets/7e72e7d6-d011-4df1-adb6-bf46f52084a1)


![Screenshot from 2025-02-13 21-06-22](https://github.com/user-attachments/assets/0549fed8-e63c-4f66-b5c7-c26b5a6fee78)
SYNTHESIS:
![Screenshot from 2025-02-13 21-33-35](https://github.com/user-attachments/assets/8a3ae0e0-cb87-4255-a8b9-743ee4ae2b86)
TIMING CORRECTION:
![Screenshot from 2025-02-14 22-06-57](https://github.com/user-attachments/assets/833196a0-d434-4a25-a215-a9ca30273542)

FLOORPLAN:
![Screenshot from 2025-02-14 22-08-43](https://github.com/user-attachments/assets/82f4a938-aec3-44fa-b979-967daedc859f)
PLACEMENT:
![Screenshot from 2025-02-14 22-43-55](https://github.com/user-attachments/assets/e96ca97b-9632-461c-b238-79a65a5040b7)
![Screenshot from 2025-02-15 09-45-38](https://github.com/user-attachments/assets/bbd40149-c232-4a54-962b-6c1c3ed9a981)

CTS:
![Screenshot from 2025-02-16 00-15-35](https://github.com/user-attachments/assets/94d57029-f987-4187-9f56-3d95002ba3ec)
![Screenshot from 2025-02-15 23-52-02](https://github.com/user-attachments/assets/e974665d-2c5f-46bb-9cfd-825002f5ae16)

![Screenshot from 2025-02-16 21-26-42](https://github.com/user-attachments/assets/99ab68bc-4d29-4fd3-9753-a1bae3f681df)
![Screenshot from 2025-02-16 21-26-45](https://github.com/user-attachments/assets/f848fc47-af88-41f5-a943-d525b0eb17fd)

PDN:
![Screenshot from 2025-02-16 21-49-08](https://github.com/user-attachments/assets/7ffa6040-3ab0-420d-b7a2-13f5af14ccb3)
![Screenshot from 2025-02-11 10-38-00](https://github.com/user-attachments/assets/ec3e1a49-930a-4fab-9248-477847f01ab3)
![power_routing1](https://github.com/user-attachments/assets/842b9ddf-8d10-4b15-b88f-2d9094e9b2d8)
![Screenshot from 2025-02-16 22-09-12](https://github.com/user-attachments/assets/18ee9b1f-0506-40bc-a6e2-19cde382df40)

ROUTING:





