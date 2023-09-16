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

<details><summary><strong>Invoking OpenLane And Run Synthesis</strong></summary>

<details><summary>Installation Of Docker</summary>

```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo docker run hello-world

sudo groupadd docker
sudo usermod -aG docker $USER
sudo reboot 


# Check for installation
sudo docker run hello-world
```



</details>
<details><summary>Installation Of OpenLane</summary>

```
cd
git clone https://github.com/The-OpenROAD-Project/OpenLane --recurse-submodules 
cd OpenLane
make
make test
cd /home/kanish/OpenLane/designs/ci
cp -r * ../
```
</details>

<details><summary>Invoking OpenLane</summary>
  
```
cd ~/OpenLane
make mount
```

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/81d0b632-725e-49f0-890a-67d5cf05f65a)

</details>

<details><summary>Running Synthesis</summary>

```
cd ~/OpenLane
make mount
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
```
![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/b03b2fe1-ccd6-4816-91f3-35d85b617881)


To view synthesis report

```
cd OpenLane/designs/picorv32a/runs/RUN_2023.09.12_13.52.53/reports/synthesis/
gedit 1-synthesis_dff.stat 
```

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/e2336b5a-c91c-4f92-a4eb-74c731b4d890)



```
cd OpenLane/designs/picorv32a/runs/RUN_2023.09.12_13.52.53/reports/synthesis/
gedit 1-synthesis.AREA_0.stat.rpt
```

```

61. Printing statistics.

=== picorv32 ===

   Number of wires:               9824
   Number of wire bits:          10206
   Number of public wires:        1512
   Number of public wire bits:    1894
   Number of memories:               0
   Number of memory bits:            0
   Number of processes:              0
   Number of cells:              10104
     sky130_fd_sc_hd__a2111o_2       2
     sky130_fd_sc_hd__a211o_2      101
     sky130_fd_sc_hd__a211oi_2       4
     sky130_fd_sc_hd__a21bo_2       19
     sky130_fd_sc_hd__a21boi_2       7
     sky130_fd_sc_hd__a21o_2       414
     sky130_fd_sc_hd__a21oi_2      127
     sky130_fd_sc_hd__a221o_2       65
     sky130_fd_sc_hd__a221oi_2       1
     sky130_fd_sc_hd__a22o_2       197
     sky130_fd_sc_hd__a22oi_2        2
     sky130_fd_sc_hd__a2bb2o_2      16
     sky130_fd_sc_hd__a311o_2       38
     sky130_fd_sc_hd__a31o_2        90
     sky130_fd_sc_hd__a31oi_2       10
     sky130_fd_sc_hd__a32o_2        89
     sky130_fd_sc_hd__a41o_2         2
     sky130_fd_sc_hd__and2_2       283
     sky130_fd_sc_hd__and2b_2       32
     sky130_fd_sc_hd__and3_2        77
     sky130_fd_sc_hd__and3b_2       76
     sky130_fd_sc_hd__and4_2        46
     sky130_fd_sc_hd__and4b_2        6
     sky130_fd_sc_hd__and4bb_2       3
     sky130_fd_sc_hd__buf_1       2735
     sky130_fd_sc_hd__buf_2         16
     sky130_fd_sc_hd__conb_1       106
     sky130_fd_sc_hd__dfxtp_2     1596
     sky130_fd_sc_hd__inv_2         83
     sky130_fd_sc_hd__mux2_2      1817
     sky130_fd_sc_hd__mux4_2       323
     sky130_fd_sc_hd__nand2_2      250
     sky130_fd_sc_hd__nand2b_2       2
     sky130_fd_sc_hd__nand3_2       18
     sky130_fd_sc_hd__nand3b_2       3
     sky130_fd_sc_hd__nand4_2        2
     sky130_fd_sc_hd__nor2_2       185
     sky130_fd_sc_hd__nor3_2        11
     sky130_fd_sc_hd__nor3b_2        3
     sky130_fd_sc_hd__nor4_2         4
     sky130_fd_sc_hd__nor4b_2        3
     sky130_fd_sc_hd__o2111a_2       1
     sky130_fd_sc_hd__o211a_2      224
     sky130_fd_sc_hd__o211ai_2       6
     sky130_fd_sc_hd__o21a_2       154
     sky130_fd_sc_hd__o21ai_2       94
     sky130_fd_sc_hd__o21ba_2       15
     sky130_fd_sc_hd__o21bai_2       3
     sky130_fd_sc_hd__o221a_2       19
     sky130_fd_sc_hd__o221ai_2       1
     sky130_fd_sc_hd__o22a_2        26
     sky130_fd_sc_hd__o22ai_2        1
     sky130_fd_sc_hd__o2bb2a_2       7
     sky130_fd_sc_hd__o311a_2       31
     sky130_fd_sc_hd__o311ai_2       2
     sky130_fd_sc_hd__o31a_2        21
     sky130_fd_sc_hd__o31ai_2        2
     sky130_fd_sc_hd__o32a_2        14
     sky130_fd_sc_hd__o41a_2         1
     sky130_fd_sc_hd__or2_2        337
     sky130_fd_sc_hd__or2b_2        20
     sky130_fd_sc_hd__or3_2        102
     sky130_fd_sc_hd__or3b_2        17
     sky130_fd_sc_hd__or4_2         29
     sky130_fd_sc_hd__or4b_2         6
     sky130_fd_sc_hd__xnor2_2       78
     sky130_fd_sc_hd__xor2_2        29

   Chip area for module '\picorv32': 102957.494400
```
```
Flop ratio = Number of D Flip flops = 1596  = 0.1579
             ______________________   _____
             Total Number of cells    10104
```






