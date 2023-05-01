Download Link: https://assignmentchef.com/product/solved-caa-homework-3
<br>
<h1>Programming</h1>

In this homework, we will use verilog to implement simple ALU, FPU and CPU in this homework.

We use <a href="http://iverilog.icarus.com/">Icarus Verilog</a> to run the simulation, and we use <a href="http://gtkwave.sourceforge.net/">gtkwave</a> to check waveform. We will score your implementations under these settings.

Folder structure for this homework:

HW3

|– ALU                                                                                 // Part 1

|             |– alu.f                                                                         &lt;– specify the files you use

|            ‘– codes                                                                       &lt;– put all the *.v here

|          |                ‘– alu.v

|             |– test_alu                                                              &lt;– run the test

|              |– testbench.v                                                         &lt;– test for corretness

|              ‘– testcases/                                                          &lt;– testcases

|                            ‘– generate.cpp                                          &lt;– used to generate testcases

|– FPU                                                                                 // Part 2

|             |– fpu.f

|            ‘– codes

|          |                ‘– fpu.v

|             |– test_fpu

|              |– testbench.v

|              ‘– testcases/

|                            ‘– generate.cpp

‘– CPU                                                                               // Part 3

|– cpu.f

‘– codes

|                 |– instruction_memory.v                        &lt;– instruction memory with access latency

|              |– data_memory.v                                    &lt;– data memory with access latency

|               ‘– cpu.v

|– test_cpu

|– testbench.v

‘– testcases/

|– generate.s

‘– generate.cpp

<h2>ALU(30%)</h2>

The ALU spec is as follows:

<table width="612">

 <tbody>

  <tr>

   <td width="79">Signal</td>

   <td width="57">I/O</td>

   <td width="52">Width</td>

   <td width="424">Functionality</td>

  </tr>

  <tr>

   <td width="79">i clk</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="424">Clock signal</td>

  </tr>

  <tr>

   <td width="79">i rst n</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="424">Active low asynchronous reset</td>

  </tr>

  <tr>

   <td width="79">i data a</td>

   <td width="57">Input</td>

   <td width="52">32</td>

   <td width="424">Input data A may be signed or unsigned depending on the i inst signal</td>

  </tr>

  <tr>

   <td width="79">i data b</td>

   <td width="57">Input</td>

   <td width="52">32</td>

   <td width="424">Input data B may be signed or unsigned depending on the i inst signal</td>

  </tr>

  <tr>

   <td width="79">i inst</td>

   <td width="57">Input</td>

   <td width="52">4</td>

   <td width="424">Instruction signal representing functions to be performed</td>

  </tr>

  <tr>

   <td width="79">i valid</td>

   <td width="57">input</td>

   <td width="52">1</td>

   <td width="424">One clock signal when input data a and b are valid</td>

  </tr>

  <tr>

   <td width="79">o data</td>

   <td width="57">Output</td>

   <td width="52">32</td>

   <td width="424">Calculation result</td>

  </tr>

  <tr>

   <td width="79">o overflow</td>

   <td width="57">Output</td>

   <td width="52">1</td>

   <td width="424">Overflow signal</td>

  </tr>

  <tr>

   <td width="79">o valid</td>

   <td width="57">Output</td>

   <td width="52">1</td>

   <td width="424">Should be <strong>one cycle signal </strong>when your results are valid</td>

  </tr>

 </tbody>

</table>

The test environment is as follows:

You are asked to implement the following functions in ALU:

<table width="367">

 <tbody>

  <tr>

   <td width="49">i inst</td>

   <td width="100">Function</td>

   <td width="218">Description</td>

  </tr>

  <tr>

   <td width="49"></td>

   <td width="100"></td>

   <td width="218"></td>

  </tr>

  <tr>

   <td width="49">4’d3</td>

   <td width="100">Signed Max</td>

   <td width="218">max(i data a, i data b) (signed)</td>

  </tr>

  <tr>

   <td width="49">4’d4</td>

   <td width="100">Signed Min</td>

   <td width="218">min(i data a, i data b) (signed)</td>

  </tr>

  <tr>

   <td width="49">4’d8</td>

   <td width="100"></td>

   <td width="218"></td>

  </tr>

  <tr>

   <td width="49">4’d9</td>

   <td width="100">Unsigned Min</td>

   <td width="218">min(i data a, i data b) (unsigned)</td>

  </tr>

  <tr>

   <td width="49">4’d10</td>

   <td width="100">And</td>

   <td width="218">i data a &amp; i data b</td>

  </tr>

  <tr>

   <td width="49">4’d11</td>

   <td width="100">Or</td>

   <td width="218">i data a | i data b</td>

  </tr>

  <tr>

   <td width="49">4’d12</td>

   <td width="100">Xor</td>

   <td width="218">i data a ^ i data b</td>

  </tr>

  <tr>

   <td width="49">4’d13</td>

   <td width="100">BitFlip</td>

   <td width="218">~ i data a</td>

  </tr>

  <tr>

   <td width="49">4’d14</td>

   <td width="100">BitReverse</td>

   <td width="218">Bit reverse i data a</td>

  </tr>

 </tbody>

</table>

More details:

<ul>

 <li>We will compare the output data and overflow signal with the provided answers</li>

 <li>For signed 32-bit integer Add, Sub, Mul, Max, Min

  <ul>

   <li>Two-input signal functions</li>

   <li>Overflow signal only needs to be considered when Add, Sub or Mul is performed. For Max and Min, set the output overflow signal to <strong>0</strong>.</li>

   <li>We will <strong>not </strong>compare the return data with the answer provided when overflow happens</li>

  </ul></li>

 <li>For unsigned 32-bit integer Add, Sub, Mul, Max, Min

  <ul>

   <li>Same criteria as signed operations’</li>

  </ul></li>

 <li>Xor, And, Or, BitFlip, and BitReverse

  <ul>

   <li>Set output overflow signal to <strong>0 </strong>when the above functions are performed.</li>

   <li>Xor, And and Or are two-input signal functions.</li>

   <li>BitFilp and BitReverse are one-input signal functions, therefore, i data b can be ignored</li>

  </ul></li>

</ul>

<h2>FPU</h2>

The FPU spec is as follows:

<table width="519">

 <tbody>

  <tr>

   <td width="62">Signal</td>

   <td width="57">I/O</td>

   <td width="52">Width</td>

   <td width="348">Functionality</td>

  </tr>

  <tr>

   <td width="62">i clk</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="348">Clock signal</td>

  </tr>

  <tr>

   <td width="62">i rst n</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="348">Active low asynchronous reset</td>

  </tr>

  <tr>

   <td width="62">i data a</td>

   <td width="57">Input</td>

   <td width="52">32</td>

   <td width="348">Single precision floating point a</td>

  </tr>

  <tr>

   <td width="62">i data b</td>

   <td width="57">Input</td>

   <td width="52">32</td>

   <td width="348">Single precision floating point b</td>

  </tr>

  <tr>

   <td width="62">i inst</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="348">Instruction signal representing functions to be performed</td>

  </tr>

  <tr>

   <td width="62">i valid</td>

   <td width="57">input</td>

   <td width="52">1</td>

   <td width="348">One clock signal when input data a and b are valid</td>

  </tr>

  <tr>

   <td width="62">o data</td>

   <td width="57">Output</td>

   <td width="52">32</td>

   <td width="348">Calculation result</td>

  </tr>

  <tr>

   <td width="62">o valid</td>

   <td width="57">Output</td>

   <td width="52">1</td>

   <td width="348">Should be <strong>one cycle signal </strong>when your results are valid</td>

  </tr>

 </tbody>

</table>

The test environment is as follows:

You are asked to implement the following functions in ALU:

<table width="426">

 <tbody>

  <tr>

   <td width="46">i inst</td>

   <td width="67">Function</td>

   <td width="313">Description</td>

  </tr>

  <tr>

   <td width="46">1’d0</td>

   <td width="67">Add</td>

   <td width="313">i data a + i data b (single precision floating point)</td>

  </tr>

  <tr>

   <td width="46">1’d1</td>

   <td width="67">Mul</td>

   <td width="313">i data a * i data b (single precision floating point)</td>

  </tr>

 </tbody>

</table>

Floating point:

More details:

