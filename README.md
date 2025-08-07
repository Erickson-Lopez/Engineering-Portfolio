# Hey, I’m Erickson 👋

Welcome to my portfolio! I’m a second year Mechanical engineering student who’s all about hands-on building, simple solutions, and making stuff that’s actually helpful. Scroll down to see my work and what I’m currently building.

---

## My Engineering Philosophy

### Keeping it Simple, Creative, and Hands-On

I’m a big believer that the best engineering is simple. If you can make something less complicated, why not? To me, simple designs and processes aren’t about cutting corners—they just work better, are easier to fix, and let you test ideas faster. I always try to solve problems with the least amount of extra work, not because I’m lazy, but because it means I can spend more time making improvements and less time fighting with my own designs.

Helping people in everyday life is what gets me excited to build stuff. I want what I make to be genuinely useful. I’m always curious about how things work, and I love experimenting with new ideas—even if they’re a little out there. Whether I’m designing in CAD or messing around with my 3D printer, I just love creating things.

Since I was a kid, I’ve been tearing apart RC cars and planes just to see how they tick, then putting them back together (sometimes with “improvements”). That curiosity is still what drives me as an engineering student. When I run into a problem, I like to get to the root cause first—fix the big thing, then handle the smaller stuff step by step. Breaking projects into chunks just makes everything more manageable.

I pick up a lot from other people too. If I see a cool trick or hack online, I’ll figure out the core idea and try it myself (like using paperclips for tank tread hinges!). I’m always looking for practical ideas to add to my own toolkit, but I still think for myself and try to find my own twist on things.

At the end of the day, I want to make stuff I’d actually use or buy myself. I’ve seen a ton of products that miss the mark for real users, and I never want to be that kind of engineer. For me, success is about building things that solve real problems, and being as hands-on as possible—because I learn best by doing, not just sitting at a desk.

---

**If you want to see what I’m working on, scroll down to my projects!**

---

## 🚧 Projects In Development

> _Live updates on what I’m building, tinkering with, or fixing. Each project has its own update feed—scroll to see the progress!_

### [Project Name: Tank Tread Hinge System] [IN PROGRESS]
- _Quick summary: Experimental tank tread using paperclip hinges for flexibility and low-cost prototyping._

#### Updates Feed:
- **2025-08-06** — Initial CAD model complete, first 3D print done.  
  _[Add photo here]_  
- **2025-08-07** — Fixed hinge binding by increasing clearance.  
  _[Add before/after diagram or quick sketch]_  
- **2025-08-10** — Mounted on RC tank chassis, improved turning.  
  _[Add video, code, or notes]_  
- **2025-08-13** — Prepping for durability testing.

---

### [Project Name: Modular RC Car Chassis] [IN PROGRESS]
- _Quick summary: Making an RC car chassis that’s super easy to swap batteries and parts._

#### Updates Feed:
- **2025-08-06** — Designed quick-swap battery compartment.

---

_Add more projects here as you start them!_

---

## 🏆 Main Projects

# Erickson Lopez Portfolio

> _Finished or stable projects, each with a build log at the bottom showing major updates and improvements over time._

---

## 🏆 Main Projects

---

### 🛡️ Rubber Band-it: Arduino Dual-ESC Turret Tank

- _A custom RC tank platform for learning and demonstrating embedded systems, real-time signal processing, and applied engineering. Designed for hobbyists, students, and as a showcase for recruiters. Combines Arduino control, a graphical OLED HUD, and mechanical FEA-validated 3D-printed parts._

#### Key Features
- Dual PWM ESC drivetrain for smooth tank and pivot control
- Interrupt-driven RC signal decoding (6 channels)
- Turret pan/tilt with exponential smoothing (ODE-based)
- Animated OLED HUD with crosshair, channel status, and startup Mario theme
- Live battery voltage via EE voltage divider
- All critical hardware designed in CAD and validated with FEA (ANSYS)
- Downloadable STL files + interactive 3D and FEA result viewers

#### Build Log
- **2025-08-07** — Integrated full FEA documentation and simulation GIFs, improved portfolio organization.
- **2025-08-01** — Added static and deformation simulations for rocker mount (PLA), confirmed safety factor ≥ 3.
- **2025-07-25** — Firmware v1.5 released: HUD upgrade, crosshair overlays, voltage readout, improved ESC logic.
- **2025-07-01** — OLED animation, Mario startup sequence, live channel splash, parametric vector math for HUD.
- **2025-06-10** — Replaced L298N with dual PWM ESCs, improved throttle mapping and failsafes.
- **2025-05-19** — Initial design: Arduino Nano, L298N, basic servo/turret logic.

---

#### 📘 Project Documentation & Source
- [Full Project Build Log & Source](./Rubber-Band-it/README.md)
- [FEA Simulation GIFs & Results](./Rubber-Band-it/feasim/)
- [Sample STL Files & Previews](./Rubber-Band-it/stl/)

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

## 📬 Contact

Want to collaborate, talk shop, or just chat about engineering?  
**Email:** lopez.h.erickson@gmail.com

---
