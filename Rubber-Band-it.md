# 🛡️ Rubber Band-it: Dual-ESC Arduino Turret Tank with Rubber Band Launcher

A fully custom Arduino-based RC tank for modular embedded systems, applied engineering, and mechanical design. Features independent track drive, a pan/tilt turret, and a sprocket-based rubber band launcher. Designed for hands-on learning, demonstration, and as a showcase for recruiters seeking practical, systems-level engineering.

---

## 1. Project Overview

- **Platform:** Arduino Nano, custom CAD chassis, dual-ESC N20 motor drivetrain
- **Control:** 6-channel Spektrum RC, interrupt-driven signal decoding
- **Features:** Turret pan/tilt, animated OLED HUD, battery voltage sensing, and semi/full-auto launcher
- **Purpose:** Modular, extensible, and robust — engineered to impress both hobbyists and seasoned technical reviewers

---

## 2. Mechanical Structure & Assembly

### Frame & Chassis
- 3D-printed, FEA-validated chassis (PLA/PETG)
- All critical load-bearing mounts verified in ANSYS (factor of safety ≥ 3)
- Downloadable STL files and simulation result viewers included

### Turret & Launcher
- Pan: Continuous rotation servo
- Tilt: Standard 180° servo
- Launcher: Sprocket-driven, continuous servo for rapid fire

### Track System
- Dual N20 motors, independently ESC-controlled for pivot/turn
- 4 cm sprocket diameter for each drive wheel

### Assembly & Fasteners
- **Bill of Materials:** (expandable — see repo for details)
    - M3 screws, brass heat inserts for plastic, wiring harnesses
- **Wiring:** Color-coded, crimped connectors; LiPo with buck converter for regulated 5V
- **Documentation:** Step-by-step assembly, wiring, and part sourcing (to be expanded)

---

## 3. Electronics & Wiring

- **Control Board:** Arduino Nano
- **Motor Driver:** L298N ZX-040 (dual ESC)
- **Power:** 7.4V LiPo → buck converter (5V logic/electronics)
- **HUD:** OLED (U8glib), live telemetry and crosshair overlay
- **RC Interface:** 6-channel Spektrum receiver, interrupt-driven PWM decoding

---

## 4. Pre-Design Science & Calculations

### A. Motor-to-Track Speed Calculation

Given:  
- Sprocket diameter $D = 4\ \text{cm} = 0.04\ \text{m}$
- Motor speed $\text{RPM} = 1000$

**Step 1:** Circumference  
$C = \pi \cdot D = \pi \cdot 0.04 \approx 0.1257\ \text{m}$

**Step 2:** Revolutions per Second  
$\text{RPS} = \frac{1000}{60} \approx 16.67$

**Step 3:** Linear Speed  
$v = \text{RPS} \cdot C \approx 16.67 \cdot 0.1257 \approx 2.10\ \text{m/s}$

**Result:**  
**Speed ≈ 2.10 m/s (~7.56 km/h, ~4.7 mph) at no load**

---

### B. Torque Output

$\tau_{\text{output}} = \tau_{\text{motor}} \cdot \text{Gear Ratio}$  
- Gear ratio (1:4) selected for balance of torque and speed

---

### C. Voltage Divider for Battery Sensing

$V_{\text{out}} = V_{\text{in}} \cdot \frac{R_2}{R_1 + R_2}$

Example: $R_1 = 15k\Omega$, $R_2 = 10k\Omega$, $V_{\text{in}} = 12.6V$  
$\rightarrow V_{\text{out}} \approx 4.44V$

---

### D. Power Budgeting

$P = V \cdot I$  
- Motors: ~2A peak each  
- Servos: ~0.5–0.8A each  
- Arduino + OLED: ~80mA  
- Buck converter rated above system max to avoid brownouts

---

### E. Track Steering Kinematics

$\omega_{\text{turn}} = \frac{v_R - v_L}{W}$  
- $v_R, v_L$: right/left track speeds  
- $W$: track width

---

### F. PWM Control Mapping

- Neutral: 1500 µs  
- Forward: 1500–2000 µs  
- Reverse: 1000–1500 µs

---

## 5. Simulation & Validation

### FEA: V-Arm Rocker Mount (ANSYS 2025R2)

- **Simulation:** Static structural (PLA, 2 lb tank load)
- **Results:** Max deformation ≤ 0.2 mm; von-Mises stress ~10–20 MPa (well below PLA yield 60 MPa)
- **Factor of Safety:** ~3.0+
- **Downloadables:**  
    - [ANSYS Project](./Rubber-Band-it/feasim/rocker_mount_sim.wbpz)  
    - [Deformed STL](./Rubber-Band-it/feasim/rocker_deformed.stl)  
    - [Simulation MP4](./Rubber-Band-it/feasim/rocker_deformation.mp4)  
    - [Interactive Viewer](https://www.viewstl.com/?model=https://raw.githubusercontent.com/Erickson-Lopez/Engineering-Portfolio/main/Rubber-Band-it/feasim/rocker_deformed.stl)

---

## 6. Embedded Code & Math Snippets

```cpp
// Exponential smoothing for actuator
currentTilt = currentTilt * (1 - alpha) + targetTilt * alpha; // α = 0.2

// Throttle/Yaw mapping
int escSignal = map(value, -127, 127, 1000, 2000);

// Battery voltage divider
float vBat = vRaw * ((10.0 + 4.7) / 4.7);
```

## 7. Visual Gallery

<details>
<summary>Expand for images & simulation GIFs</summary>

- **Tank Chassis Preview:**  
  ![Chassis Preview](./Rubber-Band-it/stl/tank_chassis_v1.5_preview.png)
- **FEA: Static Stress:**  
  ![Static Structural GIF](./Rubber-Band-it/feasim/rocker_vonmises_static_structural.gif)
- **FEA: Deformation:**  
  ![Deformation GIF](./Rubber-Band-it/feasim/rocker_total_deformation.gif)

</details>

---

## 8. Downloads & Resources

- [Latest Firmware](./Rubber-Band-it/firmware/Rubber-Band-it_v1.5.ino)
- [Tank Chassis STL](./Rubber-Band-it/stl/tank_chassis_v1.5.stl)
- [Rocker Deformed STL](./Rubber-Band-it/feasim/rocker_deformed.stl)

---

## 9. Project Timeline

- 2025-08-07: FEA docs, simulation GIFs, portfolio reorg
- 2025-08-01: Static/deformation sims, safety factor ≥ 3
- 2025-07-25: v1.5 firmware, HUD, crosshair overlays, voltage readout
- 2025-07-01: OLED animation, Mario startup, vector math HUD
- 2025-06-10: Dual ESCs, improved throttle, failsafes
- 2025-05-19: Initial Arduino/L298N/servo logic

---

## 10. Engineering Skills Demonstrated

- Embedded systems, real-time code
- PWM motor & servo control
- Voltage sensing, power distribution
- CAD, FEA, and mechanical validation
- Kinematics, torque, and speed calculations

---

## References

- [u8glib OLED Library](https://github.com/olikraus/u8glib)
- [PinChangeInterrupt Playground](https://playground.arduino.cc/Main/PinChangeInterrupt/)
- [Servo.h Docs](https://www.arduino.cc/en/Reference/Servo)
- [Mario Theme Arduino](https://www.instructables.com/Arduino-Mario-Bros-Theme-Song/)

---

*Assembly, wiring diagrams, and BOM details will be expanded in future commits. See repo for STL, code, and simulation downloads.*
