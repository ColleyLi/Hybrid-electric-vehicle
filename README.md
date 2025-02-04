# Hybrid-electric-vehicle

This repository contains simulation and modeling works related to hybrid electric vehicle powertrain and control. Some of the works are under Hybrid Vehicle Systems Graduate Certificate from Purdue University.

<img src="https://github.com/sudokhan112/Hybrid-electric-vehicle/blob/main/admin.png" width="600" height="400">

### Basics
* The salient features of the various possible hybrid electric powertrain configurations can be listed via the following table
![Screenshot from 2021-03-27 14-40-38](https://user-images.githubusercontent.com/77024625/112732869-98be8600-8f0a-11eb-8ede-f8374a8f4996.png)

* The salient features of the various possible hybrid electric powertrain configurations in terms of energy efficiency & performance
![Screenshot from 2021-03-27 14-43-29](https://user-images.githubusercontent.com/77024625/112732930-e9ce7a00-8f0a-11eb-8c49-93dfd2fea30f.png)

* [Review of paper](https://github.com/sudokhan112/Hybrid-electric-vehicle/tree/main/papers) on the state of the art of hybrid, electric, and fuel cell powertrain 
![Screenshot from 2021-03-27 15-08-03](https://user-images.githubusercontent.com/77024625/112733491-5b5bf780-8f0e-11eb-9efa-651008d4f3d9.png)

The above represents a schematic line diagram representing the various layouts. In the series-parallel powertrain, the engine works a
backup to the electrification side. It only uses the engine power to the transmission, but it is also coupled to a generator to produce the
required electricity for recharging the batteries. In case of the coupled system the engine is couple to a starter motor cum generator that
functions as a start/stop system at traffic signal and starts the engine on the go. Similarly, during a descend, the generator recoups the
energy as electricity and is stored via the battery management system



### Analysis of Mild Parallel Hybrid Electric Vehicle

The primary objective of the first project is to analyze the performance of a mild parallel hybrid gas/electric vehicle. In this vehicle, an electric machine is to propel the vehicle at low speeds with the main engine disengaged. The electric machine is also used as a boost motor to improve high-speed accelerating characteristics. This permits a smaller internal combustion engine to be used without sacrificing overall performance. A block diagram of the vehicle is depicted here.

<img src="https://github.com/sudokhan112/Hybrid-electric-vehicle/blob/main/mild-hev/vehmod.png" width="600" height="400">

**Overall Conclusions:**
* Increasing Engine cutoff power (Pmin) increases mpg. But it also needs higher power from battery (bigger battery). Increasing battery size also increases battery weight which adversely affects mpg. This shows the importance of research on battery capacity to increase hybrid vehicle mpg. Increasing the battery size does not increase mpg and also maintain SOC within the desired limit. This indicates the given battery energy density is too low.
* Mpg increases more rapidly in urban stop and go cycle (LA92), than moderately highway cycle (US06).
* Increasing battery size (keeping very other variables same) decreases mpg.
* Decreasing the threshold to a certain limit in charge sustaining mode increases mpg. After that, battery weight is too high for any improvement.
* Using more aggressive power management (taking more power from motor) increases mpg more rapidly but decreases SOC more rapidly too.
* Decreasing Max engine power decreases mpg but increases SOC.
* Rule based optimization (what we are doing) is easy to implement and also provides insight into the system. But when too many variables are involved, it is hard to keep track of all the variables. A generalized optimization method may show us where the highest optimization (max mpg) happens. Then going to that optimization point through rule-based method could be a good exercise.
* Engine and motor mass can be considered separately to analyze how that affects when different sizes of engine (based on Pmax and Pmin) and motor is used.

**[Download code and detailed report](https://github.com/sudokhan112/Hybrid-electric-vehicle/tree/main/mild-hev)**


### Acceleration of Toyota Prius

The objective is to accelerate the vehicle as rapidly as possible without violating any physical constraints (e.g. maximum motor, generator, or engine speeds and torques, |Pbatt| < |Pbattmax| etc.).![Screenshot from 2021-03-27 15-08-03](https://user-images.githubusercontent.com/77024625/112733481-4da67200-8f0e-11eb-9c59-40c82cb3cf7b.png)


The general control strategy is as follows. For a given vehicle speed, and a desired output power determined by the drive cycle, or driver inputs, the desired operating point of the engine can be determined based on the maximum efficiency curve of the engine. From the vehicle speed and engine speed, the desired generator speed can then be calculated. The generator speed is regulated through the inverter by controlling the output power of the generator (either as generator or motor). Motor torque is determined by looking at the difference between the total vehicle torque demand and the engine torque that is delivered to the ring gear. The battery provides power to the motors along with the electricity generated by the engine. For this project (accelerating as rapidly as possible), if desired tractive power less than 21 kW, assume all-electric launch (Teng = Tgen = 0). Otherwise, assume that Pbatt = 21 kW, and Peng = Ptrac - Pbatt

**Conclusions:**
* It took 10.25 seconds to reach 60 mph. 
* 0.0568 KWhr is supplied by the battery to reach 60 mph. Battery capacity 1.7 KW hr. (1.7/.0568) = 29 times Prius can go 0-60 mph before it completely drains the battery from 100% SOC to 0. Delta SOC is 0.033 to reach 60 mph.
* Mechanical energy is supplied by engine. 0.1069 KWhr is supplied by the engine to reach 60 mph. It is almost twice the energy supplied by battery. 

**[Download code and detailed report](https://github.com/sudokhan112/Hybrid-electric-vehicle/tree/main/prius-acceleration)**

### Permanent-magnet ac motor drive
The objective of the project is to develop a Simulink-based semi-detailed simulation of a permanent-magnet ac motor drive that utilizes a sine-triangle modulator with third-harmonic injection. We need to observe how the model response to develop 100 Nm of torque at 3000 rpm (mechanical). Then repeat the process for -100 Nm torque development at 3000 rpm.

**Conclusions**
* Simulation results showed acceptable ranges in PMACM outputs. Some losses (eddy current, hysteresis) are not modeled. But model outputs are within range.
* Dissecting the voltage and current plots from the simulation helped to grow intuitions about this machine. Some efficiency analysis may have been helpful to get real world outputs.
* The simulation results showed that we can control the Torque near instantly if we don’t ask for too much.
* The changes in torque and output values in this project also validated our assumption that, changes in electrical system is instantaneous and losses are negligible.

**[Download code and detailed report](https://github.com/sudokhan112/Hybrid-electric-vehicle/tree/main/AC-motor)**

### Battery model charge-discharge

We will examine several charge-discharge cycles to examine the effects on losses and round-trip efficiency. To achieve these goals, you are to develop a Simulink battery model that accepts Ibatt versus time as an input and outputs battery terminal voltage. The current will be used to determine the state of charge (SOC) of the battery using the Coulomb-counting method.
Consider the following charge/discharge cycles.
* The battery starts at SOCinit = 0:2. It is charged at a C-rate of 0.2 to SOC = 1:0. Then, it is discharged at a C-rate of 0.2 to SOC = 0:2. (slow charge and discharge).
* The battery starts at SOCinit = 0:2. It is charged at a C-rate of 2 to SOCmax = 1:0. Then, it is discharged at C-rate = 0.2 to SOCfinal = 0:2. (fast charge, slow discharge).
* The battery starts at SOCinit = 0:2. It is charged at a C-rate of 2.0 to SOC = 1:0. Then, it is discharged at C-rate = 2.0 to SOCfinal = 0:2. (fast charge, fast discharge).
* The battery starts at SOCinit = 0:5. It is charged at a C-rate of 5.0 to SOCmax = 0:6. Then, it is discharged at C-rate = 5.0 to SOCfinal = 0:5. (fast charge, fast discharge, relatively short-term storage).

**Conclusions**
* Slow charge-discharge (case-1) has the highest efficiency. Fast-charge-discharge (case-3) has the lower efficiency. Ridiculous fast charge-discharge (case-4) has lowest efficiency. Which shows slow charge-discharge is good for battery health and performance (if we need longer range from EV).
* Increasing charge-rate increases the current flow through battery. This increases the energy loss and decreases efficiency.
* Battery is drawing more power during charge cycle (higher negative value) than delivering during discharge cycle (lower positive value). Remaining power (or energy) is lost through Ro and R1 (P = I2R). Higher the amount of current, higher the loss. Case-4 has the highest amount of net losses compared to net energy delivered.
* Ibattery during charge and Ibattery during discharge remains constant. During charge, as SOC goes towards 1, Vbattery increases . Maximum, Vbattery and Pbattery (power needed to charge) at SOC = 1. This indicated, may be fully charging the battery is not always a good idea. Charging upto 90- 95% SOC is better in terms of power consumption and battery health. But round-trip efficiency goes down if we charge upto SOC 0.95 instead of 1. So, there is a tradeoff.
* For SOC between 0.2 and 1, the variation in open-circuit will be between 3.6 V and 4.2 V. With 80 cells in series, the variation in open-circuit battery (Voc) voltage will be between 288 V and 336 V. However, the cell “terminal” voltage during charge or discharge (Vbattery in Fig 7-10) will be different due to the voltage drops across R0 and R1. The range in cell (hence battery) terminal voltage will be substantially greater than range in “open-circuit” voltage. Vcell = Voc – VR0 -VC1. But, we are within manufacturer-supplied limits in all charge/discharge cycles considered except for case-4.

**[Download code and detailed report](https://github.com/sudokhan112/Hybrid-electric-vehicle/tree/main/Battery-model-charge-discharge)**


### Intake mnifold diagnostic

Design and implement (in SIMULINK) a manifold air intake diagnostics system for a 4 cylinder engine with an electronic throttle control (ETC) system. Assume that the ETC system has a DC servo control system that uses a PID controller. The closed loop servo response must meet the following requirements: omega = 25 rad/sec and zeta = 0.45. The DC servo open loop poles are at (0,-6) and DC gain of 1. Consider the faults in the Mass Air Flow (MAF) sensor, Manifold Air Pressure (MAP) sensor, Throttle Angle Position (TAS) sensor, and the Throttle Actuator (control input). Assume that the
additive faults are as follows: A pulse starting after 10 seconds and lasts for 20 seconds at which
time the pulse is set to zero again. The amplitude of the pulse should be 10% of the signal for all
cases except for throttle actuator fault where 20% pulse amplitude is used.

**[Download code and detailed report](https://github.com/sudokhan112/Hybrid-electric-vehicle/tree/main/manifold-air-intake-diagnostics-system)**



