# Digital Logic Lab 05 - Verilog Intro

## References:
- [FPGA Prototyping By Verilog Examples: Xilinx Spartan-3 Version](https://www.amazon.com/FPGA-Prototyping-Verilog-Examples-Spartan-3/dp/0470185325/)
- [Quick Reference Guide](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf)

## [Transistor Count of CPUs](https://en.wikipedia.org/wiki/Transistor_count)

| Processor | Year | Transistor count|
| --------- |:----:| ----------------:|
| MOS Technology 6502 | 1975 | 3,510 |
| Intel 8085 | 1976 | 6,500 |
| Intel 8086 | 1978 | 29,000 |
| Quad-core + GPU GT2 Core i7 Skylake K | 2015 | 1,750,000,000
| NVIDIA GV100 Volta | 2017 | 21,100,000,000 |

## Commonly used HDL (Hardware Description Languages)

- Verilog
- VHDL
- [Chisel (Constructing Hardware in a Scala Embedded Language)](https://chisel.eecs.berkeley.edu)


## Verilog

- It is a **H**ardware **D**escription **L**anguage. 
  - A specification language, not a programming language.
- It is used for
  - Behavior modeling
  - Gate level modeling
  - Transistor level modeling
  - Simulation for all the modeling


<!-- ### [Reserved Keywords](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=7) -->
<!-- ### [Concurrency](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=8) -->
- [Basic Syntax](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=8)
- [Data Type Declarations](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=15)
  - **wire**
    - Interconnecting wire, connect output to input
    - Its value is driven by whatever the output it is connected to.
    - Can be either input or output type.
  <!-- - **reg** -->
  <!--   - A variable whose behavior need to be defined. **NOTE: It's not a register** -->
  <!--   - Driver / behavior is defined in ```always``` or ```initial``` block. -->
  <!--   - Could be used as output type. -->
  <!--   - Should not be used as input type. -->
  - Logic Values

	 | Logic Values | Description | Simulation Color |
	 |:------------:|:----------- |:---------------- |
	 | 0 | zero, low, or false | Green |
	 | 1 | one, high, or true | Green |
	 | **z** or **Z** | high impedence (tri-stated or floating) | Blue |
	 | **x** or **X** | unknown or uninitialized or don't-care | Red |

- [Operators (page 33)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=33)
- [Module Definition (page 12)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=12)

  Example:
  - Behavior modeling:
  ``` verilog
  module halfadder (input a, b,
                    output s, c);

     assign s = a ^ b;
     assign c = a & b;

  endmodule // halfadder
  ```

  - Gate level modeling:
  ``` verilog
  module halfadder (input a, b,
                    output s, c);

     xor(s, a, b);
     and(c, a, b);

  endmodule // halfadder
  ```

  - By default, if you just specify input or output, the signal is assumed to be wire.
  - **Any undeclared signal** is assumed to be 1 bit wire.

- [Module Instances (page 21)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=21)
  Example:
  ```verilog
  module fulladder (input a, b, cin,
                    output sum, cout);

     wire                  s1, c1, c2;

     halfadder HA1(.a(a), .b(b), .s(s1), .c(c1));
     halfadder HA2(.a(s1), .b(cin), .s(sum), .c(c2));

     assign cout = c1 | c2;
     // and(cout, c1, c2);

  endmodule // fulladder
  ```
  - **Must** use dot syntax to instantiate modules for assignments

- [Primitive Instances (page 23)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=23)
  - Primitive instances do not use dot syntax

- [Vector Bit Select and Part Selects (page 23)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=23)
  Example:
  ```verilog
  module ripple_adder_2bits(input [1:0] a, b,
                            input cin,
                            output [1:0] sum,
                            output cout);
  endmodule
  ```
  Here, the two inputs a, b are vector bits, which means they are 2-bit input wires. While sum is a 2-bit output wire.
  
- [Procedural Blocks](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=25)
  - ```initial```
    - Mostly used in simulation (or initializing registers, depending on compiler support)
    - Could have multiple ```initial``` block
  <!-- - ```always``` -->
  <!--   - It is used for defining behaviors of **reg** type -->
  <!--   - We will talk more about this in the future -->

<!-- - [Common System Tasks and Functions](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=42) -->
<!-- - [Generate Block](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=25) -->

## Vivado

### [Download Vivado 2017.2](https://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/vivado-design-tools/2017-2.html)

### Installation
  - Make sure you select the WebPACK edition (first option). It's free, no license required, and has all the features we need.
  - After installed vivado, [install board files](https://reference.digilentinc.com/reference/software/vivado/board-files)

### Creating Project
**Note**: the following screenshots are captured with Vivado 2017.2.1, layout might be a bit different but you should be able find all the buttons in 2014 version.

1. Clone this assignment repo to your local machine, make sure you know the path

![clone_repo](pics/clone_repo.png)

Note that the path of my assignment repo is ```/home/zcai/repos/digital-logic-lab-05```

2. Create project
  Choose your project path and project name **DO NOT** create project subdirectory.
  ![startup](pics/startup.png)
  
  when choosing path, make sure:
  
  - **Uncheck** "create project subdirectory" option, **It's a MUST**
  - Choose the path to be your assignment repository's folder
    
  ![name_and_path](pics/project_name_marked.png)

  Hardware part is not important this time, choose anything and go to next.
  
  ![select_part](pics/create_project_select_part.png)

3. Add or create files
  <!-- - All sources files, i.e. files end with .v extention, must be stored in src directory in your assignment. (If src is not there, create a folder named "src"). -->
  Verilog files can be created inside or outside vivado. If you created the file outside vivado, you need to add it to the project when you want to use it.

  There are two different types of source files to Vivado:
  - Design source:
    Regular modules that can be implmeneted in hardware
  - Simulation source:
    Modules that strickly only used in simulation, usually these are just modules contain your test code.

  There is also a type of file called constraint file that specify your target hardware's configuration. They are not considered sources, and are usually provided by hardware vendors. Since we are only doing simulation here, we won't be need it this time.

  **For this lab, I require ALL source files, i.e. both design sources and simulation sources, to be placed in "src" folder of assignment folder.**
  Constraint file should be placed in "constrs" folder.
  
  We will only be dealing with simulation for this lab. So we will need to create a simulation set. **Note that, for assignment, I will specify the exact simulation set's name, you need to name your simulation sets to be the exact name I specified in the assignment**
  
  Right click anywhere on "Sources" window, and choose "Edit simulation Sets ...":
  ![edit_simulation_set](pics/edit_simulation_set.png)
  
  Then click on the drop down menu and choose "Create Simulation Set ..."
  
  ![create_simulation_set](pics/create_simulation_set_marked.png)
  
  We will name the simulation set as "halfadder_test". **Note: there cannot be space in any simulation set's name**.
  Since we are going to use this simulation, we will mark this simulation set as **active**. (You can also do this in Sources window by right clicking a non-active simulation set, and choose "make active" from the menu)
  
  ![make_active](pics/edit_simulation_set_make_active_marked.png)
  
  To add a file click on the "Add Files" button in the same window, browse and select desired file. However, do make sure **UNCHECK the "copy sources into project" option**.
  
  ![add_files_no_copy](pics/add_files_uncheck.png)
  
  In the same window, you can also create file. However, do make sure you **specify the file location**. Otherwise, Vivado will automatically store it in a location that will not be tracked by git.

  ![choose_location](pics/create_file_choose_location.png)
  
  The location must be the "src" directory inside your assignment folder
  
  ![file_location](pics/file_location.png)
  
  This what it looks like after adding a file and creating a file, not that they both in "src" directory:
  
  ![files_added_and_created](pics/files_added_and_created.png)
  
  Whenever you are creating a file with Vivado, the following window will pop up and asking you to specify inputs and outputs. Skip this window, we will type in inputs and outputs manually.
  
  ![skip IO](pics/create_file_IO_spec.png)
  
  At the end, you will see the files we added and created will show up in "Sources" window and under halfadder_test.
  
  ![added_and_created](pics/added_and_created.png)

### Simulation

Click on run simulation, and here is the default layout:

![default_layout](pics/simulation_default_layout.png)

Click on "zoom fit" to have the best view of your timing diagram

![zoom_fit](pics/zoom_fit_marked.png)

### [Vivado Naming Convention](https://www.xilinx.com/support/documentation/sw_manuals/xilinx2017_2/ug973-vivado-release-notes-install-license.pdf#page=5)
