# refer below link
# caution
# this is an trial and error code can not be trustfull still under construction 🏗️ 🚧 
https://github.com/AdamKlerkx/8-bit-computer-in-python


To be completely honest with you, this code sits somewhere in the middle. It is a genuine simulation of the **Instruction Cycle (Fetch-Decode-Execute)**, but it is "faking" the **Gate-Level Hardware and Control Logic**.
It is a fantastic educational visualizer, but calling it "100% faithful" to the original SAP-1 (Simple As Possible) architecture is a bit of a stretch.
Here is the breakdown of what is actually happening under the hood.
### What is Actually Real (Faithful Simulation)
 * **The Clock Cycle (T-States):** The code genuinely simulates the micro-steps of a CPU. In the stepCPU() function, it actively walks through states T1 through T6. It doesn't just jump to the answer; it executes the Fetch phase (PC -> MAR, PC++, RAM -> IR) sequentially.
 * **Register Transfers:** The data genuinely moves between the simulated components. When an LDA (Load Accumulator) instruction happens, the code genuinely reads from the RAM array and places that value into the A variable.
 * **Opcode Execution:** The code actually parses the hexadecimal instructions loaded into RAM. When it calculates the BODMAS equation, it isn't just printing the expectedTarget it calculated in the setup. It is actively stepping through the opcodes (0x0C, 0x4D, 0x5E, etc.) and processing them one by one.
### Where it is "Faking" It (High-Level Abstraction)
 * **The ALU (Arithmetic Logic Unit):** A true low-level hardware emulator would simulate full-adders, XOR gates, and bitwise logic to perform addition or subtraction. This code bypasses hardware logic entirely and just uses standard Java-level math: A = (A + B) & 0xFF.
 * **Missing Control Words:** In a real SAP-1, the Control Unit (Sequencer) outputs a multi-bit "Control Word" (signals like Ep, Lm, Ce, Li, Ei, etc.). These electrical signals tell the bus buffers to open or close. This visualizer ignores control words completely and just uses direct variable assignment, like MAR = PC.
 * **The Shared Bus:** In real hardware, only one component can write to the W-Bus at a time. Here, the "bus" is just a visual line drawn on the screen (drawWBus()), not a functional data structure acting as a bottleneck.
### The "Extended" Architecture
You should also note that the original SAP-1, designed by Albert Paul Malvino, is extremely limited. It only has five instructions: **LDA, ADD, SUB, OUT,** and **HLT**.
This code refers to itself as an "Extended Architecture" because it adds **MUL, DIV,** and **STA** (Store Accumulator). While adding STA makes it closer to a SAP-2 architecture, hardware multiplication and division require significantly more complex internal ALU circuitry than what exists in a base SAP-1.
### The Verdict
This code is a **high-level functional emulator**. It accurately simulates the *behavior* and *flow* of a simple 8-bit computer for a human to visualize, but it does not simulate the physical electrical architecture (logic gates and control lines) required to actually build one.

