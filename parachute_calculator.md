# Parachute Size Calculation Guide

> SRC Rocket & Exploration Program / Pumpkin Factory Makerspace  
> A reference guide to physics formulas and design variables for parachute design and fabrication

---

## 1. Core Physics Formula

Parachute size is determined by the condition where **Drag Force = Weight**.

```
D = ½ · ρ · Cd · A · v²  =  m · g
```

Solving for the required canopy area A:

```
A = (2 · m · g) / (ρ · Cd · v²)
```

| Symbol | Meaning | Unit |
|--------|---------|------|
| A | Canopy deployed area | m² |
| m | Payload mass | kg |
| g | Gravitational acceleration | m/s² |
| ρ | Air density | kg/m³ |
| Cd | Drag coefficient | dimensionless |
| v | Target landing velocity | m/s |

**Diameter of a circular parachute:**

```
d = √(4A / π)
```

---

## 2. Environmental Variables

### 2-1. Gravity and Atmospheric Density by Planet

| Environment | Gravity (m/s²) | Sea-level Density (kg/m³) | Notes |
|-------------|---------------|--------------------------|-------|
| Earth (sea level) | 9.81 | 1.225 | Standard atmosphere |
| Earth (altitude 10 km) | 9.76 | 0.414 | Typical aircraft cruise altitude |
| Earth (altitude 30 km) | 9.70 | 0.018 | Stratosphere |
| Mars (surface) | 3.72 | 0.020 | CO₂ atmosphere |
| Venus (surface) | 8.87 | 65.0 | Extremely dense atmosphere |
| Titan (surface) | 1.35 | 5.3 | N₂ atmosphere |
| Moon | 1.62 | 0 | No atmosphere — parachute not viable |

### 2-2. Altitude-Based Density Correction (Exponential Atmosphere Model)

```
ρ(h) = ρ₀ · exp(−h / H)
```

| Body | Atmospheric Scale Height H (m) |
|------|-------------------------------|
| Earth | 8,500 |
| Mars | 11,000 |
| Venus | 15,900 |
| Titan | 18,000 |

---

## 3. Drag Coefficient (Cd) by Parachute Type

| Type | Cd | Characteristics | Recommended Use |
|------|----|-----------------|-----------------|
| Flat circular | 1.05 | Simple shape, easy to make | Low-speed model rockets, education |
| Hemispherical | 0.75 | Stable, standard shape | General rockets, drone payloads |
| Cross (cruciform) | 1.00 | Suppresses lateral drift | Precision landing, sounding rockets |
| Annular | 0.85 | Central opening reduces oscillation | Mid-speed, stability-critical |
| Ribbon | 0.55 | Optimised for high-speed stabilisation | Drogue chutes, supersonic deployment |
| X-form | 0.90 | Rectangular variant, military/exploration | Special missions |

> **Drogue + Main parachute dual system**: Use a ribbon drogue (Cd 0.55) for high-speed stabilisation, then deploy the main canopy (e.g. hemispherical) at low altitude.

---

## 4. Additional Design Variables for Stable Landing

### 4-1. Safety Factor (SF)

```
A_design = A_theoretical × SF
```

| Application | Recommended SF |
|-------------|---------------|
| Educational model | 1.2 |
| General unmanned payload | 1.3 – 1.5 |
| Precision instrument payload | 1.5 – 2.0 |
| Crewed system | 2.0 – 3.0 |

---

### 4-2. Opening Shock Factor (Cx)

The shock load at deployment is significantly higher than the steady-state drag force.

```
F_shock = Cx · ½ · ρ · Cd · A · v_deploy²
```

| Deployment Method | Cx Range |
|-------------------|----------|
| Free deployment | 1.5 – 2.5 |
| Slider-equipped | 1.1 – 1.3 |
| Reefed deployment | 1.0 – 1.2 |

> **Minimum suspension line tensile strength** = F_shock ÷ number of lines — use this to find the required strength per line.

---

### 4-3. Suspension Lines

**Number of lines (N):** As a rule of thumb, use at least half the canopy diameter in centimetres.

```
N ≥ d(cm) / 2
```

Example: 60 cm diameter canopy → minimum 30 lines (practical minimum 8–16 lines)

**Line length ratio (L/D):**

```
L = k · d  (k = 1.0 – 1.5 recommended)
```

| L/D Ratio | Behaviour |
|-----------|-----------|
| Below 0.8 | Heavy oscillation, unstable |
| 1.0 | Baseline stability |
| 1.2 – 1.5 | Minimum oscillation — recommended range |
| 2.0 and above | Excessively long, impractical |

---

### 4-4. Vent Hole

An opening at the apex of the canopy reduces oscillation and improves stability.

```
Vent ratio = D_vent / D_canopy × 100 (%)
```

| Vent Ratio | Effect |
|------------|--------|
| 0 % (none) | Heavy oscillation (bag effect) |
| 5 – 10 % | Improved stability, slight Cd reduction |
| 15 – 20 % | Very stable, Cd reduced by 5–8 % |
| 25 % and above | Sharp Cd drop; landing speed increases — use with caution |

