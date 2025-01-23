# 

![image](./media/image1.png)

**Digital VLSI SoC Design and Planning**

2 Week digital VLSI SoC design and planning workshop with complete
RTL2GDSII flow organized by VSD in collaboration with NASSCOM.
### Theory 

**Package**

-   In any embedded board, the \"chip\" we observe is actually the
    PACKAGE, which encases and protects the actual chip. The chip,
    located at the package center, connects to the package via WIRE
    BONDING, a basic wired connection method.

![image](./media/image2.png)

               A simple illustration of Arduino

![](./media/image3.png)

**Chip**

-   Inside the chip, signals flow through PADS to and from the external
    world. The area surrounded by pads is the CORE, housing the chip\'s
    digital logic. Together, the core and pads form the DIE, the
    fundamental semiconductor manufacturing unit.

-   Semiconductor chips are produced in FOUNDRIES, which also create
    FOUNDRY IPs---intellectual properties requiring specific expertise.
    Repeatable logic blocks within chips are called MACROS.

![](./media/image4.png)

                        Parameters of the chip

**ISA (Instruction Set Architecture)**

To execute a C program on hardware, a series of steps are followed:

1\. The program is compiled into assembly language, such as RISC-V ISA.\
2. Assembly code is translated into machine language (binary 0s and
1s).\
3. Using RTL (Hardware Description Language), RISC-V specifications are
implemented.\
4. The RTL is processed through a standard PnR flow, producing the final
layout (GDSII format).

5. System software, including the OS, compiler, and assembler, convert application code into binary language. For example, a stopwatch app on a RISC-V core transitions from C functions (via OS) to RISC-V instructions (via compiler) and binary code (via assembler), ready for hardware
execution.

![Screenshot (278)](./media/image5.png)

-   There are mainly 3 different parts in this course. They are:

1.  RISC-V ISA

2.  RTL and synthesis of RISC-V based CPU core - picorv32

3.  Physical design implementation of picorv32

![Screenshot (283)](./media/image6.png)

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

![image](./media/image1.png)

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

![stackup](./media/image7.png)

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

Flop Ratio =
$\frac{Number\ of\ D\ Flip\ Flops}{Total\ Number\ of\ Cells}$

Percentage of DFF′s = Flop Ratio∗100

-   All section 1 logs, reports and results can be found in following
    run folder:

In the runs folder [Section
1-Run-17-01_08-01](openlane/designs/picorv32a/runs/17-01_08-01)

-   Run \'picorv32a\' design synthesis using OpenLANE flow and generate
    necessary outputs.

Commands to invoke the OpenLANE flow and perform synthesis

\# Change directory to openlane flow directory

cd Desktop/work/tools/openlane_working_dir/openlane

\# alias docker=\'docker run -it -v \$(pwd):/openLANE_flow -v
\$PDK_ROOT: \$PDK_ROOT -e PDK_ROOT=\$PDK_ROOT -u \$(id -u \$USER): \$(id
-g \$USER) efabless/openlane: v0.21\'

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

\# Initially we have to prep the design creating some necessary files
and directories for running a specific design which in our case is
\'picorv32a\'

prep -design picorv32a

\# Now that the design is prepped and ready, we can run synthesis using
following command

run_synthesis

\# Exit from OpenLANE flow

exit

\# Exit from OpenLANE flow docker sub-system

exit

Screenshots of running each
commands![](./media/image8.png)

![](./media/image9.png)

2\. Calculate the flop ratio.

Screenshots of synthesis statistics report file with required values
highlighted

![](./media/image10.png){width="5.201609798775153in"
height="4.195269028871391in"}

![](./media/image11.png)

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

\# Since we have aliased the long command to \'docker\' we can invoke
the OpenLANE flow docker sub-system by just running this command

docker

\# To invoke the OpenLANE flow in the Interactive mode using the
following command

./flow.tcl -interactive

\# Now that OpenLANE flow is open we have to input the required packages
for proper functionality of the OpenLANE flow

package require openlane 0.9

\# Now the OpenLANE flow is ready to run any design and initially we
have to prep the design creating some necessary files and directories
for running a specific design which in our case is \'picorv32a\'

prep -design picorv32a

