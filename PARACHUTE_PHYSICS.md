# 🪂 Parachute Size Calculation Guide
### Across the Solar System — Physics, Formulas & Real Mission Data

> **Part of the Lunar Lander GNC Simulator curriculum.**  
> This document explains how to calculate the correct parachute diameter for safe landing on any planet with an atmosphere — and why some planets make it nearly impossible.

---

## 🌌 Why Parachute Size Matters

A lander falling through an atmosphere experiences two competing forces:

- **Weight (W)** — gravity pulling it *down*  
- **Drag (D)** — atmosphere pushing it *up*

When drag equals weight, acceleration becomes zero and the lander falls at a constant speed called **terminal velocity**. If terminal velocity is too high, the lander crashes. The parachute's job is to increase drag enough to bring terminal velocity below a safe threshold.

> **Safe landing threshold: v < 3 m/s** *(used in this simulator)*  
> Real missions target 2–10 m/s depending on landing gear design.

---

## 📐 Core Physics Formulas

### 1. Drag Force
```
F_drag = ½ × ρ × v² × Cd × A
```

| Symbol | Meaning | Unit |
|--------|---------|------|
| ρ (rho) | Atmospheric density | kg/m³ |
| v | Velocity | m/s |
| Cd | Drag coefficient (≈ 1.5 for parachute) | — |
| A | Parachute area = π × r² | m² |

### 2. Terminal Velocity (at equilibrium: F_drag = Weight)
```
F_drag = W
½ × ρ × v_t² × Cd × A = m × g

→ v_t = √( 2mg / (ρ × Cd × A) )
```

### 3. Required Parachute Area (for target landing speed v_target)
```
A_required = 2mg / (ρ × Cd × v_target²)
```

### 4. Required Parachute Radius
```
r = √( A_required / π )
```

### 5. Full Calculation Chain
```
Given:  m (mass), g (gravity), ρ (atm. density), v_target (safe speed)
        Cd = 1.5 (parachute drag coefficient)

Step 1: A = 2 × m × g / (ρ × Cd × v_target²)
Step 2: r = √(A / π)
Step 3: diameter = 2r
```

---

## 🪐 Planet-by-Planet Calculations

### Reference conditions
- **Lander mass:** 10 kg  
- **Target landing speed:** 3 m/s  
- **Parachute Cd:** 1.5  

### Formula applied:  `r = √( 2mg / (π × ρ × Cd × v²) )`

---

### ☿ Mercury
| Parameter | Value |
|-----------|-------|
| Gravity | 3.7 m/s² |
| Atm. density | ~0.0001 kg/m³ |
| Required parachute radius | **~593 m** ⚠️ |
| Verdict | ❌ **Impossible** — no usable atmosphere |

```
A = (2 × 10 × 3.7) / (0.0001 × 1.5 × 9) = 74 / 0.00135 ≈ 54,815 m²
r = √(54,815 / π) ≈ 132 m  ← absurdly large, effectively no atmosphere
```
> **Conclusion:** Mercury has virtually no atmosphere. Parachutes are completely useless.  
> Only **rocket retropropulsion** can slow a lander on Mercury.

---

### ♀ Venus
| Parameter | Value |
|-----------|-------|
| Gravity | 8.87 m/s² |
| Atm. density | **65.0 kg/m³** (92× Earth!) |
| Required parachute radius | **~0.25 m** ✅ |
| Verdict | ✅ **Tiny parachute sufficient** |

```
A = (2 × 10 × 8.87) / (65.0 × 1.5 × 9) = 177.4 / 877.5 ≈ 0.202 m²
r = √(0.202 / π) ≈ 0.25 m  (diameter ≈ 50 cm!)
```
> **Real mission:** Soviet **Venera probes** used small parachutes only in the upper atmosphere  
> (altitude > 50 km). Below 50 km, the atmosphere is so dense that even aerodynamic drag  
> from the lander body alone slows it to safe terminal velocity (~7 m/s). Venera 9 landed  
> using just a 2 m disc brake — no parachute needed in the lower layers.

---

### ⊕ Earth
| Parameter | Value |
|-----------|-------|
| Gravity | 9.81 m/s² |
| Atm. density | 1.225 kg/m³ |
| Required parachute radius | **~1.94 m** ✅ |
| Verdict | ✅ **Standard parachute works well** |

```
A = (2 × 10 × 9.81) / (1.225 × 1.5 × 9) = 196.2 / 16.54 ≈ 11.87 m²
r = √(11.87 / π) ≈ 1.94 m  (diameter ≈ 3.9 m)
```
> **Scale reference:** A 10 kg payload needs roughly a 4 m diameter parachute to land at 3 m/s.  
> The ISS crew returns in a 20 m Soyuz parachute carrying ~3 crew members (~270 kg total).

---

### ☽ Moon
| Parameter | Value |
|-----------|-------|
| Gravity | 1.62 m/s² |
| Atm. density | **0 kg/m³** |
| Required parachute radius | **∞ (infinite)** |
| Verdict | ❌ **Impossible** — vacuum |

```
A = 2mg / (0 × Cd × v²) → division by zero → no solution exists
```
> **Conclusion:** The Moon has zero atmosphere. This is *the* fundamental challenge of lunar landing.  
> **Only solution: rocket retropropulsion** — the lander fires engines downward to cancel gravity.  
> Apollo's Lunar Module burned ~8,000 kg of propellant during the powered descent.  
> This is exactly why GNC systems are so critical on the Moon!

---

### ♂ Mars
| Parameter | Value |
|-----------|-------|
| Gravity | 3.72 m/s² |
| Atm. density | 0.020 kg/m³ (1.6% of Earth) |
| Required parachute radius | **~5.0 m** ⚠️ |
| Verdict | ⚠️ **Large parachute needed, rockets still required** |

```
A = (2 × 10 × 3.72) / (0.020 × 1.5 × 9) = 74.4 / 0.27 ≈ 275.6 m²
r = √(275.6 / π) ≈ 9.4 m  (diameter ≈ 18.7 m) for 10 kg lander
```
> **Real mission comparison:** NASA **Perseverance** (mass: 1,025 kg) used a **21.5 m diameter**  
> supersonic parachute — matching our formula prediction when scaled to its mass!  
> Even so, Perseverance was still traveling at **~320 km/h** after parachute deployment  
> and needed rocket engines (sky crane system) for the final 2 km of descent.

---

### ♃ Jupiter (Upper Atmosphere Entry)
| Parameter | Value |
|-----------|-------|
| Gravity | 24.79 m/s² |
| Atm. density (upper) | 0.16 kg/m³ |
| Required parachute radius | **~8.1 m** ⚠️ |
| Verdict | ⚠️ **Huge gravity dominates** — no solid surface to land on |

```
A = (2 × 10 × 24.79) / (0.16 × 1.5 × 9) = 495.8 / 2.16 ≈ 229.5 m²
r = √(229.5 / π) ≈ 8.5 m
```
> **Real mission:** NASA **Galileo probe** (339 kg) entered Jupiter's atmosphere in 1995  
> using a 3.7 m parachute. It survived for 58 minutes before being crushed by pressure  
> at 22× Earth atmospheric pressure. There is no surface — pressure increases until  
> the probe is destroyed.

---

### ♄ Saturn
| Parameter | Value |
|-----------|-------|
| Gravity | 10.44 m/s² |
| Atm. density | 0.10 kg/m³ |
| Required parachute radius | **~6.6 m** |
| Verdict | ⚠️ **Large parachute, no solid surface** |

```
A = (2 × 10 × 10.44) / (0.10 × 1.5 × 9) = 208.8 / 1.35 ≈ 154.7 m²
r = √(154.7 / π) ≈ 7.0 m
```
> Saturn itself has no solid surface. However its moon **Titan** (g=1.35, ρ=5.2 kg/m³)  
> is a far better candidate! ESA's **Huygens probe** (319 kg) descended through Titan's  
> atmosphere in 2005 using an 8.3 m main parachute, landing safely after 2.5 hours of descent.

---

### ⛢ Uranus
| Parameter | Value |
|-----------|-------|
| Gravity | 8.87 m/s² |
| Atm. density | 0.09 kg/m³ |
| Required parachute radius | **~7.2 m** |
| Verdict | ⚠️ **Large parachute, no solid surface** |

```
A = (2 × 10 × 8.87) / (0.09 × 1.5 × 9) = 177.4 / 1.215 ≈ 146.0 m²
r = √(146.0 / π) ≈ 6.8 m
```

---

### ♆ Neptune
| Parameter | Value |
|-----------|-------|
| Gravity | 11.15 m/s² |
| Atm. density | 0.12 kg/m³ |
| Required parachute radius | **~7.0 m** |
| Verdict | ⚠️ **Large parachute, no solid surface** |

