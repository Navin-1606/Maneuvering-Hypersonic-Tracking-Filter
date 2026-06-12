# Maneuvering-Hypersonic-Tracking-Filter
A Python-based simulation modeling real-time kinematic tracking and Directed Energy System interception of maneuvering hypersonic targets using a Constant Acceleration Filter.
# Maneuvering Hypersonic Target Tracking & Laser Intercept Simulator

A real-time, software-in-the-loop simulation modeling the detection, kinematic tracking, and directed-energy interception of an incoming hypersonic warhead executing active terminal-phase evasion maneuvers. 

Built completely from scratch during my first-year summer holidays to explore core principles of Guidance, Navigation, and Control (GNC) loops, sensor fusion architectures, and atmospheric flight mechanics.

---

## 🚀 System Architecture & Engineering Pipeline

The simulator operates as a continuous real-time pipeline split into four logical phases:

### 1. Target Trajectory Generation (The Physics Engine)
* Models a 500 kg aerodynamic warhead diving from an altitude of 30,000 meters at velocities exceeding **Mach 5 (~1700 m/s)**.
* Incorporates a variable **exponential barometric atmospheric density profile** based on the US Standard Atmosphere model to dynamically compute changing aerodynamic drag forces vectorially.

### 2. Terminal Evasion & Radar Corruption
* Halfway through the descent profile, the warhead executes an aggressive, high-G **sinusoidal weave maneuver along the Y-axis** to simulate an automated countermeasure system designed to bypass defensive cross-sections.
* Simulates real-world sensor clutter and plasma attenuation by corrupting the true flight coordinates with **Gaussian White Noise ($\pm 150\text{m}$ standard deviation)**.

### 3. Kinematic State Estimation Filter
* Implements a **Constant Acceleration (CA) Filter** using the `filterpy` library to manage state estimation.
* Tracks a 3D kinematic state vector containing position, velocity, and acceleration matrices for each axis ($x = [p, v, a]^T$).
* Dynamically weighs predictive physics equations against noisy sensor tracking arrays using process noise variance overrides to instantly latch onto unexpected sharp turns.

### 4. Directed Energy Targeting Link (The Laser)
* Couples the noise-filtered position stream to a ground-based **Laser Air Defense System** located at the origin coordinates $(0,0,0)$.
* Simulates an uninterrupted high-energy thermal laser transfer link locking instantly to the target vector with an incredibly low terminal tracking error margin.

---

## 🛠️ Core Technologies & Libraries Used

* **Language:** Python
* **Environment:** Visual Studio Code / Jupyter Notebooks (`.ipynb`)
* **Mathematical Operations:** `NumPy`
* **Differential Math & Optimization:** `SciPy`
* **Sensor Fusion/Estimation Math:** `FilterPy` (Kalman Filter Framework)
* **Visualization Engine:** `Matplotlib` (3D Interactive Animation Engine)

---

## 📊 Core Simulation Output Visuals

### Real-Time Intercept Performance Loop
The system tracks the target dynamically through its entry sequence, dampens the input sensor variance, and continuously project a zero-latency directed energy laser beam line directly to the filtered target node:
https://github.com/user-attachments/assets/cb7dbc46-a9dd-43d7-8ebe-670ee7da7e48