\# Now that the design is prepped and ready, we can run synthesis using
following command

run_synthesis

\# Now we can run floorplan

run_floorplan

Screenshot of floorplan run

![](./media/image12.png)

![](./media/image13.png)

**2. Calculate the die area in microns from the values in floorplan
def.**

Screenshot of contents of floorplan def

![](./media/image14.png)

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

![](./media/image15.png)

Equidistant placement of ports

![](./media/image16.png)

Port layer as set through config.tcl

![](./media/image17.png)

![](./media/image18.png)

Decap Cells and Equidistant Tap Cells

![](./media/image16.png)

Unplaced standard cells at the origin

![](./media/image19.png)

**4. Run \'picorv32a\' design congestion aware placement using OpenLANE
flow and generate necessary outputs.**

Command to run placement

\# To run placement by default different switchs are available for other aware operations

run_placement

Screenshots of placement run

![](./media/image20.png)

![](./media/image21.png)

5\. Load generated placement def in magic tool and explore the
placement.

Commands to load placement def in magic in another terminal

\# Change directory to path containing generated placement def

cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/13-01_08-24/results/placement/

\# Command to load the placement def in magic tool

magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

Screenshots of Placement def in magic

![](./media/image22.png)

Standard cells legally placed

![](./media/image23.png)

Commands to exit from current run

\# Exit from OpenLANE flow

exit

\# Exit from OpenLANE flow docker sub-system

exit

## Section 3 - Design library cell using Magic Layout and ngspice characterization (13/01/2025 - 16/01/2025)

### Implementation

## Section 3 tasks: -

