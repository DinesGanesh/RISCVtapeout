# RISCVtapeout
10 Weeks Schedule of RISC-V VSD_IITGN  
Tool Installation: (OpenSource)   
1.Yosys  - Synthesis.  
2.iVerilog - Verilog Simualtion.  
3.GTK Wave - Waveform Viewer.<br>            
**Week-1 Day1**:    
Initial introduction of Test Bench & Stimulus (Test Vectors)
- Tried to create a new verilog file with a simple XOR gate.
- Developed test bench(tb) for the XOR gate.
- Fixed some bugs with the tb Code with the dumpvars.
- compiler using iverilog, created dump value file and viewed waveform using gtkwave analyser.<br>  
  
**Week-1 Day2**:  
Synthesis of design file and netlist file.
- run Yosys for synthesis after read_verilog, read_liberty, synth -top, abc -liberty.
- Show the Synthesis mapping for good_mux.v - using sky130nm PDK
- Synthesized Netlist was input to iverilog along with library sky130_fd_sc_hd.v
- $ iverilog -o sim_netlist.out \
  synth_netlist.v \
  tb.v \
  /path/to/sky130_fd_sc_hd.v \
  /path/to/primitives.v
- $ vvp sim_netlist.out
- $ gtkwave dump.vcd
- compiled using iverilog, created dump value file and viewed waveform using gtkwave analyser.<br>

**Week-2**:  
SOC Introduction:  
**BabySoC** is a minimal, open-source System-on-Chip (SoC) developed and released by VSD (VLSI System Design Corp) as an educational platform to help learners and engineers:
Understand digital design, SoC architecture, and RISC-V integration
Learn the design flow: from RTL to GDSII
Simulate and synthesize a full chip using open-source tools
Library: Sky130 PDK <br>
What does BabySoC include?
- A RISC-V core
- PLL
- 10-bit DAC
Written in Verilog, tlv for simulation and synthesis.
Integrates cleanly with OpenLANE, the open-source ASIC flow.<br>
**Reference Repo:**:
https://github.com/hemanthkumardm/SFAL-VSD-SoC-Journey/tree/main/12.%20VSDBabySoC%20Project
https://github.com/manili/VSDBabySoC.git

**Week3:**  
**Gate Level simulation of BabySOC** -  
**Tool: Yosys **  
1.Reading Verilog files  
2.Reading Library files  
3.synth -top  
4.Optimization and Technology mapping  
5.Finally Staticstics    
output Post synthesis netlist.v    



**Tool: iverilog -o**  
1.run the netlist file using necessary dependent design files and library files.  
2.waveform viewing the same dump file created in the previous step.   
3.Analog Waveform format of "dout" is clearly the same as that fo functional simulation. (Week2)  
**Error Log are highlight in the week's folder.**      

iverilog -o /home/vsduser/Desktop/work/tools/VSDBabySoC/output/post_synth_sim/post_synth_sim.out \
  -DPOST_SYNTH_SIM \
  -DFUNCTIONAL \
  -DUNIT_DELAY='#1' \
  -I /home/vsduser/Desktop/work/tools/VSDBabySoC/src/include \
  -I /home/vsduser/Desktop/work/tools/VSDBabySoC/src/module \
  -I /home/vsduser/Desktop/work/tools/VSDBabySoC/output/post_synth_sim \
  -I /home/vsduser/Desktop/work/tools/VSDBabySoC/src/gls_model \
  /home/vsduser/Desktop/work/tools/VSDBabySoC/src/gls_model/sky130_fd_sc_hd.v \
  /home/vsduser/Desktop/work/tools/VSDBabySoC/src/gls_model/primitives.v \
  /home/vsduser/Desktop/work/tools/VSDBabySoC/src/module/testbench.v
    
**Reference Repo:**  
https://github.com/Ananya-KM/VSD_HDP/blob/main/Day6.md  

**Static Timing Analysis:**
1. Setup time and hold time are two of the most critical timing constraints in digital design, especially in synchronous circuits.  
Setup Time Constraint : Tclk_Q + Tcomb + Tsetup ≤ Tclk  
2. Hold Time Constraint:  
Tclk_Q + Tmin_comb ≥ Thold  
3. Arrival Time (AT):  
The actual time at which a signal reaches a particular point (usually a flip-flop input or output) in a timing path.
4. Required Time (RT)  
The latest time by which a signal must arrive at a certain point to meet timing constraints, like setup or hold time.
Slack = Required Time – Arrival Time
Slack = -ve means timing not met.

**Week4 :**  
Tools : LTSPICE, NGSPICE  
Started with CMOS Characteristics - Pull-up Network & Pull-Down Network.
CMOS Inverter VTC Curve.


