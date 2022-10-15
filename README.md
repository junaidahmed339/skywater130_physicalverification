# Physical Verification using SKY130
# Table of Contents

1. Lab1 (Tool installation and basic LVS/DRC design flow)
   - PV_D1SK2_L1 - Check Tool Installations
   - PV_D1SK2_L2 - Creating Sky130 Device Layout In Magic
   - PV_D1SK2_L3 - Creating Simple Schematic In Xschem
   - PV_D1SK2_L4 - Creating Symbol And Exporting Schematic In Xschem
   - PV_D1SK2_L5 - Importing Schematic To Layout And Inverter Layout Steps
   - PV_D1SK2_L6 - Final DRC/LVS Checks And Post Layout Simulations
  
2. Lab2 (Labs for GDS read/write, extraction, DRC, LVS and XOR setup)
   - PV_D2SK2_L1 - GDS Read
   - PV_D2SK2_L2 - Ports
   - PV_D2SK2_L3 - Abstract Views
   - PV_D2SK2_L4 - Basic Extraction
   - PV_D2SK2_L5 - Setup For DRC
   - PV_D2SK2_L6 - Setup For LVS
   - PV_D2SK2_L7 - Setup For XOR

3. Lab3 (Labs for all DRC rules)
   - PV_D3SK2_L1 - Lab For Width Rule And Spacing Rule
   - PV_D3SK2_L2 - Lab For Wide Spacing Rule And Notch Rule
   - PV_D3SK2_L3 - Lab For Via Size, Multiple Vias, Via Overlap and Autogenerate Vias
   - PV_D3SK2_L4 - Lab For Minumum Area Rule And Minimum Hole Rule
   - PV_D3SK2_L5 - Lab For Wells And Deep N-Well
   - PV_D3SK2_L6 - Lab For Derived Layers
   - PV_D3SK2_L7 - Lab For Paramterized And PDK Devices
   - PV_D3SK2_L8 - Lab For Angle Error And Overlap Rule
   - PV_D3SK2_L9 - Lab For Unimplemented Rules
   - PV_D3SK2_L10 - Latch-up And Antenna Rules
   - PV_D3SK2_L11 - Lab For Density Rules

4. Lab5 (LVS labs)
   - PV_D5SK2_L1 - Simple LVS Experiment
   - PV_D5SK2_L2 - LVS With Subcircuits
   - PV_D5SK2_L3 - LVS With Blackboxes Subcircuits
   - PV_D5SK2_L4 - LVS With SPICE Low Level Components
   - PV_D5SK2_L5 and L6 - LVS For Small Analog Block - Power-On Reset - Part 1 and 2
   - PV_D5SK2_L7 - LVS Layout Vs Verilog For Standard Cell
   - PV_D5SK2_L8 - LVS For Macros
   - PV_D5SK2_L9 and L10- LVS Digital PLL - Part 1 and 2
   - PV_D5SK2_L11 - LVS With Property Errors

## Lab1 (Tool installation and basic LVS/DRC design flow)
### PV_D1SK2_L1 - Check Tool Installations

#### xschem (for schemtic design)  
First of all, xschem steup is checked by using the following commad:  
- <i>xschem</i>  
- <i>xschem –tcl test.tcl -q</i>  
![This is an image](lab1/1.PNG)
![This is an image](lab1/2.PNG)
#### netgen (for LVS)
netgen is checked by using the following commad:  
- <i>netgen</i>  
![This is an image](lab1/netgen.PNG)
#### ngspice (for simulation)
ngspice is checked by using the following commad:  
- <i>ngspice</i>  
![This is an image](lab1/ngspice.PNG)
#### magic (for layout design and extraction)
magic is checked by using the following commad:  
<i>magic</i>  
- </i>  magic -noconsole</i>  
- </i>  magic -dnull -noconsole  (without graphics)</i>  
- </i>  magic -dnull -noconsole test.tcl</i>  
![This is an image](lab1/magic.PNG)

### PV_D1SK2_L2 - Creating Sky130 Device Layout In Magic
#### For layout cration we have used the following commands:
- </i> magic -d XR (icons colors are saturated)</i> 
- </i>magic -d OGL</i> 
- </i>U -> undo</i> 
- </i>P -> fill color</i> 
- </i>Z zoom in</i> 
- </i>shift+Z (zoom out)</i> 
- </i>E to erase</i> 
- </i>:erase on command window</i>  
![This is an image](lab1/3.PNG)  

