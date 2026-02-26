# FDM Process Parameters — Complete Guide

## Overview

Seven machine parameters control the outcome of every FDM print. Understanding what each one does — and how they interact — is essential for producing high-quality parts. This document explains each parameter in plain language and describes the effect of tuning it up or down.

---

## The Seven Key Parameters

```
┌─────────────────────────────────────────────────────────────────────┐
│                        FDM PROCESS PARAMETERS                       │
│                                                                     │
│  1. Build Orientation        5. Print Speed                         │
│  2. Layer Thickness          6. Flow Rate                           │
│  3. Air Gap                  7. Extrusion Temperature               │
│  4. Raster Angle                                                    │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 1. Build Orientation

### What it is
The angle at which the part is positioned on the print bed relative to the X, Y, and Z axes of the printer.

### Why it matters
FDM parts are **anisotropic** — they are stronger in some directions than others. Specifically:
- Parts are generally **stronger in the X-Y plane** (horizontal layers) than in the **Z direction** (perpendicular to layers)
- This is because layer interfaces are always the weakest point in the part
- By rotating the part, you can align the weakest direction away from where the load will be applied

### Effect of changing it

| Orientation | Strength | Surface Quality | Support Required | Print Time |
|-------------|----------|-----------------|-----------------|------------|
| Flat (X-Y) | High in XY, weak in Z | Good on top faces | Minimal | Often shorter |
| Upright (Z) | Weak — many layer boundaries | Rough on sides | Often needed | Often longer |
| Angled | Balanced but complex | Variable | Often needed | Moderate |

### Practical rule
Orient the part so that the **primary load path** runs parallel to the layers (in the X-Y plane), not across them.

---

## 2. Layer Thickness

### What it is
The height of each deposited bead of material, measured in millimeters. Typical range: 0.05mm – 0.35mm.

### Why it matters
Layer thickness is a trade-off between **print speed** and **surface quality / strength**.

### Effect of changing it

| Thinner Layers (e.g., 0.1mm) | Thicker Layers (e.g., 0.3mm) |
|-------------------------------|-------------------------------|
| Smoother surface finish | Rougher, visible layer lines |
| Better dimensional accuracy on curved surfaces | Less accurate on curves |
| More layers → longer print time | Fewer layers → faster print |
| Slightly better interlayer bonding | Can have weak bonding if too thick |
| Lower maximum overhang angle | |

### Golden rule
Use **0.1–0.15mm** for visual/display parts. Use **0.2–0.3mm** for functional parts where strength and speed matter more than cosmetics.

---

## 3. Air Gap

### What it is
The space between adjacent raster lines (beads) deposited in the same layer. Can be positive (gap between beads), zero (beads just touching), or negative (beads overlapping).

### Why it matters
Air gap directly controls the **density and strength** of each layer.

### Effect of changing it

| Positive Air Gap (e.g., +0.1mm) | Zero Gap | Negative Air Gap (e.g., −0.1mm) |
|----------------------------------|----------|----------------------------------|
| Lighter, uses less material | Standard | Denser, stronger |
| Weaker — gaps reduce cross-section | | Slower — more material |
| Used for infill patterns | | Better for perimeters/shell |

### Practical note
For functional parts, use zero or slightly negative air gap for the outer shells/perimeters. For internal infill, a positive gap is normal and saves material without significantly affecting strength.

---

## 4. Raster Angle

### What it is
The direction in which the extruder deposits material within a layer, measured as an angle from the X-axis. Common values: 0°, 45°, 90°, or alternating ±45°.

### Why it matters
Like fiber orientation in composites, the raster angle determines the **directional strength** of each layer. Since beads are stronger along their length than across their width, the raster angle controls which direction the layer is strongest.

### Effect of changing it

| Raster Angle | Behavior |
|-------------|----------|
| 0° (all horizontal) | Strong in X, weak in Y |
| 90° (all vertical) | Strong in Y, weak in X |
| ±45° alternating | Best balanced in-plane strength (most common) |
| 0°/90° alternating | Good but slightly less isotropic than ±45° |

### Standard practice
Most slicing software defaults to **±45° alternating** between layers, which gives the most balanced mechanical properties for general use.

---

## 5. Print Speed

### What it is
How fast the print head moves while depositing material, measured in mm/s. Typical range: 30–120 mm/s.

### Why it matters
Print speed affects **time available for each bead to bond** to the previous layer and **quality of material deposition**.

### Effect of changing it

| Slower (e.g., 30 mm/s) | Faster (e.g., 100 mm/s) |
|------------------------|------------------------|
| Better surface quality | Rougher finish |
| Better layer adhesion | Risk of under-extrusion |
| Better dimensional accuracy | Vibrations can cause artifacts (ringing) |
| Much longer print time | Much faster print time |

### Speed–Temperature interaction
When printing faster, the material spends less time in the melt zone — it may not be fully molten by the time it exits the nozzle. This is why printing at higher speeds often requires slightly **increasing the extrusion temperature** to compensate.

### Practical rule
Start at 50 mm/s for a new material or printer calibration. Optimize surface quality first, then gradually increase speed.

---

## 6. Flow Rate (Extrusion Multiplier)

### What it is
A multiplier (typically 90–110%) that scales how much material the printer extrudes relative to what the slicer calculated. Also called the "extrusion multiplier" in some slicers.

### Why it matters
If the actual filament diameter varies from the nominal value, or if the extruder is not perfectly calibrated, the printer may over- or under-extrude. Flow rate compensates for this.

### Effect of changing it

| Flow Rate Too Low (< 100%) | Flow Rate Correct (100%) | Flow Rate Too High (> 100%) |
|---------------------------|--------------------------|------------------------------|
| Under-extrusion — gaps in surfaces | Solid, well-filled layers | Over-extrusion — blobs and stringing |
| Weak parts | Strong, accurate parts | Dimensional inaccuracy (oversize) |
| Visible holes in walls | Smooth surfaces | Nozzle clogs in extreme cases |

### How to calibrate
Print a single-wall calibration cube, measure the wall thickness with calipers, and adjust the flow rate until the measured thickness matches the expected value.

---

## 7. Extrusion Temperature

### What it is
The temperature of the heater block at the nozzle, in °C. This determines how fluid the molten plastic is when it is deposited.

### Why it matters
Temperature controls the **viscosity of the melt** and therefore how well it flows, bonds to adjacent material, and fills fine features.

### Effect of changing it

| Too Cold | Correct Temperature | Too Hot |
|----------|---------------------|---------|
| Under-extrusion — material won't flow | Good layer adhesion and surface | Stringing and oozing |
| Layer delamination | Accurate dimensions | Material degradation (burning) |
| Nozzle clog | Clean surface finish | Fumes (especially ABS) |
| Rough surface | | Reduced mechanical properties |

### Material-Specific Temperatures

| Material | Optimal Range |
|----------|--------------|
| PLA | 190–220°C |
| ABS | 215–230°C |
| PETG | 230–250°C |
| Nylon | 240–260°C |
| Composites | 200–300°C (matrix-dependent) |

### Temperature–Speed relationship
Higher print speed → less dwell time in the hot end → may need higher temperature to fully melt the material. Always recalibrate temperature when changing print speed significantly.

---

## How Parameters Interact

The seven parameters are not independent — changing one often requires adjusting others:

```
Increase PRINT SPEED
    → Underfusion risk → Increase EXTRUSION TEMPERATURE
    → Possible vibration → Check FLOW RATE and slow down if needed