1.  Clone custom inverter standard cell design from github
    repository: [Standard cell design and characterization using
    OpenLANE
    flow.](https://github.com/nickson-jose/vsdstdcelldesign.git)

2.  Load the custom inverter layout in magic and explore.

3.  Spice extraction of inverter in magic.

4.  Editing the spice model file for analysis through simulation.

5.  Post-layout ngspice simulations.

6.  Find problem in the DRC section of the old magic tech file for the
    skywater process and fix them.

## Section 3 - Tasks 1 to 5 files, reports and logs can be found in the following folder.

[Section 3 - For task 1 to 5 -
vsdstdcelldesign](openlane/vsdstdcelldesign)

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
>
> ls
> \# Command to open custom inverter layout in magic
>
> magic -T sky130A.tech sky130_inv.mag &

Screenshot of commands run

![](./media/image24.png)

2\. Load the custom inverter layout in magic and explore.

Screenshot of custom inverter layout in magic

![A computer screen shot of a computer Description automatically
generated](./media/image25.png)

NMOS and PMOS identified

![A computer screen shot of a computer screen Description automatically
generated](./media/image26.png)
![A computer screen shot of a computer Description automatically
generated](./media/image27.png)

3\. Spice extraction of inverter in magic.

Commands for spice extraction of the custom inverter layout to be used
in tkcon window of magic

    \# Check current directory

    pwd

    \# Extraction command to extract to. ext format

    extract all

    \# Before converting ext to spice this command enable the parasitic
    extraction also

    ext2spice cthresh 0 rthresh 0

    \# Converting to ext to spice

    ext2spice

Screenshot of tkcon window after running above commands

![A computer screen shot of a
computer](./media/image28.png)

Screenshot of created spice file

![A screenshot of a computer Description automatically
generated](./media/image29.png)

4\. Editing the spice model file for analysis through simulation.

Measuring unit distance in layout grid

-   If grid is not seen, then go to window 🡪 press Grid on

![](./media/image30.png)

Final edited spice file ready for ngspice simulation

![](./media/image31.png)

**5. Post-layout ngspice simulations.**

Commands for ngspice simulation

> \# Command to directly load spice file for simulation to ngspice
>
> ngspice sky130_inv.spice
>
> \# Now that we have entered ngspice with the simulation spice file
> loaded we just have to load the plot
>
> plot y vs time a

Screenshots of ngspice run

![A screenshot of a computer program Description automatically
generated](./media/image32.png)

Screenshot of generated plot

![A screen shot of a graph Description automatically
generated](./media/image33.png)

Rise transition time calculation

Rise transition time = Time taken for output to rise to 80% −
Time taken for output to rise to 20%

                              20% of output=660 mV
                              80% of output=2.64 V

20% Screenshots

![A graph on a black background Description automatically
generated](./media/image34.png)

80% Screenshots

![](./media/image35.png)

![A screenshot of a computer Description automatically
generated](./media/image36.png)

*       Rise transition time = 2.180−2.119 = 0.061 ns = 61 ps*

Fall transition time calculation

Fall transition time=Time taken for output to fall to 20% − Time taken for output to fall to 80%

                               20% of output=660 mV
                               80% of output=2.64 V

20% Screenshots

![A screen shot of a graph Description automatically
generated](./media/image37.png)

80% Screenshots

![A screen shot of a graph Description automatically
generated](./media/image38.png)

![A screenshot of a computer Description automatically
generated](./media/image36.png)

    Fall transition time = 4.0779 − 4.0497 = 0.0331 ns = 33.1 ps

Rise Cell Delay Calculation

Rise Cell Delay=Time taken for output to rise to 50% − Time taken for input to fall to 50%

                           50% of 3.3 V=1.65 V

50% Screenshots

![](./media/image39.png)

![A computer screen shot of a black screen Description automatically
generated](./media/image40.png)

       Rise Cell Delay = 2.21144−2.15008 = 0.06136 ns = 61.36 ps

Fall Cell Delay Calculation

*Fall Cell Delay=Time taken for output to fall to 50% − Time taken for input to rise to 50%*

                      50% of 3.3 V=1.65 V

50% Screenshot

![A screen shot of a graph Description automatically
generated](./media/image41.png)

![A computer screen shot of a black screen Description automatically
generated](./media/image40.png)

      Fall Cell Delay = 4.0779 − 4.049 = 0.0282 ns = 28.2 ps

6\. Find problem in the DRC section of the old magic tech file for the
skywater process and fix them.

Link to Sky130 Periphery rules:
<https://skywaterpdk.readthedocs.io/en/main/rules/periphery.html>

Commands to download and view the corrupted skywater process magic tech
file and associated files to perform drc corrections

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

![A computer screen shot of a building Description automatically
generated](./media/image42.png){width="7.702309711286089in"
height="5.013903105861767in"}

Screenshot of .magicrc file

![A screenshot of a computer Description automatically
generated](./media/image43.png)

**Incorrectly implemented poly.9 simple rule correction**

Screenshot of poly rules

![](./media/image44.png)

Incorrectly implemented poly.9 rule no drc violation even though spacing
\< 0.48u

![A computer screen shot of a computer Description automatically
generated](./media/image45.png)

New commands inserted in sky130A.tech file to update drc

![](./media/image46.png)

![](./media/image47.png)

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

![](./media/image48.png)

**Incorrectly implemented difftap.2 simple rule correction**

Screenshot of difftap rules

![](./media/image49.png)

Incorrectly implemented difftap.2 rule no drc violation even though
spacing \< 0.42u

![](./media/image50.png)

New commands inserted in sky130A.tech file to update drc

![](./media/image51.png)

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

![](./media/image52.png)

Incorrectly implemented nwell.4 rule no drc violation even though no tap
present in nwell

![](./media/image53.png) 

New commands inserted in sky130A.tech file to update drc

![A screenshot of a computer Description automatically
generated](./media/image54.png)

![A screenshot of a computer Description automatically
generated](./media/image55.png)

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

![A screenshot of a computer Description automatically
generated](./media/image56.png)

## Section 4 - Pre-layout timing analysis and importance of good clock tree (16/01/2025 - 19/01/2025)

### Implementation

### Section 4 tasks: -

1.  Fix up small DRC errors and verify the design is ready to be
    inserted into our flow.

2.  Save the finalized layout with custom name and open it.

3.  Generate lef from the layout.

4.  Copy the newly generated lef and associated required lib files to
    \'picorv32a\' design \'src\' directory.

5.  Edit \'config.tcl\' to change lib file and add the new extra lef
    into the openlane flow.

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

![](./media/image57.png)

Commands for tkcon window to set grid as tracks of locali layer

> \# Get syntax for grid command
>
> help grid
>
> \# Set grid values accordingly
>
> grid 0.46um 0.34um 0.23um 0.17um

Screenshot of commands run

![](./media/image58.png)

Condition 1 verified

![A screenshot of a computer Description automatically
generated](./media/image59.png)

Condition 2 verified

*Horizontal track pitch=0.46 um*

![A screenshot of a computer Description automatically
generated](./media/image60.png)

*Width of standard cell=1.38 um=0.46∗3*

Condition 3 verified

*Vertical track pitch=0.34 um*

![A computer screen shot of a computer Description automatically
generated](./media/image61.png)

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

![](./media/image62.png)

3\. Generate lef from the layout.

Command for tkcon window to write lef

> \# lef command
>
> lef write

Screenshot of newly created lef file

![](./media/image63.png)

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
> cp libs/sky130_fd_sc_hd\_\_\*
> \~/Desktop/work/tools/openlane_working_dir/
> openlane/designs/picorv32a/src/
>
> \# List and check whether it\'s copied
>
> ls
> \~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

Screenshot of commands run

![](./media/image64.png)

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

![](./media/image65.png)

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

![](./media/image66.png){width="6.6108398950131235in"
height="6.403169291338583in"}

![](./media/image67.png){width="6.8537992125984255in"
height="6.638824365704287in"}

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

![](./media/image68.png)

Screenshots of commands run

![](./media/image69.png)

Comparing to previously noted run values area has increased and worst
negative slack has become 0

![](./media/image70.png)

8\. Once synthesis has accepted our custom inverter, we can now run
floorplan and placement and verify the cell is accepted in PnR flow.

Now that our custom inverter is properly accepted in synthesis, we can
now run floorplan using following command

> \# Now we can run floorplan
>
> run_floorplan

Screenshots of command run

![A screenshot of a computer Description automatically
generated](./media/image71.png)

Since we are facing unexpected un-explainable error while using run_floorplan command, we can instead use the following set of
commands available based on information from Desktop/work/tools/openlane_working_dir/openlane/scripts/tcl_commands/floorplan.tcl and
also based on Floorplan Commands section in Desktop/work/tools/openlane_working_dir/openlane/docs/source/OpenLANE_commands.md

\# Following commands are altogether sourced in \"run_floorplan\"
command

init_floorplan

place_io

tap_decap_or

Screenshots of commands run

![](./media/image72.png)

![](./media/image73.png)

![](./media/image74.png)

Now that floorplan is done, we can do placement using following command

\# Now we are ready to run placement

run_placement

Screenshots of command run

![](./media/image74.png)

![](./media/image75.png)

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

![A screen shot of a computer Description automatically
generated](./media/image76.png)

Screenshot of custom inverter inserted in placement def with proper
abutment

![A screenshot of a computer Description automatically
generated](./media/image77.png)

Command for tkcon window to view internal layers of cells

\# Command to view internal connectivity layers

expand

Abutment of power pins with another cell from library clearly visible

![A computer screen shot of a computer screen Description automatically
generated](./media/image78.png)

![A screenshot of a computer Description automatically
generated](./media/image79.png)

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

![](./media/image80.png)

Newly created pre_sta.conf for STA analysis in openlane directory

![A screenshot of a computer Description automatically
generated](./media/image81.png)}