<ul>

 <li>We will compare the output data with provided answers.</li>

 <li>Follow <a href="https://en.wikipedia.org/wiki/IEEE_754">IEEE-754</a> single precision floating point format</li>

 <li>The inputs will not be denormal numbers, infinites, and NaNs, nor will the calculated result.</li>

 <li>Simple testcases</li>

 <li>During the computation, the one with smaller exponent will be shifted, you should keep the precision until rounding. As for rounding mode, we use default <strong>rounding to nearest even</strong>.

  <ul>

   <li>I find this <a href="http://indico.ictp.it/event/7657/session/3/contribution/12/material/0/0.pdf">pdf</a> useful to explain the rounding and the GRS bits.</li>

   <li>The testcases may be too easy to worry about the rounding.</li>

  </ul></li>

</ul>

You may want to reference the diagram described in class to have better idea implementing FPU.

<h2>CPU</h2>

In this section, you are asked to implement a CPU that supports basic RV64I (not all of them). The CPU spec is as follows:

<table width="686">

 <tbody>

  <tr>

   <td width="101">Signal</td>

   <td width="57">I/O</td>

   <td width="52">Width</td>

   <td width="475">Functionality</td>

  </tr>

  <tr>

   <td width="101">i clk</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="475">Clock signal</td>

  </tr>

  <tr>

   <td width="101">i rst n</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="475">Active low asynchronous reset</td>

  </tr>

  <tr>

   <td width="101">i   valid inst</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="475">One cycle signal when the instruction form instruction memory is ready</td>

  </tr>

  <tr>

   <td width="101">i    inst</td>

   <td width="57">Input</td>

   <td width="52">32</td>

   <td width="475">32-bits instruction from instruction memory</td>

  </tr>

  <tr>

   <td width="101">i     d valid data</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="475">One cycle signal when the data form data memory is ready (used when ld happens)</td>

  </tr>

  <tr>

   <td width="101">i d data</td>

   <td width="57">Input</td>

   <td width="52">64</td>

   <td width="475">64-bits data from data memory (used when ld happens)</td>

  </tr>

  <tr>

   <td width="101">o <u>i </u>valid addr</td>

   <td width="57">Output</td>

   <td width="52">1</td>

   <td width="475">One cycle signal when the pc-address is ready to be sent to instruction memory (fetch the instruction)</td>

  </tr>

  <tr>

   <td width="101">o <u>i </u>addr</td>

   <td width="57">Output</td>

   <td width="52">64</td>

   <td width="475">64-bits address to instruction memory (fetch the instruction)</td>

  </tr>

  <tr>

   <td width="101">o d data</td>

   <td width="57">Output</td>

   <td width="52">64</td>

   <td width="475">64-bits data to data memory (used when sd happens)</td>

  </tr>

  <tr>

   <td width="101">o d addr</td>

   <td width="57">Output</td>

   <td width="52">64</td>

   <td width="475">64-bits address to data memory (used when ld or sd happens)</td>

  </tr>

  <tr>

   <td width="101">o d MemRead</td>

   <td width="57">Output</td>

   <td width="52">1</td>

   <td width="475">One cycle siganl telling data memory that the current mode is reading (used when ld happens)</td>

  </tr>

  <tr>

   <td width="101">o d MemWrite</td>

   <td width="57">Output</td>

   <td width="52">1</td>

   <td width="475">One cycle siganl telling data memory that the current mode is writing (used when sd happens)</td>

  </tr>

  <tr>

   <td width="101">o finish</td>

   <td width="57">Output</td>

   <td width="52">1</td>

   <td width="475">Stop signal when EOF happens</td>

  </tr>

 </tbody>

</table>

The provided instruction memory is as follows:

