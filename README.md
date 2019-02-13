- [Digital Logic Lab 05 - Verilog Intro](#digital-logic-lab-05---verilog-intro)
  - [References:](#references)
  - [[Transistor Count of CPUs](https://en.wikipedia.org/wiki/Transistor_count)](#transistor-count-of-cpus)
  - [Commonly used HDL (Hardware Description Languages)](#commonly-used-hdl-hardware-description-languages)
  - [Verilog Usage](#verilog)
- [Verilog Intro](#orgb62c4e0)
  - [Basic Building Block &#x2013; modules](#org66cdedb)
  - [Procedural Blocks](#org09ea4fe)
    - [Types](#org9fb25d4)
  - [Data Types:](#org1a8abc7)
    - [wire](#orgf9b40ae)
    - [reg](#org4a3e310)
    - [other types:](#org38c6b65)
  - [Logic Values](#org1cba00a)
  - [Literal Integer Numbers](#org0737ce4)
  - [Operators](#org00f08e7)
  - [Module Instances](#org5125ad9)
  - [Primitive Instances](#org4d33ff1)
  - [Vector bits](#orgee2f835)
  - [Testing](#org142a858)



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


<a id="orgb62c4e0"></a>

# Verilog Intro


<a id="org66cdedb"></a>

## Basic Building Block &#x2013; modules

-   See [Module Definition (page 12)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=12)

```verilog
module module_name
   #(parameter_declaration, parameter_declaration, ...) // <--- optional
   (port_declaration port_name, port_name, ...,
    port_declaration port_name, port_name, ...); // <--- if the module does not have any ports, the empty parenthesis
                                                 //      can be omitted, but the ";" should always be there.
   module_items
endmodule
```

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


<a id="org09ea4fe"></a>

## Procedural Blocks

See [Procedural Blocks (page 27)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=27)


<a id="org9fb25d4"></a>

### Types

-   **Initial** blocks process statements one time
    -   Mostly used for testing.
    -   Sometimes could be used for initializing variables.
-   **always** blocks are an infinite loop which process statements repeatedly.


<a id="org1a8abc7"></a>

## Data Types:

See [Data Type Declarations (page 15)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=15)


<a id="orgf9b40ae"></a>

### wire

-   Used outside procedural blocks
-   Used in IO ports by default
-   Interconnecting wire, connect output to input
-   Its value is driven by whatever the output it is connected to.
-   **Note:** Any variable that is not declared, it is assumed to be 1-bit wire.


<a id="org4a3e310"></a>

### reg

-   The driver (behavior) of any `reg` variable must be define in the module the variable is declared.
-   Used inside procedural blocks
-   Must be declared outside procedural blocks
-   **Note:** reg is **not** register. Used to be, not anymore.
-   When used in IO ports, only outputs can be declared as `reg`


<a id="org38c6b65"></a>

### other types:

There are several other types available in Verilog (see ), but we are going to stick with just `wire` and `reg` in this class.

By default, IO ports are considered as `wire`, unless `reg` is declared, for example:

```verilog
module halfadder (input a, b,       // a, b are implicitly declared as wire
                  output reg s, c); // s, c are explicitly declared as reg

endmodule // halfadder
```


<a id="org1cba00a"></a>

## Logic Values

| Logic Values                          | Description                             |
|------------------------------------- |--------------------------------------- |
| <font color="green"> 0</font>         | zero, low, or false                     |
| <font color="green"> 1</font>         | one, high, or true                      |
| <font color="blue"> *z* or *Z*</font> | high impedence (tri-stated or floating) |
| <font color="red"> *x* or *X*</font>  | unknown or uninitialized or don't-care  |


<a id="org0737ce4"></a>

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


<a id="org00f08e7"></a>

## Operators

See [Operators (page 33)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=33)

```verilog
module halfadder (input a, b,
                  output s, c);

     assign s = a ^ b;  // <---- this is called continues assignment, s must be a "wire" type
     assign c = a & b;

endmodule // halfadder
```

This is always called behavior modeling, since the xor and and operation is done using a operator.


<a id="org5125ad9"></a>

## Module Instances

See [Module Instances (page 21)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=21)

Basic syntax:

```
module_name instance_name  (.port_name(signal), .port_name(signal), ... );
```

Example:

```verilog
module fulladder (input a, b, cin,
                  output sum, cout);

   wire s1, c1, c2;

   halfadder HA1(.a(a), .b(b), .s(s1), .c(c1)); // <-------- the a, b, s, c outside the parenthesis referring to
                                                //           the IO ports of halfadder module
   halfadder HA2(.a(s1), .b(cin), .s(sum), .c(c2));

   assign cout = c1 | c2; // and(cout, c1, c2);

endmodule // fulladder
```


<a id="org4d33ff1"></a>

## Primitive Instances

See [Primitive Instances (page 19)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=23)

This is gate level modeling

```verilog
module halfadder (input a, b,
                  output s, c);

 xor(s, a, b);  // <------- when using primitive instances output is always the first port
 and(c, a, b);

endmodule // halfadder
```


<a id="orgee2f835"></a>

## Vector bits

See [Vector Bit Select and Part Selects (page 16)](http://sutherland-hdl.com/pdfs/verilog_2001_ref_guide.pdf#page=16)

| **Selection**        | **Syntax**                                                                                             |
|-------------------- |------------------------------------------------------------------------------------------------------ |
| Bit Select           | vector<sub>name</sub> [bit<sub>number</sub>]                                                           |
| Constant Part Select | vector<sub>name</sub> [bit<sub>number</sub> : bit<sub>number</sub>]                                    |
| Variable Part Select | vector<sub>name</sub> [starting<sub>bit</sub><sub>number</sub>+:part<sub>select</sub><sub>width</sub>] |
|                      | vector<sub>name</sub> [starting<sub>bit</sub><sub>number</sub>+:part<sub>select</sub><sub>width</sub>] |

Example:

```verilog
module ripple_adder_2bits(input [3:0] a, b,   // <--- both a and b are 2-bit
                          input cin,
                          output [3:0] sum,
                          output cout);
   assign sum = 4'hA;  // <----- sum refers to all 4-bit
   assign sum[1:0] = a[1:0] ^ b[1:0]; // <--- you can select just a part of sum
   assign sum[3-:3] = a[3:1] ^ b[3:1]; // <---- sum[3-:3] is equivalent to sum[3:1] here
endmodule
```


<a id="org142a858"></a>

## Testing

```verilog
module halfadder_test;
   reg a_in, b_in;   // <--- since we need to change inputs, they need to be declared as reg
   wire c_out, s_out; // <---- since the outputs will be driven by the halfadder instance,
                      //       they need to be declared as wire
   halfadder HA(.a(a_in), .b(b_in), .c(c_out), .s(s_out)); // <--- You need to have a instance of
                                                           //      the module you want to build
   initial
      begin
         {a_in, b_in} = 2'b00; // <--- For simplicity we are changing a_in, b_in together
         #10;                  // <--- Need to specify a delay so cat we can observe the output
                               //      for this test case
         {a_in, b_in} = 2'b01; #10;
         {a_in, b_in} = 2'b10; #10;
         {a_in, b_in} = 2'b11; #10;
         $finish;              // <--- If you know exactly how long the testing need to run
                               //      stop the simulation when it is done.
      end
endmodule
```

You can use a for loop for testing, for example:

```verilog
module halfadder_test;
   reg a_in, b_in;   // <--- since we need to change inputs, they need to be declared as reg
   wire c_out, s_out; // <---- since the outputs will be driven by the halfadder instance,
                      //       they need to be declared as wire
   halfadder HA(.a(a_in), .b(b_in), .c(c_out), .s(s_out)); // <--- You need to have a instance of
                                                           //      the module you want to build
   initial
      begin
        integer i;
        for (i = 0; i <= 3; i = i + 1)
          begin
            {a_in, b_in} = i[1:0];
            #10;
          end
        $finish;
      end
endmodule
```