</details>







</details>

## Day-2 Good Floorplan vs Bad Floorplan And Introduction To Library Cells

<details><summary><strong>Chip Floor Planning Considerations</strong></summary>

### Utilization Factor
The Utilization Factor in ASIC (Application-Specific Integrated Circuit) design flow is a metric that measures how efficiently the physical area of the chip is being utilized. It represents the ratio of the occupied area (the area filled with logic, standard cells, and other components) to the total available area on the semiconductor core.<br>
Try to set the utilisation factor 0.5 or 0.6 so that there will be space for optimisations, routing, inserting buffers etc.,

### Aspect Ratio
The Aspect Ratio is defined as the ratio of height to the width of the die. If it is '1', it implies that the die is of square shape.

### Pre-placed Cells
Pre-placed cells (or pre-placed blocks) in ASIC (Application-Specific Integrated Circuit) design refer to predefined and fixed blocks of logic or circuitry that are manually placed in specific locations on the semiconductor chip's layout before the automated placement and routing process.<br>
Pre-placed cells are designed with specific functionality in mind and are placed on the chip layout at precise locations. These cells typically perform critical functions that require precise control over their placement and connectivity.

### Decoupling Capacitor 
Decoupling capacitors help maintain a constant voltage level at the power supply pins of ICs. When an IC switches or draws transient current, the decoupling capacitor supplies the required charge to keep the voltage stable, preventing glitches or erratic behavior.

### Power Planning
Let us suppose that there are multiple macros in a chip and output changes from '1' to '0', then it discharged into ground line because of which we can see ground bumpp. Similarly when it is charged from 0 to 1 we can see voltage droop in power supply.<br>

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/6cc77d51-cb10-42ce-86ce-8e1625fae6c1)

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/f386b46d-c198-4bea-89df-e0b08d91657a)



Hence to resolve this we can have multiple supply line for vdd as well as ground as shown below:




![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/d016b55b-0ae0-41f8-abd7-f06556235e88)

### Pin Placement
Let us suppose we have following design:

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/e44da8f1-0d2f-4d71-9bb2-b9ab92718d0f)

Now we have to place the pins in the chip as shown below:
![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/f788f55c-2875-4c8f-ae81-c39fc8ab4722)

The Clock port are bigger than the normal I/O pins because of it's continuous use and larger area offers less resistance.

<details><summary><strong>Steps To Run Floorplan and Placement</strong></summary>
  
### Floorplanning
Command:

```
run_floorplan
```
![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/ba13b068-b64d-427b-80ef-09fc14bab3e3)

To view the floorplanning in magic:

```
cd OpenLane/designs/picorv32a/runs/RUN_2023.09.12_13.52.53/results/floorplan/
magic  /home/nancy/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32.def &

```

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/163c44a0-65db-46f3-ab1f-914b5e7fd135)

### Placement

Command:

```
run_placement
```



![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/234e070e-d0d5-41e2-a458-1f8214b95902)


To view placement :

```
cd OpenLane/designs/picorv32a/runs/RUN_2023.09.12_13.52.53/results/placement/
magic /home/nancy/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32.def &
```


![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/60c2f9cd-5ea1-4de9-be73-7e340f56fc1a)





</details>
</details>

<details><summary><strong>Library Binding And Placement</strong></summary>

