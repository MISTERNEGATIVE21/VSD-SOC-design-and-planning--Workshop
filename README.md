# 
![Picture6](https://github.com/user-attachments/assets/5aab9ad4-f55a-4004-b2d2-a1692b09a92f)

**Digital VLSI SoC Design and Planning**

2 Week digital VLSI SoC design and planning workshop with complete RTL2GDSII flow organized by VSD in collaboration with NASSCOM.
### Theory 
**Package**

-   In any embedded board, the \"chip\" we observe is actually the PACKAGE, which encases and protects the actual chip. The chip, located at the package center, connects to the package via WIRE BONDING, a basic wired connection method.

  ![Picture1](https://github.com/user-attachments/assets/1ea0fd55-9b42-4c81-b8e4-1aec2e23a098)

                               A simple illustration of Arduino

![Picture2](https://github.com/user-attachments/assets/1803e4b6-549b-460a-a47e-269c027f3f35)


**Chip**

-   Inside the chip, signals flow through PADS to and from the external world. The are surrounded by pads is the CORE, housing the chip\'s digital logic. Together, the core and pads form the DIE, the fundamental semiconductor manufacturing unit.

-   Semiconductor chips are produced in FOUNDRIES, which also create FOUNDRY IPs intellectual properties requiring specific expertise.Repeatable logic blocks within chips are called MACROS.

   ![Picture3](https://github.com/user-attachments/assets/0fbb9322-f79c-4d88-9ca0-b4a932c73212)


                                   Parameters of the chip

**ISA (Instruction Set Architecture)**

To execute a C program on hardware, a series of steps are followed:

1\. The program is compiled into assembly language, such as RISC-V ISA.\
2. Assembly code is translated into machine language (binary 0s and 1s).\
3. Using RTL (Hardware Description Language), RISC-V specifications are implemented.\
4. The RTL is processed through a standard PnR flow, producing the final layout (GDSII format).
5. System software, including the OS, compiler, and assembler, convert application code into binary language. For example, a stopwatch app on a RISC-V core transitions from C functions (via OS) to RISC-V instructions (via compiler) and binary code (via assembler), ready for hardware execution.

![Picture4](https://github.com/user-attachments/assets/1db21174-a5b2-4f43-9a31-7512e4bd89fe)

-   There are mainly 3 different parts in this course. They are:

1.  RISC-V ISA

2.  RTL and synthesis of RISC-V based CPU core - picorv32a

3.  Physical design implementation of picorv32a

![Picture5](https://github.com/user-attachments/assets/210ede21-673a-4b29-b6de-9bc4e757ac3c)

Open-Source Implementation

Open-source ASIC design relies on:
- RTL Designs\
- EDA Tools\
- PDK Data\

Initially, IC design and fabrication were tightly coupled. In 1979,
Conway and Mead introduced structured methodologies separating design
from fabrication, spawning fabless companies and pure-play fabs. The
Process Design Kit (PDK), containing essential data (device models,
design rules, libraries, etc.), bridges designers and fabs.

![Picture6](https://github.com/user-attachments/assets/c78a0673-481b-41ae-95ba-a1a52e61cf98)

In 2020, Google and SkyWater released the first open-source PDK for
130nm, making ASIC design more accessible.

ASIC Design Flow

ASIC design involves multiple steps and tools integrated via the ASIC
design flow, which transitions from RTL to GDSII format.

Key Steps:

1\. Synthesis: Converts RTL to a gate-level netlist using Standard Cell Libraries (SCLs).\
2. Floorplanning: Arranges macros and plans power distribution.\
3. Placement: Assigns cell positions (global and detailed).\
4. Clock Tree Synthesis: Aligns clock arrival times (mitigating skew).\
5. Routing: Establishes interconnections across routing layers (e.g.,SkyWater PDK uses 6 layers).

![Picture7](https://github.com/user-attachments/assets/2daf7a94-18b5-4075-a782-4cd94adec7c0)

Sign-Off Checks:

\- Design Rule Checking (DRC) ensures fabrication rules are met.\
- Layout vs. Schematic (LVS) verifies layout matches the gate-level
netlist.\
- Static Timing Analysis (STA) ensures timing compliance.

### Section 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK (8/01/2025 - 10/01/2025)

## Section 1 tasks: -

1.  Run \'picorv32a\' design synthesis using OpenLANE flow and generate
    necessary outputs.

2.  Calculate the flop ratio.


 	 Flop Ratio = $\frac{Number\ of\ D\ Flip\ Flops}{Total\ Number\ of\ Cells}$

   Percentage of DFF′s = Flop Ratio∗100

-   All section 1 logs, reports and results can be found in following run folder:

In the runs folder [Section 1-Run-17-01_08-01](openlane/designs/picorv32a/runs/17-01_08-01)

-   Run \'picorv32a\' design synthesis using OpenLANE flow and generate necessary outputs.

Commands to invoke the OpenLANE flow and perform synthesis

\# Change directory to openlane flow directory

cd Desktop/work/tools/openlane_working_dir/openlane

\# alias docker=\'docker run -it -v \$(pwd):/openLANE_flow -v \$PDK_ROOT: \$PDK_ROOT -e PDK_ROOT=\$PDK_ROOT -u \$(id -u \$USER): \$(id -g \$USER) efabless/openlane: v0.21\'

\# Since we have aliased the long command to \'docker\' we can invoke the OpenLANE flow docker sub-system by just running this command

docker

\# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command

./flow.tcl -interactive

\# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow

package require openlane 0.9

\# Initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is \'picorv32a\'

prep -design picorv32a

\# Now that the design is prepped and ready, we can run synthesis using following command

run_synthesis

\# Exit from OpenLANE flow

exit

\# Exit from OpenLANE flow docker sub-system

exit

Screenshots of running each commands

![Picture8](https://github.com/user-attachments/assets/24dd57e0-2d6f-4fdc-aa18-1a851d76d5d1)

![Picture9](https://github.com/user-attachments/assets/9ea4c692-93a2-422a-8307-9aa4cbb73e62)

2\. Calculate the flop ratio.

Screenshots of synthesis statistics report file with required values
highlighted

![Picture10](https://github.com/user-attachments/assets/ca2e20bd-aaca-4aa1-a590-b317f8825d96)


![Picture11](https://github.com/user-attachments/assets/e4a009c5-df58-46a6-a1c3-c47de3eb4a07)


Calculation of Flop Ratio and DFF % from synthesis results

No of D-FF are: 1613\
No of total no of FF is: 14876

Flop Ratio = $\frac{1613}{14876}$ = 0.108429685

Percentage of DFF′s = 0.108429685∗100 = 10.842 %

## Section 2 - Good floorplan vs bad floorplan and introduction to library cells (11/01/2025 - 16/01/2025)

### Implementation

## Section 2 tasks: -

1.  Run \'picorv32a\' design floorplan using OpenLANE flow and generate
    necessary outputs.

2.  Calculate the die area in microns from the values in floorplan def.

3.  Load generated floorplan def in magic tool and explore the
    floorplan.

4.  Run \'picorv32a\' design congestion aware placement using OpenLANE
    flow and generate necessary outputs.

5.  Load generated placement def in magic tool and explore the
    placement.

*Area of die in microns = Die width in microns ∗ Die height in microns*

-   All section 2 logs, reports and results can be found in following
    run folder.

[Section_2-runs/17-01_08-01](openlane/designs/picorv32a/runs/17-01_08-01)

-   **Run \'picorv32a\' design floorplan using OpenLANE flow and
    generate necessary outputs.**

Commands to invoke the OpenLANE flow and perform floorplan

\# Change directory to openlane flow directory

cd Desktop/work/tools/openlane_working_dir/openlane

\# Since we have aliased the long command to \'docker\' we can invoke the OpenLANE flow docker sub-system by just running this command

docker

\# To invoke the OpenLANE flow in the Interactive mode using the following command

./flow.tcl -interactive

\# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow

package require openlane 0.9

\# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is \'picorv32a\'

prep -design picorv32a

\# Now that the design is prepped and ready, we can run synthesis using following command

run_synthesis

\# Now we can run floorplan

run_floorplan

Screenshot of floorplan run

![Picture12](https://github.com/user-attachments/assets/446878a2-5681-4005-872d-7b3ed6ffd6d9)

![Picture13](https://github.com/user-attachments/assets/e63def47-6cd4-4f5d-9cc8-3539459fb233)

**2. Calculate the die area in microns from the values in floorplan
def.**

Screenshot of contents of floorplan def

![Picture14](https://github.com/user-attachments/assets/b7390062-e23d-4b86-9a9b-61c1d4e7490a)


According to floorplan def File

1000 Unit Distance = 1 Micron

Die width in unit distance = 720865 -- 0 = 720865

Die height in unit distance = 731585 -- 0 = 731585

Distance in microns = Value in Unit Distance1000

Die width in microns = $\frac{720865}{1000}$ = 720.865 Microns

Die height in microns = $\frac{731585}{1000}$ = 731.585 Microns

Area of die in microns = 720.865 \* 731.585 = 527374.021 Square Microns

**3. Load generated floorplan def in magic tool and explore the
floorplan**.

Commands to load floorplan def in magic in another terminal.

\# Change directory to path containing generated floorplan def

cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/13-01_08-24/results/floorplan/

\# Command to load the floorplan def in magic tool

magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A /libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &

Screenshots of floorplan def in magic

![image15](https://github.com/user-attachments/assets/8862178d-0410-47c1-964f-e12612606a46)

Equidistant placement of ports

![Screenshot from 2025-01-13 14-27-45](https://github.com/user-attachments/assets/5a4a5924-dd54-49a1-b110-fb8bb872f06c)

Port layer as set through config.tcl

![Screenshot from 2025-01-13 14-48-24](https://github.com/user-attachments/assets/7069fe4c-25c1-46f1-ab74-d379d928eb2f)

![image18](https://github.com/user-attachments/assets/7d67606c-a8f3-40fa-9627-5e9f0b3683eb)

Decap Cells and Equidistant Tap Cells

![image16](https://github.com/user-attachments/assets/fcfacf86-8b4a-4ac8-abf9-8b956e3320fc)

Unplaced standard cells at the origin

![image19](https://github.com/user-attachments/assets/e536a745-f72a-444f-a11a-92185140a5da)

**4. Run \'picorv32a\' design congestion aware placement using OpenLANE
flow and generate necessary outputs.**

Command to run placement

\# To run placement by default different switchs are available for other aware operations

run_placement

Screenshots of placement run

![image20](https://github.com/user-attachments/assets/4670cafe-d0b2-4b81-bf04-22b799b92eba)


![image21](https://github.com/user-attachments/assets/6746df2c-c908-4085-9360-850d3b2ab033)


5\. Load generated placement def in magic tool and explore the
placement.

Commands to load placement def in magic in another terminal

\# Change directory to path containing generated placement def

cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/13-01_08-24/results/placement/

\# Command to load the placement def in magic tool

magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

Commands to exit from current run

\# Exit from OpenLANE flow

exit

\# Exit from OpenLANE flow docker sub-system

exit

Screenshots of Placement def in magic

![image22](https://github.com/user-attachments/assets/63e65d70-cd5c-42c3-b5d0-95f5461e6a46)

Standard cells legally placed

![image22](https://github.com/user-attachments/assets/7c2d13df-9443-46b3-bf55-68ead08c8bd4)

## Section 3 - Design library cell using Magic Layout and ngspice characterization (13/01/2025 - 16/01/2025)

### Implementation

## Section 3 tasks: -

1.  Clone custom inverter standard cell design from github
    repository: [Standard cell design and characterization using OpenLANE flow.](https://github.com/nickson-jose/vsdstdcelldesign.git)

2.  Load the custom inverter layout in magic and explore.

3.  Spice extraction of inverter in magic.

4.  Editing the spice model file for analysis through simulation.

5.  Post-layout ngspice simulations.

6.  Find problem in the DRC section of the old magic tech file for the skywater process and fix them.

## Section 3 - Tasks 1 to 5 files, reports and logs can be found in the following folder.

[Section 3 - For task 1 to 5 -vsdstdcelldesign](openlane/vsdstdcelldesign)

## Section 3 - Task 6 files, reports and logs can be found in the following folder.

[Section 3 -- Task 6 (drc_tests)](drc_tests)

1\. Clone custom inverter standard cell design from github repository

> \# Change directory to openlane
>
> cd Desktop/work/tools/openlane_working_dir/openlane
>
> \# Clone the repository with custom inverter design
>
> git clone https://github.com/nickson-jose/vsdstdcelldesign
>
> \# Change into repository directory
>
> cd vsdstdcelldesign
>
> \# Copy magic tech file to the repo directory for easy access
>
> cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech.
>
> \# Check contents whether everything is present
> ls
> \# Command to open custom inverter layout in magic
>
> magic -T sky130A.tech sky130_inv.mag &

Screenshot of commands run

![image24](https://github.com/user-attachments/assets/57d691a4-52f7-4585-8e63-a43d6882c57f)

2\. Load the custom inverter layout in magic and explore.

Screenshot of custom inverter layout in magic

 ![image25](https://github.com/user-attachments/assets/be35c5db-3251-43c6-b783-6f92cd5ef789)

NMOS and PMOS identified

![image26](https://github.com/user-attachments/assets/3d833ab1-8423-4ac7-a989-a7c9df1cea92)

![image27](https://github.com/user-attachments/assets/0f8687d7-469d-41f7-af42-bdd598245d60)

3\. Spice extraction of inverter in magic.

Commands for spice extraction of the custom inverter layout to be used
in tkcon window of magic

    \# Check current directory

    pwd

    \# Extraction command to extract to. ext format

    extract all

    \# Before converting ext to spice this command enable the parasitic extraction also

    ext2spice cthresh 0 rthresh 0

    \# Converting to ext to spice

    ext2spice

Screenshot of tkcon window after running above commands

![image28](https://github.com/user-attachments/assets/245df9d4-f23d-4ca7-92fd-748475e52d2f)

Screenshot of created spice file

 ![image28](https://github.com/user-attachments/assets/390fe119-2115-4eee-a2ba-546237efa5b9)

4\. Editing the spice model file for analysis through simulation.

Measuring unit distance in layout grid

-   If grid is not visible when you open the Magic, then go to window 🡪 press Grid on

![image30](https://github.com/user-attachments/assets/dbab1e20-0936-4de4-8d22-c04f9860fcd6) 

Final edited spice file ready for ngspice simulation

![image31](https://github.com/user-attachments/assets/7d71e8d6-6878-43fd-80e0-7e1fac541073)

**5. Post-layout ngspice simulations.**

Commands for ngspice simulation

> \# Command to directly load spice file for simulation to ngspice
>
> ngspice sky130_inv.spice
>
> \# Now that we have entered ngspice with the simulation spice file loaded we just have to load the plot
>
> plot y vs time a

Screenshots of ngspice run

![image32](https://github.com/user-attachments/assets/7e78dd48-b5df-40a5-aca5-3b6665735ba6)

Screenshot of generated plot

 ![image33](https://github.com/user-attachments/assets/070ffca7-862c-45fb-bf19-78173e9b6809)

Rise transition time calculation

Rise transition time = Time taken for output to rise to 80% −
Time taken for output to rise to 20%

		                              20% of output=660 mV
		                              80% of output=2.64 V

20% Screenshots

 ![image34](https://github.com/user-attachments/assets/dcd984ba-c159-4a61-b89f-f71556489d44)

80% Screenshots

![image35](https://github.com/user-attachments/assets/03acff86-16a2-4953-bd82-d29fb5480e02)

![image36](https://github.com/user-attachments/assets/746fabf0-378d-4031-88d9-5402965a4abd)

                     *Rise transition time = 2.180−2.119 = 0.061 ns = 61 ps*

Fall transition time calculation

Fall transition time=Time taken for output to fall to 20% − Time taken for output to fall to 80%

	                               20% of output=660 mV
	                               80% of output=2.64 V

20% Screenshots

 ![image37](https://github.com/user-attachments/assets/482c44f5-f2fa-4b7d-9ca0-0bcdc662e458)

80% Screenshots

![image38](https://github.com/user-attachments/assets/d2850758-e586-4452-96f1-98b60fae88da)

![image36](https://github.com/user-attachments/assets/a763f35d-907f-47f0-a7a7-b6072d054b32)


    		Fall transition time = 4.0779 − 4.0497 = 0.0331 ns = 33.1 ps

Rise Cell Delay Calculation

Rise Cell Delay=Time taken for output to rise to 50% − Time taken for input to fall to 50%

                           	50% of 3.3 V=1.65 V

50% Screenshots

![image39](https://github.com/user-attachments/assets/5c89879b-c7ec-40ae-96d0-b3380e9a13ae)

![image40](https://github.com/user-attachments/assets/635b00e8-1c61-42eb-921b-73c80812a0ae)


      		 Rise Cell Delay = 2.21144−2.15008 = 0.06136 ns = 61.36 ps

Fall Cell Delay Calculation

*Fall Cell Delay=Time taken for output to fall to 50% − Time taken for input to rise to 50%*

                     		 50% of 3.3 V=1.65 V

50% Screenshot

 ![image41](https://github.com/user-attachments/assets/843fabe4-4013-46bd-8421-d11cce386932)

![image40](https://github.com/user-attachments/assets/635b00e8-1c61-42eb-921b-73c80812a0ae)

     		 Fall Cell Delay = 4.0779 − 4.049 = 0.0282 ns = 28.2 ps

6\. Find problem in the DRC section of the old magic tech file for the
skywater process and fix them.

Link to Sky130 Periphery rules: <https://skywaterpdk.readthedocs.io/en/main/rules/periphery.html>

Commands to download and view the corrupted skywater process magic tech file and associated files to perform drc corrections

> \# Change to home directory
>
> cd
>
> \# Command to download the lab files
>
> wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
>
> \# Since lab file is compressed command to extract it
>
> tar xfz drc_tests.tgz
>
> \# Change directory into the lab folder
>
> cd drc_tests
>
> \# List all files and directories present in the current directory
>
> ls -al
>
> \# Command to view .magicrc file
>
> gvim .magicrc
>
> \# Command to open magic tool in better graphics
>
> magic -d XR &

Screenshots of commands run

 ![image42](https://github.com/user-attachments/assets/7874ea95-36a1-469f-a403-de9ad7590de1)

Screenshot of .magicrc file

 ![image43](https://github.com/user-attachments/assets/268599f8-12c8-4484-a109-83fdf130e62a)

**Incorrectly implemented poly.9 simple rule correction**

Screenshot of poly rules

![image44](https://github.com/user-attachments/assets/ff2d7a4c-2379-4d0f-9c66-3adefb608893)

Incorrectly implemented poly.9 rule no drc violation even though spacing < 0.48u

![image45](https://github.com/user-attachments/assets/0eb346a7-610a-4aef-a9a5-39e5e8c7c623)

New commands inserted in sky130A.tech file to update drc

![image46](https://github.com/user-attachments/assets/c97dcc68-4816-40e2-ae69-b4913825c315)

![image47](https://github.com/user-attachments/assets/7969459f-6fee-4d45-8282-fd2455b8dc47)

Commands to run in tkcon window

> \# Loading updated tech file
>
> tech load sky130A.tech
>
> \# Must re-run drc check to see updated drc errors
>
> drc check
>
> \# Selecting region displaying the new errors and getting the error
> messages
>
> drc why

Screenshot of magic window with rule implemented

![image48](https://github.com/user-attachments/assets/f61746ef-0f7c-4a3b-9eee-bfc21032ef3a)

**Incorrectly implemented difftap.2 simple rule correction**

Screenshot of difftap rules

 ![image49](https://github.com/user-attachments/assets/cdda2fd1-56ae-4b4f-8395-3a4507400dd6)

Incorrectly implemented difftap.2 rule no drc violation even though spacing \< 0.42u

 ![image50](https://github.com/user-attachments/assets/6fc50c94-027a-4f01-adc4-957b494fd44a)

New commands inserted in sky130A.tech file to update drc

 ![image51](https://github.com/user-attachments/assets/38415a53-42dc-4a0a-a5b1-c28d13916552)

Commands to run in tkcon window

    \# Loading updated tech file

    tech load sky130A.tech

    \# Must re-run drc check to see updated drc errors

    drc check

    \# Selecting region displaying the new errors and getting the error
    messages

    drc why

**Incorrectly implemented nwell.4 complex rule correction**

Screenshot of nwell rules

![image52](https://github.com/user-attachments/assets/71e6d24d-9b2b-486d-a09a-9e3cf2f44ec1)

Incorrectly implemented nwell.4 rule no drc violation even though no tap
present in nwell

![image53](https://github.com/user-attachments/assets/fd74f262-d8ac-46e7-8138-5040eccee00f)

New commands inserted in sky130A.tech file to update drc

![image54](https://github.com/user-attachments/assets/a29fb465-1b2a-4227-bf2c-fdb6580e239c)

![image55](https://github.com/user-attachments/assets/551a431b-519a-4eb4-9c6e-eead3d30a6c1)

Commands to run in tkcon window

    \# Loading updated tech file
	
    tech load sky130A.tech

    \# Change drc style to drc full

    drc style drc(full)

    \# Must re-run drc check to see updated drc errors

    drc check

    \# Selecting region displaying the new errors and getting the error
    messages

    drc why

Screenshot of magic window with rule implemented

![image56](https://github.com/user-attachments/assets/cb0101c3-9721-443a-86aa-0e84b2ba7be9)

## Section 4 - Pre-layout timing analysis and importance of good clock tree (16/01/2025 - 19/01/2025)

### Implementation

### Section 4 tasks: -

1.  Fix up small DRC errors and verify the design is ready to be inserted into our flow.

2.  Save the finalized layout with custom name and open it.

3.  Generate lef from the layout.

4.  Copy the newly generated lef and associated required lib files to \'picorv32a\' design \'src\' directory.

5.  Edit \'config.tcl\' to change lib file and add the new extra lef into the openlane flow.

6.  Run openlane flow synthesis with newly inserted custom inverter
    cell.

7.  Remove/reduce the newly introduced violations with the introduction
    of custom inverter cell by modifying design parameters.

8.  Once synthesis has accepted our custom inverter, we can now run
    floorplan and placement and verify the cell is accepted in PnR flow.

9.  Do post-synthesis timing analysis with OpenSTA tool.

10. Make timing ECO fixes to remove all violations.

11. Replace the old netlist with the new netlist generated after timing
    ECO fix and implement the floorplan, placement and cts.

12. Post-CTS OpenROAD timing analysis.

13. Explore post-CTS OpenROAD timing analysis by removing
    \'sky130_fd_sc_hd\_\_clkbuf_1\' cell from clock buffer list variable
    \'CTS_CLK_BUFFER_LIST\'.

## Section 4 -Task 4, reports and logs can be found in the following folder.

[Section 4 - for the Tasks 1 to 4 files
(vsdstdcelldesign)](openlane/vsdstdcelldesign)

[Section 4 -- Task 4 (src)](openlane/designs/picorv32a/src)

-   Section 4 -- Task 5 files, reports and logs can be found in the
    following folder.

[Section 4 - for Task 5 (picorv32a)](openlane/designs/picorv32a/src)

-   Section 4 - Tasks 6 to 8 & 11 to 13 logs, reports and results can be
    found in following run folder.

[Section 4 - Tasks 6 to 8 & 11 to 13 Run
(17-01_14-04)](openlane/designs/picorv32a/runs/17-01_14-04)

-   Section 4 - Tasks 9 to 11 logs, reports and results can be found in
    following run folder.

[Tasks from 9 to 11
(17-01_14-28)](openlane/designs/picorv32a/runs/17-01_14-28)

1\. Fix up small DRC errors and verify the design is ready to be
inserted into our flow.

Conditions to be verified before moving forward with custom designed
cell layout:

-   Condition 1: The input and output ports of the standard cell should
    lie on the intersection of the vertical and horizontal tracks.

-   Condition 2: Width of the standard cell should be odd multiples of
    the horizontal track pitch.

-   Condition 3: Height of the standard cell should be even multiples of
    the vertical track pitch.

Commands to open the custom inverter layout

> \# Change directory to vsdstdcelldesign
>
> cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign
>
> \# Command to open custom inverter layout in magic
>
> magic -T sky130A.tech sky130_inv.mag &

Screenshot of tracks.info of sky130_fd_sc_hd

![image57](https://github.com/user-attachments/assets/55f07813-d5f9-4a51-9d9c-71dd2032e7cc)

Commands for tkcon window to set grid as tracks of locali layer

> \# Get syntax for grid command
>
> help grid
>
> \# Set grid values accordingly
>
> grid 0.46um 0.34um 0.23um 0.17um

Screenshot of commands run

![image58](https://github.com/user-attachments/assets/b8a320e0-b7a6-450f-aa8c-dc4a72d92a29)

Condition 1 verified

![image59](https://github.com/user-attachments/assets/83715a59-d195-4b2e-a013-a84f0aef5096)

Condition 2 verified

*Horizontal track pitch=0.46 um*

![image60](https://github.com/user-attachments/assets/2aa9ccca-8491-4dc6-8793-cb27349c8b94)

*Width of standard cell=1.38 um=0.46∗3*

Condition 3 verified

*Vertical track pitch=0.34 um*

 ![image61](https://github.com/user-attachments/assets/8b4ac5d7-8ed3-4989-b997-587f41a3749c)

*Height of standard cell=2.72 um=0.34∗8*

**2. Save the finalized layout with custom name and open it.**

Command for tkcon window to save the layout with custom name

> \# Command to save as
>
> save sky130_vsdinv.mag

Command to open the newly saved layout

> \# Command to open custom inverter layout in magic
>
> magic -T sky130A.tech sky130_vsdinv.mag &

Screenshot of newly saved layout

![image62](https://github.com/user-attachments/assets/1e63313f-708f-4726-9958-617c8b1d0678)

3\. Generate lef from the layout.

Command for tkcon window to write lef

> \# lef command
>
> lef write

Screenshot of newly created lef file

![image63](https://github.com/user-attachments/assets/5c51b254-c6ac-440c-a4bf-942692661399)

4\. Copy the newly generated lef and associated required lib files to
\'picorv32a\' design \'src\' directory.

Commands to copy necessary files to \'picorv32a\' design \'src\'
directory

> \# Copy lef file
>
> cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
>
> \# List and check whether it\'s copied
>
> ls
> \~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
>
> \# Copy lib files
>
> cp libs/sky130_fd_sc_hd\_\_\* \~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
>
> \# List and check whether it\'s copied
>
> ls \~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

Screenshot of commands run

![image64](https://github.com/user-attachments/assets/7c4e1ab0-c3cc-41f5-bc0e-1e81263760ab)

5\. Edit \'config.tcl\' to change lib file and add the new extra lef
into the openlane flow.

Commands to be added to config.tcl to include our custom cell in the
openlane flow

> set ::env(LIB_SYNTH) "\$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd\_\_typical.lib\"
>
> set ::env(LIB_FASTEST)
> \"\$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd\_\_fast.lib\"
>
> set ::env(LIB_SLOWEST)
> \"\$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd\_\_slow.lib\"
>
> set ::env(LIB_TYPICAL)
> \"\$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd\_\_typical.lib\"
>
> set ::env(EXTRA_LEFS) \[glob
> \$::env(OPENLANE_ROOT)/designs/\$::env(DESIGN_NAME)/src/\*.lef\]

Edited config.tcl to include the added lef and change library to ones we
added in src directory

![image65](https://github.com/user-attachments/assets/2c128663-0e7b-45c6-9513-75a699c9f3c0)

6\. Run openlane flow synthesis with newly inserted custom inverter
cell.

Commands to invoke the OpenLANE flow include new lef and perform
synthesis

> \# Change directory to openlane flow directory
>
> cd Desktop/work/tools/openlane_working_dir/openlane
>
> \# alias docker=\'docker run -it -v \$(pwd):/openLANE_flow -v
> \$PDK_ROOT:\$PDK_ROOT -e PDK_ROOT=\$PDK_ROOT -u \$(id -u \$USER):\$(id
> -g \$USER) efabless/openlane:v0.21\'
>
> \# Since we have aliased the long command to \'docker\' we can invoke
> the OpenLANE flow docker sub-system by just running this command
>
> docker
>
> \# Now that we have entered the OpenLANE flow contained docker
> sub-system we can invoke the OpenLANE flow in the Interactive mode
> using the following command
>
> ./flow.tcl -interactive
>
> \# Now that OpenLANE flow is open we have to input the required
> packages for proper functionality of the OpenLANE flow
>
> package require openlane 0.9
>
> \# Now the OpenLANE flow is ready to run any design and initially we
> have to prep the design creating some necessary files and directories
> for running a specific design which in our case is \'picorv32a\'
>
> prep -design picorv32a
>
> \# Additional commands to include newly added lef to openlane flow
>
> set lefs \[glob \$::env(DESIGN_DIR)/src/\*.lef\]
>
> add_lefs -src \$lefs
>
> \# Now that the design is prepped and ready, we can run synthesis
> using following command
>
> run_synthesis

Screenshots of commands run

![image66](https://github.com/user-attachments/assets/b62865db-f585-4913-9ffb-6f78acede505)

![image67](https://github.com/user-attachments/assets/6c9eb1e1-1023-4014-baa6-93ef48225565)

7\. Remove/reduce the newly introduced violations with the introduction
of custom inverter cell by modifying design parameters.

Commands to view and change parameters to improve timing and run
synthesis

> \# Now once again we have to prep design so as to update variables
>
> prep -design picorv32a -tag 17_01_08-01 -overwrite
>
> \# Additional commands to include newly added lef to openlane flow
> merged.lef
>
> set lefs \[glob \$::env(DESIGN_DIR)/src/\*.lef\]
>
> add_lefs -src \$lefs
>
> \# Command to display current value of variable SYNTH_STRATEGY
>
> echo \$::env(SYNTH_STRATEGY)
>
> \# Command to set new value for SYNTH_STRATEGY
>
> set ::env(SYNTH_STRATEGY) \"DELAY 3\"
>
> \# Command to display current value of variable SYNTH_BUFFERING to
> check whether it\'s enabled
>
> echo \$::env(SYNTH_BUFFERING)
>
> \# Command to display current value of variable SYNTH_SIZING
>
> echo \$::env(SYNTH_SIZING)
>
> \# Command to set new value for SYNTH_SIZING
>
> set ::env(SYNTH_SIZING) 1
>
> \# Command to display current value of variable SYNTH_DRIVING_CELL to
> check whether it\'s the proper cell or not
>
> echo \$::env(SYNTH_DRIVING_CELL)
>
> \# Now that the design is prepped and ready, we can run synthesis
> using following command
>
> run_synthesis

Screenshot of merged.lef in tmp directory with our custom inverter as
macro

![image68](https://github.com/user-attachments/assets/02cd5bb0-e076-49a1-9fad-e6eb3b968717)

Screenshots of commands run

![image69](https://github.com/user-attachments/assets/55c69401-c444-439f-89d6-749a00f733fb)

Comparing to previously noted run values area has increased and worst
negative slack has become 0

![image70](https://github.com/user-attachments/assets/903af536-2972-4058-b812-97a0f4e64eae)

8\. Once synthesis has accepted our custom inverter, we can now run
floorplan and placement and verify the cell is accepted in PnR flow.

Now that our custom inverter is properly accepted in synthesis, we can
now run floorplan using following command

> \# Now we can run floorplan
>
> run_floorplan

Screenshots of command run

![image71](https://github.com/user-attachments/assets/89e97916-8560-4d6c-9db1-db643099c5e0)

Since we are facing unexpected un-explainable error while using run_floorplan command, we can instead use the following set of
commands available based on information from Desktop/work/tools/openlane_working_dir/openlane/scripts/tcl_commands/floorplan.tcl and
also based on Floorplan Commands section in Desktop/work/tools/openlane_working_dir/openlane/docs/source/OpenLANE_commands.md

\# Following commands are altogether sourced in \"run_floorplan\"
command

init_floorplan

place_io

tap_decap_or

Screenshots of commands run

![image72](https://github.com/user-attachments/assets/62ae355a-e3e6-48f9-b6a6-d467f8ad032a)

![image73](https://github.com/user-attachments/assets/19b29766-9b64-4982-93c6-a93a2a58a510)

![image74](https://github.com/user-attachments/assets/e1bb751c-217d-4de9-8bda-3f25c34a93c6)

Now that floorplan is done, we can do placement using following command

\# Now we are ready to run placement

run_placement

Screenshots of command run

![image74](https://github.com/user-attachments/assets/e1bb751c-217d-4de9-8bda-3f25c34a93c6)

![image75](https://github.com/user-attachments/assets/524c0255-27c6-4ccc-a7d6-8fad6aa5cfc0)

Commands to load placement def in magic in another terminal

> \# Change directory to path containing generated placement def
>
> cd
> Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-01_08-01/results/placement/
>
> \# Command to load the placement def in magic tool
>
> magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

Screenshot of placement def in magic

![image76](https://github.com/user-attachments/assets/8247459a-df13-47ab-b6c1-8623ed71feb9)

Screenshot of custom inverter inserted in placement def with proper
abutment

![image77](https://github.com/user-attachments/assets/fb7e6af1-a405-4e42-9643-a7c836079565)

Command for tkcon window to view internal layers of cells

	\# Command to view internal connectivity layers
	
	expand

Abutment of power pins with another cell from library clearly visible

 ![image78](https://github.com/user-attachments/assets/91160a21-2cd5-487f-9056-e8bd03127ef1)

![image79](https://github.com/user-attachments/assets/8def47eb-8bae-471b-9690-41e699a07870)

9\. Do post-synthesis timing analysis with OpenSTA tool.

Since we are having 0 wns after improved timing run, we are going to do
timing analysis on initial run of synthesis which has lots of violations
and no parameters were added to improve timing

Commands to invoke the OpenLANE flow include new lef and perform
synthesis

    \# Change directory to openlane flow directory

    cd Desktop/work/tools/openlane_working_dir/openlane

    \# Since we have aliased the long command to \'docker\' we can invoke
    the OpenLANE flow docker sub-system by just running this command

    docker

    \# Now that we have entered the OpenLANE flow contained docker
    sub-system we can invoke the OpenLANE flow in the Interactive mode using
    the following command

    ./flow.tcl -interactive

    \# Now that OpenLANE flow is open we have to input the required packages
    for proper functionality of the OpenLANE flow

    package require openlane 0.9

    \# Now the OpenLANE flow is ready to run any design and initially we
    have to prep the design creating some necessary files and directories
    for running a specific design which in our case is \'picorv32a\'

    prep -design picorv32a

    \# Additional commands to include newly added lef to openlane flow

    set lefs \[glob \$::env(DESIGN_DIR)/src/\*.lef\]

    add_lefs -src \$lefs

    \# Command to set new value for SYNTH_SIZING

    set ::env(SYNTH_SIZING) 1

    \# Now that the design is prepped and ready, we can run synthesis using
    following command

    run_synthesis

Commands run final screenshot

![image80](https://github.com/user-attachments/assets/aef5d6a4-c1a1-4413-bd90-89f0a460bdac)

Newly created pre_sta.conf for STA analysis in openlane directory

![image81](https://github.com/user-attachments/assets/2b3d422b-5c15-4eb7-98c0-f954e0aec421)

Newly created my_base.sdc for STA analysis in openlane/designs/picorv32a/src directory based on the
file openlane/scripts/base.sdc

![image82](https://github.com/user-attachments/assets/c948322b-d555-4698-bd03-918b10d4c467)

Commands to run STA in another terminal

    \# Change directory to openlane

    cd Desktop/work/tools/openlane_working_dir/openlane

    \# Command to invoke OpenSTA tool with script

    sta pre_sta.conf

Screenshots of commands run

![image83](https://github.com/user-attachments/assets/8cd3ace7-a66f-4556-9666-389547e53a40)

![image84](https://github.com/user-attachments/assets/19b5a127-ae2d-4cd2-832b-8ac4bf313c6f)

Since more fanout is causing more delay, we can add parameter to reduce
fanout and do synthesis again

Commands to include new lef and perform synthesis

> \# Now the OpenLANE flow is ready to run any design and initially we
> have to prep the design creating some necessary files and directories
> for running a specific design which in our case is \'picorv32a\'
>
> prep -design picorv32a -tag 25-03_18-52 -overwrite
>
> \# Additional commands to include newly added lef to openlane flow
>
> set lefs \[glob \$::env(DESIGN_DIR)/src/\*.lef\]
>
> add_lefs -src \$lefs
>
> \# Command to set new value for SYNTH_SIZING
>
> set ::env(SYNTH_SIZING)
>
> \# Command to set new value for SYNTH_MAX_FANOUT
>
> set ::env(SYNTH_MAX_FANOUT) 4
>
> \# Command to display current value of variable SYNTH_DRIVING_CELL to
> check whether it\'s the proper cell or not
>
> echo \$::env(SYNTH_DRIVING_CELL)
>
> \# Now that the design is prepped and ready, we can run synthesis
> using following command
>
> run_synthesis

Commands run final screenshot

![image85](https://github.com/user-attachments/assets/a5aae804-50bf-41f5-a487-4f30df42036c)

Commands to run STA in another terminal

    \# Change directory to openlane

    cd Desktop/work/tools/openlane_working_dir/openlane

    \# Command to invoke OpenSTA tool with script

    sta pre_sta.conf

10\. Make timing ECO fixes to remove all violations.

OA gate of drive strength 2 is driving 4 fanouts

![image86](https://github.com/user-attachments/assets/a57ad14b-4a73-48db-81b5-d2a966538e26)

Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4

    \# Reports all the connections to a net

    report_net -connections \_11643\_

    \# Checking command syntax

    help replace_cell

    \# Replacing cell

    replace_cell \_14481\_ sky130_fd_sc_hd\_\_or4_4

    \# Generating custom timing report

    report_checks -fields {net cap slew input_pins} -digits 4

Result - slack reduced

![image87](https://github.com/user-attachments/assets/8a0e3870-9a67-4934-b1d4-8696a0269f8d)

OR gate of drive strength 2 is driving 4 fanouts

![image88](https://github.com/user-attachments/assets/fe19eecd-955f-4d3e-9be3-87ca72ea615d)

Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4

    \# Reports all the connections to a net

    report_net -connections \_11672\_

    \# Replacing cell

    replace_cell \_14510 \_ sky130_fd_sc_hd\_\_or3_4

    \# Generating custom timing report

    report_checks -fields {net cap slew input_pins} -digits 4

Result - slack reduced

![image89](https://github.com/user-attachments/assets/2ea9c328-9c7c-4006-8fe0-d02a4154e444)

OR gate of drive strength 2 driving needs more drive strength

![image90](https://github.com/user-attachments/assets/8b5fb772-0b18-46f1-a847-40f0ec5ee6f2)

![image91](https://github.com/user-attachments/assets/c24c992e-0974-4fb1-900e-91e1fe5b797b)

Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4

    \# Reports all the connections to a net

    report_net -connections \_11672\_

    \# Replacing cell

    replace_cell \_14510\_ sky130_fd_sc_hd\_\_or4_4

    \# Generating custom timing report

    report_checks -fields {net cap slew input_pins} -digits 4

Result - slack reduced

![image91](https://github.com/user-attachments/assets/cb405bdc-69f2-4d49-b689-a380aa1b4f83)

OR gate of drive strength 2 driving OA gate has more delay

![image86](https://github.com/user-attachments/assets/13d91b84-3774-4395-9ccc-8821c248ec70)

Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4

    \# Reports all the connections to a net

    report_net -connections \_11643\_

    \# Replacing cell

    replace_cell \_14481\_ sky130_fd_sc_hd\_\_or4_4

    \# Generating custom timing report

    report_checks -fields {net cap slew input_pins} -digits 4

Result - slack reduced

![image92](https://github.com/user-attachments/assets/33917bc3-2a7a-426e-b7b4-882e161c9c7f)

![image93](https://github.com/user-attachments/assets/647378f9-fd23-49f8-9b3f-e93295d95907)

Commands to verify instance \_14881\_ is replaced with sky130_fd_sc_hd\_\_or4_4

    \# Generating custom timing report

    report_checks -from \_29052\_ -to \_30440\_ -through \_14506\_

Screenshot of replaced instance

![image94](https://github.com/user-attachments/assets/a049c1a5-6836-4858-b83d-2868fde6989d)

*We started ECO fixes at wns -23.9000 and now we stand at wns -22.980 we reduced around 910ps of violation*

11\. Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.

Now to insert this updated netlist to PnR flow and we can use write_verilog and overwrite the synthesis netlist but before that we are going to make a copy of the old old netlist

Commands to make copy of netlist

    \# Change from home directory to synthesis results directory

    cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/25-03_18-52/results/synthesis/

    \# List contents of the directory

    ls

    \# Copy and rename the netlist

    cp picorv32a.synthesis.v picorv32a.synthesis_old.v

    \# List contents of the directory

    ls

Screenshot of commands run

![image95](https://github.com/user-attachments/assets/55632b61-97f1-4a7e-96c6-d723eca46f69)

Commands to write verilog

    \# Check syntax

    help write_verilog

    \# Overwriting current synthesis netlist

    write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-01_14-04/results/synthesis/picorv32a.synthesis.v

    \# Exit from OpenSTA since timing analysis is done

    exit

Screenshot of commands run

![image96](https://github.com/user-attachments/assets/c378802b-cab8-4da8-b316-a43c99dd53b5)

Verified that the netlist is overwritten by checking that instance \_14506\_ is replaced with sky130_fd_sc_hd\_\_or4_4

![image97](https://github.com/user-attachments/assets/bb61d38e-6e07-42dd-a83c-7947aceef7b3)


Since we confirmed that netlist is replaced and will be loaded in PnR but since we want to follow up on the earlier 0 violation design, we are continuing with the clean design to further stages

Commands load the design and run necessary stages

    \# Now once again we have to prep design so as to update variables

    prep -design picorv32a -tag 17_01_14-04 -overwrite

    \# Additional commands to include newly added lef to openlane flow merged.lef

    set lefs \[glob \$::env(DESIGN_DIR)/src/\*.lef\]

    add_lefs -src \$lefs

    \# Command to set new value for SYNTH_STRATEGY

    set ::env(SYNTH_STRATEGY) \"DELAY 3\"

    \# Command to set new value for SYNTH_SIZING

    set ::env(SYNTH_SIZING) 1

    \# Now that the design is prepped and ready, we can run synthesis using following command

    run_synthesis

    \# Follwing commands are alltogather sourced in \"run_floorplan\" command

    init_floorplan

    place_io

    tap_decap_or

    \# Now we are ready to run placement

    run_placement

    \# Incase getting error

    unset ::env(LIB_CTS)

    \# With placement done we are now ready to run CTS

    run_cts

Screenshots of commands run

![image98](https://github.com/user-attachments/assets/e5f46cb2-2dfe-4e07-9a3b-e5391401cbf3)

![image99](https://github.com/user-attachments/assets/003bf77c-63dc-463e-b1c6-53f2b71df5a7)

![image100](https://github.com/user-attachments/assets/4cbf6b53-4cd4-4cbd-8273-a29327514553)

![image75](https://github.com/user-attachments/assets/524c0255-27c6-4ccc-a7d6-8fad6aa5cfc0)

![image101](https://github.com/user-attachments/assets/9cd1604f-3cc1-43a0-a330-a2198a003e3f)

 ![image102](https://github.com/user-attachments/assets/565cfb3d-cbc3-4193-b9c3-f1870518f311)

![image103](https://github.com/user-attachments/assets/dc6ed680-9eda-4087-8594-f7179a9043f4)

12\. Post-CTS OpenROAD timing analysis.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis with integrated OpenSTA in OpenROAD

    \# Command to run OpenROAD tool

    openroad

    \# Reading lef file

    read_lef /openLANE_flow/designs/picorv32a/runs/17-01_14-04/tmp/merged.lef

    \# Reading def file

    read_def /openLANE_flow/designs/picorv32a/runs/17-01_14-04/results/cts/picorv32a.cts.def

    \# Creating an OpenROAD database to work with

    write_db pico_cts.db

    \# Loading the created database in OpenROAD

    read_db pico_cts.db

    \# Read netlist post CTS

    read_verilog /openLANE_flow/designs/picorv32a/runs/17-01_14-04/results/synthesis/picorv32a.synthesis_cts.v

    \# Read library for design

    read_liberty \$::env(LIB_SYNTH_COMPLETE)

    \# Link design and library

    link_design picorv32a

    \# Read in the custom sdc we created

    read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

    \# Setting all clocks as propagated clocks

    set_propagated_clock \[all_clocks\]

    \# Check syntax of \'report_checks\' command

    help report_checks

    \# Generating custom timing report

    report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

    \# Exit to OpenLANE flow

    exit

Screenshots of commands run and timing report generated

![image104](https://github.com/user-attachments/assets/ad60f34b-8649-436a-9337-23390c1bbc36)

![image105](https://github.com/user-attachments/assets/a23a544a-c161-48c0-b99d-944fa4efda72)

![image106](https://github.com/user-attachments/assets/a35a4e4a-3ff3-47de-b526-9a6342aeb45e)

![image107](https://github.com/user-attachments/assets/47571f04-9a2a-4325-b8e3-daa093905416)

**13. Explore post-CTS OpenROAD timing analysis by removing \'sky130_fd_sc_hd\_\_clkbuf_1\' cell from clock buffer list variable \'CTS_CLK_BUFFER_LIST\'.**

Commands to be run in OpenLANE flow to do OpenROAD timing analysis after changing CTS_CLK_BUFFER_LIST

    \# Checking current value of \'CTS_CLK_BUFFER_LIST\'

    echo \$::env(CTS_CLK_BUFFER_LIST)

    \# Removing \'sky130_fd_sc_hd\_\_clkbuf_1\' from the list

    set ::env(CTS_CLK_BUFFER_LIST) \[lreplace \$::env(CTS_CLK_BUFFER_LIST) 0 0\]

    \# Checking current value of \'CTS_CLK_BUFFER_LIST\'

    echo \$::env(CTS_CLK_BUFFER_LIST)

    \# Checking current value of \'CURRENT_DEF\'

    echo \$::env(CURRENT_DEF)

    \# Setting def as placement def

    set ::env(CURRENT_DEF)/openLANE_flow/designs/picorv32a/runs/17-01_14-04/results/placement/picorv32a.placement.def

    \# Run CTS again

    run_cts

    \# Checking current value of \'CTS_CLK_BUFFER_LIST\'

    echo \$::env(CTS_CLK_BUFFER_LIST)

    \# Command to run OpenROAD tool

    openroad

    \# Reading lef file

    read_lef /openLANE_flow/designs/picorv32a/runs/17-01_14-04/tmp/merged.lef

    \# Reading def file

    read_def /openLANE_flow/designs/picorv32a/runs/17-01_14-04/results/cts/picorv32a.cts.def

    \# Creating an OpenROAD database to work with

    write_db pico_cts1.db

    \# Loading the created database in OpenROAD

    read_db pico_cts.db

    \# Read netlist post CTS

    read_verilog /openLANE_flow/designs/picorv32a/runs/17-01_14-04/results/synthesis/picorv32a.synthesis_cts.v

    \# Read library for design

    read_liberty \$::env(LIB_SYNTH_COMPLETE)

    \# Link design and library

    link_design picorv32a

    \# Read in the custom sdc we created

    read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

    \# Setting all cloks as propagated clocks

    set_propagated_clock \[all_clocks\]

    \# Generating custom timing report

    report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

    \# Report hold skew

    report_clock_skew -hold

    \# Report setup skew

    report_clock_skew -setup

    \# Exit to OpenLANE flow

    exit

    \# Checking current value of \'CTS_CLK_BUFFER_LIST\'

    echo \$::env(CTS_CLK_BUFFER_LIST)

    \# Inserting \'sky130_fd_sc_hd\_\_clkbuf_1\' to first index of list

    set ::env(CTS_CLK_BUFFER_LIST) \[linsert \$::env(CTS_CLK_BUFFER_LIST) 0
    sky130_fd_sc_hd\_\_clkbuf_1\]

    \# Checking current value of \'CTS_CLK_BUFFER_LIST\'

    echo \$::env(CTS_CLK_BUFFER_LIST)

Screenshots of commands run and timing report generated

![image108](https://github.com/user-attachments/assets/03d53bd1-eb0d-4ec9-a5e5-12b08a0e10f8)

![image109](https://github.com/user-attachments/assets/b0aa8f36-13d3-443d-8f2a-f272342e231e)

![image110](https://github.com/user-attachments/assets/f4c7951d-494a-4534-9c30-44083163e954)

![image111](https://github.com/user-attachments/assets/6e1da316-9d00-4359-a33f-31a776b379d6)

![image112](https://github.com/user-attachments/assets/c5cd2db1-0d1f-4690-b503-3ed4d560a958)

![image113](https://github.com/user-attachments/assets/c803db0c-da5b-4718-aa59-145065089ed6)

## Section 5 - Final steps for RTL2GDS using tritonRoute and openSTA (20/01/2025 - 22/01/2025)

### Implementation

### Section 5 tasks: -

1.  Perform generation of Power Distribution Network (PDN) and explore
    the PDN layout.

2.  Perform detailed routing using TritonRoute.

3.  Post-Route parasitic extraction using SPEF extractor.

4.  Post-Route OpenSTA timing analysis with the extracted parasitics of
    the route.

-   All section 5 logs, reports and results can be found in following
    run folder:

[Section 5 runs-18-01_13-08](openlane/designs/picorv32a/runs/18-01_13-08)

1\. Perform generation of Power Distribution Network (PDN) and explore the PDN layout.

Commands to perform all necessary stages up until now

    \# Change directory to openlane flow directory

    cd Desktop/work/tools/openlane_working_dir/openlane

    \# Since we have aliased the long command to \'docker\' we can invoke the OpenLANE flow docker sub-system by just running this command

    docker

    \# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using
    the following command

    ./flow.tcl -interactive

    \# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow

    package require openlane 0.9

    \# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific 
    design which in our case is \'picorv32a\'

    prep -design picorv32a

    \# Additional commands to include newly added lef to openlane flow merged.lef

    set lefs \[glob \$::env(DESIGN_DIR)/src/\*.lef\]

    add_lefs -src \$lefs

    \# Command to set new value for SYNTH_STRATEGY

    set ::env(SYNTH_STRATEGY) \"DELAY 3\"

    \# Command to set new value for SYNTH_SIZING

    set ::env(SYNTH_SIZING) 1

    \# Now that the design is prepped and ready, we can run synthesis using following command

    run_synthesis

    \# Following commands are alltogather sourced in \"run_floorplan\" command

    init_floorplan

    place_io

    tap_decap_or

    \# Now we are ready to run placement

    run_placement

    \# Incase getting error

    unset ::env(LIB_CTS)

    \# With placement done we are now ready to run CTS

    run_cts

    \# Now that CTS is done we can do power distribution network

    gen_pdn

Screenshots of power distribution network run

![image114](https://github.com/user-attachments/assets/23d33dff-77c6-4a18-a57f-27b91c19b35d)

![image115](https://github.com/user-attachments/assets/0ac69559-114f-4292-a0eb-e680d4ecb6f7)

Commands to load PDN def in magic in another terminal

    \# Change directory to path containing generated PDN def

    cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/18-01_13_08/tmp/floorplan/

    \# Command to load the PDN def in magic tool

    magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 14-pdn.def &

Screenshots of PDN def

![image116](https://github.com/user-attachments/assets/5a2b671f-c24a-414c-8e22-d41aec1bd421)

![image117](https://github.com/user-attachments/assets/f44f1b54-06d6-49d7-8cf4-65e745a21b10)

2\. Perfrom detailed routing using TritonRoute and explore the routed layout.

Command to perform routing

    \# Check value of \'CURRENT_DEF\'

    echo \$::env(CURRENT_DEF)

    \# Check value of \'ROUTING_STRATEGY\'

    echo \$::env(ROUTING_STRATEGY)

    \# Command for detailed route using TritonRoute

    run_routing

Screenshots of routing run

![image118](https://github.com/user-attachments/assets/c52dadae-03cf-4d66-b211-7ec05608702e)

![image119](https://github.com/user-attachments/assets/bb7a5a6c-6d5f-40fb-aa84-71b3ea82a199)

Commands to load routed def in magic in another terminal

    \# Change directory to path containing routed def

    cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/18-01_13-08/results/routing/

    \# Command to load the routed def in magic tool

    magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.def &

Screenshots of routed def

![image120](https://github.com/user-attachments/assets/e86f920f-da9f-42e5-89e7-efbafcf10d35)

![image121](https://github.com/user-attachments/assets/aca68bdf-13f2-4c1c-b763-3b0022f8e287)

![image122](https://github.com/user-attachments/assets/15fc935c-db0d-43b4-a774-693b1d747eb4)

![image123](https://github.com/user-attachments/assets/cb7b95b5-a475-4091-bcc8-41603fed0547)

3\. Post-Route parasitic extraction using SPEF extractor.

Commands for SPEF extraction using external tool

    \# Change directory

    cd Desktop/work/tools/SPEF_EXTRACTOR

    \# Command extract spef

    python3 main.py /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/18-01_13-08/tmp/merged.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/18-01_13-08/results/routing/picorv32a.def

4\. Post-Route OpenSTA timing analysis with the extracted parasitics of the route.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis with integrated OpenSTA in OpenROAD

	\# Command to run OpenROAD tool
	
	openroad
	
	\# Reading lef file
	
	read_lef /openLANE_flow/designs/picorv32a/runs/18-01_13-08/tmp/merged.lef
	
	\# Reading def file
	
	read_def /openLANE_flow/designs/picorv32a/runs/18-01_13-08/results/routing/picorv32a.def
	
	\# Creating an OpenROAD database to work with
	
	write_db pico_route.db
	
	\# Loading the created database in OpenROAD
	
	read_db pico_route.db
	
	\# Read netlist post CTS
	
	read_verilog /openLANE_flow/designs/picorv32a/runs/18-01_13-08/results/synthesis/picorv32a.synthesis_preroute.v
	
	\# Read library for design
	
	read_liberty \$::env(LIB_SYNTH_COMPLETE)
	
	\# Link design and library
	
	link_design picorv32a
	
	\# Read in the custom sdc we created
	
	read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
	
	\# Setting all cloks as propagated clocks
	
	set_propagated_clock \[all_clocks\]
	
	\# Read SPEF
	
	read_spef /openLANE_flow/designs/picorv32a/runs/18-01_13-08/results/routing/picorv32a.spef
	
	\# Generating custom timing report
	
	report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
	
	\# Exit to OpenLANE flow
	
	exit

Screenshots of commands run and timing report generated

![image124](https://github.com/user-attachments/assets/f42ffb58-03da-4132-8330-b893cf1745a5)

![image125](https://github.com/user-attachments/assets/8a96eff1-c906-4202-834c-e0a5ed49acf1)

**Certificate**



**Acknowledgements**

-   [Kunal Ghosh](https://github.com/kunalg123), Co-founder, VSD Corp.Pvt. Ltd.

-   [Nickson P Jose](https://github.com/nickson-jose/), Physical Design Engineer, Intel Corporation.

-   [R. Timothy Edwards](https://github.com/RTimothyEdwards), Senior Vice President of Analog and Design, Efabless Corporation.
