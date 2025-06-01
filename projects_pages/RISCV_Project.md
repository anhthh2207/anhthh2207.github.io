---
name: Pipelined RISCV Processor 
# tools: [SystemVerilog, FPGA, Yosys, Cocotb]
image: ../../assets/projects/riscv_core/cover_pic.png
permalink: /projects/riscv/
description: A custom 32-bit RISC-V core featuring a fully pipelined datapath, along with direct-mapped I$ and D$, which interface with memory using the AXIL protocol.


---

# Pipelined RISC-V Processor 
This project was carried out by myself and my teammate, Khanh Tran (Eddie), as part of the CIS 5710 course during Spring 2025 at the University of Pennsylvania.

<figure style="text-align: center;">
  <img src="../../assets/projects/riscv_core/system_architecture.png" alt="Single Image" width="800" />
  <!-- <figcaption>SRAM array</figcaption> -->
</figure>

In this project, we developed a custom 32-bit RISC-V core using SystemVerilog. The technical specifications of our design are as follows:
- **Architecture**: 32-bit RISC-V core implemented in SystemVerilog
- **Pipeline**: Five-stage fully pipelined datapath featuring:
  - Full bypassing (forwarding) logic
  - Comprehensive stall control to handle data and control hazards
- **Cache**:
  - Direct-mapped data cache (D$)
  - Direct-mapped instruction cache (I$) (currently under development)
  - Communication with main memory via the AXI4-Lite protocol
- **Arithmetic Logic**:
  - Carry-Lookahead Adder (CLA) for low-latency arithmetic operations
  - 8-cycle divider to reduce critical path delays and improve maximum clock frequency

<!-- | **Component**        | **Description**                                                                 | -->
<!-- |----------------------|---------------------------------------------------------------------------------|
| **Architecture**     | 32-bit RISC-V core implemented in SystemVerilog                                 |
|----------------------|---------------------------------------------------------------------------------|
| **Pipeline**         | Five-stage fully pipelined datapath featuring:                                  |
|                      | - Full bypassing (forwarding) logic                                             |
|                      | - Comprehensive stall control for data and control hazards                      |
|----------------------|---------------------------------------------------------------------------------|
| **Cache System**     | - Direct-mapped instruction cache (I$) *(currently in progress)*                |
|                      | - Direct-mapped data cache (D$)                                                 |
|                      | - Interfaces with main memory via AXI4-Lite protocol                            |
|----------------------|---------------------------------------------------------------------------------|
| **Arithmetic Logic** | - Carry-Lookahead Adder (CLA) for low-latency arithmetic operations             |
|                      | - 8-cycle divider to reduce critical path delays and improve clock frequency    | -->


Our implementation is functionally correct, as verified by the Dhrystone benchmark. The design was synthesized using the Yosys toolchain and deployed on a Lattice ECP5 FPGA board.

Performance metrics and resource utilization of our  design are reported in the table below:
<table style="margin: 0 auto;">
  <thead>
    <tr>
      <th>Metric</th>
      <th>Without caches</th>
      <th>With caches</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Max frequency</td>
      <td>30.78 MHz</td>
      <td>26.64 MHz</td>
    </tr>
    <tr>
      <td>LUT</td>
      <td>30.9%</td>
      <td>22.8%</td>
    </tr>
    <tr>
      <td>Flip-Flop</td>
      <td>4.1%</td>
      <td>3.9%</td>
    </tr>
    <tr>
      <td>Multiplier Blocks</td>
      <td>3.2%</td>
      <td>2.6%</td>
    </tr>
    <tr>
      <td>BRAM</td>
      <td>1.0%</td>
      <td>15.4%</td>
    </tr>
    <tr>
      <td>I/O Blocks</td>
      <td>4.4%</td>
      <td>4.4%</td>
    </tr>
  </tbody>
</table>
<br>
**Note:** Since the *with-caches* version was later developed, several logic optimizations were made by us. As a result, its LUT and flip-flop usage is slightly more efficient compared to its predecessor.


<div align="center"> <i> As part of the course policy, we are unable to publicly share our code. However, our full SystemVerilog implementation and other technical details can be made available upon request and will be considered on a case-by-case basis (typically shared in cases like recruitment processes or work unrelated to CIS 5710).</i> </div>



<!-- pic sources:
https://stackoverflow.com/questions/71474153/5-stage-risc-how-are-loads-handled
https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.logic-fruit.com%2Fblog%2Fdigital-interfaces%2Faxi-full-axi-lite-interfaces%2F&psig=AOvVaw0pcoEapEplWRkzAPQ5HTrQ&ust=1748064446211000&source=images&cd=vfe&opi=89978449&ved=0CBcQjhxqFwoTCKC7r9TtuI0DFQAAAAAdAAAAABAE
https://github.com/ulx3s -->