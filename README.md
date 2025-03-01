# 🚀 MIPS Project - Single Cycle & Pipeline Architecture

## 🏗️ Project Overview

This project simulates the MIPS architecture using two main approaches: **Single Cycle** and **Pipeline**. It’s designed to emulate how MIPS instructions are processed and executed on a hardware platform, with functional verification done on a development board. 🎯

The goal is to build an efficient simulation for understanding MIPS instruction flow, control units, and data manipulation in processors. 🖥️⚙️

### 🌟 Functional Elements

1. **Instruction Fetch (IFetch)** 🔍
   - **Role**: Fetches the instruction from memory at the beginning of each cycle.
   - **Purpose**: Ensures that the correct instructions are fetched for execution.

2. **Instruction Decode (ID)** 📜
   - **Role**: Decodes the instruction and prepares it for execution.
   - **Purpose**: Determines the type of instruction and the registers it will operate on.

3. **Execution (EX)** ⚡
   - **Role**: Executes arithmetic/logical operations or prepares branch addresses.
   - **Purpose**: The core of the processor’s logic, responsible for ALU operations, shifts, and more.

4. **Memory (MEM)** 🧠
   - **Role**: Handles data memory operations, such as loading and storing data.
   - **Purpose**: Provides access to both instruction and data memory.

5. **Write-Back (WB)** 💾
   - **Role**: Writes the results of computations back to registers.
   - **Purpose**: Ensures that the results of operations are saved and available for subsequent instructions.

6. **Control Unit (CU)** 🕹️
   - **Role**: Decides which signals to activate in the processor.
   - **Purpose**: Ensures the correct instruction processing flow by managing data paths and control signals.

7. **Monostable Pulse Generator (MPG)** 🕰️
   - **Role**: Generates a single-cycle pulse to synchronize operations.
   - **Purpose**: Controls the timing for instruction fetch and execution, ensuring the correct order of operations.

8. **Seven Segment Display (SSD)** 🔢
   - **Role**: Displays the result of calculations or status codes on a 7-segment display.
   - **Purpose**: Provides real-time feedback on the processor’s status or result.

---
## Single Cycle Implementation RTL Diagram
![Single Cycle](images/SingleCycle.png)
## Pipeline Implementation RTL Diagram
![Pipeline](images/Pipeline.png)
## 🔧 Functionalities Implemented

This project simulates a full MIPS processor by integrating both the **Single Cycle** and **Pipeline** approaches. Here's a closer look at the functionality:

### 1. **Single Cycle Execution** 🕒
In this model, each instruction is executed in a single clock cycle. All stages (fetch, decode, execute, memory, write-back) occur in parallel for one instruction, ensuring that the processor runs in a very straightforward, albeit slower, manner.

### 2. **Pipeline Execution** 🔄
In the pipeline version, instructions are processed in stages: 
- **IF** (Instruction Fetch),
- **ID** (Instruction Decode),
- **EX** (Execute),
- **MEM** (Memory access),
- **WB** (Write-back).

Each stage processes one instruction at a time in parallel with others. This greatly improves processing speed by overlapping the execution of multiple instructions at once. ⚡✨

---

## 🧑‍💻 Implemented Instructions

The following MIPS instructions are implemented in this project:

### Register Instructions 💻

1. **SRA - Shift-Right Arithmetic** (Arithmetic Shift) ↔️
   - **Function**: Shifts the bits of a register to the right while maintaining the sign bit (arithmetic shift).
   - **Control Signals**: `RegDst=1`, `RegWrite=1`, `ALUOp=10`, `ALUCtrl=111`

2. **XOR - Exclusive OR** 🔐
   - **Function**: Performs a bitwise XOR operation between two registers.
   - **Control Signals**: `RegDst=1`, `RegWrite=1`, `ALUOp=10`, `ALUCtrl=110`

---

### Immediate Instructions 💥

1. **BGEZ - Branch on Greater than or Equal to Zero** 🚦
   - **Function**: Conditionally branches if a register is greater than or equal to zero.
   - **Control Signals**: `ExtOp=1`, `Br_gez=1`, `ALUOp=01 (-)`, `ALUCtrl=100`

2. **ORI - OR Immediate** 🔗
   - **Function**: Performs bitwise OR between a register and an immediate value.
   - **Control Signals**: `ALUSrc=1`, `RegWrite=1`, `ALUOp=11`, `ALUCtrl=010`

---

### ⚙️ Key Functional Modifications

- **SRA & XOR**: To implement these operations, modifications were made to the **Control Unit** and the **EX Stage** for performing the respective operations.
- **BGEZ**: A new **"gez"** flag was introduced in the EX stage, indicating whether the register value is greater than or equal to zero. The Control Unit was also updated to manage these branch conditions.
- **ORI**: Similar modifications as the others, involving the **Control Unit** to handle immediate operations.

---

## 💡 Key Features and Functional Flow

### **Instruction Fetching** 🔍
The instruction fetch process ensures that the processor correctly retrieves instructions from memory, beginning the execution cycle. This is done by the **IFetch** unit, which works in tandem with the **Program Counter (PC)**.

### **Instruction Decoding** 📜
The **Instruction Decode (ID)** phase prepares the instruction by interpreting it, setting up the necessary signals, and determining which registers need to be accessed. Here, the **Control Unit** comes into play, guiding the rest of the pipeline stages.

### **Execution Stage** ⚡
During the **EX** phase, the arithmetic and logic operations are performed. The processor executes the instructions based on the decoded values, using the **ALU** to perform operations like shifts and XORs.

### **Memory Access** 🧠
In the **MEM** stage, the processor either reads or writes data to memory, depending on the type of instruction being processed.

### **Write-Back** 💾
Finally, the results from the execution phase are written back to the registers in the **WB** stage, completing the instruction cycle.

---

## 🏁 How to Use

1. **Setup**:
   - Make sure you have the required simulation tools like **ModelSim** or **Vivado** installed.
   - Open the project files in your chosen simulator.

2. **Compilation & Execution**:
   - Compile and run the project using the commands for your simulator.
   - Observe the execution and control signal behaviors.

3. **Test on Hardware** 🖥️:
   - Connect to the development board and load the compiled design to see it in action!
   - Watch how the instructions are executed step-by-step, with real-time feedback displayed on the **Seven Segment Display (SSD)**.
