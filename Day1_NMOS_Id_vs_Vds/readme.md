
# ⚙️ **Day 1 — Basics of NMOS Drain Current (Id) vs Drain-to-Source Voltage (Vds)**

### *NgspiceSky130 — CMOS Circuit Design and SPICE Simulation Journey*

---

## 📘 **Introduction to Circuit Design and SPICE Simulations**

In this session, we begin our **hands-on journey** into **analog device-level circuit design** using **NGSPICE** with the **Sky130 open-source PDK**.
We start by analyzing the **NMOS transistor**, the fundamental building block of digital and analog ICs, and explore how its **drain current (Id)** varies with **drain-to-source voltage (Vds)** for different **gate voltages (Vgs)**.

---

## 🔍 **Why Do We Need SPICE Simulations?**

SPICE (**Simulation Program with Integrated Circuit Emphasis**) is the heart of all modern circuit design and verification tools.
It helps engineers simulate circuit behavior **before fabrication**, saving time, cost, and debugging effort.

### 🎯 **Key Reasons for Using SPICE Simulations**

1. ✅ **Functional Verification** — Validate the circuit operation under different bias and input conditions.
2. ⚡ **Performance Evaluation** — Check timing, gain, and speed before physical implementation.
3. 🔋 **Power Analysis** — Measure static and dynamic power consumption.
4. 🔧 **Design Optimization** — Tune transistor sizes, bias voltages, and other parameters for efficiency.
5. 🧠 **Learning Insight** — Visualize the relationship between electrical quantities like voltage, current, and threshold behavior.

---

## 🧩 **Introduction to the Basic Element — NMOS Transistor**

An **NMOS transistor** is a **voltage-controlled device** where current flows between **Drain (D)** and **Source (S)** terminals, controlled by the **Gate (G)** voltage.

### 📘 **Structure Overview**

* **Gate (G):** Controls the conductivity of the channel.
* **Source (S):** Where carriers (electrons) enter.
* **Drain (D):** Where carriers leave.
* **Body/Substrate (B):** Usually tied to the lowest potential (GND for NMOS).

🖼️ *Marker for image — "NMOS Structure and Terminals"*

---

## ⚡ **Strong Inversion and Threshold Voltage**

When **V<sub>GS</sub> (Gate-Source Voltage)** exceeds a certain value, called the **Threshold Voltage $(V<sub>th</sub>)$**, the transistor forms a conductive channel between the source and drain.

### ✨ **Key Points**

* Below **V<sub>th</sub>**, transistor is **OFF** (no current flows).
* Above **V<sub>th</sub>**, electrons form a strong inversion layer — the transistor turns **ON**.
* The region where this transition occurs is crucial for switching circuits.

🖼️ *Marker for image — "Strong Inversion vs Weak Inversion"*

---

## 🧲 **Threshold Voltage with Positive Substrate Potential**

When the **substrate (body)** is at a **higher potential than the source**, a **body effect** occurs.
This increases the **threshold voltage**, making it harder to turn ON the NMOS.

### 🧮 **Body Effect Equation**

$[
V_T = V_{T0} + \gamma \left( \sqrt{2\Phi_F + V_{SB}} - \sqrt{2\Phi_F} \right)
]$
Where:

* $(V_{T0})$: Zero-bias threshold voltage
* $(V_{SB})$: Source-to-body voltage
* $(\gamma)$: Body effect coefficient
* $(\Phi_F)$: Fermi potential

🖼️ *Marker for image — "Body Effect Illustration and Equation"*

---

## 🔬 **NMOS Resistive and Saturation Regions**

Now, let’s explore how NMOS behaves in two key operating regions: **Resistive (Linear)** and **Saturation (Active)**.

---

### 🧮 **Resistive Region (Linear Operation)**

Occurs when:
$[
V_{DS} < (V_{GS} - V_T)
]$

Here, the channel is **uniformly formed** along its length, and the transistor acts as a **voltage-controlled resistor**.

**Drain current equation:**
$[
I_D = \mu_n C_{ox} \frac{W}{L} \left[ (V_{GS} - V_T)V_{DS} - \frac{V_{DS}^2}{2} \right]
]$

* Current increases linearly with **V<sub>DS</sub>**.
* Suitable for **analog amplifiers and switches**.

🖼️ *Marker for image — "Linear Region Id-Vds Curve"*

---

### 💨 **Drift Current Theory**

In the linear region:

* Current flow is mainly **drift current** caused by the **electric field** across the channel.
* The induced charge density in the channel at a point *x* is:
  $[
  Q_i(x) = -C_{ox}\left[(V_{GS} - V(x)) - V_T\right]
  ]$