<table width="443">

 <tbody>

  <tr>

   <td width="57">Signal</td>

   <td width="57">I/O</td>

   <td width="52">Width</td>

   <td width="277">Functionality</td>

  </tr>

  <tr>

   <td width="57">i clk</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="277">Clock signal</td>

  </tr>

  <tr>

   <td width="57">i rst n</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="277">Active low asynchronous reset</td>

  </tr>

  <tr>

   <td width="57">i valid</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="277">Signal that tells pc-address from cpu is ready</td>

  </tr>

  <tr>

   <td width="57">i addr</td>

   <td width="57">Input</td>

   <td width="52">64</td>

   <td width="277">64-bits address from cpu</td>

  </tr>

  <tr>

   <td width="57">o valid</td>

   <td width="57">Output</td>

   <td width="52">1</td>

   <td width="277">Valid when instruction is ready</td>

  </tr>

  <tr>

   <td width="57">o inst</td>

   <td width="57">Output</td>

   <td width="52">32</td>

   <td width="277">32-bits instruction to cpu</td>

  </tr>

 </tbody>

</table>

And the provided data memory is as follows:

<table width="644">

 <tbody>

  <tr>

   <td width="86">Signal</td>

   <td width="57">I/O</td>

   <td width="52">Width</td>

   <td width="449">Functionality</td>

  </tr>

  <tr>

   <td width="86">i clk</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="449">Clock signal</td>

  </tr>

  <tr>

   <td width="86">i rst n</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="449">Active low asynchronous reset</td>

  </tr>

  <tr>

   <td width="86">i data</td>

   <td width="57">Input</td>

   <td width="52">64</td>

   <td width="449">64-bits data that will be stored (used when sd happens)</td>

  </tr>

  <tr>

   <td width="86">i addr</td>

   <td width="57">Input</td>

   <td width="52">64</td>

   <td width="449">Write to or read from target 64-bits address (used when ld or sd happens)</td>

  </tr>

  <tr>

   <td width="86">i MemRead</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="449">One cycle signal and set current mode to reading</td>

  </tr>

  <tr>

   <td width="86">i MemWrite</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="449">One cycle signal and set current mode to writing</td>

  </tr>

  <tr>

   <td width="86">o valid</td>

   <td width="57">Output</td>

   <td width="52">1</td>

   <td width="449">One cycle signal telling data is ready (used when ld happens)</td>

  </tr>

  <tr>

   <td width="86">o data</td>

   <td width="57">Output</td>

   <td width="52">64</td>

   <td width="449">64-bits data from data memory (used when ld happens)</td>

  </tr>

 </tbody>

</table>

The test environment is as follows:

We will only test the instructions highlighted in the red box, as the figures below

And one more instruction to be implemented is

<table width="507">

 <tbody>

  <tr>

   <td width="277">i inst</td>

   <td width="67">Function</td>

   <td width="162">Description</td>

  </tr>

  <tr>

   <td width="277">32’b11111111111111111111111111111111</td>

   <td width="67">Stop</td>

   <td width="162">Stop and set o finish to 1</td>

  </tr>

 </tbody>

</table>

More details:

<ul>

 <li>The instruction_memory.v, data_memory.v and testbench.v files <strong>should not be modified</strong></li>

 <li>We will compare the mem[1024] in data_memory.v result with provided answers to check for correctness</li>

 <li>There are 1024 bytes memory in data memory module and 16×32 bits memory for instruction memory. No invalid access to instruction or data memory will be involved in the testcases. Hence, there is no need to handle these issues.</li>

 <li>All the arithmetic operations here are unsigned, including A + B and A + imm. And there is no need to deal with overflow here.</li>

 <li>You may notice that there’s latency when we want to access the memory

  <ul>

   <li>For instruction memory, when i_valid is set, the instruction memory will stall for 5 cycles, and then return the instruction to cpu</li>

   <li>For data memory, when i_MemRead or i_MemWrite is set, the data memory will stall for 7 cycles in both cases, and then return the data to cpu or write the data to memory</li>

   <li>The latency comes from freezing the module for certain amount of cycles, as shows below</li>

  </ul></li>

</ul>

You may want to reference the block diagram of cpu from slides or textbook to have better idea implementing cpu. Notice that the diagram provided here is single cycle cpu, while in this homework, there’s additional latency accessing memory that needs to be considered.

Grading:

<ul>

 <li>There are 8 testcases. 5% each. (eof, store, load, add, sub, and, or, xor, andi, ori, xori, slli, srli, bne, beq)</li>

</ul>

<h1>Report</h1>

Write a report about how you implement ALU, FPU, and CPU.