> When a vent is added, the effective Cd decreases by approximately 3–8 %, so increase the calculated area by the corresponding amount to compensate.

---

### 4-5. Wind Effect and Drift Distance

Predicting the landing point:

```
drift (m) = wind speed (m/s) × descent time (s)
descent time (s) = deployment altitude (m) / landing speed (m/s)
```

Effective landing speed including wind:

```
v_effective = √(v_vertical² + v_wind²)
```

---

### 4-6. Maximum Allowable Landing Speed

| Payload Type | Recommended Landing Speed |
|--------------|--------------------------|
| Robust metal structure | ≤ 10 m/s |
| General electronics | ≤ 7 m/s |
| Camera / optical instruments | ≤ 5 m/s |
| Egg drop experiment | ≤ 3 m/s |
| Crewed system | ≤ 6 m/s (military) / ≤ 5 m/s (civilian) |

---

## 5. DIY Fabrication Guide

### 5-1. Material Selection

**Canopy fabric:**

| Material | Areal Weight | Characteristics | Recommended Use |
|----------|-------------|-----------------|-----------------|
| Nylon ripstop 30D | ~40 g/m² | Lightweight, strong, water-resistant | Small model rockets |
| Nylon ripstop 70D | ~80 g/m² | Excellent durability | Medium-class payloads |
| Polyester fabric | ~100 g/m² | Low cost, slightly stretchy | Educational experiments |
| Mylar | ~20 g/m² | Ultra-light, heat-sensitive | Ultra-small models |
| Parachute nylon | ~55 g/m² | Standard canopy fabric | Reliability-critical missions |

**Suspension line materials:**

| Material | Rated Strength | Characteristics |
|----------|---------------|-----------------|
| 550 paracord | 250 kg | Affordable, heavier |
| Kevlar line | High | Light and strong, expensive |
| Monofilament fishing line | Low | Educational use only |
| Polyester thread | Low | Micro-model applications only |

---

### 5-2. Construction Steps for a Flat Circular Parachute

1. **Pattern cutting**: Cut a circle with the calculated diameter plus 2–3 cm seam allowance.
2. **Gore panels (optional)**: For a better canopy shape, cut the circle into 8–16 gore panels and sew them together.
3. **Vent hole**: Cut a circular hole at the apex with the calculated vent diameter; reinforce the edge.
4. **Suspension point marking**: Divide the canopy hem equally into N attachment points and mark them.
5. **Tape reinforcement**: Sew radial reinforcement tape along the hem and at each suspension attachment point.
6. **Ring link attachment**: Attach a metal or slide ring at the point where all lines converge.
7. **Line attachment**: Cut lines to the calculated length (d × 1.2) and connect canopy to ring link.
8. **Harness connection**: Connect the ring link to the payload harness or eyebolt.

---

### 5-3. Packing (Folding)

| Method | Characteristics |
|--------|-----------------|
| Z-fold | Most common; high deployment reliability |
| Radial fold | Designed for circular canopies; uniform opening |
| Bundle method | Simple but prone to tangling |

> Estimated deployment cylinder diameter after packing:  
> `d_cylinder ≈ √(A_canopy × t_fabric) / π` (empirical reference only)

---

## 6. Worked Example

**Conditions:** Earth sea level, mass 0.5 kg, landing speed 5 m/s, hemispherical canopy, SF = 1.3

```
A = (2 × 0.5 × 9.81) / (1.225 × 0.75 × 5²)
  = 9.81 / 22.97
  = 0.427 m²

A_design = 0.427 × 1.3 = 0.555 m²

d = √(4 × 0.555 / π) = √(0.707) = 0.841 m ≈ 84 cm
```

Vent hole (10%): `d_vent = 84 × 0.10 = 8.4 cm`  
Number of lines: `N = 84 / 2 = 42 → practical choice: 16 lines`  
Line length: `L = 84 × 1.2 = 100.8 cm ≈ 101 cm`

---

## 7. Frequently Asked Questions

**Q. Why is parachute deployment so challenging on Mars?**  
Atmospheric density on Mars is roughly 1/60 that of Earth (0.020 kg/m³). Under identical mass and velocity conditions, a parachute approximately 60 times larger in area is required. NASA's Perseverance rover used a 21.5 m diameter supersonic parachute to manage this.

**Q. What if the parachute fails to deploy?**  
A drogue (pilot) parachute is used to force the main canopy open — a dual deployment system. The drogue is small and deploys first at high speed to stabilise the vehicle, then pulls out the main canopy.

**Q. What size parachute is appropriate for an egg drop experiment?**  
Egg + container ≈ 100 g, target speed ≤ 3 m/s, Earth sea level, hemispherical canopy (Cd 0.75), SF 1.3:

```
A_design = (2 × 0.1 × 9.81) / (1.225 × 0.75 × 9) × 1.3 ≈ 0.310 m²
d ≈ 63 cm
```

---

*This document is an educational resource for the Pumpkin Factory Makerspace SRC Program.*  
*All formulas assume quasi-static descent conditions. Transient dynamics during the deployment phase require separate analysis.*