### Netlist Binding
In ASIC (Application-Specific Integrated Circuit) design, a netlist is a critical representation of the electronic components and their interconnections within the chip. Netlist binding is a crucial step in the ASIC design flow, which involves mapping the logical components described in a high-level hardware description language (HDL) like Verilog or VHDL to physical components in the target technology library. <br>
Netlist binding is the step where the gate-level netlist is mapped to the physical cells in the technology library. The synthesis tool selects specific cells from the library to implement each gate in the netlist. This mapping is done based on various factors such as timing constraints, area constraints, and power considerations.


### Initial Design

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/08613bef-1b46-4bb8-9f27-5346f73f5e69)

### Final Optimized Design

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/cb19310d-480e-4e27-ba2b-eb908b602d8b)



  
</details>






<details><summary><strong>Cell Design And Characterization Flow</strong></summary>

### Cell Design

The standard cell design flow is a structured process used to create custom digital integrated circuits. It encompasses several key stages, starting with inputs and culminating in various outputs. Here's a rephrased breakdown of the standard cell design flow:

**Inputs**:

1. **Process Design Kits (PDKs)**: These are provided by semiconductor foundries and contain essential information about the target manufacturing process, including standard cell libraries and design rules.

2. **DRC & LVS Rules**: Design Rule Checking (DRC) and Layout vs. Schematic (LVS) rules are guidelines that ensure the design adheres to manufacturing and electrical specifications.

3. **SPICE Models**: These are mathematical representations of electronic components used for simulation and verification.

4. **Libraries**: Standard cell libraries with pre-designed logic gates and flip-flops are crucial building blocks for the design.

5. **User-Defined Specifications**: Design requirements and constraints set by the designer, such as performance targets, power budget, and functionality.

**Design Steps**:

1. **Circuit Design**: Creating the logical representation of the circuit using hardware description languages (HDLs) like Verilog or VHDL, taking into account the provided libraries and user-defined specifications.

2. **Layout Design**: Translating the logical circuit into a physical layout using layout design techniques. This includes considerations like Euler's path and stick diagrams to optimize for area and performance.

3. **Extraction of Parasitics**: Extracting parasitic elements (such as capacitance and resistance) from the layout to refine the circuit's performance simulation.

4. **Characterization**: Evaluating the circuit's behavior under various conditions, including timing analysis (setup and hold times), noise analysis, and power consumption estimation.

**Outputs**:

1. **Circuit Description Language (CDL)**: A human-readable or machine-readable representation of the circuit, often used for simulation and documentation.

2. **Library Exchange Format (LEF)**: A file format that defines the physical properties of standard cells and facilitates the integration of these cells into the chip's layout.

3. **GDSII**: A file format used to describe the final layout of the chip in a format that can be sent to the semiconductor foundry for manufacturing.

4. **Extracted SPICE Netlist (.cir)**: A netlist that includes parasitic elements extracted from the layout, used for more accurate electrical simulations.

5. **Timing, Noise, and Power .lib Files**: Libraries containing information on the timing characteristics, noise margins, and power consumption of the designed cells, essential for further chip-level analysis and integration.

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/13d62dd0-6fae-4e88-a85b-7733fae9b0c1)

### Characterisation Flow

The standard cell characterization flow typically involves a structured series of steps to determine the electrical behavior and performance characteristics of individual standard cells within an ASIC design. This process is essential for accurately modeling the cells' behavior under various conditions. Here's a rephrased breakdown of the typical standard cell characterization flow:

**1. Model and Technology Data Setup**:
   - Import semiconductor process technology files (tech files) and the transistor-level models (usually SPICE models) for the standard cells.

**2. Read Extracted Spice Netlist**:
   - Input the extracted SPICE netlist that represents the specific standard cell to be characterized.

**3. Behavior Recognition**:
   - Identify and understand the expected behavior and functionality of the standard cell being characterized.

**4. Subcircuit Handling**:
   - Handle any subcircuits or hierarchical structures within the cell design, ensuring accurate simulation.

**5. Power Source Attachment**:
   - Connect appropriate power sources to the standard cell to simulate its behavior under different supply voltages and conditions.

**6. Characterization Setup**:
   - Configure the characterization setup, including specifying input stimulus patterns, test vectors, and conditions for the simulations.

**7. Output Load Configuration**:
   - Define and apply the necessary output capacitance loads to simulate the cell's response to different output loading conditions.

