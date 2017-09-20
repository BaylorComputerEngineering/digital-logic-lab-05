# Assignment for Lab 05 Verilog Into

When using Vivado, we **must** using the following structure to store you project and source files:
- src: All verilog files must be placed in this folder
- sim: All simulation files, i.e. .wcfg files must be placed in this folder
- .xpr file: the project's .xpr file must be placed in assignment folder.

So when I'm grading your assignment, I will clone your assignment to my machine, and open your project by open the xpr file from Vivado. All your project's simulation set and source files must be loaded. 

## Grading:
- For each problem, you **must** have a seperate simulation set in the same project. If I loaded your project, and the simulation set is not there, you will not get any points for the problem even if you have the correct files.
- If you have a simulation set for the problem, but no test bench for the module you are asked to implement, you will lose half of the points even if you implemented it correctly.
- Make sure when you creating the project for this assignment, the project folder is this assignment folder. You can verify this by see if the xpr file is directly (not in sny sub-folders) inside this assignment folder. 
- All source files (.v files) **must** be stored in src folder
- All waveform configuation (.wcfg files, when you save the simulation setting) files **must** be stored in sim folder

### 0. Implement and test ripple adder (1 pt)
- Name this simulation set as "ripple_test"

### 1. Implement and test variable width adder subtractor (1 pt)
- Name this simulation set as "adder_subtractor_test"

### 2. Implement and test variable width 2-bit multiplexer (2 pts) 
- Name this simulation set as "mux2_test"

### 3. Implement and test variable width 4-bit multiplexer (2 pts)
- Name this simulation set as "mux4_test"

### 4. Implement and test variable width comparator of two inputs (2 pts)
- Implement the comparator using the combinational logic shown in figure 4.17 in text book.
- Name this simulation set as "comparator_test"

### 5. Implement a 8-bit comparator using 2 4-bit comparator. The 4-bit comparator should be instantiated using the module you created in problem 4. (2 pts)
- Name this simulation set as "comparator8bits_test"