Decrease LAYER THICKNESS
    → More layers → Consider increasing PRINT SPEED to compensate time
    → Better surface quality → Can reduce EXTRUSION TEMPERATURE slightly

Change MATERIAL
    → Adjust EXTRUSION TEMPERATURE (material-specific)
    → Re-check BUILD ORIENTATION (different materials have different warping)
    → Re-calibrate FLOW RATE (different densities)
```

---

## Quick Reference: Effect on Key Quality Metrics

| Parameter | Surface Quality | Mechanical Strength | Print Time | Dimensional Accuracy |
|-----------|----------------|--------------------|-----------|--------------------|
| ↓ Layer Thickness | ✅ Better | ✅ Better | ❌ Longer | ✅ Better |
| ↑ Print Speed | ❌ Worse | ❌ Worse | ✅ Faster | ❌ Worse |
| ↑ Extrusion Temp | Neutral/Better | ✅ Better (bonding) | Neutral | ❌ Slight worse |
| Negative Air Gap | ✅ Better | ✅ Better | ❌ Slightly longer | ✅ Better |
| ±45° Raster | ✅ Best balance | ✅ Best balance | Neutral | Neutral |
| Correct Flow Rate | ✅ Best | ✅ Best | Neutral | ✅ Best |

---

## References

- Narang, R. & Chhabra, D. (2017). *Analysis of Process Parameters of Fused Deposition Modeling (FDM) Technique*.
- Mwema, F. & Akinlabi, E. (2020). *Basics of Fused Deposition Modelling (FDM)*. DOI: 10.1007/978-3-030-48259-6_1
