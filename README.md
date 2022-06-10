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