**8. Simulation Commands**:
   - Set up and execute simulation commands for the standard cell, which may include transient simulations, DC analyses, or other relevant simulation types.

**9. GUNA Software Integration**:
   - Utilize open-source software like GUNA to automate and streamline the characterization process.
   - Feed the data from steps 1 through 8 into the GUNA software.

**10. Model Generation**:
    - Use the GUNA software to generate comprehensive models for the standard cell, including timing models (setup time, hold time, propagation delay), noise models (noise margins, sensitivity to noise), and power models (static power, dynamic power).

**11. Model Validation**:
    - Verify and validate the generated models against simulation results to ensure accuracy and reliability.

**12. Documentation and Reporting**:
    - Document the generated models and their characteristics for future use in ASIC design.
    - Create reports summarizing the characterization results and models.

By following this standardized flow and using tools like GUNA, designers can efficiently characterize standard cells, which are essential building blocks in ASIC designs. These models are crucial for accurate timing analysis, power estimation, and noise margin assessments in the overall ASIC design process.


</details>

<details><summary><strong>Timing Characterization Parameters</strong></summary>
  
#### Timing threshold definitions 
Timing defintion |	Value
-------------- | --------------
slew_low_rise_thr	| 20% value
slew_high_rise_thr | 80% value
slew_low_fall_thr |	20% value
slew_high_fall_thr |	80% value
in_rise_thr	| 50% value
in_fall_thr |	50% value
out_rise_thr |	50% value
out_fall_thr | 50% value

#### Propagation Delay and Transition Time 

**Propagation Delay** 
The time difference between when the transitional input reaches 50% of its final value and when the output reaches 50% of its final value. Poor choice of threshold values lead to negative delay values. Even thought you have taken good threshold values, sometimes depending upon how good or bad the slew, the dealy might be still +ve or -ve.

```
Propagation delay = time(out_thr) - time(in_thr)
```
**Transition Time**

The time it takes the signal to move between states is the transition time , where the time is measured between 10% and 90% or 20% to 80% of the signal levels.

```
Rise transition time = time(slew_high_rise_thr) - time (slew_low_rise_thr)

Low transition time = time(slew_high_fall_thr) - time (slew_low_fall_thr)
```



</details>


## Day-3 Design Library Cell using magic layout and ngspice charcterization

<details><summary><strong>Lab For CMOS Inverter </strong></summary>

### Spice Deck Creation

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/4cf35a52-e98a-4e58-bc54-948b255fbea2)

Spice Deck for above :

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/755586da-9522-4f12-ab35-b457a64e317d)

### Spice Simulation

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/c9f1274a-1418-4ba5-9332-8c0c9b692d11)


### Switching Threshold

The switching threshold of a CMOS inverter occurs at the point on its transfer characteristic where the input voltage (Vin) matches the output voltage (Vout), denoted as Vm. This specific threshold results in both the PMOS and NMOS transistors being in an active state, which can lead to the generation of a leakage current.

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/4ba63234-bb49-44c2-8146-985150da73fc)




![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/cbd5f6c0-45c5-4fb8-b0cf-420f96c981c8)



</details>

<details><summary><strong>Inception Of Layout </strong></summary>
  
### CMOS Fabrication Process

The 16-mask CMOS fabrication process involves a series of critical steps to create integrated circuits. Here's a simplified overview:

1. **Substrate Selection**: Choose the appropriate material for the semiconductor substrate, typically silicon.

2. **Active Region Formation**: Isolate active regions where transistors will be built by depositing layers of silicon dioxide (SiO2) and silicon nitride (Si3N4). Use photolithography and etching techniques to define these regions.

3. **N-Well and P-Well Formation**: Introduce impurities through ion implantation, such as boron for P-wells and phosphorus for N-wells, to create the necessary regions for NMOS and PMOS transistors.

4. **Gate Terminal Formation**: Create the gate terminals for NMOS and PMOS transistors using photolithography techniques.

5. **Lightly Doped Drain (LDD) Formation**: Form LDD regions to prevent the hot electron effect in transistors.

6. **Source and Drain Formation**: Add screen oxide to prevent ion channeling during implantation. Implant arsenic to form the source and drain regions. Annealing helps activate these regions.

7. **Local Interconnect Formation**: Remove the screen oxide layer using hydrofluoric acid (HF) etching. Deposit titanium (Ti) for low-resistance electrical contacts.

8. **Higher-Level Metal Formation**: Achieve planarization through chemical mechanical polishing (CMP). Deposit layers of titanium nitride (TiN) and tungsten to form higher-level metal interconnects. Add a top silicon nitride (SiN) layer for chip protection.

