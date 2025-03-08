---
name: Configurable Logic Block Design, Verification and Optimization
tools: [Cadence]
# image: https://www.sketchappsources.com/resources/source-image/project-neon-groove-music-ui.png
image: ..\resources\projects\clb\cover_pic.png

description: This project focuses on optimizing Configurable Logic Blocks (CLB) design by addressing timing hazards, and power-performance trade-offs to minimize the Figure of Merit.


# external_url: https://www.google.com
---

# Configurable Logic Block (CLB) Design, Verification and Optimization
Configurable Logic Blocks (CLBs) are essential components of Field-Programmable Gate Arrays (FPGAs) that enable dynamic hardware updates and high-speed parallel computations. Designing a CLB involves overcoming challenges such as managing timing hazards among components, optimizing layout and wiring, and balancing power efficiency with computational performance. This project outlines our approach to these challenges and the procedures employed to minimize the Figure of Merit.

## Table of Contents
- [16-input Lookup Table (LUT)](#16-input-lookup-table-lut)
- [SRAM Array Design](#sram-array-design)
- [Non-overlapping Clock generator](#non-overlapping-clock-generator)
- [Serial In Parallel Out (SIPO) Register](#serial-in-parallel-out-sipo-register)
- [Configurable Logic Block](#configurable-logic-block-clb)


### 16-input Lookup Table (LUT)
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


### SRAM Array Design
<!-- <figure style="text-align: center;">
  <img src="..\resources\projects\clb\sram\sram_cell.png" alt="Single Image" width="400" />
  <figcaption>Main caption for the image</figcaption>
</figure> -->
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


<figure style="text-align: center;">
  <img src="..\resources\projects\clb\sram\sram_array.png" alt="Single Image" width="800" />
  <figcaption>SRAM array</figcaption>
</figure>



### Serial In Parallel Out (SIPO) Register
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
  <figcaption>SIPO funtionality and design</figcaption>
</figure>


### Non-overlapping Clock Generator
<figure style="text-align: center;">
  <div style="display: flex; justify-content: center; margin-bottom: 10px;">
    <div style="margin-right: 10px;">
      <img src="..\resources\projects\clb\clk\clock_circuit.png" alt="Image 1" width="600" />
      <p style="text-align: center;">Clock generator schematic</p>
    </div>
    <div>
      <img src="..\resources\projects\clb\clk\clock_symbol.png" alt="Image 2" width="200" />
      <p style="text-align: center;">Clock generator symbol</p>
    </div>
  </div>
</figure>


### Configurable Logic Block (CLB)
<figure style="text-align: center;">
  <img src="..\resources\projects\clb\CLB_full_design.png" alt="Single Image" width="800" />
  <figcaption>Full design of CLB</figcaption>
</figure>
