# Week-2-VSD: BabySoC Fundamentals & Functional Modelling 
<details>
  <summary>Part 1 – Theory (Conceptual Understanding)</summary>
  
## What is a System-on-Chip (SoC)?

A **System-on-a-Chip (SoC)** is essentially a complete computing system built on a single chip. Instead of requiring separate hardware units for the CPU, memory, input/output, and specialized functions, an SoC integrates them all together.  
This makes SoCs the backbone of modern electronics, powering everything from smartphones and wearables to IoT devices, cars, and home appliances.

Key benefits of SoCs include:
- **Compactness**: All major components fit into a small chip.
- **Energy efficiency**: Reduced power consumption, critical for battery-driven devices.
- **High performance**: Faster communication between components due to short on-chip interconnects.
- **Reliability**: Fewer discrete parts mean fewer points of failure.

---

## Components of a Typical SoC

A typical SoC integrates multiple building blocks into one silicon chip:

1. **CPU (Central Processing Unit)**  
   - Acts as the “brain,” handling instructions, data processing, and application logic.  
   - In BabySoC, this role is played by the **RVMYTH RISC-V core**.

2. **Memory**  
   - **RAM**: Temporary workspace for active processes.  
   - **ROM/Flash**: Stores permanent instructions and data.  

3. **Interconnect (Bus/Network-on-Chip)**  
   - Provides communication pathways among CPU, memory, and peripherals.  
   - Ensures data transfer and synchronization across modules.

4. **Peripherals & Specialized Blocks**  
   - **Input/Output Ports**: Enable connectivity with external devices.  
   - **Graphics or DSP Units**: Handle video, audio, or signal processing.  
   - **Power Management**: Controls energy distribution.  
   - In BabySoC, key peripherals include:  
     - **Phase-Locked Loop (PLL)** for stable clock generation.  
     - **10-bit Digital-to-Analog Converter (DAC)** for analog signal output.  

---

## Why BabySoC?

**BabySoC** is a simplified, educational SoC model built using open-source IPs. It integrates:
- **RVMYTH RISC-V CPU** for digital processing,  
- **PLL** for precise clock synchronization, and  
- **DAC** for bridging the digital-to-analog world.  

By keeping the design compact and focusing on a few essential components, BabySoC makes it easier to:
- Learn **how CPUs, clocks, and converters interact** within an SoC,  
- Explore **digital-to-analog interfacing**, and  
- Understand **timing, synchronization, and modular integration** without the overwhelming complexity of industrial SoCs.

**BabySoC Block Diagram:**  
![BabySoC Block Diagram](https://github.com/user-attachments/assets/38253bb7-b658-496d-a043-15402219e089)

---

## The Role of Functional Modeling

Designing a real SoC goes through multiple stages:

1. **Functional Modeling**  
   - High-level behavioral simulation of the SoC.  
   - Ensures that the CPU, memory, PLL, and DAC interact correctly.  
   - Helps in debugging logic early, before committing to hardware.

2. **RTL Design (Register Transfer Level)**  
   - Hardware description in Verilog/VHDL.  
   - Focuses on clock cycles, registers, and data paths.  

3. **Physical Design**  
   - Translating RTL into layouts, gates, and silicon fabrication details.  

**BabySoC** emphasizes **functional modeling** as the crucial first step. By experimenting with BabySoC’s behavior, learners grasp core SoC principles before tackling RTL coding or silicon-level challenges.

**SoC Design Flow Diagram:**  
![SoC Design Flow](https://github.com/user-attachments/assets/54b5e8f9-f03d-4b53-a535-859360589119)

---

## Summary

- A **System-on-Chip** integrates CPU, memory, interconnect, and peripherals into a single chip.  
- **BabySoC** is a small, open-source educational SoC that demonstrates how processors, PLLs, and DACs work together.  
- It provides a **hands-on foundation** in SoC design, bridging theory and practice.  
- Functional modeling with BabySoC equips learners to transition smoothly toward RTL and physical design in real-world SoC development.

---
</details>
<details>
  <summary>Part 2 – Labs (Hands-on Functional Modelling) </summary>
  
## Overview
BabySoC is a minimal System‑on‑Chip (SoC) integration project combining the **RVMYTH RISC‑V core**, **PLL**, and **DAC** modules. The objective is to simulate the SoC behavior before synthesis and visualize signal interactions using GTKWave.

This guide explains how to clone the repository, run the pre‑synthesis simulation, and analyze the resulting waveform.

---

## Repository Setup

### Clone the Repository
```bash
git clone https://github.com/manili/VSDBabySoC.git
```
### Run Pre‑Synthesis Simulation
```bash
cd VSDBabySoC
make pre_synth_sim
```
This command compiles and simulates the design, generating the waveform file:
```bash
output/pre_synth_sim/pre_synth_sim.vcd
```
### View the Waveform
Open the VCD file in GTKWave:
```bash
gtkwave output/pre_synth_sim/pre_synth_sim.vcd
```

---

## Waveform Analysis

### 1. Reset Operation
<img width="640" height="511" alt="Screenshot from 2025-10-04 10-06-32" src="https://github.com/user-attachments/assets/4a678872-257b-47b5-8ed3-cf5240bb9c9f" />

At the beginning of the simulation, the **reset** signal is asserted (`1`), forcing all registers and internal states to their initial conditions. When reset is **deasserted** (`0`), the system transitions to normal operation, confirming that initialization works correctly.

### 2. Clocking
<img width="1170" height="394" alt="Screenshot from 2025-10-04 10-21-58" src="https://github.com/user-attachments/assets/b0f7a8ff-721e-424b-88eb-8ce828e5b2f7" />

`CLK`(highlighted in yellow) is the input clock signal of the **RVMYTH core**. This signal is derived from the output of the PLL. The CLK waveform shows a periodic square wave driving all synchronous elements of the BabySoC. Each rising edge triggers state transitions inside flip-flops and sequential logic.

### 3. Dataflow Between Modules
<img width="1546" height="431" alt="Screenshot from 2025-10-04 11-05-54" src="https://github.com/user-attachments/assets/3833ffc7-24a9-4246-878e-af7d73095db7" />

- **CLK** is the **PLL output** that drives the **RVMYTH core**.  
- **OUT[9:0]** is the core’s **10‑bit bus** feeding the **DAC** as **D[9:0]**.  
- The **first OUT trace (blue)** represents the **DAC’s internal analog output**.  
- The **second OUT trace (yellow)** corresponds to the **top‑level SoC output**.  
- The **top‑level SoC OUT** is **digital** in this simulation and can take only **two values**, so it appears as a **1‑bit step** instead of a continuous analog level.

After reset deasserts, a change on **OUT[9:0]** is followed on subsequent clock cycles by an update on **dac.OUT**, and then a corresponding change on the **top‑level OUT**, demonstrating **producer‑to‑consumer propagation** under the **PLL‑generated clock**.  
This confirms the intended **CPU→DAC dataflow**: the **RVMYTH executes instructions**, updates a register driving **OUT[9:0]**, the **DAC converts** this to an **analog‑modeled level**, and the **SoC boundary reflects it**.  

**Example:**  
In the above example, the core outputs `0x011` (17 in decimal). The **10‑bit DAC** interprets this as a normalized level of `17/1023 ≈ 0.0166`, producing a **small analog step** at its output. However, the **top‑level SoC output** is a **digital signal** that can take only two values, so it reads this low‑level result as `0`.


---

</details>