#### Modifying properties of sky130 standard cells:  
<img src="lab1/4.PNG" width="800" height="400">  
<img src="lab1/5.PNG" width="800" height="400">  
<img src="lab1/6.PNG" width="600" height="400">  

###  PV_D1SK2_L3 - Creating Simple Schematic In Xschem
Schematic of inverter has been designed in xschem, two transistor symbols have been used: pfet_01v8 and nfet_01v8. Transistor parameters have been modified. Final schematic have been exported as symbol for simulation in testbench.
<img src="lab1/7.PNG" width="800" height="400">  

###  PV_D1SK2_L4 - Creating Symbol And Exporting Schematic In Xschem
A testbench circuit has been developed and schematic of inverter has been imported. Two power sources has been applied, one with constant volatage source, because the pfet and nfet are designed for that and second source voltage is sweep on the gate terminal of each device to check the final outcome.  
<img src="lab1/8.PNG" width="600" height="400">    
<img src="lab1/9.PNG" width="800" height="400">    

###  PV_D1SK2_L5 - Importing Schematic To Layout And Inverter Layout Steps
Now inverter netlist has been exported from xschem to magic as shown below, all blocks have been arragned and connection have been made.
<img src="lab1/10.PNG" width="800" height="400">    
<img src="lab1/11.PNG" width="800" height="400">    

###  PV_D1SK2_L6 - Final DRC/LVS Checks And Post Layout Simulations
Now layout is complete, at this point we are not checking drc errors, although there is no drc error in this layout. The following commands are used for extract the final layout netlist for layout to schematic comparison:
- </i>extract do local (extract in local directory)</i>
- </i>extracl all</i>
- </i>ext2spice lvs (extract for lvs)</i>
- </i>ext2spice (final extraction)</i>

For comparison in netgen we have used following command:
- </i>netgen -batch lvs “../mag/inverter.spice inverter” “../xschem/inverter.spice inverter”</i>
<img src="lab1/netgen_out.PNG" width="800" height="400">  


## Lab2 (Labs for GDS read/write, extraction, DRC, LVS and XOR setup)
### PV_D2SK2_L1 - GDS Read
- </i>cif listall istyle: to get list of all known styles for gdsv
- </i>cif list istyle: current set style</i>
- </i>cif istyle xxx: current and all possible styles</i>
- </i>gds read /usr/share/pdk/sky130A/libs.ref/sky130_fd_sc_hd/gds/sky130_fd_sc_hd.gds</i>
After loading gds, we have seleted a standard cell: sky130_fd_sc_hd__and2_1
<img src="lab2/2.PNG" width="800" height="400">   
Now change the style to vendor and read again
- </i>cif istyle gds(vendor)</i>
<img src="lab2/1.PNG" width="800" height="400">   
- </i>gds noduplicates (check cells can be override or not)</i> 
- </i>gds noduplicates true (current cell will not update)</i>
<img src="lab2/3.PNG" width="500" height="200">   

### PV_D2SK2_L2 - Ports
Port index is meta data so it cannt be stored in gds. It can be checked using following commands
- </i>Port index</i>
- </i>port first</i>
- </i>port 1 name</i>
- </i>port 1 class (meta data)</i>
- </i>port 1 use (meta data)</i>  
<img src="lab2/4.PNG" width="500" height="200">     
Meta data can be found in lef file.  
- </i>lef read /usr/share/pdk/sky130A/libs.ref/sky130_fd_sc_hd/lef/sky130_fd_sc_hd.lef</i>  
<img src="lab2/5.PNG" width="500" height="200"> 
For port consistency we can read from .spice file
- </i> readspice /usr/share/pdk/sky130A/libs.ref/sky130_fd_sc_hd/spice/sky130_fd_sc_hd.spice</i>  
<img src="lab2/6.PNG" width="500" height="200">   
<img src="lab2/7.PNG" width="500" height="200">   

