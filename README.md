# DC Motor Speed Control Using MATLAB/Simulink

A closed-loop DC motor drive simulation using MATLAB/Simulink to study speed regulation, thyristor-based power conversion, and feedback control.

## Overview

DC motors are widely used in industrial drives because their speed can be controlled by adjusting the applied armature voltage. Closed-loop speed control continuously compares the actual motor speed with a reference value and adjusts the drive input to minimise the speed error.

This project models a thyristor-controlled DC motor drive in MATLAB/Simulink. The system incorporates a four-thyristor converter, a DC motor, speed feedback, and a control system that regulates the motor speed around a reference of 1400 RPM.

The simulation demonstrates the transient response of the motor, including initial overshoot and subsequent speed regulation.

## Objectives

- Model a DC motor drive using MATLAB/Simulink.
- Implement closed-loop motor speed regulation.
- Study thyristor-based power conversion for DC motor control.
- Analyse reference-speed tracking and transient response.
- Observe overshoot and steady-state speed oscillations.
- Understand the application of feedback control in electrical drives.

## Simulink Model

The complete drive system is modelled in MATLAB/Simulink. The block diagram shows the power converter, DC motor, speed feedback, reference input, and firing-pulse generation logic.

![Simulink block diagram of the DC motor speed-control system](results/block_diagram.png)

**Key components of the model:**

- **Thyristor Converter (T1–T4):** Controls the power supplied to the DC motor through controlled rectification.
- **DC Motor:** Converts electrical energy into mechanical rotational energy.
- **Reference Speed:** Specifies the desired motor speed of 1400 RPM.
- **Speed Feedback:** Provides the actual motor speed for comparison with the reference.
- **Load Torque:** A load torque input of 15 is specified in the model; its unit depends on the motor block configuration.
- **Gate Pulse Generation:** Produces the thyristor firing signals according to the implemented control logic.
- **Scope:** Displays the reference and actual motor speed.

The feedback loop compares the reference and actual speed. The controller uses the resulting error to adjust the thyristor firing signals and regulate the motor speed.

## Control Strategy

### Closed-Loop Speed Control

The speed error is defined as:

$$
e_\omega(t)=\omega_{\mathrm{ref}}(t)-\omega(t)
$$

**Where:**

- **eω(t):** Speed error.
- **ωref(t):** Reference motor speed.
- **ω(t):** Actual motor speed.

The controller processes the speed error and adjusts the converter firing signals to bring the motor speed closer to the reference value.

### DC Motor Mathematical Model

For a separately excited DC motor, the armature circuit is described by:

$$
V_a(t)=R_a i_a(t)+L_a\frac{di_a(t)}{dt}+E_b(t)
$$

The back electromotive force is:

$$
E_b(t)=K_e\omega(t)
$$

The electromagnetic torque is:

$$
T_e(t)=K_t i_a(t)
$$

The mechanical dynamics are:

$$
J\frac{d\omega(t)}{dt}+B_m\omega(t)=T_e(t)-T_L(t)
$$

**Where:**

- **Va:** Armature voltage.
- **ia:** Armature current.
- **Ra:** Armature resistance.
- **La:** Armature inductance.
- **Eb:** Back electromotive force.
- **Ke:** Back-EMF constant.
- **Te:** Electromagnetic torque.
- **Kt:** Torque constant.
- **J:** Equivalent moment of inertia.
- **Bm:** Viscous friction coefficient.
- **TL:** Load torque.

These equations describe the general behaviour of a separately excited DC motor. The exact model and parameters depend on the motor configuration used in Simulink.

## Simulation Results

### Closed-Loop Speed Response

The following plot compares the reference motor speed with the actual motor speed over a 10-second simulation.

![Closed-loop DC motor speed response showing reference and actual speed](results/speed_response.png)

**Observations:**

- The reference speed is maintained at **1400 RPM**.
- The actual motor speed rises rapidly toward the reference value.
- The response exhibits an initial overshoot, with the motor speed reaching approximately 1530 RPM.
- Following the overshoot, the actual speed decreases toward the reference.
- The motor speed remains close to 1400 RPM for the remainder of the simulation, with small persistent oscillations.

The response demonstrates successful reference-speed tracking, although the remaining oscillations indicate that the transient and steady-state performance could be investigated further through controller tuning.

## Performance Evaluation

The speed response can be evaluated using the following parameters:

| Performance measure | Description |
|---|---|
| Reference Speed | Desired motor speed of 1400 RPM. |
| Peak Speed | Approximately 1530 RPM, estimated from the plotted response. |
| Maximum Overshoot | Approximately 9.3%, estimated from the plot. |
| Rise Time | Time required for the motor speed to rise toward the reference. |
| Settling Time | Time required for the response to remain within a specified tolerance band. |
| Steady-State Error | Difference between the reference speed and the final average motor speed. |

The estimated overshoot is calculated as:

$$
M_p=\frac{N_{\max}-N_{\mathrm{ref}}}{N_{\mathrm{ref}}}\times100\%
$$

Using the approximate peak speed:

$$
M_p\approx\frac{1530-1400}{1400}\times100\%
$$

$$
M_p\approx9.3\%
$$

The peak speed and overshoot are approximate visual estimates. More accurate values can be obtained from the simulation data. Since small oscillations persist in the plotted response, the settling time should be calculated using a defined tolerance band.

## Technologies Used

- **MATLAB** — modelling and simulation.
- **Simulink** — block-based system modelling.
- **Power Electronics** — thyristor-based controlled rectification.
- **Control Systems** — feedback-based speed regulation.
- **Electrical Machines** — DC motor dynamics and drive operation.

## Requirements

- MATLAB.
- Simulink.
- Any additional toolbox required by the blocks used in the model.

## How to Run

1. Clone the repository:

   ```bash
   git clone https://github.com/FaisalGit-hub/Speed-Control-of-a-DC-Motor.git
   ```

2. Open MATLAB and navigate to the cloned repository folder.

3. Open the Simulink model file included in the repository.

4. Check the motor parameters, controller settings, reference speed, and load torque.

5. Run the simulation using the **Run** button or `Ctrl+T`.

6. Observe the reference and actual motor speed through the Scope block.

7. Experiment with the controller parameters and operating conditions to investigate their effects on speed regulation.

## Repository Structure

```text
Speed-Control-of-a-DC-Motor/
├── README.md
├── [Simulink model file]
└── results/
    ├── block_diagram.png
    └── speed_response.png
```

Replace `[Simulink model file]` with the actual model filename in your repository. Ensure both result images are uploaded to the `results` folder with the exact filenames used in the Markdown image links.

## Possible Extensions

- Tune controller parameters to reduce overshoot and steady-state oscillations.
- Investigate speed regulation under different load torque conditions.
- Analyse armature current and electromagnetic torque during acceleration.
- Compare alternative speed-control strategies.
- Evaluate the response using numerical performance metrics obtained from simulation data.

## Conclusion

This project demonstrates closed-loop DC motor speed control using a thyristor-based converter and MATLAB/Simulink. The simulated response shows that the motor approaches the 1400 RPM reference following an initial overshoot, with small oscillations persisting around the desired speed.

The model provides a practical foundation for understanding electrical drive dynamics, controlled rectification, feedback control, and transient performance analysis.

---

**Project:** DC Motor Speed Control  
**Platform:** MATLAB/Simulink  
**Reference Speed:** 1400 RPM  
**Power Converter:** Four-thyristor controlled converter  
**Primary Analysis:** Closed-loop speed response