You can draw some block diagrams to show your execution method more clearly.

<a href="https://app.diagrams.net/">”draw.io”</a> is suggested to help you to draw the block diagrams easily.

<h1>Programming</h1>

In this homework, we will use verilog to implement simple ALU, FPU and CPU in this homework.

We use <a href="http://iverilog.icarus.com/">Icarus Verilog</a> to run the simulation, and we use <a href="http://gtkwave.sourceforge.net/">gtkwave</a> to check waveform. We will score your implementations under these settings.

Folder structure for this homework:

HW3

|– ALU                                                                                 // Part 1

|             |– alu.f                                                                         &lt;– specify the files you use

|            ‘– codes                                                                       &lt;– put all the *.v here

|          |                ‘– alu.v

|             |– test_alu                                                              &lt;– run the test

|              |– testbench.v                                                         &lt;– test for corretness

|              ‘– testcases/                                                          &lt;– testcases

|                            ‘– generate.cpp                                          &lt;– used to generate testcases

|– FPU                                                                                 // Part 2

|             |– fpu.f

|            ‘– codes

|          |                ‘– fpu.v

|             |– test_fpu

|              |– testbench.v

|              ‘– testcases/

|                            ‘– generate.cpp

‘– CPU                                                                               // Part 3

|– cpu.f

‘– codes

|                 |– instruction_memory.v                        &lt;– instruction memory with access latency

|              |– data_memory.v                                    &lt;– data memory with access latency

|               ‘– cpu.v

|– test_cpu

|– testbench.v

‘– testcases/

|– generate.s

‘– generate.cpp

<h2>ALU(30%)</h2>

The ALU spec is as follows:

<table width="612">

 <tbody>

  <tr>

   <td width="79">Signal</td>

   <td width="57">I/O</td>

   <td width="52">Width</td>

   <td width="424">Functionality</td>

  </tr>

  <tr>

   <td width="79">i clk</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="424">Clock signal</td>

  </tr>

  <tr>

   <td width="79">i rst n</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="424">Active low asynchronous reset</td>

  </tr>

  <tr>

   <td width="79">i data a</td>

   <td width="57">Input</td>

   <td width="52">32</td>

   <td width="424">Input data A may be signed or unsigned depending on the i inst signal</td>

  </tr>

  <tr>

   <td width="79">i data b</td>

   <td width="57">Input</td>

   <td width="52">32</td>

   <td width="424">Input data B may be signed or unsigned depending on the i inst signal</td>

  </tr>

  <tr>

   <td width="79">i inst</td>

   <td width="57">Input</td>

   <td width="52">4</td>

   <td width="424">Instruction signal representing functions to be performed</td>

  </tr>

  <tr>

   <td width="79">i valid</td>

   <td width="57">input</td>

   <td width="52">1</td>

   <td width="424">One clock signal when input data a and b are valid</td>

  </tr>

  <tr>

   <td width="79">o data</td>

   <td width="57">Output</td>

   <td width="52">32</td>

   <td width="424">Calculation result</td>

  </tr>

  <tr>

   <td width="79">o overflow</td>

   <td width="57">Output</td>

   <td width="52">1</td>

   <td width="424">Overflow signal</td>

  </tr>

  <tr>

   <td width="79">o valid</td>

   <td width="57">Output</td>

   <td width="52">1</td>

   <td width="424">Should be <strong>one cycle signal </strong>when your results are valid</td>

  </tr>

 </tbody>

</table>

The test environment is as follows:

You are asked to implement the following functions in ALU:

