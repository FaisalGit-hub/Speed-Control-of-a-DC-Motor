# DC Motor Speed Control Using MATLAB/Simulink

A closed-loop DC motor drive simulation using MATLAB/Simulink to study speed regulation, transient response, and feedback control.

## Overview

DC motors are widely used in industrial drives because their speed can be controlled by adjusting the applied armature voltage. In closed-loop operation, the actual motor speed is continuously compared with the reference speed, and the controller adjusts its output to reduce the resulting error.

This project models a closed-loop DC motor speed-control system in MATLAB/Simulink. The simulation demonstrates how the motor responds to a reference speed command and examines the effectiveness of feedback control in achieving the desired operating speed.

## Objectives

- Model a DC motor drive using MATLAB/Simulink.
- Implement feedback-based speed regulation.
- Analyse the transient response following a speed reference command.
- Observe overshoot and steady-state speed variations.
- Evaluate the ability of the controller to track the reference speed.

## System Model

The closed-loop system consists of the following functional components:

| Component | Function |
|---|---|
| Reference Speed | Specifies the desired motor speed. |
| Feedback Signal | Provides the actual motor speed for comparison. |
| Error Calculation | Determines the difference between reference and actual speed. |
| Speed Controller | Generates a control command based on the speed error. |
| Power Converter | Regulates the electrical input supplied to the motor. |
| DC Motor | Converts electrical energy into mechanical rotation. |

The controller adjusts the motor input according to the speed error, allowing the actual speed to approach the reference value.

## Control Strategy

The speed error is calculated as:

$$
e_\omega(t)=\omega_{\mathrm{ref}}(t)-\omega(t)
$$

**Where:**

- **eω(t):** Speed error.
- **ωref(t):** Reference motor speed.
- **ω(t):** Actual motor speed.

The controller processes this error and adjusts the drive input to regulate motor speed.

## Simulation Results

### Closed-Loop Speed Response

The following plot shows the reference speed and actual motor speed obtained from the Simulink simulation.

![Closed-loop DC motor speed response](results/speed_response.png)

**Observations:**

- The reference speed is set to **1400 RPM**.
- The actual motor speed rises rapidly toward the reference.
- An initial overshoot occurs, with the actual speed temporarily exceeding the desired value.
- The speed subsequently settles toward the reference, with small oscillations remaining in the response.
- The controller maintains the motor speed close to the desired operating point over the remainder of the simulation.

The response demonstrates reference-speed tracking and the transient behaviour of the closed-loop drive.

## Performance Evaluation

The speed response can be evaluated using the following parameters:

| Performance measure | Description |
|---|---|
| Reference Speed | Desired motor speed: 1400 RPM |
| Rise Time | Time taken for the motor speed to rise toward the reference. |
| Maximum Overshoot | Amount by which the peak speed exceeds the reference. |
| Settling Time | Time taken for the response to remain within a specified tolerance band. |
| Steady-State Error | Difference between the reference and final average motor speed. |

These measures can be calculated more precisely using the simulation data. The small persistent oscillations visible in the plot should also be considered when assessing settling time and steady-state performance.

## Technologies Used

- **MATLAB** — modelling and simulation.
- **Simulink** — block-based system modelling.
- **Control Systems** — feedback control and speed regulation.
- **Power Electronics** — electrical power conversion for motor operation.

## Requirements

- MATLAB.
- Simulink.
- Additional toolboxes if required by the blocks used in the model.

## How to Run

1. Clone the repository:

   ```bash
   git clone https://github.com/FaisalGit-hub/Speed-Control-of-a-DC-Motor.git
   ```

2. Open MATLAB and navigate to the downloaded repository folder.

3. Open the Simulink model file included in the repository.

4. Check the motor parameters, controller settings, and reference speed.

5. Run the simulation using the **Run** button or `Ctrl+T`.

6. Observe the reference and actual motor speed through the Scope block.

## Repository Structure

```text
Speed-Control-of-a-DC-Motor/
├── README.md
├── [Simulink model file]
└── results/
    └── speed_response.png
```

Replace the placeholder model filename with the actual file in your repository. The `results` directory contains the speed response displayed in this README.

## Possible Extensions

- Compare different controller gains and their effect on overshoot.
- Investigate speed regulation under varying load torque.
- Analyse armature current and electromagnetic torque during acceleration.
- Compare alternative speed-control strategies.
- Quantitatively evaluate rise time, settling time, and steady-state error using simulation data.

## Conclusion

This project demonstrates closed-loop DC motor speed regulation using MATLAB/Simulink. The simulated response shows that the motor approaches the 1400 RPM reference after an initial overshoot, followed by small persistent oscillations around the desired speed.

The model provides a foundation for studying feedback control, transient response, and speed regulation in electrical drive systems.

---

**Project:** DC Motor Speed Control  
**Platform:** MATLAB/Simulink  
**Reference Speed:** 1400 RPM  
**Primary Analysis:** Closed-loop speed response
