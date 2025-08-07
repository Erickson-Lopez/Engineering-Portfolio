
---

### 🛡️ Rubber Band-it: Arduino Dual-ESC Turret Tank

_A custom RC tank platform for learning and demonstrating embedded systems, real-time signal processing, and applied engineering. Designed for hobbyists, students, and as a showcase for recruiters. Combines Arduino control, a graphical OLED HUD, and mechanical FEA-validated 3D-printed parts._

#### Key Features

- Dual PWM ESC drivetrain for smooth tank and pivot control
- Interrupt-driven RC signal decoding (6 channels)
- Turret pan/tilt with exponential smoothing (ODE-based)
- Animated OLED HUD with crosshair, channel status, and startup Mario theme
- Live battery voltage via EE voltage divider
- All critical hardware designed in CAD and validated with FEA (ANSYS)
- Downloadable STL files + interactive 3D and FEA result viewers

---

#### 📚 Project Overview

Rubber Band-it is a fully custom, Arduino-powered RC tank designed to maximize modularity, smooth motion, and hands-on learning in embedded systems and mechanical design. Each hardware, software, and math iteration is logged—highlighting engineering insight and real-world troubleshooting.

---

#### 🧩 Engineering Highlights

- **Math & Physics:**  
  - Exponential smoothing (ODE) for actuator filtering
  - Parametric mapping and vector fields for HUD visualization
  - EE voltage divider for live battery readout
  - Physics-based speed estimation (RPM, diameter)
- **FEA Validated:**  
  - 3D-printed load-bearing mount analyzed in ANSYS (static load, safety factor ≥ 3, full animated and static results)
  - PLA, PETG, and future-proofing for material upgrades

---

#### 🖼️ Visual Gallery

<details>
<summary>Expand for key images and simulation GIFs</summary>

- **Tank Chassis Preview:**  
  ![Tank Chassis Preview](./Rubber-Band-it/stl/tank_chassis_v1.5_preview.png)

- **FEA: Static Structural (von-Mises stress):**  
  ![Static Structural GIF](./Rubber-Band-it/feasim/rocker_vonmises_static_structural.gif)

- **FEA: Total Deformation Animation:**  
  ![Total Deformation GIF](./Rubber-Band-it/feasim/rocker_total_deformation.gif)

</details>

---

#### 📈 FEA Simulation: V-Arm Rocker Mount (ANSYS 2025R2)

- **Simulation Type:** Static Structural (ANSYS Student)
- **Objective:** Validate 3D-printed PLA rocker-arm mount under vertical tank loading
- **Results:**  
  - _Deformation:_ ≤ 0.2 mm (localized)
  - _von-Mises Stress:_ ~10–20 MPa (well below PLA yield of 60 MPa)
  - _Factor of Safety:_ ~3.0+
- **Engineering Takeaways:**  
  - Structurally sound under 2 lb (~8.9 N) tank
  - Minimal deformation, safe for tracked vehicle use
- **Downloads:**  
  - [ANSYS Project (.wbpz)](./Rubber-Band-it/feasim/rocker_mount_sim.wbpz)
  - [Deformed STL](./Rubber-Band-it/feasim/rocker_deformed.stl) ([View interactively](https://www.viewstl.com/?model=https://raw.githubusercontent.com/Erickson-Lopez/your-repo/main/Rubber-Band-it/feasim/rocker_deformed.stl))
  - [Simulation video (MP4)](./Rubber-Band-it/feasim/rocker_deformation.mp4)

---

#### 🧮 Math, Code & Engineering Principles

- **Smoothing:**  
  ```cpp
  currentTilt = currentTilt * (1 - alpha) + targetTilt * alpha; // α = 0.2
  ```
- **Throttle/Yaw Mapping:**  
  ```cpp
  int escSignal = map(value, -127, 127, 1000, 2000);
  ```
- **Voltage Divider:**  
  ```cpp
  float vBat = vRaw * ((10.0 + 4.7) / 4.7);
  ```
- **Vector Math (HUD):**  
  $$
  \vec{F}(t) = \langle \text{throttle}(t), \text{yaw}(t) \rangle
  $$
- **Physics:**  
  $$
  \text{Speed} = \text{RPM} \cdot \frac{D\pi}{60}
  $$

---

#### 📁 Downloads

- [Latest Firmware](./Rubber-Band-it/firmware/Rubber-Band-it_v1.5.ino)
- [Tank Chassis STL](./Rubber-Band-it/stl/tank_chassis_v1.5.stl) ([Preview](./Rubber-Band-it/stl/tank_chassis_v1.5_preview.png)) ([View STL](https://www.viewstl.com/?model=https://raw.githubusercontent.com/Erickson-Lopez/your-repo/main/Rubber-Band-it/stl/tank_chassis_v1.5.stl))
- [Rocker Deformed STL](./Rubber-Band-it/feasim/rocker_deformed.stl) ([View STL](https://www.viewstl.com/?model=https://raw.githubusercontent.com/Erickson-Lopez/your-repo/main/Rubber-Band-it/feasim/rocker_deformed.stl))

---

#### 🔗 References

- [u8glib OLED Library](https://github.com/olikraus/u8glib)
- [PinChangeInterrupt Arduino Playground](https://playground.arduino.cc/Main/PinChangeInterrupt/)
- [Servo.h Docs](https://www.arduino.cc/en/Reference/Servo)
- [Mario Theme Arduino](https://www.instructables.com/Arduino-Mario-Bros-Theme-Song/)

---

#### Build Log

- **2025-08-07** — Integrated full FEA documentation and simulation GIFs, improved portfolio organization.
- **2025-08-01** — Added static and deformation simulations for rocker mount (PLA), confirmed safety factor ≥ 3.
- **2025-07-25** — Firmware v1.5 released: HUD upgrade, crosshair overlays, voltage readout, improved ESC logic.
- **2025-07-01** — OLED animation, Mario startup sequence, live channel splash, parametric vector math for HUD.
- **2025-06-10** — Replaced L298N with dual PWM ESCs, improved throttle mapping and failsafes.
- **2025-05-19** — Initial design: Arduino Nano, L298N, basic servo/turret logic.