```
A = (2 × 10 × 11.15) / (0.12 × 1.5 × 9) = 223.0 / 1.62 ≈ 137.7 m²
r = √(137.7 / π) ≈ 6.6 m
```
> Neptune has the strongest winds in the solar system (~2,100 km/h).  
> Wind drift would be the dominant landing challenge, not terminal velocity.

---

## 📊 Complete Solar System Summary Table

| Planet | g (m/s²) | ρ (kg/m³) | Parachute? | Req. Radius (10 kg, 3 m/s) | Real Mission Example |
|--------|----------|-----------|-----------|---------------------------|---------------------|
| ☿ Mercury | 3.70 | 0.0001 | ❌ No | ~132 m (impossible) | None (no atmo) |
| ♀ Venus | 8.87 | 65.0 | ✅ Tiny | **0.25 m** | Venera 9 (disc brake only) |
| ⊕ Earth | 9.81 | 1.225 | ✅ Yes | **1.94 m** | Apollo capsule ~23 m (5,800 kg) |
| ☽ Moon | 1.62 | 0 | ❌ No | ∞ (impossible) | Apollo LM (rockets only) |
| ♂ Mars | 3.72 | 0.020 | ⚠️ Large | **9.4 m** | Perseverance 21.5 m (1,025 kg) |
| ♃ Jupiter | 24.79 | 0.16 | ⚠️ Large | **8.5 m** | Galileo probe 3.7 m (339 kg) |
| ♄ Saturn | 10.44 | 0.10 | ⚠️ Large | **7.0 m** | Huygens/Titan 8.3 m (319 kg) |
| ⛢ Uranus | 8.87 | 0.09 | ⚠️ Large | **6.8 m** | None (not visited) |
| ♆ Neptune | 11.15 | 0.12 | ⚠️ Large | **6.6 m** | None (not visited) |

> ⚠️ Note: Jupiter, Saturn, Uranus, Neptune values use upper atmosphere density.  
> These gas giants have no solid surface — the pressure becomes lethal before any "landing."

---

## 📏 How Mass Affects Required Size

The required parachute area scales **linearly** with mass:

```
A_required ∝ m × g

If mass doubles → parachute area doubles → radius increases by √2 ≈ 1.41×
```

### Example: Mars landing, target 3 m/s

| Lander Mass | Required Area | Required Radius | Real Example |
|------------|--------------|----------------|-------------|
| 1 kg | 27.6 m² | 2.96 m | Small cubesat |
| 10 kg | 275.6 m² | 9.4 m | Small rover |
| 100 kg | 2,756 m² | 29.6 m | Medium lander |
| 1,025 kg | 28,244 m² | **94.8 m** | Perseverance size |

> **Why does Perseverance only use a 21.5 m parachute?**  
> Because it doesn't need to reach 3 m/s from the parachute alone!  
> The parachute only needs to slow it from 1,500 km/h to ~320 km/h,  
> then rocket engines handle the final phase. This is the **two-phase EDL strategy**.

---

## 🎯 Two-Phase Entry, Descent & Landing (EDL) Strategy

For planets with thin atmospheres (Mars, Mercury) or no atmosphere (Moon):

```
Phase 1: Aeroshell / heatshield    1,500°C+ heating, hypersonic drag
          ↓
Phase 2: Parachute (if atmosphere) Subsonic to ~300-500 km/h
          ↓
Phase 3: Rocket retropropulsion    Final 2 km, reduce to 0 m/s
          ↓
Phase 4: Landing legs absorb impact Last 1-2 m, crush/spring shock absorption
```

On the Moon and Mercury: **Phase 2 is skipped entirely.**  
On Venus: **Phase 3 is often skipped** (atmosphere is thick enough).

---

## 🔢 Simulator Code Implementation

This is exactly how the GNC Simulator calculates drag and terminal velocity:

```javascript
// From the simulator's physics engine
function computeDrag(state) {
  const { rho, v, Ac, Ab } = state;   // Ac = chute area, Ab = body area
  const Cd_chute = 1.5;
  const Cd_body  = 0.5;
  
  // Combined drag: parachute + lander body
  const drag = 0.5 * rho * v * v * (Cd_chute * Ac + Cd_body * Ab);
  return drag;
}

// Terminal velocity (when drag = weight)
function terminalVelocity(mass, gravity, rho, parachuteRadius, bodyWidth) {
  const Ac = Math.PI * parachuteRadius ** 2;
  const Ab = (bodyWidth / 100) ** 2 * 0.45;
  const totalCdA = 1.5 * Ac + 0.5 * Ab;
  
  if (rho === 0) return Infinity;  // No atmosphere → no terminal velocity
  return Math.sqrt((2 * mass * gravity) / (rho * totalCdA));
}

// Required parachute radius for safe landing
function requiredRadius(mass, gravity, rho, targetSpeed) {
  if (rho === 0) return Infinity;
  const A = (2 * mass * gravity) / (rho * 1.5 * targetSpeed ** 2);
  return Math.sqrt(A / Math.PI);
}
```