* Drain current:
  $[
  I_D = \mu_n C_{ox} \frac{W}{L} (V_{GS} - V_T - \frac{V_{DS}}{2})V_{DS}
  ]$

🖼️ *Marker for image — "Drift Current Channel Diagram"*

---

### ⚙️ **Pinch-Off Condition and Saturation Region**

When:
$[
V_{DS} \ge (V_{GS} - V_T)
]$

* The channel near the **drain** end depletes — this point is called the **pinch-off point**.
* Beyond this point, **current saturates** and becomes nearly constant.

**Saturation region drain current:**
$[
I_D = \frac{1}{2}\mu_n C_{ox}\frac{W}{L}(V_{GS} - V_T)^2
]$

🖼️ *Marker for image — "Saturation Region Id-Vds Curve with Pinch-off"*

---

### 🧾 **SPICE Observation for Resistive & Saturation Operation**

In **Ngspice**, you can simulate the NMOS transistor behavior by sweeping **V<sub>DS</sub>** for different **V<sub>GS</sub>** values and plotting **I<sub>D</sub>**.

* At low **V<sub>DS</sub>**, Id increases linearly → resistive region.
* At higher **V<sub>DS</sub>**, Id flattens → saturation region.

🖼️ *Marker for image — "Ngspice Simulation: Id-Vds Curves"*

---

## 💻 **Introduction to SPICE**

### ⚙️ **Basic SPICE Setup**

* SPICE netlist (.cir) file defines the **circuit**, **models**, and **simulation commands**.
* Typical setup:

  ```spice
  * NMOS Id vs Vds Simulation
  .include ./models/sky130.lib
  M1 D G S B sky130_fd_pr__nfet_01v8 W=2u L=0.15u
  VGS G S DC 1.8
  VDS D S DC 0
  .dc VDS 0 1.8 0.05 VGS 0.7 1.8 0.2
  .plot dc I(M1)
  .end
  ```

🖼️ *Marker for image — "SPICE Netlist Example"*

---

### ✍️ **Circuit Description in SPICE Syntax**

Each component is defined using a compact syntax:

* **M1** — MOSFET instance name
* **D G S B** — Drain, Gate, Source, Body nodes
* **Model name** — References Sky130 transistor model
* **Parameters** — W (width), L (length)

🧱 Example:
`M1 D G S B sky130_fd_pr__nfet_01v8 W=2u L=0.15u`

---

### 🧪 **Define Technology Parameters**

The `.include` statement adds **Sky130 PDK model files** to ensure accurate transistor behavior:

```spice
.include /usr/local/share/pdk/sky130A/libs.tech/ngspice/sky130.lib.spice
```

🖼️ *Marker for image — "Sky130 Model File Reference"*

---

### 🚀 **First SPICE Simulation**

To run the simulation:

```bash
ngspice nmos_id_vds.cir
```

* Use `.dc` sweep commands for varying **VDS** and **VGS**.
* Observe **Id-Vds characteristics** using Ngspice plot viewer or export data for analysis.

🖼️ *Marker for image — "Ngspice Command-Line Output"*

---

### 🧫 **SPICE Lab with Sky130 Models**

Here, you’ll visualize:

* The **drain current** increasing linearly at first (resistive region).
* Flattening at higher voltages (saturation region).
* Effects of changing **Vgs** on **Id-Vds curves**.

These plots confirm the theoretical **MOSFET I-V relationship** and solidify your understanding of **device physics** through real model simulations.

🖼️ *Marker for image — "Final Ngspice Output Plot — Id vs Vds for multiple Vgs"*

---

## 🧠 **Summary**

| Concept           | Key Takeaway                                                  |
| ----------------- | ------------------------------------------------------------- |
| SPICE Simulation  | Essential for pre-fabrication circuit testing                 |
| NMOS Device       | Controlled by gate voltage (Vgs)                              |
| Resistive Region  | Linear Id–Vds behavior                                        |
| Saturation Region | Current saturates; depends on (Vgs - Vth)²                    |
| Body Effect       | Increases threshold voltage when substrate potential rises    |
| Ngspice           | Practical tool for simulating and visualizing device behavior |

---

## 🔗 **Next Step**

> In **[Day 2](../Day2)**, we’ll explore **velocity saturation** and dive deeper into **CMOS inverter Voltage Transfer Characteristics (VTC)** to bridge transistor-level physics with digital logic behavior. ⚡

---