### PV_D2SK2_L3 - Abstract Views
lef file is a library, have no concept of top level cell. Now by loading cells using lef commad, we can see the abstract view of cell. This information is not hold by gds format.  
- </i>lef read /usr/share/pdk/sky130A/libs.ref/sky130_fd_sc_hd/lef/sky130_fd_sc_hd.lef</i>  
Abstract view of AND cell and usefull commands by using lef file:
- </i>port index</i>
- </i>port first</i>
- </i>port 1 name</i>
- </i>port 1 class</i>
- </i>port 1 use</i>
<img src="lab2/abstract_view/8.PNG" width="800" height="400"> 
<img src="lab2/abstract_view/9.PNG" width="800" height="400"> 
Now writing abstract view to gds and reading it back:  
<img src="lab2/abstract_view/10_writing_gds.PNG" width="800" height="400"> 
<img src="lab2/abstract_view/11_read_gds.PNG" width="800" height="400"> 
Making cell writable and painting interconnect over the cell:  
loaded using vendor and default cif style:  
<img src="lab2/abstract_view/12_load_test.PNG" width="800" height="400"> 
<img src="lab2/abstract_view/13_property.PNG" width="800" height="400"> 
<img src="lab2/abstract_view/14_writen_sky130_cell.PNG" width="800" height="400"> 
<img src="lab2/abstract_view/15_read_gds_after_writing.PNG" width="800" height="400"> 

### PV_D2SK2_L4 - Basic Extraction
Now performing basic netlist extraction from magic. Default netlist, with capacitance and with RC have been extracted using following commands:
- </i>ext2spice lvs</i>
- </i>ext2spice</i>
- </i>ext2spice cthrush 0</i>
- </i>extresist tolerance 10</i>
- </i>extresist</i>

simple netlist:  
<img src="lab2/extraction/1_simple_extraction.PNG" width="800" height="400">   
Now with capacitances:  
<img src="lab2/extraction/2_c_extraction.PNG" width="800" height="400">   
Now with resisters:  
<img src="lab2/extraction/3_enabled_extresist.PNG" width="800" height="400">   
<img src="lab2/extraction/3_enabled_resist.PNG" width="800" height="400">   
Overall:  
<img src="lab2/extraction/4_all_on.PNG" width="800" height="400">   
### PV_D2SK2_L5 - Setup For DRC
Following commands are used for performing and analyzing DRC analysis:
- </i>drc style</i>
- </i>drc listall style</i>
- </i>drc style drc(full)</i>
- </i>drc check</i>
- </i>drc why</i>
- </i>drc find</i>

Selecting and applying DRC check:  
<img src="lab2/drc/1.PNG" width="800" height="400">     
Adding another component and checking DRC errors:  
<img src="lab2/drc/2.PNG" width="800" height="400">     
Fixing DRC errors in the layout:  
<img src="lab2/drc/3_nodrc_error.PNG" width="800" height="400">   
And gate subcell:  
<img src="lab2/drc/4_andgate_subcell.PNG" width="800" height="400">    

### PV_D2SK2_L6 - Setup For LVS and PV_D2SK2_L7 - Setup For XOR
Setting lvs using already available spice files for a specific gate usinf following command:  
- </i>netgen -batch lvs “../mag/sky130_fd_sc_hd__and2_1.spice sky130_fd_sc_hd__and2_1” “/usr/share/pdk/sky130A/libs.ref/sky130_fd_sc_hd/spice/sky130_fd_sc_hd.spice sky130_fd_sc_hd__and2_1”</i>    
<img src="lab2/lvs/5_netlish_comp.PNG" width="800" height="400">    
Performing XOR to get mismatch on two layouts in magic to check whether they are same or not:  
<img src="lab2/lvs/6.PNG" width="800" height="400">    


## Lab3 (Labs for all DRC rules)
### PV_D3SK2_L1 - Lab For Width Rule And Spacing Rule   
Now working on DRC fixes in Magic:  
<img src="lab3/exercise1/1.PNG" width="800" height="400">  
We have to fix error in 1a first:  
<img src="lab3/exercise1/2.PNG" width="800" height="400">  
Problem is in metal width:  
<img src="lab3/exercise1/3_drc_error.PNG" width="800" height="400">  
Measuring width:  
<img src="lab3/exercise1/4_width_measurement.PNG" width="800" height="400">  
Appying DRC fix:  
<img src="lab3/exercise1/5_drc_resolved.PNG" width="800" height="400">  
Spacing problem in 6b:  
<img src="lab3/exercise1/6_b.PNG" width="800" height="400">  
Fixing DRC error:  
<img src="lab3/exercise1/6_select_colon.PNG" width="800" height="400">   
DRC issue resolved:  
<img src="lab3/exercise1/7_b_fix_drc.PNG" width="800" height="400">  
Fixed width spacing issue in 1c:   
<img src="lab3/exercise1/8_3_drc_fix.PNG" width="800" height="400">  
Fixed using notch rule: expanded the box using "A" and then shift+(2,4,6,8)  
<img src="lab3/exercise1/9_drc_4_fixed.PNG" width="800" height="400">  
<img src="lab3/exercise1/10_shift_6.PNG" width="800" height="400">  

