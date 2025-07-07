# Simulink Modeling and Control of a Thermal System

This project involves the modeling, simulation, and control of a two-capacitance thermal system using MATLAB & Simulink. The project is divided into two main parts:
1.  **Open-Loop Analysis**: Simulating the system's response to a defined disturbance in the ambient temperature.
2.  **Closed-Loop Control**: Proposing and simulating a proportional (P) control system to regulate the temperature of the first thermal mass.

---

## 1. System Modeling

### 1.1. Physical System
The system consists of two thermal masses, represented by capacitances **$C_1$** and **$C_2$**, connected to each other and to the environment. The thermal energy transfer is modeled by three thermal resistances: **$R_1$**, **$R_2$**, and **$R_3$**.

The system has the following inputs:
* **$q_1$**: Heat flow supplied to the first mass.
* **$q_2$**: Heat flow supplied to the second mass.
* **$\theta_a$**: Ambient temperature, which also acts as a disturbance.

The state variables and outputs of the system are the temperatures of the two masses:
* **$\theta_1$**: Temperature of the first mass.
* **$\theta_2$**: Temperature of the second mass.

### 1.2. Mathematical Model
The dynamic behavior of the system is described by the following set of differential equations, derived from energy balance principles:

$$C_1 \frac{d\theta_1}{dt} = q_1 - \frac{1}{R_1}(\theta_1 - \theta_a) - \frac{1}{R_2}(\theta_1 - \theta_2)$$

$$C_2 \frac{d\theta_2}{dt} = q_2 + \frac{1}{R_2}(\theta_1 - \theta_2) - \frac{1}{R_3}(\theta_2 - \theta_a)$$

### 1.3. System Parameters
The simulations use the following numerical values for the system parameters:

| Parameter | Value     | Unit  |
| :-------- | :-------- | :---- |
| $R_1$     | 1         | K/W   |
| $R_2$     | 5         | K/W   |
| $R_3$     | 10        | K/W   |
| $C_1$     | 250       | J/K   |
| $C_2$     | 300       | J/K   |

---

## 2. Part 1: Open-Loop Simulation

### 2.1. Objective
The goal of this part is to analyze the system's open-loop behavior when subjected to a specific disturbance in the ambient temperature, $\theta_a$. The heat inputs are considered constant at **$q_1 = 1000$ W** and **$q_2 = 1000$ W**.

### 2.2. Disturbance Signal
The disturbance applied to the ambient temperature $\theta_a$ is defined as:

$$\text{Perturbatia}(t) = T_{step} + A \cdot e^{-\alpha t}$$

The parameters for this disturbance are:
* **$T_{step} = 5$**
* **$A = 2$**

### 2.3. Simulation Scenarios
The simulation is performed for three different scenarios, corresponding to three distinct values for the parameter $\alpha$:
1.  **$\alpha = 0.1$**
2.  **$\alpha = 0.5$**
3.  **$\alpha = 1.0$**

The Simulink model simulates the system's response for each of these three cases, showing the evolution of temperatures $\theta_1$ and $\theta_2$ over time.

---

## 3. Part 2: Proportional Control System

### 3.1. Objective
The objective of this part is to propose and implement a closed-loop automatic control system to regulate the temperature of the first mass, $\theta_1$.

### 3.2. Control Strategy
A proportional (P) controller is used. The controller adjusts one of the heat inputs, $q_1$, to maintain $\theta_1$ at a desired setpoint, $\theta_r$.

The control law is given by the deviation of the control signal from its steady-state value ($\bar{u}$):

$$\Delta u = u - \bar{u} = K_p ( \theta_r - \theta_1 )$$

where:
* **$K_p$** is the proportional gain of the controller.
* **$\theta_r$** is the reference (setpoint) temperature.
* **$\theta_1$** is the measured process variable (the temperature of the first mass).

### 3.3. Simulation
The Simulink model is expanded to include this feedback control loop. The simulation demonstrates the controller's effectiveness in tracking the setpoint and rejecting disturbances.

---

## 4. How to Run the Project

1.  **Open the Files**: Launch MATLAB and open the project folder.
2.  **Run Simulink Model**: Open the `.slx` file containing the Simulink model.
3.  **Select Scenario**:
    * For the **open-loop analysis**, ensure the disturbance block is correctly configured for the desired value of $\alpha$.
    * For the **closed-loop simulation**, enable the control loop subsystem.
4.  **Run Simulation**: Click the "Run" button in the Simulink toolbar to start the simulation.
5.  **View Results**: The evolution of the temperatures $\theta_1$ and $\theta_2$ can be observed in the corresponding Scopes within the model.
