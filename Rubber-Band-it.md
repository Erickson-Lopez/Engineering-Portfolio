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

  ![Tank Test](https://raw.githubusercontent.com/Erickson-Lopez/Engineering-Portfolio/74a3ea7ed9607d8e97fb11ad39e1f762bfb68a6e/assets/RubberBand-it/StaticStructuralTankTest.gif)  
  Static structural simulation (ANSYS 2025R2) on critical parts.
  
  Max deformation ≤ 0.2 mm; von-Mises stress well below PLA yield.  

- **Manufacturing & Design Choices:**  
  Designed around FDM 3D printing for easy replication and modification. Fasteners chosen for plastic (M3 screws, no heat inserts).  
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

- **Raw Code:**
  <details>

```cpp
// Alpha test V1.5
// Credit to:
// ChatGPT (for structuring and debugging)

#include <Servo.h>
#include <PinChangeInterrupt.h>
#include "U8glib.h"

// I2C on A4=SDA, A5=SCL
U8GLIB_SSD1306_128X64 u8g(U8G_I2C_OPT_NONE | U8G_I2C_OPT_DEV_0);

// —— Startup animation params —— 
const unsigned long ANIM_DURATION = 3000;
const int  TRACK_LINKS = 10;
const float SPEED      = 0.01;
const int  BOTTOM_Y    = 62, TOP_Y = 38;
const int  BOTTOM_X0   = 42, BOTTOM_X1 = 86;
const int  TOP_X0      = 38, TOP_X1   = 90;

// —— Mario tune params —— 
const int  buzzerPin    = 11;  
const int  marioNotes[] = {1318,1318,1318,1046,1318,1568,784};
const float marioBeats[] = {2,3,3,2,3,6,6};  
const int   marioCount   = sizeof(marioNotes)/sizeof(int);
const int   TEMPO = 700;

const int voltPin = A0;

// draw static tank chassis
void drawChassis() {
  u8g.drawLine(39,63,89,63);
  u8g.drawCircle(39,58,5);
  u8g.drawCircle(55,58,5);
  u8g.drawCircle(73,58,5);
  u8g.drawCircle(89,58,5);
  u8g.drawLine(35,37,93,37);
  u8g.drawCircle(35,42,5);
  u8g.drawCircle(93,42,5);
  u8g.drawLine(34,58,30,42);
  u8g.drawLine(98,42,94,58);
  u8g.drawFrame(56,28,13,10);
  u8g.drawCircle(62,24,3);
  u8g.drawLine(55,20,55,26);
  u8g.drawLine(69,20,69,26);
  u8g.drawLine(55,26,57,26);
  u8g.drawLine(67,26,69,26);
  u8g.drawLine(57,27,59,22);
  u8g.drawLine(67,27,65,22);
  u8g.drawFrame(50,4,44,12);
  u8g.drawLine(43,20,96,20);
  u8g.drawLine(43,20,43,7);
  u8g.drawLine(43,7,50,7);
  u8g.drawLine(96,20,96,7);
  u8g.drawLine(94,7,96,7);
  u8g.drawLine(51,9,93,9);
  u8g.drawFrame(38,10,6,8);
}

void drawAnimatedFrame(float t) {
  drawChassis();
  for(int i=0;i<TRACK_LINKS;i++){
    float p = fmod(i + t + TRACK_LINKS/3.0, TRACK_LINKS) / TRACK_LINKS;
    int x = BOTTOM_X1 - p*(BOTTOM_X1-BOTTOM_X0);
    u8g.drawDisc(x, BOTTOM_Y, 1);
  }
  for(int i=0;i<TRACK_LINKS;i++){
    float p = fmod(i + t + TRACK_LINKS/2.0, TRACK_LINKS) / TRACK_LINKS;
    int x = TOP_X0 + p*(TOP_X1-TOP_X0);
    u8g.drawDisc(x, TOP_Y, 1);
  }
  for(int i=0;i<2;i++){
    float p = fmod(i + t, 2) / 2;
    int x=94 + p*(97-93), y=54 - p*(57-42);
    u8g.drawDisc(x,y,1);
  }
  for(int i=0;i<2;i++){
    float p = fmod(i + t, 3) / 3;
    int x=32 + p*(34-32), y=46 + p*(57-42);
    u8g.drawDisc(x,y,1);
  }
  for(int d=0; d<7; d++){
    int dx = random(BOTTOM_X0-35, BOTTOM_X1);
    int dy = BOTTOM_Y - random(2,7);
    u8g.drawDisc(dx, dy, random(1,3));
  }
}

void playAnimation() {
  unsigned long start = millis();
  while(millis() - start < ANIM_DURATION) {
    float t = (millis() - start) * SPEED;
    u8g.firstPage();
    do {
      drawAnimatedFrame(t);
    } while(u8g.nextPage());
    delay(50);
  }
}

void holdLastFrame() {
  float t = (ANIM_DURATION) * SPEED;
  u8g.firstPage();
  do {
    drawAnimatedFrame(t);
  } while(u8g.nextPage());
}

void playMario() {
  pinMode(buzzerPin, OUTPUT);
  for(int i=0; i<marioCount; i++){
    int noteDur = (60000 / TEMPO) * marioBeats[i];
    tone(buzzerPin, marioNotes[i], noteDur);
    delay(noteDur * 1.30);
  }
  noTone(buzzerPin);
}

// Turret + RC + HUD setup
Servo turretX, turretY, fireServo, escThrottle, escSteering;
const int turretXPin=2, turretYPin=3, fireServoPin=10, ESC_THROTTLE_PIN=5, ESC_YAW_PIN=6;
const int ch1Pin=A2, ch2Pin=A3, ch3Pin=7, ch4Pin=8, ch5Pin=4;
volatile uint32_t ch1Start,ch2Start,ch3Start,ch4Start,ch5Start;
volatile int ch1,ch2,ch3,ch4,ch5;

void ISR_CH1(){ if(digitalRead(ch1Pin)) ch1Start=micros(); else ch1=micros()-ch1Start; }
void ISR_CH2(){ if(digitalRead(ch2Pin)) ch2Start=micros(); else ch2=micros()-ch2Start; }
void ISR_CH3(){ if(digitalRead(ch3Pin)) ch3Start=micros(); else ch3=micros()-ch3Start; }
void ISR_CH4(){ if(digitalRead(ch4Pin)) ch4Start=micros(); else ch4=micros()-ch4Start; }
void ISR_CH5(){ if(digitalRead(ch5Pin)) ch5Start=micros(); else ch5=micros()-ch5Start; }

void setup(){
  playAnimation();
  holdLastFrame();
  playMario();

  for(int i=1;i<=5;i++){
    u8g.firstPage();
    do {
      u8g.setFont(u8g_font_chikita);
      u8g.setPrintPos(28,34);
      u8g.print("CHANNEL "); u8g.print(i); u8g.print(" - ON");
    } while(u8g.nextPage());
    delay(500);
  }

  u8g.firstPage();
  do {
    u8g.setFont(u8g_font_chikita);
    u8g.setPrintPos(22,32);
    u8g.print("SYSTEMS - ONLINE");
  } while(u8g.nextPage());
  delay(1000);

  pinMode(ch1Pin, INPUT); attachPCINT(digitalPinToPCINT(ch1Pin), ISR_CH1, CHANGE);
  pinMode(ch2Pin, INPUT); attachPCINT(digitalPinToPCINT(ch2Pin), ISR_CH2, CHANGE);
  pinMode(ch3Pin, INPUT); attachPCINT(digitalPinToPCINT(ch3Pin), ISR_CH3, CHANGE);
  pinMode(ch4Pin, INPUT); attachPCINT(digitalPinToPCINT(ch4Pin), ISR_CH4, CHANGE);
  pinMode(ch5Pin, INPUT); attachPCINT(digitalPinToPCINT(ch5Pin), ISR_CH5, CHANGE);

  turretX.attach(turretXPin);
  turretY.attach(turretYPin, 1000,2000);
  fireServo.attach(fireServoPin); fireServo.write(90);
  escThrottle.attach(ESC_THROTTLE_PIN);
  escSteering.attach(ESC_YAW_PIN);
}

void loop(){
  bool fireState = (ch5>1000 && ch5<1500);
  static bool prevFire=false, hasFired=false;
  if(ch5>800){
    if(fireState && !prevFire && !hasFired){
      fireServo.write(100); delay(520); fireServo.write(90);
      for(int i=0;i<5;i++){ tone(buzzerPin, random(1000,2000), 10); delay(15); }
      hasFired=true;
    } else if(!fireState){ hasFired=false; }
    prevFire=fireState;
  }

  if(ch3>800 && ch4>800){
    int thr=map(ch3,1092,2000,-127,127),
        yawRaw=ch4-1496,
        yw=(abs(yawRaw)<10?0:map(ch4,1000,2000,-127,127));
    escThrottle.writeMicroseconds(map(thr,-127,127,1000,2000));
    escSteering.writeMicroseconds(map(yw,-127,127,1000,2000));
  } else {
    escThrottle.writeMicroseconds(1500);
    escSteering.writeMicroseconds(1500);
  }

  if(ch1>800) turretX.write(map(ch1,1100,1950,80,105));
  const int center2=1500, deadz2=20;
  const float gain2=0.12;
  static int pulse=1500;
  if(ch2>=1000 && ch2<=2000){
    int dev=ch2-center2;
    if(abs(dev)>deadz2){ pulse+=dev*gain2; pulse=constrain(pulse,1300,1700); }
    turretY.writeMicroseconds(pulse);
  }

  float vRaw = analogRead(voltPin)*(5.0/1023.0);
  float vBat = vRaw*((10.0+4.7)/4.7);

  u8g.firstPage();
  do {
    u8g.setFont(u8g_font_chikita);
    u8g.setPrintPos(62,10);
    u8g.print(vBat,1); u8g.print("V");

    int lx=32,ly=32,sz=20;
    u8g.drawLine(lx-sz,ly,lx+sz,ly); u8g.drawLine(lx,ly-sz,lx,ly+sz);
    int lxDot=map(ch4,1000,2000,lx+sz,lx-sz);
    int lyDot=map(ch3,1000,2000,ly+sz,ly-sz);
    u8g.drawDisc(lxDot,lyDot,2);

    int rx=96,ry=32;
    u8g.drawLine(rx-sz,ry,rx+sz,ry); u8g.drawLine(rx,ry-sz,rx,ry+sz);
    int rxDot=map(ch1,1000,2000,rx+sz,rx-sz);
    int ryDot=map(ch2,1000,2000,ry+sz,ry-sz);
    u8g.drawDisc(rxDot,ryDot,2);
  } while(u8g.nextPage());

  delay(20);
}
```
</details> 

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