These steps represent the major stages in a 16-mask CMOS process, which is essential for building complex integrated circuits with both NMOS and PMOS transistors. This process ensures the precise creation of the various components and connections required for semiconductor devices.


### VSDSTDCelldesign 

The Magic layout of a CMOS inverter will be used so as to intergate the inverter with the picorv32a design. To do this, inverter magic file is sourced from vsdstdcelldesign by cloning it within the openlane directory as follows:

```
cd OpenLane/
git clone https://github.com/nickson-jose/vsdstdcelldesign
```

To view the layout of the inverter in magic :
```
magic -T ./libs/sky130A.tech sky130_inv.mag &
```

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/522a7bb6-0325-4b4b-aa21-656598d49a92)

**Identification Of NMOS AND PMOS**

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/0e758480-6ad3-4b51-befd-015935029d7b)

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/8c42ac19-20a9-4453-94ed-f28dc5e9edc1)

**Connectivity Of Source And Drain**

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/b03277f4-a81a-4a1d-b91b-d8ca7878af8e)


### Steps To Create Standard Cell and Extract Spice Netlist

Following are the commands to extract the spice netlist

```
extract all
ext2spice cthresh 0 rthresh 0
ext2spice
```
Following file is created:

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/588f5544-ac09-4cc2-a2d9-5cba37af187c)


</details>

<details><summary><strong>Sky130 Tech File Labs</strong></summary>
  
After extracting the spice netlist, modify the the netlist as shown below:

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/1648cb73-704e-4105-a47b-62a671d18323)


Now run the netlist in ngspice using the following commands as shown below:

```
ngspice sky130_inv.spice
```

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/607eb25b-aa5e-4e97-a1ab-4113da363e3c)


Now plot the graph

```
plot y vs time a
```


![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/8192db1e-2cef-4c76-9e51-b4a6ac346fe8)

Now zoom and calculate the following parameters:


1. Rise transition: Time taken for the output to rise from 20% of max value to 80% of max value
2. Fall transition- Time taken for the output to fall from 80% of max value to 20% of max value
3. Cell rise delay = time(50% output rise) - time(50% input fall)
4. Cell fall delay  = time(50% output fall) - time(50% input rise)

The above timing parameters can be computed by noting down various values from the ngspice waveform.

 ``` 
 Rise Transition : 2.25421 - 2.18636 = 0.006785 ns / 67.85ps
 ```
 ```
 Fall Transitio : 4.09605 - 4.05554 = 0.04051ns/40.51ps 
 ```
 ```
 Cell Rise Delay : 2.21701 - 2.14989 = 0.06689ns/66.89ps 
 ```
 ```
 Cell Fall Delay : 4.07816 - 4.05011 = 0.02805ns/28.05ps 
 ```



### MAGIC DRC

To download the packages from the web and extract it use the following command:

```
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
tar xfz drc_tests.tgz
```

Now lets run the met3.mag file on magic and lets see an example of a set of rules failing in the Metal 1 layer could involve errors in the metal layer's patterning, such as shorts or opens, which may disrupt electrical connectivity in an integrated circuit design.

```
magic -d XR met3.mag
```

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/ae5e9997-7333-435c-94e0-cbdcbe37a83c)

Use the following command to see the metal cut:

```
cif see VIA2

```

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/c73fb5d8-2cfb-452d-875e-f85b7dfa067d)


### Lab To Fix poly.9 error in SKY130 Tech File

To load the poly file use the following command:

```
load poly.mag
```

The following screen will appear:

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/ef965c8a-2701-4ab8-842d-65d3c64d1df8)

As you see there is som error in it1:


![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/5a351b31-3503-49e3-9b88-7e9df229edcd)

To rectify these issues, adjustments need to be made in the SKY130 technology file.
To make the necessary corrections, you should open the SKY130 technology file and perform a search for "poly.9."

You will find the following command :

```
spacing npres *nsd 480 touching_illegal \
	"poly.resistor spacing to N-tap < %d (poly.9)"
```

Now add the another command below this:

```
spacing npres allpolynonres 480 touching_illegal \
	"poly.resistor spacing to N-tap < %d (poly.9)"
```

Similarly, <br>

Search for the following command:

```
spacing xhrpoly,uhrpoly,xpc alldiff 480 touching_illegal \
      "xhrpoly/uhrpoly resistor spacing to diffusion < %d (poly.9)"
```
And add the following command:

```
spacing xhrpoly,uhrpoly,xpc allpolynonres 480 touching_illegal \
      "xhrpoly/uhrpoly resistor spacing to diffusion < %d (poly.9)"
```
Now write and quit the tech file 
To reload the magic layout write the following command:

```
tech load sky130A.tech
drc check
```
Note: Click on yes inacse any warning appears on the screen.

The modifie layout is shown below:

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/2e2b42a5-0019-4da6-9129-9c3592cf3079)


### To Implement Poly Resistor Spacing to Diff and tap

Now copy the three resistor and create ndiffusion and p diffusion regions as shown below:









![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/263b3f07-2489-4bab-93ee-09af68a30c80)








</details>



## Day-4 Pre-layout Timing Analysis And Importance Of Good Clock Tree

<details><summary><strong>Timing Modelling Using Delay Tables</strong></summary>

### Coverting Grid Info To Track Info

To meet the requirement for ports, specifically for the CMOS Inverter's A and Y ports located on the li1 layer, it is essential to verify that they are positioned at the intersection of horizontal and vertical tracks. This validation can be achieved by referring to the tracks.info file, which provides information about track pitch and direction.

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/f5353416-ee02-43e5-b171-08553df7531a)

To ensure that the ports are positioned at the intersection point, you should adjust the grid spacing in Magic (tkcon) to match the li1 layer's X and Y values. This alignment between the grid and tracks can be achieved using the following command:

```
grid 0.46um 0.34um 0.23um 0.17um
```

Below is the after grid representation:

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/ef657858-6d85-4847-99d1-d30617cbd1dd)


### Create Port Definition

After completing the layout, the subsequent step involves extracting an LEF (Library Exchange Format) file for the cell. During this process, it's crucial to configure properties and definitions for the cell's pins to assist the placer and router tools. In LEF files, a cell that includes ports is represented as a macro cell, and these ports are defined as the declared PINs of the macro. The initial step in this procedure is defining the ports and ensuring that the correct class and use attributes are set for each port in compliance with the standard format.

To configure the ports effectively, follow these steps in the Magic console:

1. Load your design's .mag file, specifically the layout for the inverter.

2. Navigate to the "Edit" menu and choose "Text." This will open a dialog box.

3. In the dialog box, double-click on the letter 'S' located at the I/O labels on the layout.

4. The text field will automatically populate with the correct string name and size for the port.

5. To confirm the port definition, ensure that the "Port enable" checkbox is selected, indicating that it functions as a port. Also, make sure that the "Default" checkbox remains unchecked.

6. Your port configuration is now correctly established as depicted in the figure.

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/a4da8676-6002-4402-a1f1-005b6947bd32)


### Standard Cell LEF generation

Before the extraction Of LEF file we have to define the function of each port using the following commands:

```
port A class input
port A use signal

port Y class output
port Y use signal

port VPWR class inout
port VPWR use power

port VGND class inout
port VPWR use ground
```

Now extract the LEF file using the following command:

```
lef write
```
![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/3bc525d3-ded3-446e-b3e3-a91a47dd68ca)

After this there is lef file generated with the same name in the current directory.

### Integrating Custom Cell In OpenLANE

You should copy the extracted LEF file to the picorv32a source directory, and additionally, the sky130_fd_sc_hd_typical.lib file from the vsdstdcelldesign/libs directory should be copied to the dpicorv32a source directory.

```
cp sky130_vsdinv.lef /home/nancy/OpenLane/designs/picorv32a/src/
cp sky130_fd_sc_hd__* /home/nancy/OpenLane/designs/picorv32a/src/
```
The config.tcl file should also be modified

```

# Design
set ::env(DESIGN_NAME) "picorv32a"

set ::env(VERILOG_FILES) "$::env(DESIGN_DIR)/src/picorv32a.v"

set ::env(CLOCK_PORT) "clk"
set ::env(CLOCK_NET) $::env(CLOCK_PORT)

set ::env(GLB_RESIZER_TIMING_OPTIMIZATIONS) {1}

set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]

set filename $::env(DESIGN_DIR)/$::env(PDK)_$::env(STD_CELL_LIBRARY)_config.tcl
if { [file exists $filename] == 1} {
	source $filename
}
```

To invoke OpenLANE and run synthesis with the new standard cell library, use the following commands:

```
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
```
![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/437c72c0-346e-4397-8cf7-6ee5c47a36a3)







</details>









  