### PV_D3SK2_L2 - Lab For Wide Spacing Rule And Notch Rule
Fixing via size issue:   
<img src="lab3/exercise2/1.PNG" width="800" height="400">  
We can use "feedback why" command for error printing  
<img src="lab3/exercise2/2_feedback_error.PNG" width="800" height="400">  
Fixing error in 2c (via overlapped drc error)
<img src="lab3/exercise2/3.PNG" width="800" height="400">  
We can switch to above layers by using shift+left click, a via will be added automatically for connection betweeen the layers  
<img src="lab3/exercise2/4_vias.PNG" width="800" height="400">    

### PV_D3SK2_L3 - Lab For Via Size, Multiple Vias, Via Overlap and Autogenerate Vias  
Fixing mimimum area rule by expanding box:    
<img src="lab3/exercise3/1.PNG" width="800" height="400">      
Filling via with metal to fix drc:   
<img src="lab3/exercise3/2_filling_layer_via.PNG" width="800" height="400">      
DRC error: hole area is small:  
<img src="lab3/exercise3/3_hole_area_is_small.PNG" width="800" height="400">   
Fixing hole area issue:  
<img src="lab3/exercise3/4_hole_drc_fixed.PNG" width="800" height="400">   

### PV_D3SK2_L4 - Lab For Minumum Area Rule And Minimum Hole Rule
Fixing nwell drc error by painting local interconnect with diffusion  
<img src="lab3/exercise4/1_fix_drc_nwell.PNG" width="800" height="400">  
Fixing pwell drc error by painting local interconnect with diffusion  
<img src="lab3/exercise4/2_fix_drc_pwell.PNG" width="800" height="400">  
Fixing deep nwell drc error by creating nwell and connecting diffusion with local interconnect  
<img src="lab3/exercise4/4c_complete_nodrc.PNG" width="800" height="400"> 

### PV_D3SK2_L5 - Lab For Wells And Deep N-Well 
Following commands are used to see different layers:
- </i>cif see DIF</i>
- </i>cif see POLY</i>
- </i>cif see NDSM</i>
- </i>cif see PDSM</i> 
- </i>cif see LVTN</i>  
- </i>cif see HVI</i>  
See diffusion using cif see DIF   
<img src="lab3/exercise5/1_see_DIFF.PNG" width="800" height="400">   
See POLY using cif see POLY  
<img src="lab3/exercise5/2_see_POLY.PNG" width="800" height="400">    
See NDSM and PDSM using cif see NDSM/PDSM  
<img src="lab3/exercise5/3_see_NSDM_PSDM.PNG" width="800" height="400">  
See LVTN using cif see LVTN  
<img src="lab3/exercise5/4_see_LVTN.PNG" width="800" height="400"> 
See HVI using cif see HVI  
Now we can see that above cell is high voltage:  
<img src="lab3/exercise5/5_see_HVI_5b.PNG" width="800" height="400">
See NPC using cif see NPC 
<img src="lab3/exercise5/6_ciff_see_NPC.PNG" width="800" height="400">   

### PV_D3SK2_L6 - Lab For Derived Layers  
Now we can expland the cell and check drc error exists inside the cell, but it has been resolved in upper heirarchy    
<img src="lab3/exercise6/1_drc_exist_in_the_cell.PNG" width="800" height="400">   

### PV_D3SK2_L7 - Lab For Paramterized And PDK Devices
<img src="lab3/exercise7/1.PNG" width="800" height="400"> 
<img src="lab3/exercise7/2.PNG" width="800" height="400"> 
<img src="lab3/exercise7/3.PNG" width="800" height="400"> 
<img src="lab3/exercise7/4.PNG" width="800" height="400"> 
<img src="lab3/exercise7/Capture5.PNG" width="800" height="400"> 
<img src="lab3/exercise7/6.PNG" width="800" height="400"> 

### PV_D3SK2_L8 - Lab For Angle Error And Overlap Rule
### PV_D3SK2_L9 - Lab For Unimplemented Rules
### PV_D3SK2_L10 - Latch-up And Antenna Rules
### PV_D3SK2_L11 - Lab For Density Rules
