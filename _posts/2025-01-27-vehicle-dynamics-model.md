---
title: Vehicle Dynamics Simulink Model homepage
date: 2025-01-27 12:00:00
categories: [dynamics,simulation]
tags: [dynamics,control,vehicle,motor]
---

# Welcome

## Abstract

In this report, we simulate the implementation of a controller for the longitudinal and lateral dynamics of an electric vehicle using BLDC motors to implement the direct torque control technique. For both cases, a standard PID controller with the Field Oriented Control (FOC) strategy was implemented; in the case of the lateral dynamics, the steering, and the powertrain for the case of the longitudinal dynamics. The overall controller is composed of an inner-loop for the actuators and an outer-loop for the vehicle dynamics. The outer-loop controller receives a reference vector for the position coordinates of the vehicle consisting of a series of waypoints. In turn, it generates the references for the position of the steering actuator and the torque of the powertrain actuator, which represent the inner-control loop. Finally, the simulation results of the complete closed-loop system are presented, which demonstrate the effectiveness of the proposed control strategy.

---

## Keywords

DC motor, BLDC, electric motor, dq model, Park-Clarke, Clarke, space vector, PID, SVPWM, SVM

---

## Introduction

Brushless direct current (BLDC) motors are one of the most marketable motors in motor technology. BLDC motors are used in industries such as industrial automation, equipment, and instrumentation [1]. The automotive industry uses this kind of motor due to its versatility and low-cost construction.

Although the BLDC motor has not been, until now, the preferred motor for the vehicle powertrain, in future work, we will explore its applicability in the power motion for electric vehicles. One of the vehicles that use the BLDC for traction is the Toyota Prius (2005) [2].

The space-vector PWM (SVPWM) technique is an advanced method, and possibly the best among all the PWM techniques, for variable-frequency drive applications [3] for electric motors. Although in this report, we do not cover the SVPWM, we controlled the motors using direct torque control in the d-q reference frame, which is the basis for the SVPWM methodology. You can download the Simulink model in [4]. The toolboxes required to run the model, besides Matlab and Simulink, are "Simscape Electrical" and "Statistics and Machine Learning Toolbox". However, for this specific report, Simscape Electrical is not required. The Statistics and Machine Learning Toolbox is required for the lateral dynamic simulation to keep track of the waypoints; the function required is "knnsearch," which can be replaced by another algorithm. The model contains the circle fit function created by [5].

---

## The BLDC Dynamical Model

The brushless DC motor is one where the rotor is a permanent magnet commonly made of Neodymium (NdFeB) [3], and the stator is supplied with an alternating current (AC) obtained from a DC source and a subsequent power inverter stage. This motor is lighter, smaller, and better at dissipating heat compared to other technologies. BLDC motors can be found in single-phase, two-phase, and three-phase configurations, with the three-phase configuration being the most common. As mentioned earlier, the BLDC is constructed with a permanent magnet rotor and wire-wound stator poles. Instead of the brush commutator, it has Hall effect sensors to detect the position of the rotor and with inverters feed the signal required to activate or deactivate the coils in the stator to produce an electrical torque and, consequently, the rotor movement [6].

The BLDC model is based on the following sources [3], [6], [7], [8], [9]. Below are the definitions of the elements of the BLDC model and the mathematical equations:
