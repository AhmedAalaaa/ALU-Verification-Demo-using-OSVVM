# ALU-Verification-Demo-using-OSVVM
## Description
This is a simple Verification environment demo for Arithmetic Logic Unit (ALU) using Open Source VHDL Verification Methodology (OSVVM)

## Overview
OSVVM is an advanced verification methodology that defines a VHDL verification framework, verification utility library, verification component library, and a scripting flow that simplifies your FPGA or ASIC verification project from start to finish. Using these libraries you can create a simple, readable, and powerful testbench that is suitable for either a simple FPGA block or a complex ASIC [\[Ref](https://github.com/OSVVM)\].

## Testbench Framework
The top level testbench Framwork which called sometimes (Test Harness) contains on three main components:

<ul>
  <li>The Device Under Test (DUT)</li>
  <li>The Test Sequencer/Control</li>
  <li>The Verification Component</li>
</ul>

![osvvm](https://user-images.githubusercontent.com/64384499/173165342-ed95767b-fb15-4f03-8588-377fcef109c0.png)

### The DUT
In our case it will be the ALU VHDL code which is intended to be tested, which it is a simple design for ALU whcich contains the follwoing operations:
| Operation   | SEL         |
| :----:      | :----:      |
| Addition    | 000         |
| Subtraction | 001         |
| A - 1       | 010         |
| A + 1       | 011         |
| A AND B     | 100         |
| A OR  B     | 101         |
| NOT A       | 110         |
| A XOR B     | 111         |

And the output will be delayed one clock cycle from the input due to an additional register has been added at the output port.

### The Test Sequencer/ Control
The Test Control contains the test cases that will be fed into our model, in this design there are two main packages have been used from OSVVM Libraries
```vhdl
  library osvvm;
    context osvvm.OsvvmContext ;
    use osvvm.RandomPkg.all;
    use osvvm.CoveragePkg.all;
```
The Randomization Package to feed the inputs signals with random values and the Coverage Package to assure that we have covered all the possible combinations on the inputs.

### Verification Component (ALUController)
The main purpose to this component to compare the output of the DUT with our golded model (the expected result), the main package used here is the Scoreboard Package.
```vhdl
library osvvm;
  context osvvm.OsvvmContext;
  use osvvm.ScoreboardPkg_slv.all;
```
## How to run this demo
First you need to download the OsvvmLibraries, you can simply run this command:
```
  $ git clone --recursive https://github.com/osvvm/OsvvmLibraries
```
after you successfully download the Libraries, you will now need a simulator that can compile VHDL - 2008

Now go to the directory that you have donwloaded the OsvvmLibraries and create a foleder called "sim", open your simulator (in my case ModelSim HDL Simulator), and in the TCL console change the directory to the "sim" directory that you hvae created before and run these commands.
```
source ../OsvvmLibraries/Scripts/StartUp.tcl
build ../OsvvmLibraries/OsvvmLibraries.pro
build ../OsvvmLibraries/DpRam/RunAllTests.pro
```

Now open a new project and add all the soucre files and the testbench files in this project and run this script:
```
source ../OsvvmLibraries/ALU/run.tcl
```

Now go to the "sim" directory you will find the Test report has been generated.
```
%% Log   PASSED  in ALU_INST,   Operation: Add              , SEL: 0  A_i: 0  B_i: 0       expected_RES: U Received : U at 0 ns
%% Log   PASSED  in ALU_INST,   Operation: NOT A            , SEL: 6  A_i: F  B_i: F       expected_RES: 0 Received : 0 at 77 ns
%% Log   PASSED  in ALU_INST,   Operation: A + 1            , SEL: 3  A_i: 0  B_i: 0       expected_RES: 0 Received : 0 at 87 ns
%% Log   PASSED  in ALU_INST,   Operation: NOT A            , SEL: 6  A_i: 3  B_i: D       expected_RES: 1 Received : 1 at 97 ns
%% Log   PASSED  in ALU_INST,   Operation: NOT A            , SEL: 6  A_i: D  B_i: 2       expected_RES: C Received : C at 107 ns
%% Log   PASSED  in ALU_INST,   Operation: NOT A            , SEL: 6  A_i: 4  B_i: 4       expected_RES: 2 Received : 2 at 117 ns
%% Log   PASSED  in ALU_INST,   Operation: A XOR B          , SEL: 7  A_i: 9  B_i: C       expected_RES: B Received : B at 127 ns
%% Log   PASSED  in ALU_INST,   Operation: A XOR B          , SEL: 7  A_i: 5  B_i: F       expected_RES: 5 Received : 5 at 137 ns
...
...
...
```
Note: Do not forget that the result will be delayed one clock cycle due to the register on the output so the result and the expected result will be calculated for the previos opertion and this is handled in the VC. 

### snippt from the waveform 
![image](https://user-images.githubusercontent.com/64384499/173166653-fc64a8b2-04b1-4f08-bcef-472a0f2b0909.png)
