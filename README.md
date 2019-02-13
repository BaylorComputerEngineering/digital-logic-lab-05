
# Table of Contents

1.  [Digital Logic Lab 05 - Verilog Intro](#digital-logic-lab-05---verilog-intro)
    1.  [References:](#references)
    2.  [Transistor Count of CPUs](#transistor-count-of-cpus)
    3.  [Commonly used HDL (Hardware Description Languages)](#commonly-used-hdl-hardware-description-languages)
    4.  [Verilog Usage](#verilog)
2.  [Verilog Intro](#org8a14163)
    1.  [Basic Building Block &#x2013; modules](#org50a4f6f)
    2.  [Procedural Blocks](#orgc3cccc0)
        1.  [Types](#org87b721d)
    3.  [Variable types:](#orgcaa7e21)
        1.  [wire](#orgaee24c4)
        2.  [reg](#orgf2f0607)
    4.  [Data Type Declarations](#org44b1526)
    5.  [Vivado](#vivado)
    6.  [Download Vivado 2017.2](#download-vivado-2017.2)
    7.  [Installation](#installation)
    8.  [Vivado Naming Convention](#vivado-naming-convention)
    9.  [Creating Project](#creating-project)
    10. [Simulation](#simulation)



<a id="digital-logic-lab-05---verilog-intro"></a>

# Digital Logic Lab 05 - Verilog Intro


<a id="references"></a>

## References:

-   [FPGA Prototyping By Verilog Examples: Xilinx Spartan-3 Version](https://www.amazon.com/FPGA-Prototyping-Verilog-Examples-Spartan-3/dp/0470185325/)
-   [Quick Reference Guide](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf)


<a id="transistor-count-of-cpus"></a>

## [Transistor Count of CPUs](https://en.wikipedia.org/wiki/Transistor_count)

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-right" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Processor</th>
<th scope="col" class="org-right">Year</th>
<th scope="col" class="org-left">Transistor count</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">MOS Technology 6502</td>
<td class="org-right">1975</td>
<td class="org-left">3,510</td>
</tr>


<tr>
<td class="org-left">Intel 8085</td>
<td class="org-right">1976</td>
<td class="org-left">6,500</td>
</tr>


<tr>
<td class="org-left">Intel 8086</td>
<td class="org-right">1978</td>
<td class="org-left">29,000</td>
</tr>


<tr>
<td class="org-left">Quad-core + GPU GT2 Core i7 Skylake K</td>
<td class="org-right">2015</td>
<td class="org-left">1,750,000,000</td>
</tr>


<tr>
<td class="org-left">NVIDIA GV100 Volta</td>
<td class="org-right">2017</td>
<td class="org-left">21,100,000,000</td>
</tr>
</tbody>
</table>


<a id="commonly-used-hdl-hardware-description-languages"></a>

## Commonly used HDL (Hardware Description Languages)

-   Verilog
-   VHDL
-   [Chisel (Constructing Hardware in a Scala Embedded Language)](https://chisel.eecs.berkeley.edu)
    -   Compiles to verilog


<a id="verilog"></a>

## Verilog Usage

-   It is a \*H\*ardware \*D\*escription \*L\*anguage.
-   A specification language, not a programming language.
-   It is used for
-   Behavior modeling
-   Gate level modeling
-   Transistor level modeling
-   Simulation for all the modeling

<div class="HTML">
<!&#x2013; ### [Reserved Keywords](<http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=7>) &#x2013;>

</div>

<div class="HTML">
<!&#x2013; ### [Concurrency](<http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=8>) &#x2013;>

</div>


<a id="org8a14163"></a>

# Verilog Intro


<a id="org50a4f6f"></a>

## Basic Building Block &#x2013; modules

-   Basic abstraction unit
-   Has input and output
    -   modules that do not have IOs are used for testing only.
-   One module per verilog file


<a id="orgc3cccc0"></a>

## Procedural Blocks


<a id="org87b721d"></a>

### Types

-   **Initial** blocks process statements one time
    -   Mostly used for testing.
    -   Sometimes could be used for initializing variables.
-   **always** blocks are an infinite loop which process statements repeatedly.


<a id="orgcaa7e21"></a>

## Variable types:


<a id="orgaee24c4"></a>

### wire

-   Used outside procedural blocks
-   Any variable that is not declared, it is assumed to be 1-bit wire.


<a id="orgf2f0607"></a>

### reg

-   Used inside procedural blocks
-   Must be declared outside procedural blocks
-   **Note:** reg is **not** register. Used to be, not anymore.

\*


<a id="org44b1526"></a>

## [Data Type Declarations](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=15)

-   **wire**
    -   Interconnecting wire, connect output to input
    -   Its value is driven by whatever the output it is connected to.
    -   Can be either input or output type. <!-- - **reg** -->
        <!--   - A variable whose behavior need to be defined. **NOTE: It's not a register** -->
        <!--   - Driver / behavior is defined in ```always``` or ```initial``` block. -->
        <!--   - Could be used as output type. -->
        <!--   - Should not be used as input type. -->

-   Logic Values

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Logic Values</th>
<th scope="col" class="org-left">Description</th>
<th scope="col" class="org-left">Simulation Color</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left"><font color="green"> 0</font></td>
<td class="org-left">zero, low, or false</td>
<td class="org-left">Green</td>
</tr>


<tr>
<td class="org-left"><font color="green"> 1</font></td>
<td class="org-left">one, high, or true</td>
<td class="org-left">Green</td>
</tr>


<tr>
<td class="org-left"><font color="blue"> *z* or *Z*</font></td>
<td class="org-left">high impedence (tri-stated or floating)</td>
<td class="org-left">Blue</td>
</tr>


<tr>
<td class="org-left"><font color="red"> *x* or *X*</font></td>
<td class="org-left">unknown or uninitialized or don't-care</td>
<td class="org-left">Red</td>
</tr>
</tbody>
</table>

-   [Operators (page 33)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=33)
-   [Module Definition (page 12)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=12)

Example:

-   Behavior modeling:

    module halfadder (input a, b,
                      output s, c);
    
         assign s = a ^ b;
         assign c = a & b;
    
    endmodule // halfadder

-   Gate level modeling:

    module halfadder (input a, b,
                      output s, c);
    
     xor(s, a, b);
     and(c, a, b);
    
    endmodule // halfadder

-   By default, if you just specify input or output, the signal is
    assumed to be wire.
-   **Any undeclared signal** is assumed to be 1 bit wire.

-   [Module Instances (page 21)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=21) Example:

    module fulladder (input a, b, cin,
                      output sum, cout);
    
       wire s1, c1, c2;
    
       halfadder HA1(.a(a), .b(b), .s(s1), .c(c1));
       halfadder HA2(.a(s1), .b(cin), .s(sum), .c(c2));
    
       assign cout = c1 | c2; // and(cout, c1, c2);
    
    endmodule // fulladder

-   **Must** use dot syntax to instantiate modules for assignments
-   [Primitive Instances (page 23)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=23)
-   Primitive instances do not use dot syntax
-   [Vector Bit Select and Part Selects (page 19)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=19) Example:

    module ripple_adder_2bits(input [1:0] a, b,
                              input cin,
                              output [1:0] sum,
                              output cout);
    endmodule

Here, the two inputs a, b are vector bits, which means they are 2-bit
input wires. While sum is a 2-bit output wire.

-   [Procedural Blocks](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=27)
-   `initial`
    -   Mostly used in simulation (or initializing registers, depending on
        compiler support)
    -   Could have multiple `initial` block
        <!-- - ```always``` -->
        <!--   - It is used for defining behaviors of **reg** type -->
        <!--   - We will talk more about this in the future -->

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

-   Make sure you select the WebPACK edition (first option). It's free,
    no license required, and has all the features we need.
-   After installed vivado,
    [install board files](https://reference.digilentinc.com/reference/software/vivado/board-files)


<a id="vivado-naming-convention"></a>

## [Vivado Naming Convention](https://www.xilinx.com/support/documentation/sw_manuals/xilinx2017_2/ug973-vivado-release-notes-install-license.pdf#page=5)


<a id="creating-project"></a>

## Creating Project

**Note**: the following screenshots are captured with Vivado 2017.2.1,
layout might be a bit different but you should be able find all the
buttons in 2014 version.

1.  Clone this assignment repo to your local machine, make sure you know
    the path

![img](pics/clone_repo.png "clone\\<sub>repo</sub>")

Note that the path of my assignment repo is
`/home/zcai/repos/digital-logic-lab-05`

1.  Create project Choose your project path and project name **DO NOT**
    create project subdirectory. ![img](pics/startup.png)

when choosing path, make sure:

-   **Uncheck** "create project subdirectory" option, **It's a MUST**
-   Choose the path to be your assignment repository's folder

![img](pics/project_name_marked.png "name\\<sub>and</sub>\\<sub>path</sub>")

Hardware part is not important this time, choose anything and go to
next.

![img](pics/create_project_select_part.png "select\\<sub>part</sub>")

1.  Add or create files
    <!-- - All sources files, i.e. files end with .v extention, must be stored in src directory in your assignment. (If src is not there, create a folder named "src"). -->
    Verilog files can be created inside or outside vivado. If you created
    the file outside vivado, you need to add it to the project when you
    want to use it.

There are two different types of source files to Vivado: - Design
source: Regular modules that can be implmeneted in hardware - Simulation
source: Modules that strickly only used in simulation, usually these are
just modules contain your test code.

There is also a type of file called constraint file that specify your
target hardware's configuration. They are not considered sources, and
are usually provided by hardware vendors. Since we are only doing
simulation here, we won't be need it this time.

**For this lab, I require ALL source files, i.e. both design sources and
simulation sources, to be placed in "src" folder of assignment folder.**
Constraint file should be placed in "constrs" folder.

We will only be dealing with simulation for this lab. So we will need to
create a simulation set. \*Note that, for assignment, I will specify the
exact simulation set's name, you need to name your simulation sets to be
the exact name I specified in the assignment\*

Right click anywhere on "Sources" window, and choose "Edit simulation
Sets &#x2026;": ![img](pics/edit_simulation_set.png)

Then click on the drop down menu and choose "Create Simulation Set &#x2026;"

![img](pics/create_simulation_set_marked.png "create\\<sub>simulation</sub>\\<sub>set</sub>")

We will name the simulation set as "halfadder\\<sub>test</sub>". **Note: there
cannot be space in any simulation set's name**. Since we are going to use
this simulation, we will mark this simulation set as **active**. (You can
also do this in Sources window by right clicking a non-active simulation
set, and choose "make active" from the menu)

![img](pics/edit_simulation_set_make_active_marked.png "make\\<sub>active</sub>")

To add a file click on the "Add Files" button in the same window, browse
and select desired file. However, do make sure **UNCHECK the "copy
sources into project" option**.

![img](pics/add_files_uncheck.png "add\\<sub>files</sub>\\<sub>no</sub>\\<sub>copy</sub>")

In the same window, you can also create file. However, do make sure you
**specify the file location**. Otherwise, Vivado will automatically store
it in a location that will not be tracked by git.

![img](pics/create_file_choose_location.png "choose\\<sub>location</sub>")

The location must be the "src" directory inside your assignment folder

![img](pics/file_location.png "file\\<sub>location</sub>")

This what it looks like after adding a file and creating a file, not
that they both in "src" directory:

![img](pics/files_added_and_created.png "files\\<sub>added</sub>\\<sub>and</sub>\\<sub>created</sub>")

Whenever you are creating a file with Vivado, the following window will
pop up and asking you to specify inputs and outputs. Skip this window,
we will type in inputs and outputs manually.

![img](pics/create_file_IO_spec.png "skip IO")

At the end, you will see the files we added and created will show up in
"Sources" window and under halfadder\\<sub>test</sub>.

![img](pics/added_and_created.png "added\\<sub>and</sub>\\<sub>created</sub>")


<a id="simulation"></a>

## Simulation

Click on run simulation, and here is the default layout:

![img](pics/simulation_default_layout.png "default\\<sub>layout</sub>")

Click on "zoom fit" to have the best view of your timing diagram

![img](pics/zoom_fit_marked.png "zoom\\<sub>fit</sub>")