<table width="367">

 <tbody>

  <tr>

   <td width="49">i inst</td>

   <td width="100">Function</td>

   <td width="218">Description</td>

  </tr>

  <tr>

   <td width="49"></td>

   <td width="100"></td>

   <td width="218"></td>

  </tr>

  <tr>

   <td width="49">4’d3</td>

   <td width="100">Signed Max</td>

   <td width="218">max(i data a, i data b) (signed)</td>

  </tr>

  <tr>

   <td width="49">4’d4</td>

   <td width="100">Signed Min</td>

   <td width="218">min(i data a, i data b) (signed)</td>

  </tr>

  <tr>

   <td width="49">4’d8</td>

   <td width="100"></td>

   <td width="218"></td>

  </tr>

  <tr>

   <td width="49">4’d9</td>

   <td width="100">Unsigned Min</td>

   <td width="218">min(i data a, i data b) (unsigned)</td>

  </tr>

  <tr>

   <td width="49">4’d10</td>

   <td width="100">And</td>

   <td width="218">i data a &amp; i data b</td>

  </tr>

  <tr>

   <td width="49">4’d11</td>

   <td width="100">Or</td>

   <td width="218">i data a | i data b</td>

  </tr>

  <tr>

   <td width="49">4’d12</td>

   <td width="100">Xor</td>

   <td width="218">i data a ^ i data b</td>

  </tr>

  <tr>

   <td width="49">4’d13</td>

   <td width="100">BitFlip</td>

   <td width="218">~ i data a</td>

  </tr>

  <tr>

   <td width="49">4’d14</td>

   <td width="100">BitReverse</td>

   <td width="218">Bit reverse i data a</td>

  </tr>

 </tbody>

</table>

More details:

<ul>

 <li>We will compare the output data and overflow signal with the provided answers</li>

 <li>For signed 32-bit integer Add, Sub, Mul, Max, Min

  <ul>

   <li>Two-input signal functions</li>

   <li>Overflow signal only needs to be considered when Add, Sub or Mul is performed. For Max and Min, set the output overflow signal to <strong>0</strong>.</li>

   <li>We will <strong>not </strong>compare the return data with the answer provided when overflow happens</li>

  </ul></li>

 <li>For unsigned 32-bit integer Add, Sub, Mul, Max, Min

  <ul>

   <li>Same criteria as signed operations’</li>

  </ul></li>

 <li>Xor, And, Or, BitFlip, and BitReverse

  <ul>

   <li>Set output overflow signal to <strong>0 </strong>when the above functions are performed.</li>

   <li>Xor, And and Or are two-input signal functions.</li>

   <li>BitFilp and BitReverse are one-input signal functions, therefore, i data b can be ignored.</li>

  </ul></li>

</ul>

<h2>FPU</h2>

The FPU spec is as follows:

<table width="519">

 <tbody>

  <tr>

   <td width="62">Signal</td>

   <td width="57">I/O</td>

   <td width="52">Width</td>

   <td width="348">Functionality</td>

  </tr>

  <tr>

   <td width="62">i clk</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="348">Clock signal</td>

  </tr>

  <tr>

   <td width="62">i rst n</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="348">Active low asynchronous reset</td>

  </tr>

  <tr>

   <td width="62">i data a</td>

   <td width="57">Input</td>

   <td width="52">32</td>

   <td width="348">Single precision floating point a</td>

  </tr>

  <tr>

   <td width="62">i data b</td>

   <td width="57">Input</td>

   <td width="52">32</td>

   <td width="348">Single precision floating point b</td>

  </tr>

  <tr>

   <td width="62">i inst</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="348">Instruction signal representing functions to be performed</td>

  </tr>

  <tr>

   <td width="62">i valid</td>

   <td width="57">input</td>

   <td width="52">1</td>

   <td width="348">One clock signal when input data a and b are valid</td>

  </tr>

  <tr>

   <td width="62">o data</td>

   <td width="57">Output</td>

   <td width="52">32</td>

   <td width="348">Calculation result</td>

  </tr>

  <tr>

   <td width="62">o valid</td>

   <td width="57">Output</td>

   <td width="52">1</td>

   <td width="348">Should be <strong>one cycle signal </strong>when your results are valid</td>

  </tr>

 </tbody>

</table>

The test environment is as follows:

You are asked to implement the following functions in ALU:

<table width="426">

 <tbody>

  <tr>

   <td width="46">i inst</td>

   <td width="67">Function</td>

   <td width="313">Description</td>

  </tr>

  <tr>

   <td width="46">1’d0</td>

   <td width="67">Add</td>

   <td width="313">i data a + i data b (single precision floating point)</td>

  </tr>

  <tr>

   <td width="46">1’d1</td>

   <td width="67">Mul</td>

   <td width="313">i data a * i data b (single precision floating point)</td>

  </tr>

 </tbody>

