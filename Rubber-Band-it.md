# 🛡️ Rubber Band-it: Dual-ESC Arduino Turret Tank with Rubber Band Launcher

A custom Arduino-based RC tank designed for modular embedded systems learning and applied engineering. Features independent track drive, pan/tilt turret, and a sprocket-based rubber band launcher.

---

## 1. Project Introduction

Brief overview of project goals, what the tank does, and why it was built. (To be expanded with more detail later.)

---

## 2. Mechanical Systems & Design

- **Chassis & Frame:**  
  3D-printed PLA/PETG chassis, FEA-validated for strength.  
  All major load-bearing mounts analyzed in ANSYS (factor of safety ≥ 3).

- **Turret & Launcher:**  
  Pan/tilt with standard and continuous servos, sprocket-driven launcher for rapid fire.

- **Track Drive:**  
  Dual N20 motors (ESC-controlled), 4cm sprocket drive wheels for pivot and turn capability.

- **FEA & Validation:**  
  Static structural simulation (ANSYS 2025R2) on critical parts.  
  Max deformation ≤ 0.2mm; von-Mises stress well below PLA yield.  
  [Downloadable simulation files and viewers available.]

- **Manufacturing & Design Choices:**  
  Designed around FDM 3D printing for easy replication and modification. Fasteners chosen for plastic (M3 screws, heat inserts).  
  Design driven by balance between ease of printing, strength, and modularity.

- **Speed Calculation (at 1000 RPM):**  
  - Sprocket diameter: 4 cm  
  - Circumference: ≈ 0.126 m  
  - RPS: ≈ 16.67  
  - Linear speed: ≈ 2.10 m/s (~7.56 km/h) at no load

---

## 3. Electronics Overview & Wiring

- **Core Components:**  
  - Arduino Nano control board  
  - L298N ZX-040 (dual ESC) motor driver  
  - 6-channel Spektrum RC receiver for wireless control  
  - 7.4V LiPo battery + buck converter for 5V rails  
  - OLED display for live telemetry and HUD

- **Function Overview:**  
  - RC inputs decoded by Arduino (interrupts)  
  - Motors/servos driven by PWM  
  - Battery voltage monitored via divider  
  - HUD shows status and crosshair

- **Wiring Diagram:**  
  *(Placeholder for wiring PDF/diagram to be added here)*

---

## 4. Firmware & Code Structure

- **Main Functions:**  
  - Interrupt-based RC signal reading  
  - ESC and servo PWM output  
  - OLED HUD and data display  
  - Battery voltage monitoring  
  - Exponential smoothing for actuator response

- **Key Code Snippets:**  
  - Exponential smoothing for tilt  
  - Mapping throttle/yaw to ESC PWM  
  - Battery voltage calculation

- **Description:**  
  Each code chunk (RC decode, drive, display, telemetry) to be described here in more detail. (Will be filled out further.)

---

## 5. Build Issues & Troubleshooting

- Tolerance problems with printed parts (fit/finish)
- Code bugs (PWM decoding, servo jitter, signal loss)
- L298N driver issues (brownouts, current limits)
- Iterative fixes and lessons learned

---

## 6. Wanna Build It Yourself?

**Coming Soon:**  
A full step-by-step build PDF (including STL files, assembly, and wiring) will be provided here for easy replication.

---

## 7. Project Timeline

- 2025-08-07: FEA docs, simulation GIFs, portfolio reorg
- 2025-08-01: Static/deformation sims, safety factor ≥ 3
- 2025-07-25: v1.5 firmware, HUD, crosshair overlays, voltage readout
- 2025-07-01: OLED animation, Mario startup, vector math HUD
- 2025-06-10: Dual ESCs, improved throttle, failsafes
- 2025-05-19: Initial Arduino/L298N/servo logic

---

## 8. Next Steps & Future Improvements

- Expand assembly instructions and troubleshooting guide
- Add full build video and wiring diagrams
- Firmware improvements (safety features, new HUD elements)
- Hardware tweaks for reliability and printability

---

## References

- [u8glib OLED Library](https://github.com/olikraus/u8glib)
- [PinChangeInterrupt Playground](https://playground.arduino.cc/Main/PinChangeInterrupt/)
- [Servo.h Docs](https://www.arduino.cc/en/Reference/Servo)
- [Mario Theme Arduino](https://www.instructables.com/Arduino-Mario-Bros-Theme-Song/)

---

*Assembly guide, wiring diagrams, and STL download links will be included in the upcoming PDF. Stay tuned!*
