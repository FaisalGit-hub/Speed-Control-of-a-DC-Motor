# DC Motor Speed Control Using MATLAB/Simulink

## Overview

This project implements a closed-loop speed control system for a separately excited DC motor using a thyristor-based controlled converter and a Proportional-Integral (PI) controller. The system is modelled and simulated in MATLAB/Simulink to analyse the motor's speed response and evaluate the performance of the controller.

The reference speed is set to 1400 RPM. The PI controller processes the speed error and adjusts the converter firing control to regulate the motor speed under a constant load torque.

## Objectives

- Model a separately excited DC motor using MATLAB/Simulink.
- Implement a thyristor-based controlled converter for motor armature voltage control.
- Develop a closed-loop speed control system using a PI controller.
- Analyse the speed response using rise time, settling time, maximum speed, and percentage overshoot.

## Simulink Model

The following figure shows the closed-loop DC motor speed control model developed in MATLAB/Simulink.

![DC Motor Speed Control Simulink Block Diagram](results/block_diagram.png)

### Main Components

- **Thyristor converter:** Controls the armature voltage supplied to the motor.
- **Separately excited DC motor:** Converts electrical energy into mechanical energy.
- **PI controller:** Processes the difference between the reference speed and actual motor speed.
- **Speed feedback:** Feeds the measured motor speed back to the controller.
- **Firing pulse generation circuit:** Generates the triggering signals required to control the thyristors.
- **Reference speed:** The desired motor speed is set to 1400 RPM.
- **Load torque:** A constant load torque is applied during the simulation.

## Control Strategy

A closed-loop PI controller is used to regulate the motor speed.

The speed error is defined as:

$$
e(t) = N_{\mathrm{ref}} - N(t)
$$

where:

- \(N_{\mathrm{ref}}\) is the reference speed.
- \(N(t)\) is the actual motor speed.
- \(e(t)\) is the speed error.

The PI controller output is given by:

$$
u(t) = K_p e(t) + K_i \int_0^t e(\tau)\,d\tau
$$

where \(K_p\) and \(K_i\) are the proportional and integral gains, respectively.

The controller output is used by the firing pulse generation circuit to regulate the thyristor converter. This adjusts the motor's armature voltage and helps the motor speed track the reference value.

## Simulation Results

The following figure shows the motor speed response obtained from the MATLAB/Simulink simulation.

![DC Motor Speed Response](results/speed_response.png)

### Performance Analysis

| Parameter | Value |
|---|---:|
| Reference speed | 1400 RPM |
| Maximum speed | 1524 RPM |
| Percentage overshoot | 8.86% |
| Rise time | Approximately 116 ms |
| Settling time | Approximately 750 ms |
| Controller | PI controller |
| Motor type | Separately excited DC motor |
| Converter type | Thyristor-based controlled converter |
| Load condition | Constant load torque |

### Percentage Overshoot Calculation

The percentage overshoot is calculated as:

$$
M_p = \frac{N_{\max}-N_{\mathrm{ref}}}{N_{\mathrm{ref}}}\times100
$$

Substituting the simulation values:

$$
M_p = \frac{1524-1400}{1400}\times100
$$

Therefore, the percentage overshoot is **8.86%**.

### Observations

- The motor speed initially rises above the reference speed of 1400 RPM.
- The maximum speed reaches approximately 1524 RPM.
- The PI controller reduces the speed error and brings the motor speed towards the reference value.
- The rise time is approximately 116 ms.
- The motor speed approaches steady state in approximately 750 ms.
- The simulation demonstrates closed-loop speed regulation using a thyristor-based converter and PI controller.

*Note: Rise time and settling time are approximate values observed from the simulation response. The settling time depends on the tolerance band used.*

## Tools and Technologies

- MATLAB
- Simulink
- Power Electronics
- DC Motor Drives
- PI Control

## How to Run the Simulation

1. Clone the repository:

   ```bash
   git clone https://github.com/FaisalGit-hub/Speed-Control-of-a-DC-Motor.git
   ```

2. Open MATLAB and navigate to the cloned repository directory.
3. Open `speedControl_dcMotor.slx`.
4. Check the reference speed, PI controller parameters, and load torque settings.
5. Run the simulation.
6. Observe the motor speed response using the Scope and compare it with the reference speed of 1400 RPM.

## Repository Structure

```text
Speed-Control-of-a-DC-Motor/
├── README.md
├── speedControl_dcMotor.slx
└── results/
    ├── block_diagram.png
    └── speed_response.png
```

## Conclusion

A closed-loop speed control system for a separately excited DC motor was modelled and simulated using MATLAB/Simulink. The system uses a thyristor-based controlled converter and a PI controller to regulate motor speed around a reference value of 1400 RPM.

The simulation produced a maximum speed of 1524 RPM, a percentage overshoot of 8.86%, a rise time of approximately 116 ms, and a settling time of approximately 750 ms. The results demonstrate the application of PI control and power electronic converters in DC motor drive speed regulation.
