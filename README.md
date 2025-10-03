# Week-2-VSD
<details>
  <summary>Part 1 – Theory (Conceptual Understanding)</summary>
# Understanding System-on-Chip (SoC) and BabySoC

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