</table>

Floating point:

More details:

<ul>

 <li>We will compare the output data with provided answers.</li>

 <li>Follow <a href="https://en.wikipedia.org/wiki/IEEE_754">IEEE-754</a> single precision floating point format</li>

 <li>The inputs will not be denormal numbers, infinites, and NaNs, nor will the calculated result.</li>

 <li>Simple testcases</li>

 <li>During the computation, the one with smaller exponent will be shifted, you should keep the precision until rounding. As for rounding mode, we use default <strong>rounding to nearest even</strong>.

  <ul>

   <li>I find this <a href="http://indico.ictp.it/event/7657/session/3/contribution/12/material/0/0.pdf">pdf</a> useful to explain the rounding and the GRS bits.</li>

   <li>The testcases may be too easy to worry about the rounding.</li>

  </ul></li>

</ul>

You may want to reference the diagram described in class to have better idea implementing FPU.

Grading:

<ul>

 <li>There are 10 test cases for add and mul. Overall, there are 20 test cases.</li>

 <li>0% for each test case</li>

</ul>

<h2>CPU(40%)</h2>

In this section, you are asked to implement a CPU that supports basic RV64I (not all of them). The CPU spec is as follows:

<table width="686">

 <tbody>

  <tr>

   <td width="101">Signal</td>

   <td width="57">I/O</td>

   <td width="52">Width</td>

   <td width="475">Functionality</td>

  </tr>

  <tr>

   <td width="101">i clk</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="475">Clock signal</td>

  </tr>

  <tr>

   <td width="101">i rst n</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="475">Active low asynchronous reset</td>

  </tr>

  <tr>

   <td width="101">i   valid inst</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="475">One cycle signal when the instruction form instruction memory is ready</td>

  </tr>

  <tr>

   <td width="101">i    inst</td>

   <td width="57">Input</td>

   <td width="52">32</td>

   <td width="475">32-bits instruction from instruction memory</td>

  </tr>

  <tr>

   <td width="101">i     d valid data</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="475">One cycle signal when the data form data memory is ready (used when ld happens)</td>

  </tr>

  <tr>

   <td width="101">i d data</td>

   <td width="57">Input</td>

   <td width="52">64</td>

   <td width="475">64-bits data from data memory (used when ld happens)</td>

  </tr>

  <tr>

   <td width="101">o <u>i </u>valid addr</td>

   <td width="57">Output</td>

   <td width="52">1</td>

   <td width="475">One cycle signal when the pc-address is ready to be sent to instruction memory (fetch the instruction)</td>

  </tr>

  <tr>

   <td width="101">o <u>i </u>addr</td>

   <td width="57">Output</td>

   <td width="52">64</td>

   <td width="475">64-bits address to instruction memory (fetch the instruction)</td>

  </tr>

  <tr>

   <td width="101">o d data</td>

   <td width="57">Output</td>

   <td width="52">64</td>

   <td width="475">64-bits data to data memory (used when sd happens)</td>

  </tr>

  <tr>

   <td width="101">o d addr</td>

   <td width="57">Output</td>

   <td width="52">64</td>

   <td width="475">64-bits address to data memory (used when ld or sd happens)</td>

  </tr>

  <tr>

   <td width="101">o d MemRead</td>

   <td width="57">Output</td>

   <td width="52">1</td>

   <td width="475">One cycle siganl telling data memory that the current mode is reading (used when ld happens)</td>

  </tr>

  <tr>

   <td width="101">o d MemWrite</td>

   <td width="57">Output</td>

   <td width="52">1</td>

   <td width="475">One cycle siganl telling data memory that the current mode is writing (used when sd happens)</td>

  </tr>

  <tr>

   <td width="101">o finish</td>

   <td width="57">Output</td>

   <td width="52">1</td>

   <td width="475">Stop signal when EOF happens</td>

  </tr>

 </tbody>

</table>

The provided instruction memory is as follows:

