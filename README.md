---

# ⚡ Week 4 — CMOS Circuit Design using Sky130 PDK

## 🧩 RISC-V Reference SoC Tapeout Program

Welcome to **Week 4** of the **RISC-V SoC Tapeout Program**, where we shift from digital abstractions to the **transistor-level fundamentals** that power every gate on silicon. 🌱

This week, you’ll simulate and analyze CMOS devices using **Ngspice** with the **Sky130 PDK**, exploring how **transistor physics** directly shapes **timing, power, and reliability** in real chips. Each day builds toward mastering how analog device behavior drives digital performance. ⚙️💡

---

## 📚 Week 4 — Task Overview

| Day       | Focus Area                                                      | Folder Link                            | Description                                                                                                                                    |
| --------- | --------------------------------------------------------------- | -------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **Day 1** | 🔍 **NMOS Drain Current (Id) vs Drain-to-Source Voltage (Vds)** | [Day1](./Day1_NMOS_Id_vs_Vds)          | Simulate **Id–Vds** curves for NMOS under various **Vgs**, identify linear and saturation regions, and understand channel-length modulation.   |
| **Day 2** | ⚡ **Velocity Saturation & CMOS Inverter VTC**                   | [Day2](./Day2_CMOS_VTC)                | Explore **Id–Vgs** behavior, estimate **Vth**, build a CMOS inverter, and plot its **Voltage Transfer Characteristic (VTC)**.                  |
| **Day 3** | ⏱️ **Switching Threshold & Dynamic Simulation**                 | [Day3](./Day3_CMOS_Switching_Dynamics) | Apply a pulse input to the inverter and analyze its **transient response**, extracting the **switching threshold** and **propagation delays**. |
| **Day 4** | 🧮 **Noise Margin & Robustness Evaluation**                     | [Day4](./Day4_Noise_Margin_Robustness) | From the VTC, compute **VOH**, **VOL**, **VIH**, **VIL** and determine **Noise Margins (NMH, NML)** to assess circuit stability.               |
| **Day 5** | ⚙️ **Power Supply & Device Variation Analysis**                 | [Day5](./Day5_Power_Supply_Variation)  | Analyze how **VDD** scaling and **W/L ratio changes** affect the inverter’s switching point, delay, and overall robustness.                    |

---

## 🌟 Key Learnings

By the end of this week, you will:

* 🧠 Understand **NMOS/PMOS device characteristics** in deep-submicron technology.
* ⚙️ Build and analyze a **CMOS inverter** from first principles.
* 📈 Evaluate **switching thresholds**, **rise/fall delays**, and **noise margins**.
* 🔋 Explore **power-supply and device variation** effects on timing.
* 🔍 Connect **analog transistor behavior** with **digital timing closure** concepts in later STA stages.

---

## 📂 Repository Structure

```
Week4_CMOS_Circuit_Design_sky130/
│
├── Day1_NMOS_Id_vs_Vds/
├── Day2_CMOS_VTC/
├── Day3_CMOS_Switching_Dynamics/
├── Day4_Noise_Margin_Robustness/
├── Day5_Power_Supply_Variation/
└── README.md
```

Each folder includes:

* 🧾 Ngspice netlist (`.cir`)
* 📊 Simulation plots (`.png`)
* 🧩 Analysis and conclusion notes

---

## 🔜 **Next Step**

> **![In Week 5](https://github.com/Nideshkanna/Week5_STA_TimingClosure_sky130)**, we move from device-level insights to **Post-Layout STA and Timing Closure**, applying parasitic data (SPEF) extracted from **OpenROAD/OpenLane** to perform final sign-off analysis. 🕒💫

---