Newly created my_base.sdc for STA analysis in openlane/designs/picorv32a/src directory based on the
file openlane/scripts/base.sdc

![A screenshot of a computer Description automatically
generated](./media/image82.png)

Commands to run STA in another terminal

    \# Change directory to openlane

    cd Desktop/work/tools/openlane_working_dir/openlane

    \# Command to invoke OpenSTA tool with script

    sta pre_sta.conf

Screenshots of commands run

![](./media/image83.png)

![](./media/image84.png)

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

![A screenshot of a computer Description automatically
generated](./media/image85.png)
Commands to run STA in another terminal

    \# Change directory to openlane

    cd Desktop/work/tools/openlane_working_dir/openlane

    \# Command to invoke OpenSTA tool with script

    sta pre_sta.conf

10\. Make timing ECO fixes to remove all violations.

OA gate of drive strength 2 is driving 4 fanouts

![](./media/image86.png)

Commands to perform analysis and optimize timing by replacing with OR
gate of drive strength 4

    \# Reports all the connections to a net

    report_net -connections \_11643\_

    \# Checking command syntax

    help replace_cell

    \# Replacing cell

    replace_cell \_14481\_ sky130_fd_sc_hd\_\_or4_4

    \# Generating custom timing report

    report_checks -fields {net cap slew input_pins} -digits 4

