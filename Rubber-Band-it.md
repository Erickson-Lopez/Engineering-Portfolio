# 🛡️ Rubber Band-it: Dual-ESC Arduino Turret Tank with Rubber Band Launcher

A custom Arduino-based RC tank designed for modular embedded systems learning and applied engineering. Features independent track drive, pan/tilt turret, and a sprocket-based rubber band launcher.

---

## 1. Project Introduction

Brief overview of project goals, what the tank does, and why it was built. (To be expanded with more detail later.)

---

## 2. Mechanical Systems & Design

- **Chassis & Frame:**  
  3D-printed PLA/PETG chassis, FEA-validated for strength.  
  All major load-bearing mounts analyzed in ANSYS.

- **Turret & Launcher:**  
  Pan/tilt with standard and continuous servos, sprocket-driven launcher for rapid fire.

- **Launcher (Gatling Gun Redesign):**  
  The turret's rubber band Gatling gun is based on [Thingiverse Thing 647475](https://www.thingiverse.com/thing:647475), but with significant modifications:
  - Reduced to half size for compactness and integration.
  - Uses a continuous rotation servo (instead of the original 90-degree gears and crank).
  - The 6 barrels rotate; each time a barrel passes the trigger, a ratchet mechanism advances the sprocket by a set degree and releases one rubber band.
  - Each barrel can be loaded with up to 3 rubber bands (18 shots total).
  - The rear barrel wheel is redesigned with a keyed servo attachment for synchronized rotation.
  - The trigger is integrated as part of a single rear/front body piece (improving rigidity over the original 3-piece trigger design).
  - The bottom slot is used to mount the gun to the turret using two M4 screws for secure attachment.
  - For proper attribution, the original design by [Thingiverse user "Cort"](https://www.thingiverse.com/cort) is referenced; see link.
  

- **Track Drive:**  
  Dual N20 motors (ESC-controlled), 4 cm sprocket drive wheels for pivot and turn capability.  
  **Track system (Thingiverse-based):** Original concept from [Thing 4009469](https://www.thingiverse.com/thing:4009469/files). For this build, regular **staples** are used in place of the recommended 1 mm wire pins. This provides very good flexibility at the hinge/pivot points and enough compliance for local compression/stretch along the track path. **Durability is still being evaluated** — real-world testing so far has been limited to a STEM class project.  
  **Sprockets (modified):** Derived from [Thing 4140332](https://www.thingiverse.com/thing:4140332/files) and customized for this platform:
  - Covered the spoke holes and **extruded the center hub** for cleaner looks and easier FDM printing.
  - Two variants:
    - **Drive sprocket:** keyed/tight-fit for **N20 motor shafts** to ensure positive torque transfer.
    - **Idler sprocket:** simple **through-hole** for a printed shaft/bushing to free-spin smoothly.
  - Tooth profile preserved for reliable meshing with the linked track design.
  - For proper attribution, the original LEGO tread design by [Thingiverse user "Polar_19"](https://www.thingiverse.com/Polar_19) is referenced; see link.
  - For proper attribution, the original LEGO sprocket design by [Thingiverse user "neumaker_42"](https://www.thingiverse.com/neumaker_42) is referenced; see link.

- **FEA & Validation:**  
  Static structural simulation (ANSYS 2025R2) on critical parts.
  ![Static Structural Test](https://raw.githubusercontent.com/yourusername/your-repo-name/main/assets/RubberBand-it/StaticStructuralTankTest.gif)
  Max deformation ≤ 0.2 mm; von-Mises stress well below PLA yield.  
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
  - 7.4 V LiPo battery + buck converter for 5 V rails  
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
- L298N driver issues (brownouts)
