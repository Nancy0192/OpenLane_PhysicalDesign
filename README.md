# OpenLane_PhysicalDesign

## Day - 1 Inception of Open-Source EDA, OpenLane and Sky130 PDK
<details><summary><strong>Introduction to RISC-V</strong></summary>
RISC-V is an open-source instruction set architecture (ISA) that has gained significant traction in the world of computer architecture. Unlike proprietary ISAs, RISC-V is freely available for anyone to use, modify, and implement, which has led to its rapid adoption and development. The name "RISC" stands for Reduced Instruction Set Computing, highlighting its design philosophy of simplicity and efficiency.

RISC-V's modular and customizable nature makes it a versatile choice for various applications, from embedded systems and Internet of Things (IoT) devices to high-performance computing. Its flexibility allows engineers and organizations to tailor the architecture to their specific requirements, promoting innovation and adaptability.

</details>

<details><summary><strong>SOC Design And OpenLane</strong></summary>

### Components Of Digital Asic Design
Following are the components Of Digital Asic Design:

- EDA Tools: Open-source ASIC design typically relies on Electronic Design Automation (EDA) tools, which include tools for schematic capture, digital logic design, layout design, and simulation. Popular open-source EDA tools include Qflow, Magic, and OpenROAD.
- RTL : RTL IPs offer several advantages. They boost productivity, help bring products to market faster, and make designs more reliable. By using RTL IPs, designers can tap into well-tested and optimized components, reducing the chances of errors. Plus, they promote the reuse of designs, allowing engineers to mix and match different blocks to create more complex systems. In essence, RTL IPs are like a shortcut to building sophisticated digital circuits.
- PDK : An Open Source Process Design Kit (PDK) is a critical component in semiconductor manufacturing, as it provides the necessary information and tools for designing integrated circuits. Open source PDKs are a relatively recent development, aimed at democratizing access to semiconductor manufacturing processes and fostering innovation in chip design.
  <br>
  ![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/177f083b-be1a-4dc4-9350-9c51a36728b6)

  ### Simplified RTL to GSDII Flow
  The flow involves:
  - RTL Design: Create or import the RTL (Register Transfer Level) design for your digital circuit using a hardware description language (HDL) like Verilog or VHDL.
  - Synthesis: Utilize the open-source synthesis tool, Yosys, to convert the RTL code into a gate-level netlist. Yosys performs technology mapping and optimization to generate a logical representation of the design.
  - Floorplanning: OpenLANE performs floorplanning to allocate space for different blocks and components within the chip's layout. This step helps optimize area utilization and manage interconnections.
  - Placement: The next stage is placement, where standard cells are placed in the designated locations on the chip. OpenLANE uses the detailed placement tool RePlAce for this purpose.
  - Clock Tree Synthesis (CTS): OpenLANE includes a CTS tool to create a clock distribution network that minimizes clock skew and ensures synchronous clock signals across the chip.
  - Routing: OpenLANE uses the FastRoute router for global and detailed routing, establishing connections between the placed standard cells and creating the metal interconnects.
  - Sign-Off GDS2: Perform a final sign-off on the GDSII file to confirm that it meets all design and manufacturing requirements. This step ensures that the layout is ready for photomask generation and foundry submission.
  - GDSII Generation: Generate the GDSII file, which contains the final geometric data for all layers of the chip. This file is used in the fabrication process.
  
   ![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/80627ef8-d9e7-4c81-a302-d50df429914c)

  
### OpenLane
OpenLane is a groundbreaking open-source ASIC (Application-Specific Integrated Circuit) design flow that has transformed the landscape of custom chip development. Developed under the aegis of the SkyWater PDK project, sponsored by Google, OpenLane represents a paradigm shift in the world of integrated circuit design. This powerful tool automates and streamlines the entire ASIC design process, from RTL (Register Transfer Level) design to GDSII file generation, making it accessible to a wider audience while significantly reducing design cycle times.

One of OpenLane's key features is its open-source nature, which promotes collaboration and transparency within the hardware design community. It integrates a multitude of open-source Electronic Design Automation (EDA) tools, including synthesis, placement, and routing tools, into a cohesive workflow. This automation not only accelerates chip development but also reduces the likelihood of human errors, ensuring higher-quality designs.

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/27ad2729-f626-4b11-8fe5-28bf8061e0aa)


  
</details>

## Day-2 Good Floorplan vs Bad Floorplan And Introduction To Library Cells

<details><summary><strong>Chi Floor Planning Considerations</strong></summary>

### Utilization Factor
The Utilization Factor in ASIC (Application-Specific Integrated Circuit) design flow is a metric that measures how efficiently the physical area of the chip is being utilized. It represents the ratio of the occupied area (the area filled with logic, standard cells, and other components) to the total available area on the semiconductor core.<br>
Try to set the utilisation factor 0.5 or 0.6 so that there will be space for optimisations, routing, inserting buffers etc.,

### Aspect Ratio
The Aspect Ratio is defined as the ratio of height to the width of the die. If it is '1', it implies that the die is of square shape.

### Pre-placed Cells
Pre-placed cells (or pre-placed blocks) in ASIC (Application-Specific Integrated Circuit) design refer to predefined and fixed blocks of logic or circuitry that are manually placed in specific locations on the semiconductor chip's layout before the automated placement and routing process.<br>
Pre-placed cells are designed with specific functionality in mind and are placed on the chip layout at precise locations. These cells typically perform critical functions that require precise control over their placement and connectivity.

### Decoupling Capacitor 

  
</details>
