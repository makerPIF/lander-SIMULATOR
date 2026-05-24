# 🚀 Lunar Lander GNC Simulator

> **Junior Engineer Mission** — An interactive web-based simulator and Arduino code generator for learning Guidance, Navigation & Control (GNC) systems used in real lunar landing spacecraft.

[![GitHub Pages](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-brightgreen?style=flat-square&logo=github)](https://yourname.github.io/lander-SIMULATOR/)
[![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)](LICENSE)
[![Arduino](https://img.shields.io/badge/Arduino-Uno-teal?style=flat-square&logo=arduino)](https://www.arduino.cc/)
[![Mobile](https://img.shields.io/badge/Mobile-Optimized-orange?style=flat-square&logo=android)](https://yourname.github.io/lander-SIMULATOR/)

---

## 📱 Live Demo

**Scan QR or visit:**
```
https://yourname.github.io/lander-SIMULATOR/
```
*(Replace `yourname` with your GitHub username)*

> Works on any smartphone, Galaxy Tab, or desktop browser — no installation required.

---

## 🌟 What Is GNC?

GNC stands for the three core systems that every spacecraft needs to land safely:

| Letter | System | What It Does | Real-World Example |
|--------|-----------|--------------|-------------------|
| **G** | Guidance | Plans *where* to go | NASA's powered descent algorithm |
| **N** | Navigation | Knows *where it is* | Radar altimeter + IMU sensors |
| **C** | Control | Moves *how to get there* | Thruster firing & attitude adjustment |

> 💡 Imagine walking blindfolded to a door: you need to **know where the door is (G)**, **feel where you are (N)**, and **move your feet correctly (C)**. That's exactly what GNC does for a lander!

---

## 🗂️ App Overview — Three Tabs

### Tab 1 — 🚀 Landing Simulator

Select any planet in our solar system and simulate a real physics-based descent.

**What you can adjust:**
- 🪂 **Parachute radius** (0 – 5 m) — drag force depends on atmosphere density
- ⚖️ **Total lander mass** (1 – 500 kg)
- 📏 **Initial altitude** (10 – 2,000 m)
- 🛸 **Lander body width** (affects aerodynamic drag cross-section)
- 🦵 **Landing leg length** (visual deployment animation)
- 💨 **Wind speed** (0 – 100 m/s) and **wind direction** (0 – 355°)

**What you see in the simulation canvas:**
- Real-time descent animation (lander + parachute + rocket exhaust)
- Landing legs deploy automatically below 20 m altitude
- HUD showing altitude, velocity, and elapsed time
- Wind direction arrow
- Safe / Crash verdict on touchdown

**Results panel shows:**
- Impact velocity (m/s) — safe threshold: **< 3 m/s**
- Total flight time (s)
- Lateral drift caused by wind (m)

---

### Tab 2 — ⚙️ Arduino Auto-Landing Code

Generate ready-to-upload Arduino code for a real autonomous landing system.

**Adjustable parameters (sliders → live code update):**

| Parameter | Range | Default | Effect |
|-----------|-------|---------|--------|
| `LANDING_THRESHOLD` | 3 – 80 cm | 10 cm | Altitude at which legs deploy |
| `LEG_DEPLOY_ANGLE` | 30 – 180° | 90° | Servo rotation for full leg extension |
| `LEG_DEPLOY_TIME` | 200 – 6000 ms | 1500 ms | How slowly legs unfold |
| `TILT_THRESHOLD` | 2000 – 16000 | 8000 | IMU raw value for dangerous tilt |
| `CHECK_INTERVAL` | 50 – 2000 ms | 500 ms | How often sensors are read |

**Hardware used:**

| Component | Purpose | Arduino Pin |
|-----------|---------|-------------|
| HC-SR04 Ultrasonic | [N] Altitude measurement | TRIG=9, ECHO=10 |
| MPU6050 IMU | [N][C] Tilt detection | SDA=A4, SCL=A5 |
| Servo × 4 | [C] Landing leg deployment | 3, 5, 6, 11 |
| Green LED | [G] Status / success indicator | Pin 13 |
| Red LED | [C] Tilt warning | Pin 12 |

**How to upload from Galaxy Tab or smartphone:**
1. **ArduinoDroid** (Google Play) + USB OTG cable ← *Recommended*
2. Arduino Web Editor at `create.arduino.cc`
3. Chrome Web Serial API (enable in `chrome://flags`)

---

### Tab 3 — 📱 QR Code Sharing

- Auto-generates a QR code from the current page URL
- Paste any custom URL to generate a QR for it
- Students scan with phone camera → instant access, no typing needed

---

## 🪐 Planet Physics Data

Each planet uses real gravitational acceleration and atmospheric density values:

| Planet | Gravity (m/s²) | Atm. Density (kg/m³) | Parachute Works? | Landing Difficulty |
|--------|---------------|----------------------|-----------------|-------------------|
| ☿ Mercury | 3.7 | ~0 | ❌ No | Medium (no air brake) |
| ♀ Venus | 8.87 | 65.0 | ✅ Very effective | Easy (thick atmosphere) |
| ⊕ Earth | 9.81 | 1.225 | ✅ Yes | Medium |
| ☽ Moon | 1.62 | 0 | ❌ No | Hard (no air, low gravity helps) |
| ♂ Mars | 3.72 | 0.020 | ⚠️ Barely | Hard (thin atmosphere) |
| ♃ Jupiter | 24.79 | 0.16 | ✅ Yes | Very Hard (extreme gravity) |
| ♄ Saturn | 10.44 | 0.10 | ✅ Yes | Hard |
| ⛢ Uranus | 8.87 | 0.09 | ✅ Yes | Hard |
| ♆ Neptune | 11.15 | 0.12 | ✅ Yes | Hard (strong winds) |

> **Physics note:** Terminal velocity = √(2mg / ρ·Cd·A). On the Moon (ρ=0) this is infinite — only rocket thrust can slow you down!

---

## 🔌 Wiring Diagram

```
Arduino Uno
    ┌─────────────────────────────────────┐
    │  Pin  9  ──── HC-SR04  TRIG         │
    │  Pin 10  ──── HC-SR04  ECHO         │
    │  5V / GND ─── HC-SR04  VCC / GND   │
    │                                     │
    │  Pin  3  ──── Servo 1 (front-left)  │
    │  Pin  5  ──── Servo 2 (front-right) │
    │  Pin  6  ──── Servo 3 (rear-left)   │
    │  Pin 11  ──── Servo 4 (rear-right)  │
    │  5V / GND ─── All servo power       │
    │                                     │
    │  A4 (SDA) ─── MPU6050 SDA           │
    │  A5 (SCL) ─── MPU6050 SCL           │
    │  5V / GND ─── MPU6050 VCC / GND    │
    │                                     │
    │  Pin 13  ──── Green LED + 220Ω      │
    │  Pin 12  ──── Red LED   + 220Ω      │
    └─────────────────────────────────────┘
```

---

## ⚡ Quick Start

### Option A — Use the Live Web App
1. Scan the QR code or visit the GitHub Pages URL
2. Select a planet and adjust parameters
3. Press **▶ Start Simulation**
4. Switch to the **Arduino** tab to generate code

### Option B — Run Locally
```bash
# No installation needed — just open the file
open index.html
# or on Windows:
start index.html
```

### Option C — Deploy Your Own Copy
```
1. Fork this repository
2. Go to Settings → Pages
3. Set Source: Deploy from a branch → main → / (root)
4. Visit https://YOUR-USERNAME.github.io/lander-SIMULATOR/
```

---

## 📚 Curriculum Connection

This simulator accompanies the **Junior Lunar Lander GNC** learning materials, which teach:

- Why spacecraft can't use wings or parachutes on the Moon
- How Apollo 11, China's Chang'e, and Korea's Danuri work
- The three components of every GNC system
- How IMU sensors, radar altimeters, and star trackers work
- Arduino programming: sensors, servos, and autonomous decision logic

**Learning objectives met:**
- [x] Understand G/N/C subsystem roles
- [x] Apply drag equation: F = ½ρCdAv²
- [x] Read IMU (MPU6050) and ultrasonic (HC-SR04) sensor data
- [x] Program servo motor sequences with timing control
- [x] Analyze simulation results and tune parameters

---

## 🛠️ Technology Stack

| Layer | Technology |
|-------|-----------|
| Frontend | Vanilla HTML5, CSS3, JavaScript (ES6+) |
| Physics | Euler integration, drag equation |
| Animation | Canvas API (requestAnimationFrame) |
| QR Code | QRCode.js (cdnjs) |
| Arduino | C++ (Servo.h, Wire.h, I2C) |
| Hosting | GitHub Pages (free, static) |

> **Single file:** The entire app is one `index.html` — no build step, no dependencies, no server needed.

---

## 📁 Repository Structure

```
lander-SIMULATOR/
├── index.html          ← Entire web app (simulator + code generator + QR)
└── README.md           ← This file
```

---

## 🤝 Contributing

Pull requests are welcome! Ideas for improvement:
- Add more celestial bodies (Titan, Europa, Pluto)
- 3D canvas rendering with Three.js
- Bluetooth Web API for direct Arduino communication
- Save/load simulation configurations
- Multi-language support (Korean/English toggle)

---

## 📄 License

MIT License — free to use, modify, and share for educational purposes.

---

<div align="center">

**Made with ❤️ for junior space engineers**

*"The Moon is a harsh mistress — but GNC makes it manageable."*

</div>
