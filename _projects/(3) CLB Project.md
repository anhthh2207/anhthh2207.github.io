---
name: Configurable Logic Block Design, Verification and Optimization
# tools: [Cadence]
image: ..\resources\projects\clb\cover_pic.png

description: This project focuses on optimizing Configurable Logic Blocks (CLB) design by addressing timing hazards, and power-performance trade-offs to minimize the Figure of Merit.


---

# Configurable Logic Block Design, Verification and Optimization
<!-- Configurable Logic Blocks (CLBs) are essential components of Field-Programmable Gate Arrays (FPGAs) that enable dynamic hardware updates and high-speed parallel computations. Designing a CLB involves overcoming challenges such as managing timing hazards among components, optimizing layout and wiring, and balancing power efficiency with computational performance. This project outlines our approach to these challenges and the procedures employed to minimize the Figure of Merit. <br> -->
In this project, I with my teammate, Linh Chu, designed a 16-bit Configurable Logic Block (CLB), a circuit that can model any 4-input combinational logic function. It is an essential block that provides flexibility for Field Programmable Gate Arrays (FPGAs). The circuit was developed in <strong>45nm Salicide 1.0V/1.8V 1P 11M</strong> technology supported in Cadence.

Key Components of the Configurable Logic Block includes:
- [16:1 Lookup Table (LUT)](#161-lookup-table-lut)
- [SRAM Array](#sram-array)
- [Serial In Parallel Out (SIPO) Register](#serial-in-parallel-out-sipo-register)
- [Non-overlapping Clock Generator](#non-overlapping-clock-generator)

Finally, these components are integrated to form a comprehensive CLB design:
- [Configurable Logic Block](#configurable-logic-block-clb)


## 16:1 Lookup Table (LUT)
The first component in our design is the 16:1 LUT. It accepts 4 binary inputs and stores 16 output values, corresponding to 2<sup>4</sup> possible input combinations. When the LUT receives 4 input values, these values are used as an address to look up the corresponding output from the pre-stored array. The beauty of LUT is its configurability; by changing the pre-stored array, the LUT can implement any logical function. 
<figure style="text-align: center;">
  <div style="display: flex; justify-content: center; margin-bottom: 10px;">
    <div style="margin-right: 10px;">
      <img src="..\resources\projects\clb\lut\mux21.png" alt="Image 1" width="400" />
      <p style="text-align: center;">2:1 Multiplexer (MUX) design </p>
    </div>
    <div>
      <img src="..\resources\projects\clb\lut\mux21_sym.png" alt="Image 2" width="300" />
      <p style="text-align: center;">2:1 MUX symbol</p>
    </div>
  </div>
  <!-- <figcaption>Main caption for both subimages</figcaption> -->
</figure>
We begin with the design of a 2:1 MUX (similar to LUT, it selects one of two outputs based on a select line). A LUT can be constructed by connecting 15 MUXes in a tree structure, as shown below. Two CMOS logic inverters at the output function as serve as a buffer, restoring the voltage after pass-transistor logic degradation in the MUXes.
<figure style="text-align: center;">
  <div style="display: flex; justify-content: center; margin-bottom: 10px;">
    <div style="margin-right: 10px;">
      <img src="..\resources\projects\clb\lut\lut.png" alt="Image 1" width="400" />
      <p style="text-align: center;">16-input LUT design</p>
    </div>
    <div>
      <img src="..\resources\projects\clb\lut\lut_symb.png" alt="Image 2" width="300" />
      <p style="text-align: center;">16-input LUT symbol</p>
    </div>
  </div>
  <!-- <figcaption>Main caption for both subimages</figcaption> -->
</figure>


## SRAM Array
<!-- <figure style="text-align: center;">
  <img src="..\resources\projects\clb\sram\sram_cell.png" alt="Single Image" width="400" />
  <figcaption>Main caption for the image</figcaption>
</figure> -->
SRAM cells are used to store the possible outputs for the LUT. The figure below shows the design of a single 6T SRAM cell, whose read-write are controlled by the Bit lines (BL and <span style="text-decoration: overline;">BL</span>) and the Word line (WL) signals through precharge and discharge actions (see a nice [tutorial](https://youtu.be/kU2SsUUsftA?si=ze4-9zVNDbIH421l) about how SRAM cell works).
<figure style="text-align: center;">
  <div style="display: flex; justify-content: center; margin-bottom: 10px;">
    <div style="margin-right: 10px;">
      <img src="..\resources\projects\clb\sram\sram_cell.png" alt="Image 1" width="400" />
      <p style="text-align: center;">6T SRAM cell</p>
    </div>
    <div>
      <img src="..\resources\projects\clb\sram\sram_symbol.png" alt="Image 2" width="300" />
      <p style="text-align: center;">6T SRAM symbol</p>
    </div>
  </div>
  <!-- <figcaption>Main caption for both subimages</figcaption> -->
</figure>
However, to control the memory cell more robustly and facilitate integration with other components, we have designed additional peripherals and ports:

- PC: Precharge condition
- W_EN: Write enable
- WL: Word line
- DATA: Write input
- OUT: Read output
<figure style="text-align: center;">
  <div style="display: flex; justify-content: center; margin-bottom: 10px;">
    <div style="margin-right: 10px;">
      <img src="..\resources\projects\clb\sram\sram_cell_full.png" alt="Image 1" width="400" />
      <p style="text-align: center;">Full SRAM cell with control peripherals</p>
    </div>
    <div>
      <img src="..\resources\projects\clb\sram\sram_cell_full_symbol.png" alt="Image 2" width="300" />
      <p style="text-align: center;">Full SRAM cell symbol</p>
    </div>
  </div>
  <!-- <figcaption>Main caption for both subimages</figcaption> -->
</figure>

Sixteen identical cells are combined into a 16-bit SRAM array.
<figure style="text-align: center;">
  <img src="..\resources\projects\clb\sram\sram_array.png" alt="Single Image" width="800" />
  <figcaption>SRAM array</figcaption>
</figure>



## Serial In Parallel Out (SIPO) Register
To load data into the SRAM array, we use a SIPO register. It converts serial data into parallel data by receiving one bit at a time and then outputting the entire set of taken bits simultaneously as a parallel word.
<figure style="text-align: center;">
  <div style="display: flex; justify-content: center; margin-bottom: 10px;">
    <div style="margin-right: 10px;">
      <img src="..\resources\projects\clb\sipo\ff_noQ_circuit.png" alt="Image 1" width="600" />
      <p style="text-align: center;">D Flip Flop schematic</p>
    </div>
    <div>
      <img src="..\resources\projects\clb\sipo\ff_noQ_symbol.png" alt="Image 2" width="200" />
      <p style="text-align: center;">D Flip Flop symbol</p>
    </div>
  </div>
</figure>

A SIPO register is constructed by cascading 16 D flip-flops, as demonstrated below.
<figure style="text-align: center;">
  <!-- Sub Image 1 -->
  <div style="margin-bottom: 1px;">
    <img src="..\resources\projects\clb\sipo\shift-register-w-arrow.gif" alt="Sub Image 1" width="400" />
    <!-- <p style="text-align: center;">Sub Image 1 Caption</p> -->
  </div>
  <!-- Sub Image 2 -->
  <div style="margin-bottom: 1px;">
    <img src="..\resources\projects\clb\sipo\sipo_visualization.png" alt="Sub Image 2" width="400" />
    <!-- <p style="text-align: center;">Sub Image 2 Caption</p> -->
  </div>
  <!-- Sub Image 3 -->
  <div style="margin-bottom: 1px;">
    <img src="..\resources\projects\clb\sipo\SIPO-1024x452.png" alt="Sub Image 3" width="400" />
    <!-- <p style="text-align: center;">Sub Image 3 Caption</p> -->
  </div>

  <!-- Single main caption for all three subimages -->
  <!-- <figcaption>SIPO funtionality and design [[source]](https://www.build-electronic-circuits.com/shift-register/)</figcaption> -->
  <figcaption>SIPO functionality and design <a href="https://www.build-electronic-circuits.com/shift-register/">[source]</a></figcaption>
</figure>


## Non-overlapping Clock Generator
As can be observed, several components, particularly the flip-flops, utilize both CLK and <span style="text-decoration: overline;">CLK</span> as inputs. Consequently, we developed a module to generate two complementary clock signals from a single source.
<figure style="text-align: center;">
  <div style="display: flex; justify-content: center; margin-bottom: 10px;">
    <div style="margin-right: 10px;">
      <img src="..\resources\projects\clb\clk\clock_circuit.png" alt="Image 1" width="600" />
      <p style="text-align: center;">Non-overlapping clock generator schematic</p>
    </div>
    <div>
      <img src="..\resources\projects\clb\clk\clock_symbol.png" alt="Image 2" width="200" />
      <p style="text-align: center;">Clock generator symbol</p>
    </div>
  </div>
</figure>


## Configurable Logic Block (CLB)
Finally, the above components are assembled to form a complete CLB.
<figure style="text-align: center;">
  <img src="..\resources\projects\clb\CLB_full_design.png" alt="Single Image" width="800" />
  <figcaption>Full design of CLB</figcaption>
</figure>

After benchmarking our design, the performance parameters of the circuit are reported in the table below:
<table style="margin: 0 auto;">
  <thead>
    <tr>
      <th>Metric</th>
      <th>Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Max frequency</td>
      <td>1 GHz</td>
    </tr>
    <tr>
      <td>Loading Energy</td>
      <!-- <td>3.212 × 10⁻³ nJ</td> -->
      <td>3.212 × 10<sup>-3</sup> nJ</td>
    </tr>
    <tr>
      <td>Active Energy</td>
      <td>1.895 × 10<sup>-3</sup> nJ</td>
    </tr>
  </tbody>
</table>
<br>
<p><strong>*</strong> <i>Loading Energy</i>: energy consumed by the entire circuit to load all the data into the SRAM</p>
<p><strong>*</strong> <i>Active Energy</i>: energy consumed to cycle through all possible input combinations from 0 to 15 at the maximum operating frequency</p>

<br>
Here is the overall design procedure from our team for designing a 16-bit CLB. Additionally, the methods for sizing, designing testing schematic, resolving timing hazards, and circuit-level optimization are presented in detail in our report, which will be available upon request. Feel free to reach out if you need any further information or have any questions about the project 😀.
