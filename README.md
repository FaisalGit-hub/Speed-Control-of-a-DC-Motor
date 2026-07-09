# Closed-Loop Speed Control of a DC Machine Using Dual-Loop PI Controllers

## Project Overview
This repository contains a MATLAB/Simulink implementation for the precision speed regulation of a separately excited DC motor driven by a single-phase AC source via a fully controlled thyristor-based bridge rectifier. The system utilizes a nested, discrete **dual-loop cascaded PI control architecture** to decouple electrical and mechanical system dynamics, ensuring high-fidelity velocity tracking and robust current limiting under dynamic load torque conditions.

---

## Architecture & Design Parameters

The model is divided into two primary subsystems: the power/plant stage and the cascaded regulation block.

### 1. Power & Plant Configuration
* **AC Voltage Source:** $230\text{V RMS}$ (Amplitude: $230 \times \sqrt{2}\text{V}$), $50\text{Hz}$ grid source.
* **Converter Bridge:** Four-thyristor fully controlled full-wave bridge ($T_1, T_2, T_3, T_4$) providing variable DC output via pulse-width firing control.
* **DC Machine Parameters (5 HP, 240V, 1750 RPM Preset):**
  * Armature Resistance ($R_a$): $2.581\,\Omega$
  * Armature Inductance ($L_a$): $0.028\,\text{H}$
  * Field Resistance ($R_f$): $281.2\,\Omega$
  * Field Inductance ($L_f$): $156\,\text{H}$
  * Torque & Machine Constant ($K_e, K_t$): $1.8$
* **Mechanical Load:** Configured at a nominal constant load torque ($T_L = 15\,\text{N}\cdot\text{m}$).

### 2. Cascaded Control Loop Structure
To prevent overcurrent damage and decouple fast electrical dynamics from slower mechanical variations, a nested control loop structure is implemented:

* **Outer Speed Loop:** Takes a reference speed ($N_{\text{ref}} = 1400\,\text{RPM}$) and compares it against the measured feedback speed ($N_{\text{actual}}$, converted from $\text{rad/s}$ to $\text{RPM}$ using a $30/\pi$ gain block). The error feeds into the primary PI controller:
  * **Proportional Gain ($P$):** $0.8$
  * **Integral Gain ($I$):** $1.0$
  * **Output Saturation Clamping:** Limited to $\pm 100$ to serve directly as a safe current demand signal ($I_{\rm a\_ref}$).
* **Inner Current Loop:** Compares the dynamically generated $I_{\rm a\_ref}$ against the instantaneous armature current ($I_a$). This fast-acting loop maintains tight current constraints:
  * **Proportional Gain ($P$):** $0.06$
  * **Integral Gain ($I$):** $1.0$
* **Modulation & Firing Logic:** The control signal from the current loop is compared against a repeating linear saw-tooth carrier wave ($[0, 10, 0, -10, 0]$) to generate synchronized gate firing pulses ($P_1, P_2$) for alternating thyristor pairs.

---

## Key Features
* **Anti-Windup Protection:** Integrated output saturation constraints on the controller blocks prevent integrator windup during severe load transitions or startup transients.
* **High-Fidelity Simulation:** Leverages the Simscape Electrical `powergui` block solver configured in a discrete simulation environment with a fixed sample time step of $50\,\mu\text{s}$ ($50\text{e-}6\,\text{s}$).

---

## How to Run

1. **Clone the Repository:**
   ```bash
   git clone [https://github.com/yourusername/dc-machine-dual-loop-control.git](https://github.com/yourusername/dc-machine-dual-loop-control.git)
   cd dc-machine-dual-loop-control
