# Analytical Thermal Model — Yardimci Bonding Model

## Overview

Before running numerical simulations in COMSOL, it is valuable to understand the **governing physics** through an analytical model. The Yardimci model describes the heat transfer in a single FDM filament during deposition and forms the theoretical foundation for this project's simulations.

---

## The Governing Equation

```
ρ (∂q/∂t) = k (∂²T/∂x²) − (h/h_eff)(T − T∞) − (k/Width²)(T − T_neigh)
```

---

## Breaking Down Each Term

### Left Side: Heat Stored in the Filament

```
ρ (∂q/∂t)
```

| Symbol | Meaning | Units |
|--------|---------|-------|
| ρ | Density of the filament material | kg/m³ |
| q | Heat content (enthalpy) per unit volume | J/m³ |
| ∂q/∂t | Rate of change of stored heat over time | W/m³ |

**Plain English:** This term says "how fast is the filament gaining or losing heat energy?" If this is positive, the filament is heating up. If negative, it's cooling down.

---

### Right Side, Term 1: Conduction Along the Filament

```
k (∂²T/∂x²)
```

| Symbol | Meaning | Units |
|--------|---------|-------|
| k | Thermal conductivity of the material | W/m·K |
| ∂²T/∂x² | Second derivative of temperature along the filament length | K/m² |

**Plain English:** Heat conducts along the length of the filament (in the direction it was deposited, the x-direction). If one section of the filament is hotter than the adjacent section, heat flows from hot to cold. For PETG with k = 0.17 W/m·K, this conduction is relatively slow — PETG doesn't conduct heat well.

---

### Right Side, Term 2: Convective Cooling to Air

```
− (h/h_eff)(T − T∞)
```

| Symbol | Meaning | Units |
|--------|---------|-------|
| h | Convective heat transfer coefficient | W/m²·K |
| h_eff | Effective convection coefficient (accounts for geometry) | W/m²·K |
| T | Local filament temperature | °C |
| T∞ | Ambient air temperature | °C |

**Plain English:** The surface of the filament loses heat to the surrounding air. The bigger the temperature difference between the filament and the air (T − T∞), the faster it cools. This is **convective heat loss** — the dominant cooling mechanism in most FDM printers without heated enclosures.

The negative sign means this term always removes heat from the filament.

---

### Right Side, Term 3: Heat Transfer to Neighboring Filaments/Layers

```
− (k/Width²)(T − T_neigh)
```

| Symbol | Meaning | Units |
|--------|---------|-------|
| k | Thermal conductivity | W/m·K |
| Width | Width of the filament bead | m |
| T_neigh | Temperature of adjacent filament or layer | °C |

**Plain English:** A newly deposited hot filament also conducts heat sideways into adjacent already-deposited filaments and into the layer below. This is critical for **interlayer bonding** — the hot new bead re-heats the nearby material, allowing polymer chains to interdiffuse and bond. The Width² term makes this transfer dependent on how closely packed the beads are.

---

## Complete Energy Balance for One Filament Element

```
Heat stored = Heat conducted in + Heat convected out + Heat to neighbors
     ↑                ↑                   ↑                   ↑
Changes with     Along filament       To the air         To adjacent
   time           (x-direction)    (cooling mechanism)   deposited
                                                           material
```

---

## Why This Model Matters for FDM Quality

The Yardimci model explains several common FDM problems:

### 1. Weak Interlayer Bonding
If **T_neigh** (the temperature of previously deposited material) has already cooled too much before the new bead arrives, the third term becomes very small — there is not enough reheating to drive polymer chain diffusion across the interface. Result: the layers peel apart easily (delamination).

**Fix:** Print faster (less time for cooling between layers), use a heated enclosure, or increase bed temperature.

### 2. Warping
If the average temperature across the part rises too high (as seen in the transient simulation), and then the part cools unevenly, different regions shrink by different amounts. The second term (convection to air) cools external surfaces faster than the interior, creating thermal stress that curls the edges up.

**Fix:** Use a heated bed, enclosed printer, or switch to a low-shrinkage material like PETG.

### 3. Stringing
Between print moves, the nozzle travels over empty space. The material in the nozzle continues to be heated by the heater block. If retraction (pulling the filament back slightly) is not tuned well, a thin string of molten polymer oozes out during travel moves.

**The model connection:** The convection term keeps cooling the deposited material, but material inside the hot nozzle stays at extrusion temperature. The thermal mismatch between these is what drives stringing.

---

## PETG Properties in the Model

For reference, PETG properties used in this project:

| Symbol | PETG Value |
|--------|-----------|
| ρ (Density) | 1270 kg/m³ |
| k (Thermal Conductivity) | 0.17 W/m·K |
| c_p (Specific Heat) | 1200 J/kg·K |
| T_extrusion | 220–250°C |
| T_glass (approx) | ~80°C |

The glass transition temperature (T_glass ≈ 80°C) is particularly important — it is the threshold below which PETG becomes rigid. For strong interlayer bonding, the interface must be briefly above T_glass when a new bead is deposited. The transient simulation confirms the maximum temperatures (~90°C) do exceed this threshold during each deposition cycle.

---

## References

- Yardimci, M.A. et al. — Original bonding model for FDM thermal analysis
- Apaçoğlu-Turan, B., Kırkköprü, K., & Çakan, M. (2024). *Numerical Modeling and Analysis of Transient and Three-Dimensional Heat Transfer in 3D Printing via FDM*. Computation, 12(2), 27.
