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






</details>







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
Decoupling capacitors help maintain a constant voltage level at the power supply pins of ICs. When an IC switches or draws transient current, the decoupling capacitor supplies the required charge to keep the voltage stable, preventing glitches or erratic behavior.

### Power Planning
Let us suppose that there are multiple macros in a chip and output changes from '1' to '0', then it discharged into ground line because of which we can see ground bumpp. Similarly when it is charged from 0 to 1 we can see voltage droop in power supply.<br>
Hence to resolve this we can have multiple supply line for vdd as well as ground as shown below:




![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/d016b55b-0ae0-41f8-abd7-f06556235e88)

### Pin Placement
Let us suppose we have following design:

![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/e44da8f1-0d2f-4d71-9bb2-b9ab92718d0f)

Now we have to place the pins in the chip as shown below:
![image](https://github.com/Nancy0192/OpenLane_PhysicalDesign/assets/140998633/f788f55c-2875-4c8f-ae81-c39fc8ab4722)

The Clock port are bigger than the normal I/O pins because of it's continuous use and larger area offers less resistance.




  
</details>