<table width="443">

 <tbody>

  <tr>

   <td width="57">Signal</td>

   <td width="57">I/O</td>

   <td width="52">Width</td>

   <td width="277">Functionality</td>

  </tr>

  <tr>

   <td width="57">i clk</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="277">Clock signal</td>

  </tr>

  <tr>

   <td width="57">i rst n</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="277">Active low asynchronous reset</td>

  </tr>

  <tr>

   <td width="57">i valid</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="277">Signal that tells pc-address from cpu is ready</td>

  </tr>

  <tr>

   <td width="57">i addr</td>

   <td width="57">Input</td>

   <td width="52">64</td>

   <td width="277">64-bits address from cpu</td>

  </tr>

  <tr>

   <td width="57">o valid</td>

   <td width="57">Output</td>

   <td width="52">1</td>

   <td width="277">Valid when instruction is ready</td>

  </tr>

  <tr>

   <td width="57">o inst</td>

   <td width="57">Output</td>

   <td width="52">32</td>

   <td width="277">32-bits instruction to cpu</td>

  </tr>

 </tbody>

</table>

And the provided data memory is as follows:

<table width="644">

 <tbody>

  <tr>

   <td width="86">Signal</td>

   <td width="57">I/O</td>

   <td width="52">Width</td>

   <td width="449">Functionality</td>

  </tr>

  <tr>

   <td width="86">i clk</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="449">Clock signal</td>

  </tr>

  <tr>

   <td width="86">i rst n</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="449">Active low asynchronous reset</td>

  </tr>

  <tr>

   <td width="86">i data</td>

   <td width="57">Input</td>

   <td width="52">64</td>

   <td width="449">64-bits data that will be stored (used when sd happens)</td>

  </tr>

  <tr>

   <td width="86">i addr</td>

   <td width="57">Input</td>

   <td width="52">64</td>

   <td width="449">Write to or read from target 64-bits address (used when ld or sd happens)</td>

  </tr>

  <tr>

   <td width="86">i MemRead</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="449">One cycle signal and set current mode to reading</td>

  </tr>

  <tr>

   <td width="86">i MemWrite</td>

   <td width="57">Input</td>

   <td width="52">1</td>

   <td width="449">One cycle signal and set current mode to writing</td>

  </tr>

  <tr>

   <td width="86">o valid</td>

   <td width="57">Output</td>

   <td width="52">1</td>

   <td width="449">One cycle signal telling data is ready (used when ld happens)</td>

  </tr>

  <tr>

   <td width="86">o data</td>

   <td width="57">Output</td>

   <td width="52">64</td>

   <td width="449">64-bits data from data memory (used when ld happens)</td>

  </tr>

 </tbody>

</table>

The test environment is as follows:

We will only test the instructions highlighted in the red box, as the figures below

And one more instruction to be implemented is

<table width="507">

 <tbody>

  <tr>

   <td width="277">i inst</td>

   <td width="67">Function</td>

   <td width="162">Description</td>

  </tr>

  <tr>

   <td width="277">32’b11111111111111111111111111111111</td>

   <td width="67">Stop</td>

   <td width="162">Stop and set o finish to 1</td>

  </tr>

 </tbody>

</table>

More details:

<ul>

 <li>The instruction_memory.v, data_memory.v and testbench.v files <strong>should not be modified</strong></li>

 <li>We will compare the mem[1024] in data_memory.v result with provided answers to check for correctness</li>

 <li>There are 1024 bytes memory in data memory module and 16×32 bits memory for instruction memory. No invalid access to instruction or data memory will be involved in the testcases. Hence, there is no need to handle these issues.</li>

 <li>All the arithmetic operations here are unsigned, including A + B and A + imm. And there is no need to deal with overflow here.</li>

 <li>You may notice that there’s latency when we want to access the memory

  <ul>

   <li>For instruction memory, when i_valid is set, the instruction memory will stall for 5 cycles, and then return the instruction to cpu</li>

   <li>For data memory, when i_MemRead or i_MemWrite is set, the data memory will stall for 7 cycles in both cases, and then return the data to cpu or write the data to memory</li>

   <li>The latency comes from freezing the module for certain amount of cycles, as shows below</li>

  </ul></li>

</ul>

You may want to reference the block diagram of cpu from slides or textbook to have better idea implementing cpu. Notice that the diagram provided here is single cycle cpu, while in this homework, there’s additional latency accessing memory that needs to be considered.


