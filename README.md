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

![osvvm](https://user-images.githubusercontent.com/64384499/173164756-8923b930-0172-4c1c-8d1b-1b7213fafbd6.png)

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