Result - slack reduced

![](./media/image87.png)

OR gate of drive strength 2 is driving 4 fanouts

![](./media/image88.png)

Commands to perform analysis and optimize timing by replacing with OR
gate of drive strength 4

    \# Reports all the connections to a net

    report_net -connections \_11672\_

    \# Replacing cell

    replace_cell \_14510 \_ sky130_fd_sc_hd\_\_or3_4

    \# Generating custom timing report

    report_checks -fields {net cap slew input_pins} -digits 4

Result - slack reduced

![](./media/image89.png)

OR gate of drive strength 2 driving needs more drive strength

![](./media/image90.png)

![](./media/image91.png)

Commands to perform analysis and optimize timing by replacing with OR
gate of drive strength 4

    \# Reports all the connections to a net

    report_net -connections \_11672\_

    \# Replacing cell

    replace_cell \_14510\_ sky130_fd_sc_hd\_\_or4_4

    \# Generating custom timing report

    report_checks -fields {net cap slew input_pins} -digits 4

Result - slack reduced

![](./media/image91.png)

OR gate of drive strength 2 driving OA gate has more delay

![](./media/image86.png)

Commands to perform analysis and optimize timing by replacing with OR
gate of drive strength 4

    \# Reports all the connections to a net

    report_net -connections \_11643\_

    \# Replacing cell

    replace_cell \_14481\_ sky130_fd_sc_hd\_\_or4_4

    \# Generating custom timing report

    report_checks -fields {net cap slew input_pins} -digits 4

Result - slack reduced

![A screenshot of a computer Description automatically
generated](./media/image92.png)

![](./media/image93.png)

Commands to verify instance \_14881\_ is replaced
with sky130_fd_sc_hd\_\_or4_4

    \# Generating custom timing report

    report_checks -from \_29052\_ -to \_30440\_ -through \_14506\_

Screenshot of replaced instance

![A screenshot of a computer Description automatically
generated](./media/image94.png)

*We started ECO fixes at wns -23.9000 and now we stand at wns -22.980 we
reduced around 910ps of violation*

11\. Replace the old netlist with the new netlist generated after timing
ECO fix and implement the floorplan, placement and cts.

Now to insert this updated netlist to PnR flow and we can use write_verilog and overwrite the synthesis netlist but before that we
are going to make a copy of the old old netlist

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

![](./media/image95.png)

Commands to write verilog

    \# Check syntax

    help write_verilog

    \# Overwriting current synthesis netlist

    write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/25-03_18-52/results/synthesis/picorv32a.synthesis.v

    \# Exit from OpenSTA since timing analysis is done

    exit

Screenshot of commands run

![](./media/image96.png)

Verified that the netlist is overwritten by checking that
instance \_14506\_ is replaced with sky130_fd_sc_hd\_\_or4_4

![](./media/image97.png)

Since we confirmed that netlist is replaced and will be loaded in PnR
but since we want to follow up on the earlier 0 violation design, we are
continuing with the clean design to further stages

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

![](./media/image98.png)

![](./media/image99.png)

![](./media/image100.png)

![](./media/image75.png)

![](./media/image101.png)

![](./media/image102.png)

![](./media/image103.png)

12\. Post-CTS OpenROAD timing analysis.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis with
integrated OpenSTA in OpenROAD

    \# Command to run OpenROAD tool

    openroad

    \# Reading lef file

    read_lef /openLANE_flow/designs/picorv32a/runs/24-03_10-03/tmp/merged.lef

    \# Reading def file

    read_def /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/cts/picorv32a.cts.def

    \# Creating an OpenROAD database to work with

    write_db pico_cts.db

    \# Loading the created database in OpenROAD

    read_db pico_cts.db

    \# Read netlist post CTS

    read_verilog /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/synthesis/picorv32a.synthesis_cts.v

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

    report_checks -path_delay min_max -fields {slew trans net cap
    input_pins} -format full_clock_expanded -digits 4

    \# Exit to OpenLANE flow

    exit

