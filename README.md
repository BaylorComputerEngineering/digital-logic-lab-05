- [Digital Logic Lab 05 - Verilog Intro](#digital-logic-lab-05---verilog-intro)
  - [References:](#references)
  - [[Transistor Count of CPUs](https://en.wikipedia.org/wiki/Transistor_count)](#transistor-count-of-cpus)
  - [Commonly used HDL (Hardware Description Languages)](#commonly-used-hdl-hardware-description-languages)
  - [Verilog Usage](#verilog)
- [Verilog Intro](#org8f9786e)
  - [Basic Building Block &#x2013; modules](#orgcb178f2)
  - [Procedural Blocks](#org83d24ce)
    - [Types](#orgef954bd)
  - [Variable types:](#orgef009cb)
    - [wire](#org37785c7)
    - [reg](#org3e21c62)
    - [other types:](#org22c4765)
  - [Logic Values](#org6231a42)
  - [Literal Integer Numbers](#org881abad)
  - [Operators](#org3ab2a03)
  - [Primitive Instances](#org2ff505a)
  - [Vivado](#vivado)
  - [[Download Vivado 2017.2](https://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/vivado-design-tools/archive.html)](#download-vivado-2017.2)
  - [Installation](#installation)
  - [[Vivado Naming Convention](https://www.xilinx.com/support/documentation/sw_manuals/xilinx2017_2/ug973-vivado-release-notes-install-license.pdf#page=5)](#vivado-naming-convention)
  - [Creating Project](#creating-project)
  - [Simulation](#simulation)



<a id="digital-logic-lab-05---verilog-intro"></a>

# Digital Logic Lab 05 - Verilog Intro


<a id="references"></a>

## References:

-   [FPGA Prototyping By Verilog Examples: Xilinx Spartan-3 Version](https://www.amazon.com/FPGA-Prototyping-Verilog-Examples-Spartan-3/dp/0470185325/)
-   [Quick Reference Guide](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf)


<a id="transistor-count-of-cpus"></a>

## [Transistor Count of CPUs](https://en.wikipedia.org/wiki/Transistor_count)

| Processor                             | Year | Transistor count |
|------------------------------------- |---- |---------------- |
| MOS Technology 6502                   | 1975 | 3,510            |
| Intel 8085                            | 1976 | 6,500            |
| Intel 8086                            | 1978 | 29,000           |
| Quad-core + GPU GT2 Core i7 Skylake K | 2015 | 1,750,000,000    |
| NVIDIA GV100 Volta                    | 2017 | 21,100,000,000   |


<a id="commonly-used-hdl-hardware-description-languages"></a>

## Commonly used HDL (Hardware Description Languages)

-   Verilog
-   VHDL
-   [Chisel (Constructing Hardware in a Scala Embedded Language)](https://chisel.eecs.berkeley.edu)
    -   Compiles to verilog or C++


<a id="verilog"></a>

## Verilog Usage

-   A specification language
-   It is used for
    -   Behavior modeling
    -   Gate level modeling
    -   Transistor level modeling
    -   Simulation for all the modeling


<a id="org8f9786e"></a>

# Verilog Intro


<a id="orgcb178f2"></a>

## Basic Building Block &#x2013; modules

-   See [Module Definition (page 12)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=12)
-   Basic abstraction unit
-   Has input and output
    -   modules that do not have IOs are used for testing only.
-   One module per verilog file (.v)
-   For example, the following is a module called `halfadder`, with two input ports name `a`, `b`, and two output ports `s`, `c`

```verilog
module halfadder (input a, input b, output s, output c); // <---- module declaration always ends with a ;

endmodule // halfadder
```

You can group ports that are the same type together and write them in multiple lines as long as you do not forget about the ending ";"

```verilog
module halfadder (input a, b,
                  output s, c); // <---- module declaration always ends with a ;

endmodule // halfadder
```


<a id="org83d24ce"></a>

## Procedural Blocks

See [Procedural Blocks (page 27)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=27)


<a id="orgef954bd"></a>

### Types

-   **Initial** blocks process statements one time
    -   Mostly used for testing.
    -   Sometimes could be used for initializing variables.
-   **always** blocks are an infinite loop which process statements repeatedly.


<a id="orgef009cb"></a>

## Variable types:

See [Data Type Declarations (page 15)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=15)


<a id="org37785c7"></a>

### wire

-   Used outside procedural blocks
-   Used in IO ports by default
-   Interconnecting wire, connect output to input
-   Its value is driven by whatever the output it is connected to.
-   **Note:** Any variable that is not declared, it is assumed to be 1-bit wire.


<a id="org3e21c62"></a>

### reg

-   The driver (behavior) of any `reg` variable must be define in the module the variable is declared.
-   Used inside procedural blocks
-   Must be declared outside procedural blocks
-   **Note:** reg is **not** register. Used to be, not anymore.
-   When used in IO ports, only outputs can be declared as `reg`


<a id="org22c4765"></a>

### other types:

There are several other types available in Verilog (see ), but we are going to stick with just `wire` and `reg` in this class.

By default, IO ports are considered as `wire`, unless `reg` is declared, for example:

```verilog
module halfadder (input a, b,       // a, b are implicitly declared as wire
                  output reg s, c); // s, c are explicitly declared as reg

endmodule // halfadder
```


<a id="org6231a42"></a>

## Logic Values

| Logic Values                          | Description                             |
|------------------------------------- |--------------------------------------- |
| <font color="green"> 0</font>         | zero, low, or false                     |
| <font color="green"> 1</font>         | one, high, or true                      |
| <font color="blue"> *z* or *Z*</font> | high impedence (tri-stated or floating) |
| <font color="red"> *x* or *X*</font>  | unknown or uninitialized or don't-care  |


<a id="org881abad"></a>

## Literal Integer Numbers

See [Literal Integer Numbers (page 11)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=11)

| **Format**      | **Representation**                       |
|--------------- |---------------------------------------- |
| value           | unsized decimal integer                  |
| size'base value | sized integer in a specific radis (base) |

| Radix      | Symbol | Legal Values                     |
|---------- |------ |-------------------------------- |
| Binary     | 'b     | 0, 1, x, X, z, Z, ?, \_          |
| Octal      | 'o     | 0-7, x, X, z, Z, ?, \_           |
| Decimal    | 'd     | 0-9, \_                          |
| Hexdecimal | 'h     | 0-9, a-f, A-F, x, X, z, Z, ?, \_ |

Example:

| Examples | Size    | Radix      | Binary Equivalent         |
|-------- |------- |---------- |------------------------- |
| 10       | unsized | decimal    | 0 &#x2026; 01010 (32-bit) |
| 'o7      | unsized | octal      | 0 &#x2026; 00111 (32-bit) |
| 1'b1     | 1 bit   | binary     | 1                         |
| 8'hAB    | 8 bits  | hexdecimal | 10101011                  |
| 6'hF0    | 6 bits  | hexdecimal | 110000 (truncated)        |
| 6'hA     | 6 bits  | hexdecimal | 001010 (zero filled)      |
| 6'bz     | 6 bits  | binary     | zzzzzz (z filled)         |


<a id="org3ab2a03"></a>

## Operators

See [Operators (page 33)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=33)


<a id="org2ff505a"></a>

## Primitive Instances

See [Primitive Instances (page 19)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=23)

```verilog
module halfadder (input a, b,
                  output s, c);

     assign s = a ^ b;
     assign c = a & b;

endmodule // halfadder
```

-   Gate level modeling:

```verilog
module halfadder (input a, b,
                  output s, c);

 xor(s, a, b);
 and(c, a, b);

endmodule // halfadder
```

-   By default, if you just specify input or output, the signal is assumed to be wire.
-   **Any undeclared signal** is assumed to be 1 bit wire.

-   [Module Instances (page 21)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=21) Example:

```verilog
module fulladder (input a, b, cin,
                  output sum, cout);

   wire s1, c1, c2;

   halfadder HA1(.a(a), .b(b), .s(s1), .c(c1));
   halfadder HA2(.a(s1), .b(cin), .s(sum), .c(c2));

   assign cout = c1 | c2; // and(cout, c1, c2);

endmodule // fulladder
```

-   **Must** use dot syntax to instantiate modules for assignments
-   [Primitive Instances (page 23)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=23)
-   Primitive instances do not use dot syntax
-   [Vector Bit Select and Part Selects (page 19)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=19) Example:

```verilog
module ripple_adder_2bits(input [1:0] a, b,
                          input cin,
                          output [1:0] sum,
                          output cout);
endmodule
```

Here, the two inputs a, b are vector bits, which means they are 2-bit input wires. While sum is a 2-bit output wire.

-   

-   `initial`
    -   Mostly used in simulation (or initializing registers, depending on compiler support)
    -   Could have multiple `initial` block <!-- - ```always``` --> <!-- - It is used for defining behaviors of **reg** type --> <!-- - We will talk more about this in the future -->

<div class="HTML">
<!&#x2013; - [Common System Tasks and Functions](<http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=42>) &#x2013;>

</div>

<div class="HTML">
<!&#x2013; - [Generate Block](<http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=25>) &#x2013;>

</div>


<a id="vivado"></a>

## Vivado


<a id="download-vivado-2017.2"></a>

## [Download Vivado 2017.2](https://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/vivado-design-tools/archive.html)


<a id="installation"></a>

## Installation

-   Make sure you select the WebPACK edition (first option). It's free, no license required, and has all the features we need.
-   After installed vivado, [install board files](https://reference.digilentinc.com/reference/software/vivado/board-files)


<a id="vivado-naming-convention"></a>

## [Vivado Naming Convention](https://www.xilinx.com/support/documentation/sw_manuals/xilinx2017_2/ug973-vivado-release-notes-install-license.pdf#page=5)


<a id="creating-project"></a>

## Creating Project

**Note**: the following screenshots are captured with Vivado 2017.2.1, layout might be a bit different but you should be able find all the buttons in 2014 version.

1.  Clone this assignment repo to your local machine, make sure you know the path

![img](pics/clone_repo.png "clone\\<sub>repo</sub>")

Note that the path of my assignment repo is `/home/zcai/repos/digital-logic-lab-05`

1.  Create project Choose your project path and project name **DO NOT** create project subdirectory. ![img](pics/startup.png)

when choosing path, make sure:

-   **Uncheck** "create project subdirectory" option, **It's a MUST**
-   Choose the path to be your assignment repository's folder

![img](pics/project_name_marked.png "name\\<sub>and</sub>\\<sub>path</sub>")

Hardware part is not important this time, choose anything and go to next.

![img](pics/create_project_select_part.png "select\\<sub>part</sub>")

1.  Add or create files <!-- - All sources files, i.e. files end with .v extention, must be stored in src directory in your assignment. (If src is not there, create a folder named "src"). --> Verilog files can be created inside or outside vivado. If you created the file outside vivado, you need to add it to the project when you want to use it.

There are two different types of source files to Vivado: - Design source: Regular modules that can be implmeneted in hardware - Simulation source: Modules that strickly only used in simulation, usually these are just modules contain your test code.

There is also a type of file called constraint file that specify your target hardware's configuration. They are not considered sources, and are usually provided by hardware vendors. Since we are only doing simulation here, we won't be need it this time.

**For this lab, I require ALL source files, i.e. both design sources and simulation sources, to be placed in "src" folder of assignment folder.** Constraint file should be placed in "constrs" folder.

We will only be dealing with simulation for this lab. So we will need to create a simulation set. \*Note that, for assignment, I will specify the exact simulation set's name, you need to name your simulation sets to be the exact name I specified in the assignment\*

Right click anywhere on "Sources" window, and choose "Edit simulation Sets &#x2026;": ![img](pics/edit_simulation_set.png)

Then click on the drop down menu and choose "Create Simulation Set &#x2026;"

![img](pics/create_simulation_set_marked.png "create\\<sub>simulation</sub>\\<sub>set</sub>")

We will name the simulation set as "halfadder\\<sub>test</sub>". **Note: there cannot be space in any simulation set's name**. Since we are going to use this simulation, we will mark this simulation set as **active**. (You can also do this in Sources window by right clicking a non-active simulation set, and choose "make active" from the menu)

![img](pics/edit_simulation_set_make_active_marked.png "make\\<sub>active</sub>")

To add a file click on the "Add Files" button in the same window, browse and select desired file. However, do make sure **UNCHECK the "copy sources into project" option**.

![img](pics/add_files_uncheck.png "add\\<sub>files</sub>\\<sub>no</sub>\\<sub>copy</sub>")

In the same window, you can also create file. However, do make sure you **specify the file location**. Otherwise, Vivado will automatically store it in a location that will not be tracked by git.

![img](pics/create_file_choose_location.png "choose\\<sub>location</sub>")

The location must be the "src" directory inside your assignment folder

![img](pics/file_location.png "file\\<sub>location</sub>")

This what it looks like after adding a file and creating a file, not that they both in "src" directory:

![img](pics/files_added_and_created.png "files\\<sub>added</sub>\\<sub>and</sub>\\<sub>created</sub>")

Whenever you are creating a file with Vivado, the following window will pop up and asking you to specify inputs and outputs. Skip this window, we will type in inputs and outputs manually.

![img](pics/create_file_IO_spec.png "skip IO")

At the end, you will see the files we added and created will show up in "Sources" window and under halfadder\\<sub>test</sub>.

![img](pics/added_and_created.png "added\\<sub>and</sub>\\<sub>created</sub>")


<a id="simulation"></a>

## Simulation

Click on run simulation, and here is the default layout:

![img](pics/simulation_default_layout.png "default\\<sub>layout</sub>")

Click on "zoom fit" to have the best view of your timing diagram

![img](pics/zoom_fit_marked.png "zoom\\<sub>fit</sub>")
