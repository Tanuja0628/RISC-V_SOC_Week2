# BabySoC Functional Flow: From RTL to Gate-Level Verification  

This repository captures the design and verification journey of the **VSD BabySoC** –  
a small but complete System-on-Chip (SoC) built using open-source tools.  
It integrates:  
- `rvmyth` → a RISC-V CPU core  
- `avsddac` → Digital-to-Analog Converter  
- `avsdpll` → Phase-Locked Loop  

The project demonstrates **RTL-to-Gate flow** with both **pre-synthesis** and **post-synthesis verification**.

---

## 📌 Objectives  

<!-- Why this project is useful -->
- Build a strong foundation in **SoC fundamentals**  
- Practice **functional modeling and verification** of BabySoC  
- Convert RTL to a **gate-level netlist** with the SkyWater 130nm library  
- Verify that **post-synthesis GLS = original RTL behavior**  

---

## 🔧 Tools & Setup  

<!-- Tools required -->
- **Yosys** → Logic synthesis  
- **Icarus Verilog** → Simulation  
- **GTKWave** → Waveform visualization  
- **Sandpiper** → Convert TL-Verilog to Verilog for `rvmyth`  

Command for Sandpiper:  

```bash
pip3 install pyyaml click sandpiper-saas
sandpiper-saas -i ./src/module/*.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir ./src/module/
This generates rvmyth.v, which is used in synthesis and simulation.

📂 Repository Structure
<!-- Tree structure helps new users navigate -->
bash
Copy code
VSDBabySoC/
 ├── assets/            # Images of waveforms, chip stats, synthesis results
 ├── reports/           # Logs and synthesized netlist
 ├── simulation/        # RTL & GLS outputs (.out, .vcd)
 ├── src/               # RTL modules, analog IPs, stubs, configs
 ├── script/            # Yosys synthesis scripts
 └── sdc/               # Timing constraints
🖥️ Workflow
1. RTL Simulation (Pre-Synthesis)
<!-- Pre-synthesis RTL check -->
Run RTL simulation with Icarus Verilog:

bash
Copy code
iverilog -o simulation/pre_synth_sim.out -DPRE_SYNTH_SIM src/module/testbench.v -I src/include -I src/module
cd simulation
./pre_synth_sim.out
gtkwave pre_synth_sim.vcd
✔ Confirms CPU writes to DAC & PLL locks properly.

2. Synthesis with Yosys
<!-- RTL -> Gate level -->
Analog IPs are black-boxed using stubs.

Run synthesis:

bash
Copy code
yosys src/script/yosys_wo_lc_shell.ys | tee reports/logs/synthesis_yosis.log
✔ Produces gate-level netlist → reports/vsdbabysoc_netlist.v

3. Debugging Notes
<!-- Mention fixes during the process -->
Missing includes → added -I src/include in Yosys script

Port mismatches in stubs → corrected IP interfaces

4. Gate-Level Simulation (GLS)
<!-- Post-synthesis verification -->
Simulate synthesized netlist:

bash
Copy code
iverilog -DFUNCTIONAL -DUNIT_DELAY=#1 \
  -o simulation/post_synth_sim.out \
  src/gls_model/primitives.v src/gls_model/sky130_fd_sc_hd.v \
  reports/vsdbabysoc_netlist.v \
  src/module/avsdpll.v src/module/avsddac.v \
  src/module/testbench.v

cd simulation
./post_synth_sim.out
gtkwave dump.vcd
✔ GLS waveform = RTL waveform → functional equivalence verified.

📊 Results
✅ RTL simulation successful

✅ Synthesized netlist generated

✅ Identical waveforms in RTL & GLS

🚀 Conclusion
This project provides a complete RTL-to-GLS verification flow for BabySoC.
The results confirm that the design is functionally sound and ready for Physical Design (PnR).