Screenshots of commands run and timing report generated

![](./media/image104.png)

![](./media/image105.png)

![](./media/image106.png)

![](./media/image107.png)

**13. Explore post-CTS OpenROAD timing analysis by removing \'sky130_fd_sc_hd\_\_clkbuf_1\' cell from clock buffer list variable
\'CTS_CLK_BUFFER_LIST\'.**

Commands to be run in OpenLANE flow to do OpenROAD timing analysis after changing CTS_CLK_BUFFER_LIST

    \# Checking current value of \'CTS_CLK_BUFFER_LIST\'

    echo \$::env(CTS_CLK_BUFFER_LIST)

    \# Removing \'sky130_fd_sc_hd\_\_clkbuf_1\' from the list

    set ::env(CTS_CLK_BUFFER_LIST) \[lreplace \$::env(CTS_CLK_BUFFER_LIST) 0
    0\]

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

    read_verilog /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/synthesis/picorv32a.synthesis_cts.v

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

![](./media/image108.png)

![](./media/image109.png)

![](./media/image110.png)

![](./media/image111.png)

![](./media/image112.png)

![](./media/image113.png)

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

[Section 5
runs-18-01_13-08](openlane/designs/picorv32a/runs/18-01_13-08)

1\. Perform generation of Power Distribution Network (PDN) and explore
the PDN layout.

Commands to perform all necessary stages up until now

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
    merged.lef

    set lefs \[glob \$::env(DESIGN_DIR)/src/\*.lef\]

    add_lefs -src \$lefs

    \# Command to set new value for SYNTH_STRATEGY

    set ::env(SYNTH_STRATEGY) \"DELAY 3\"

    \# Command to set new value for SYNTH_SIZING

    set ::env(SYNTH_SIZING) 1

    \# Now that the design is prepped and ready, we can run synthesis using
    following command

    run_synthesis

    \# Following commands are alltogather sourced in \"run_floorplan\"
    command

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

![](./media/image114.png)

![](./media/image115.png)

Commands to load PDN def in magic in another terminal

    \# Change directory to path containing generated PDN def

    cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/18-01_13_08/tmp/floorplan/

    \# Command to load the PDN def in magic tool

    magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 14-pdn.def &

Screenshots of PDN def

![](./media/image116.png)

![](./media/image117.png)

2\. Perfrom detailed routing using TritonRoute and explore the routed
layout.

Command to perform routing

    \# Check value of \'CURRENT_DEF\'

    echo \$::env(CURRENT_DEF)

    \# Check value of \'ROUTING_STRATEGY\'

    echo \$::env(ROUTING_STRATEGY)

    \# Command for detailed route using TritonRoute

    run_routing

Screenshots of routing run

![](./media/image118.png)

![](./media/image119.png)

Commands to load routed def in magic in another terminal

    \# Change directory to path containing routed def

    cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/18-01_13-08/results/routing/

    \# Command to load the routed def in magic tool

    magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.def &

Screenshots of routed def

![](./media/image120.png)

![](./media/image121.png)

![](./media/image122.png)

![](./media/image123.png)

3\. Post-Route parasitic extraction using SPEF extractor.

Commands for SPEF extraction using external tool

    \# Change directory

    cd Desktop/work/tools/SPEF_EXTRACTOR

    \# Command extract spef

    python3 main.py /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/18-01_13-08/tmp/merged.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/18-01_13-08/results/routing/picorv32a.def

4\. Post-Route OpenSTA timing analysis with the extracted parasitics of
the route.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis with
integrated OpenSTA in OpenROAD

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

![](./media/image124.png)

![](./media/image125.png)

**Certificate**

**Acknowledgements**

-   [Kunal Ghosh](https://github.com/kunalg123), Co-founder, VSD Corp.
    Pvt. Ltd.

-   [Nickson P Jose](https://github.com/nickson-jose/), Physical Design
    Engineer, Intel Corporation.

-   [R. Timothy Edwards](https://github.com/RTimothyEdwards), Senior
    Vice President of Analog and Design, Efabless Corporation.
