# Project overview
This project introduces beginners to how a System on Chip (SoC) works using a small open-source design called VSDBabySoC, which is based on the RVMYTH RISC-V processor core. It explains the main components of SoCs, their importance, and how different digital and analog elements work together within a chip.

---
## Understanding SoC Basics  
A System on Chip combines all major functions, including the processor, memory, input/output ports, power control, and sometimes additional modules like Wi-Fi, onto a single chip. This integration makes devices:

- Smaller and more portable  
- Power-efficient  
- Faster and more reliable  
- Cost-effective to produce  

SoCs are used in phones, wearables, IoT devices, and smart appliances because they efficiently handle multiple tasks in limited space.

---
## Types of SoCs  
- Microcontroller-based SoC: For simple, low-power tasks (e.g., sensors, appliances).  
- Microprocessor-based SoC: For complex tasks that run operating systems (e.g., smartphones).  
- Application-Specific SoC: Built for specific, high-speed jobs like graphics or AI.  

---
## The VSDBabySoC Design  
VSDBabySoC is a small educational SoC built using Sky130 technology. It contains:

- RVMYTH (CPU): A simple RISC-V processor that executes instructions and controls data.  
- PLL (Phase-Locked Loop): Generates a stable internal clock so all components work in sync.  
- DAC (Digital-to-Analog Converter): Converts processed digital data into analog signals for audio or video output.  

### The SoC operates as follows:

1. The PLL produces a synchronized clock signal.  
2. The RVMYTH CPU processes data stored in its registers (like r17).  
3. The DAC converts this digital data into analog form, which can be output to devices like TVs or speakers.  

---
## PLL (Phase-Locked Loop)  
A PLL aligns an output signal with the phase and frequency of an input signal. It contains:

- A Phase Detector (compares signals)  
- A Loop Filter (smooths the signal)  
- A Voltage-Controlled Oscillator (adjusts frequency)  

PLLs are preferred over off-chip clocks because on-chip solutions reduce timing delays, jitter, and frequency mismatches that external sources may cause.

---
## DAC (Digital-to-Analog Converter)  
A DAC converts binary digital values into smooth analog voltages or currents. Types include:

- Weighted Resistor DAC: Uses different resistor values for each bit.  
- R-2R Ladder DAC: Uses repeating resistor pairs for easier scalability.  

In VSDBabySoC, a 10-bit DAC means it can represent 1024 levels of analog output, allowing for precise audio or visual signal generation.

---
In Summary  
VSDBabySoC shows how digital and analog building blocks come together in an SoC.

*Digital side:* RVMYTH processor and PLL ensure synchronized processing.  
*Analog side:* DAC creates real-world signals.  

This project helps beginners understand how modern chips blend computation, timing, and signal conversion to power everyday smart devices.