---

## 🏆 Real Mission Parachute Data

| Mission | Planet | Lander Mass | Parachute Diameter | Entry Speed | Speed After Chute |
|---------|--------|-------------|-------------------|-------------|-------------------|
| Apollo (CM) | Earth | 5,800 kg | 23 m × 3 chutes | 11 km/s | 8.5 m/s |
| Venera 9 | Venus | 660 kg | Small + disc brake | 10.7 km/s | 7 m/s (disc only) |
| Mars Pathfinder | Mars | 360 kg | 8.4 m | 7.6 km/s | ~80 m/s* |
| Curiosity | Mars | 900 kg | 19.7 m | 5.9 km/s | ~90 m/s* |
| Perseverance | Mars | 1,025 kg | **21.5 m** | 5.5 km/s | ~90 m/s* |
| Galileo probe | Jupiter | 339 kg | 3.7 m + 1.2 m pilot | — | stable descent |
| Huygens | Titan/Saturn | 319 kg | 8.3 m (main) | 6 km/s | ~5 m/s |

> *Mars landers still travel at ~80-90 m/s after parachute deployment and require  
> rocket engines, airbags, or sky crane systems for the final landing phase.

---

## 🧮 Try It Yourself: Calculation Worksheet

### Problem 1 — Moon Landing
> A lander (mass = 50 kg) must land on the Moon at ≤ 3 m/s.  
> Can a parachute help? If not, what thrust must the rockets provide?

**Answer:**  
Moon ρ = 0 → Parachute **cannot work**.  
Required rocket thrust: F = m × g = 50 × 1.62 = **81 N** minimum  
(must exceed 81 N to decelerate)

---

### Problem 2 — Mars Landing  
> Design a parachute for a 5 kg Mars lander targeting 8 m/s terminal velocity.

```
A = 2 × 5 × 3.72 / (0.020 × 1.5 × 64) = 37.2 / 1.92 ≈ 19.4 m²
r = √(19.4 / π) ≈ 2.49 m  → diameter ≈ 4.97 m
```
**Answer: ~5 m diameter parachute**

---

### Problem 3 — Venus Landing  
> A 20 kg lander descends to Venus. What is terminal velocity with a 1 m radius parachute?

```
A_chute = π × 1² ≈ 3.14 m²
v_t = √(2 × 20 × 8.87 / (65 × 1.5 × 3.14))
    = √(354.8 / 306.2)
    = √1.159 ≈ 1.08 m/s
```
**Answer: ~1.1 m/s** — extremely slow, safe landing!  
Venus's thick atmosphere makes parachute design very easy.

---

## 📚 Key Takeaways

1. **No atmosphere = no parachute.** Moon and Mercury require 100% rocket power.

2. **Mars is the hardest parachute problem** — thin atmosphere forces very large parachutes,  
   and they still can't slow landers to safe speeds alone.

3. **Venus is the easiest** — dense atmosphere requires tiny parachutes and they often aren't  
   even needed in the lower atmosphere.

4. **Parachute area scales with mass, not volume** — doubling mass doubles the required area,  
   but only increases radius by ~41%.

5. **Real missions use staged EDL** — parachute + rockets together, not one or the other.

6. **Wind is the other challenge** — Neptune's 2,100 km/h winds would make lateral drift  
   far more dangerous than vertical impact speed.

---

## 🔗 References & Further Reading

- NASA Mars 2020 EDL overview: [mars.nasa.gov](https://mars.nasa.gov)
- Galileo probe Jupiter entry: [nssdc.gsfc.nasa.gov](https://nssdc.gsfc.nasa.gov)
- Huygens Titan descent: ESA Cassini-Huygens mission archive
- Venera program descent data: Soviet Academy of Sciences archives
- Perseverance parachute specs: JPL Technical Reports (2021)

---

*This document is part of the [Lunar Lander GNC Simulator](../index.html) educational project.*  
*Physics formulas verified against NASA JPL Entry, Descent & Landing engineering documentation.*
