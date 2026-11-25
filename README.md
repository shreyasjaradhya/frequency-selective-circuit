# Dual-Band Frequency-Selective Indicator Circuit

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Domain: Analog Electronics](https://img.shields.io/badge/Domain-Analog%20Circuits-38bdf8.svg)]()
[![Institution: NMAMIT](https://img.shields.io/badge/Institution-NMAM%20Institute%20of%20Technology-green.svg)]()

> Designed, simulated, and hardware-verified a single-input analog frequency-selective indicator circuit for **Analog Electronics Circuits (AEC)**.
> 
> * **LED-1** turns ON when input frequency is **0 – 5 kHz** (Low-Pass Band).
> * **LED-2** turns ON when input frequency is **6 – 12 kHz** (Band-Pass Band).

---

## 👥 Authors & Attribution
* **J Shreyas Aradhya** — `NNM24EC065`
* **Jayanth** — `NNM24EC066`
* **J Anvidh** — `NNM24EC064`
* **Department**: Electronics & Communication Engineering, NMAM Institute of Technology, Nitte

---

## 📐 System Specifications & Frequency Response

| Stage | Input Range | Active Indicator | Filter Topology | Key Components |
|---|---|---|---|---|
| **Band 1** | $0\text{ kHz} - 5\text{ kHz}$ | **LED 1 (Green)** | Passive 1st-order RC LPF + LM358 Buffer | $R_1 = 3.3\text{ k}\Omega, C_1 = 0.01\,\mu\text{F}$ |
| **Band 2** | $6\text{ kHz} - 12\text{ kHz}$ | **LED 2 (Amber/Red)** | Cascaded High-Pass & Low-Pass Filter | $R_{HP} = 2.7\text{ k}\Omega, R_{LP} = 1.3\text{ k}\Omega, C = 0.01\,\mu\text{F}$ |
| **Transition** | $5\text{ kHz} - 6\text{ kHz}$ | Attenuated / Transition band | Mutual transition slope | Peak Detectors + Dual Comparators |

---

## ⚡ Circuit Architecture & Design Calculations

### 1. Low-Pass Filter (0 – 5 kHz)
$$f_c = \frac{1}{2\pi R C}$$
Using $C = 0.01\,\mu\text{F} = 10\text{ nF}$:
$$R = \frac{1}{2\pi \times 5000 \times 10 \times 10^{-9}} \approx 3.18\text{ k}\Omega \implies \text{Standard Value } 3.3\text{ k}\Omega$$

### 2. Band-Pass Filter (6 – 12 kHz)
Cascaded passive High-Pass Filter ($f_{L} = 6\text{ kHz}$) and Low-Pass Filter ($f_{H} = 12\text{ kHz}$):
* **High-Pass Cutoff ($6\text{ kHz}$)**:
  $$R_{HP} = \frac{1}{2\pi \times 6000 \times 10\times 10^{-9}} \approx 2.65\text{ k}\Omega \implies 2.7\text{ k}\Omega$$
* **Low-Pass Cutoff ($12\text{ kHz}$)**:
  $$R_{LP} = \frac{1}{2\pi \times 12000 \times 10\times 10^{-9}} \approx 1.32\text{ k}\Omega \implies 1.3\text{ k}\Omega$$

### 3. Rectification & Threshold Detection
* **Peak Detector**: Fast-recovery Schottky diodes (`1N5819` / `1N4148`) charge smoothing capacitors ($C_{filter} = 100\text{ nF}$) with a discharge bleed resistor ($R_{bleed} = 100\text{ k}\Omega$).
* **Comparators**: LM358 operational amplifiers configured as open-loop voltage comparators comparing rectified envelope against a reference voltage set by a 10 kΩ multi-turn potentiometer.
* **Output Driving**: 330 Ω series current-limiting resistors driving standard high-efficiency 5 mm indicator LEDs.

---

## 🧪 Hardware Verification Matrix

| Test Frequency | Signal Amplitude | LED 1 Status | LED 2 Status | Observation |
|---|---|---|---|---|
| $1.0\text{ kHz}$ | $2.0\text{ V}_{pp}$ | **ON (Bright)** | OFF | In-band pass for LPF |
| $3.5\text{ kHz}$ | $2.0\text{ V}_{pp}$ | **ON** | OFF | Normal LPF operation |
| $5.0\text{ kHz}$ | $2.0\text{ V}_{pp}$ | **ON (Threshold)** | OFF | $-3\text{ dB}$ cutoff boundary |
| $5.5\text{ kHz}$ | $2.0\text{ V}_{pp}$ | OFF | OFF | Stop-band separation guard |
| $6.0\text{ kHz}$ | $2.0\text{ V}_{pp}$ | OFF | **ON (Threshold)** | HPF cutoff boundary reached |
| $9.0\text{ kHz}$ | $2.0\text{ V}_{pp}$ | OFF | **ON (Bright)** | Center of BPF passband |
| $12.0\text{ kHz}$ | $2.0\text{ V}_{pp}$ | OFF | **ON (Threshold)** | Upper cutoff boundary |
| $15.0\text{ kHz}$ | $2.0\text{ V}_{pp}$ | OFF | OFF | High-frequency rejection |

---

## 📁 Repository Structure
```
├── docs/
│   └── AEC_Project_report.pdf    # Full official course engineering project report
├── simulation/
│   └── frequency_selective.cir   # SPICE netlist for LTspice / Multisim
├── schematics/
│   └── circuit_architecture.md   # Detailed stage-by-stage pinout & wiring diagram
├── .gitignore
├── LICENSE
└── README.md
```
