# About, Pre-synthesis simulation and GLS of VSDBabySoC

## What is SOC 
A System on a Chip (SoC) is like a mini-computer built on a single chip. Instead of needing separate parts for each function, an SoC combines everything into one small package. This makes it especially useful for devices where space, power, and efficiency are important, like smartphones, smartwatches, and tablets.

## Components of SOC
1. **CPU (Central Processing Unit)**:
   - The brain of the SoC, handling all main instructions and decisions.
   - Manages tasks like calculations, data processing, and running applications.

2. **Memory**:
   - **RAM** (Random Access Memory) for temporarily storing data as you use the device.
   - **ROM** or **Flash Storage** for keeping information saved even when the device is off.

3. **I/O Ports (Input/Output)**:
   - Connects the SoC to other parts or devices, like a camera, USB, or even your headphones.
   - These ports let the SoC send and receive data externally.

4. **Graphics Processing Unit (GPU)**:
   - Responsible for creating visuals on your screen.
   - Used for gaming, watching videos, or any activity involving images or animations.

5. **Digital Signal Processor (DSP)**:
   - Specialized in processing audio and video signals.
   - Helps with tasks like noise reduction in phone calls or enhancing video quality.

6. **Power Management**:
   - Regulates power usage within the SoC, making sure the chip operates efficiently.
   - This is crucial for extending battery life in portable devices.

7. **Special Features**:
   - Additional features may include Wi-Fi, Bluetooth, and even security modules for safe data handling.
   - These features vary depending on the specific purpose of the SoC.
     
## What is BabySOC and why BabySoC is a simplified model for learning SoC concepts
BabySoC is a very small, simplified open-source System-on-Chip (SoC) design that is used as a teaching and learning platform for SoC design concepts.

- It’s typically built around a RISC-V CPU core (like PicoRV32 or similar).

- Contains minimal peripherals (UART, GPIO, timers).

- Can be run in simulators (like Verilator or Makerchip) or even on FPGAs.

- Designed in TL-Verilog and converted into Verilog/SystemVerilog using tools like SandPiper.

**Why is BabySoC a simplified model for learning**

1. Minimal complexity:

    -  A commercial SoC (like Snapdragon or Apple A-series) has billions of transistors, advanced GPUs, AI accelerators, etc.

    - BabySoC strips this down to the bare essentials → just CPU + memory + a few peripherals.

2. Focus on fundamentals:

    - Teaches how components connect via buses, how CPU interacts with memory and I/O, and how interrupts work — without drowning in complexity.

3. Open-source and educational:

    - Designed for students, hobbyists, and beginners in digital/SoC design.

    - You can simulate it, modify it, and understand it without needing access to proprietary EDA tools.

4. Hands-on experience:

    - Lets learners write Verilog/TL-Verilog, simulate programs running on the CPU, and even load it onto an FPGA to see real execution.

5. Stepping stone:

    - Once you understand BabySoC, it’s easier to scale up to bigger SoCs (e.g., RocketChip, OpenPiton, PULP, etc.).

## What is the role of functional modelling before RTL and physical design stages
Functional modelling is used before RTL design to verify that the system’s behavior matches the specification, without worrying about hardware details.It allows early simulation and debugging of algorithms, protocols, and data flow.
By catching logical/architectural errors early, it saves time before committing to RTL coding.This ensures a smoother transition into RTL implementation and later physical design.

---
## Introduction to VSDBabySoC
VSDBabySoC is a compact yet highly capable System on Chip (SoC) based on the RISC-V architecture. The primary objective of designing this small-scale SoC is to facilitate the simultaneous testing of three open-source intellectual property (IP) cores for the first time while also calibrating its analog components. The VSDBabySoC incorporates an RVMYTH microprocessor, an 8x phase-locked loop (PLL) for generating a stable clock signal, and a 10-bit digital-to-analog converter (DAC) that enables communication with various analog devices.

1. **Initialization and Clock Generation**: Upon receiving an initial input signal, BabySoC activates the PLL. The PLL generates a stable and synchronized clock signal, which is essential for coordinating the activities of the RVMYTH processor and DAC. By synchronizing the system, the PLL ensures that all components operate in harmony, avoiding timing mismatches and ensuring data integrity.

2. **Data Processing in RVMYTH**: Within BabySoC, RVMYTH plays a central role in processing data. Specifically, it utilizes its `r17` register to hold and cycle through values that are used by the DAC. As RVMYTH executes instructions, it sequentially updates `r17` with new data, preparing it for analog conversion. This cyclical processing allows BabySoC to generate continuous data streams that the DAC can output.

3. **Analog Signal Generation via DAC**: The DAC receives the processed digital values from RVMYTH and converts them into an analog signal. This output, saved in a file named `OUT`, can be fed to external devices like TVs and mobile phones, which interpret the analog signals to produce sound or video. This functionality enables BabySoC to interface with consumer electronics, showcasing how digital data can drive multimedia outputs in real-world applications.

   ![333622249-04238eab-4d48-4d57-9061-f8b660a83d6e](https://github.com/user-attachments/assets/38253bb7-b658-496d-a043-15402219e089)


### BabySoC components

   - **RVMYTH (RISC-V CPU)**: RVMYTH is the brain of BabySoC, based on the open-source RISC-V design. It's a simple, customizable CPU that handles processing tasks and communicates with other parts of the SoC. This flexibility makes RVMYTH ideal for learning and experimenting with CPU architecture.

   - **Phase-Locked Loop (PLL)**: The PLL generates a stable clock signal to keep everything in BabySoC running in sync. It matches the SoC's clock with a reference frequency, ensuring reliable timing for RVMYTH and DAC. PLLs are widely used to keep signals aligned in communication and timing circuits.

   - **Digital-to-Analog Converter (DAC)**: The DAC turns digital signals from RVMYTH into analog output, like sound or video. This allows BabySoC to connect with external devices that use analog signals, such as speakers or displays.
