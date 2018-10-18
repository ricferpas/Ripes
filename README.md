## Ripes
[![Build Status](https://travis-ci.org/mortbopet/Ripes.svg?branch=master)](https://travis-ci.org/mortbopet/Ripes/)

Ripes is a graphical 5-stage processor pipeline simulator and assembly code editor built for the [RISC-V instruction set architecture](https://content.riscv.org/wp-content/uploads/2017/05/riscv-spec-v2.2.pdf), suitable for teaching how assembly level code is executed on a classic pipelined architecture. Ripes is especially suitable for illustrating how concepts such as forwarding and stalling works, giving a visual representation of both cases.
<p align="center">
    <img src="https://github.com/mortbopet/Ripes/blob/master/resources/animation.gif?raw=true" />
</p>

## Features
* **Simulator**:
  * 5-stage graphical pipeline simulator with visualization for multiplexer input selection, register write/enable signals and more.
  * Stage information: Current stage instructions are displayed above each stage, as well as in the instruction memory view
  * Breakpoint setting
  * Supports RISC-V assembly files & RISC-V binary files (extracted *.text* segments) - supported instructions are the **RV32I** Base Instruction Set as well as **RV32M** Standard Extension.
* **Memory**:
  * Display type selection for various display formats (Hex, Decimal, ...)
  * Memory view with features such as scrolling adress saving and adress jumping
* **Editor**:
  * Syntax highlighting and syntax error information
  * Real-time assembler for side-by-side comparison of assembly code and (disassembled) binary code

## Downloading & installation
Prebuilt applications are available for Linux, Windows & Mac/OSX. No installation is required - all required libraries are packaged with the compiled executable - these are available at the [Releases page](https://github.com/mortbopet/Ripes/releases).  
**It is recommended to use the *continuous releases*, since they contain all of the most-recent bug-fixes.**

### Linux
Releases for Linux are distributed in the AppImage format. To run an AppImage:
* Run `chmod a+x` on the AppImage file
* Run the file!
The AppImage for Linux should be compatible with most Linux distributions.

### Windows
For Windows, the C++ runtime library must be available (if not, a msvcp140.dll error will be produced). You most likely already have this installed, but if this is not the case, you download it [here](https://www.microsoft.com/en-us/download/details.aspx?id=48145).

### Mac/OSX
Please note that the Mac/OSX is *mostly untested* and as such, there may be various visual glitches as well as performance issues.

# Usage
The [Ripes wiki](https://github.com/mortbopet/Ripes/wiki) contains various pages relating to writing RISC-V assembly code, as well as a list of the supported simulator features in terms of assembler directives etc.  
To simulate C/C++ code in Ripes, [Matt Godbolt's](https://github.com/mattgodbolt) [Compiler Explorer](https://godbolt.org/) is a fast and easy-to-use web-based tool for generating RISC-V assembly code from C/C++. With minor modifications, the output from Compiler Explorer can be inserted into Ripes and simulated. For instructions on how to run code generated by Compiler Explorer, [refer to this wiki page](https://github.com/mortbopet/Ripes/wiki/Adapting-Compiler-Explorer-generated-RISC-V-assembly-code).

## Editor
Get started by selecting one of the assembly examples through *File->Load Example->assembly*. In the **Editor** tab, you should now see that some RISC-V assembly code is present in the left view.
Try changing some values or adding more instructions - you should see that the right side will change accordingly. By default, this view shows the disassembled version of the binary instructions that the left view has been assembled into.
If you want to view the raw binary information, select *Binary* as *View mode*.

<p align="center">
    <img src="https://github.com/mortbopet/Ripes/blob/master/resources/asmeditorpng.png?raw=true"/>
</p>

## Processor
Once no syntax errors have been found in your assembly code, your code will automatically be assembled and loaded into the simulator.
Switching to the **Processor** tab, you'll be greeted by a datapath picturing a classic 5-stage RISC pipeline architecture. Note that a *Control* component nor most control signals aren't included in the view. This descision has been made to reduce clutter. All control signals are generated in the ID (Instruction decode) stage, and are propagated through the stage-separating registers accordingly.

<p align="center">
    <img src="https://github.com/mortbopet/Ripes/blob/master/resources/processortab.png?raw=true"/>
</p>

Besides the datapath, this tab contains the following elements:
* Simulator control:
    * **(1) Run** will run the program until a breakpoint is encountered or execution is finished. This will postpone updating the visualized datapath until the break is encountered.
    * **(2) Autostepping** will automatically step through the program with a speed determined by the execution speed slider **(5)**. 
    * **(3) Step** is equal to activating the clock signal in the circuit. This will clock next-state signals into the registers, and new signals are calculated (propagate through the circuit)
    * **(4) Reset** resets the simulator, resetting all stages and setting the program counter to point to the first instruction
* **(6) Display all signal values** will show the underlying output signals for most signals in the datapath
* **(7) Pipeline table**: see below
* **(8)** Various buttons are available for zooming & expanding the datapath view
* **(9) Registers** is a view of the value of all registers in the processor, with highlighting for the most-recently used register
* **(10) Instruction memory**: A view of the disassembled instructions that are currently loaded in the processor. This view displays which instructions are present in each pipeline stage, as well as breakpoint setting functionality
Furthermore, the following options are available:

### Pipelining table 
<p align="center">
    <img src="https://github.com/mortbopet/Ripes/blob/master/resources/ptable.PNG?raw=true"/>
</p>
will display a pop-up window with the stage information for the current program. The program must be run to propagate the chart. The pipeline table can be copied and pasted to spreadsheets.

## Memory
Selecting the **Memory** tab will show you three different views:
* Registers - similar to the view presented in the processor tab
* A memory view, where all parts of the program memory can be inspected. To navigate, one can use the scroll view or select one of the predefined destinations (or to a specific address) via the *Go to* combobox. A label for an address can be saved for future use, via. the *Save address* button. 
* A list of the most recent memory accesses. Selecting an entry and pressing *Go to selected address* sets the right side memory view to center at the address for the given entry

<p align="center">
    <img src="https://github.com/mortbopet/Ripes/blob/master/resources/memorytab.png?raw=true"/>
</p>

## Building
Since Ripes is built using pure C++ and Qt, all platforms that support Qt should be able to build and run the app.
Ripes contains no external dependencies and (Assuming you have a Qt environment in your PATH) can be built by the following commands:
```
Unix:               Windows:
cd Ripes/           cd Ripes/
qmake               qmake.exe
make                jom.exe
```
Download Qt for Open Source development at https://www.qt.io/download.
Using the Qt installer, only the prebuilt components for your chosen compiler needs to be selected.

---
Icons kindly provided by Flaticon authors: [Smashicons](https://www.flaticon.com/authors/smashicons), [Freepik](https://www.flaticon.com/authors/freepik), [Vectors Market](https://www.flaticon.com/authors/vectors-market) & [Pixel Buddha](https://www.flaticon.com/authors/pixel-buddha).

<a href="https://www.qt.io/">
    <img src="https://github.com/mortbopet/Ripes/blob/master/resources/QtIcon.png" width="60" height="60" />
</a>
