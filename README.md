# DC Motor Speed Control Using MATLAB/Simulink

A closed-loop DC motor drive simulation using MATLAB/Simulink, featuring a PI speed controller and a four-thyristor controlled converter.

## Overview

DC motors are widely used in industrial applications because their speed can be regulated by controlling the electrical power supplied to the motor. Closed-loop speed control continuously compares the actual motor speed with a reference value and adjusts the control input to minimise the speed error.

This project models a **separately excited DC motor drive** using MATLAB/Simulink. The system incorporates a four-thyristor controlled converter, a PI speed controller, speed feedback, and a constant load torque.

The simulation investigates the motor's transient response and reference-speed tracking, focusing on rise time, peak overshoot, settling time, and steady-state speed variations.

## Objectives

- Model a separately excited DC motor drive in MATLAB/Simulink.
- Implement closed-loop speed regulation using a PI controller.
- Study the operation of a four-thyristor controlled converter.
- Analyse reference-speed tracking and transient response.
- Evaluate rise time, maximum overshoot, and settling time.
- Understand the role of feedback control in electrical drives.

## Simulink Model

The complete system is modelled in MATLAB/Simulink. The block diagram illustrates the power converter, DC motor, reference-speed input, feedback loop, and thyristor firing-pulse generation subsystem.

![MATLAB/Simulink block diagram of the DC motor speed-control system](results/block_diagram.png)

### Main Components

- **Thyristor Converter (T1–T4):** Controls the electrical power supplied to the motor through controlled rectification.
- **Separately Excited DC Motor:** Converts electrical energy into mechanical rotational energy, with separate armature and field circuits.
- **PI Speed Controller:** Processes the speed error to generate the control command.
- **Reference Speed:** Specifies the desired operating speed of 1400 RPM.
- **Speed Feedback:** Provides the measured motor speed for comparison with the reference.
- **Load Torque:** A constant load torque input of 15 is applied during the simulation.
- **Gate Pulse Generation:** Generates the thyristor firing signals according to the implemented control logic.
- **Scope:** Displays the reference and actual motor speed.

The feedback loop allows the controller to adjust the converter firing signals in response to speed deviations, helping the motor track the reference speed.

## Control Strategy

### PI Speed Control

The speed error is calculated as:

$$
e(t)=N_{\mathrm{ref}}(t)-N_{\mathrm{actual}}(t)
$$

The PI controller generates the control signal according to:

$$
u(t)=K_p e(t)+K_i\int_0^t e(\tau)\,d\tau
$$

**Where:**

- **e(t):** Speed error.
- **Nref:** Reference motor speed.
- **Nactual:** Actual motor speed.
- **u(t):** Controller output.
- **Kp:** Proportional gain.
- **Ki:** Integral gain.

The proportional term responds to the instantaneous speed error, while the integral term accumulates the error over time to improve steady-state accuracy.

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
J\frac{d\omega(t)}{dt}
+B_m\omega(t)=T_e(t)-T_L(t)
$$

**Where:**

- **Va:** Armature voltage.
- **Ra:** Armature resistance.
- **La:** Armature inductance.
- **ia:** Armature current.
- **Eb:** Back electromotive force.
- **Ke:** Back-EMF constant.
- **Kt:** Torque constant.
- **ω:** Angular speed in radians per second.
- **J:** Equivalent moment of inertia.
- **Bm:** Viscous friction coefficient.
- **Te:** Electromagnetic torque.
- **TL:** Load torque.

These equations describe the general behaviour of a separately excited DC motor. The actual parameter values depend on the motor block configuration used in Simulink.

## Simulation Results

### Closed-Loop Speed Response

The following plot compares the reference speed with the actual motor speed over a 10-second simulation.

![Closed-loop DC motor speed response showing reference and actual speed](results/speed_response.png)

### Observations

- The reference speed is maintained at **1400 RPM**.
- The actual motor speed rises rapidly toward the reference.
- The maximum speed reaches **1524 RPM**, resulting in an overshoot of approximately **8.86%**.
- After reaching the peak, the actual speed decreases toward the reference.
- The response has an approximate rise time of **116 ms**.
- The settling time is approximately **750 ms**.
- Small oscillations remain visible around the reference speed during the remainder of the simulation.

The response demonstrates reference-speed tracking under the specified operating conditions. The remaining oscillations provide an opportunity to investigate further PI controller tuning.

## Performance Evaluation

| Performance parameter | Result |
|---|---|
| Reference speed | 1400 RPM |
| Maximum speed | 1524 RPM |
| Peak overshoot | 8.86% |
| Rise time | 116 ms |
| Settling time | Approximately 750 ms |
| Controller | PI |
| Motor type | Separately excited DC motor |
| Load torque | Constant, set to 15 |

The percentage overshoot is calculated as:

$$
M_p=\frac{N_{\max}-N_{\mathrm{ref}}}{N_{\mathrm{ref}}}\times100\%
$$

Substituting the measured peak and reference speeds:

$$
M_p=\frac{1524-1400}{1400}\times100\%
$$

$$
\boxed{M_p=8.86\%}
$$

The motor exhibits a rapid response, reaching its reference-speed region in approximately 116 ms and settling in approximately 750 ms. The settling-time value depends on the tolerance band used to define when the response has settled.

## Technologies Used

- **MATLAB** — modelling and simulation.
- **Simulink** — block-based system modelling.
- **Power Electronics** — thyristor-based controlled rectification.
- **Control Systems** — PI feedback control and speed regulation.
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

4. Verify the motor parameters, PI controller gains, reference speed, and load torque.

5. Run the simulation using the **Run** button or `Ctrl+T`.

6. Observe the reference and actual motor speed using the Scope block.

7. Experiment with the PI controller gains and operating conditions to study their effects on the transient response.

## Repository Structure

```text
Speed-Control-of-a-DC-Motor/
├── README.md
├── [Simulink model file]
└── results/
    ├── block_diagram.png
    └── speed_response.png
```

Replace `[Simulink model file]` with the actual model filename in your repository.

Ensure both images are uploaded to the `results` folder using the exact filenames referenced in the README. GitHub will then display them automatically.

## Possible Extensions

- Tune the PI controller gains to reduce overshoot and persistent oscillations.
- Investigate speed regulation under varying load torque.
- Analyse armature current and electromagnetic torque during acceleration.
- Compare different controller settings under identical operating conditions.
- Calculate rise time, settling time, and steady-state error from exported simulation data.

## Conclusion

This project demonstrates closed-loop speed control of a separately excited DC motor using a PI controller and a four-thyristor controlled converter in MATLAB/Simulink.

For a reference speed of 1400 RPM, the simulated motor response reaches a peak speed of 1524 RPM, corresponding to an overshoot of 8.86%. The response has a rise time of approximately 116 ms and a settling time of approximately 750 ms.

The project provides practical experience in electrical drive modelling, power electronic conversion, feedback control, and transient-response analysis.

---

**Project:** DC Motor Speed Control  
**Platform:** MATLAB/Simulink  
**Motor:** Separately Excited DC Motor  
**Controller:** PI  
**Converter:** Four-Thyristor Controlled Converter  
**Reference Speed:** 1400 RPM
