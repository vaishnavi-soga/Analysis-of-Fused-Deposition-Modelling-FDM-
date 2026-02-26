# Steady-State Thermal Simulation

## Overview

The steady-state thermal analysis determines the **equilibrium temperature distribution** across the print bed and deposited PETG filament — i.e., what the temperatures look like once the system has fully settled and is no longer changing with time.

This is the **first simulation** in the workflow. Its result is also used as the **initial condition** for the transient (time-dependent) simulation.

---

## Software

- **Tool:** COMSOL Multiphysics
- **Analysis Type:** Stationary (Heat Transfer in Solids)

---

## Geometry

| Component | Dimensions |
|-----------|-----------|
| Print Bed | 50 mm × 50 mm × 30 mm |
| PETG Filament (bead) | 15 mm × 10 mm × 2 mm |

The filament is modelled as a **rectangular solid** sitting on top of the print bed. This is a simplification — real filament beads have a slightly rounded cross-section — but it is a standard and accepted approximation for thermal analysis.

---

## Material Properties (PETG)

Both the print bed substrate and the deposited filament are assigned PETG properties:

| Property | Value | Units |
|----------|-------|-------|
| Density | 1270 | kg/m³ |
| Thermal Conductivity | 0.17 | W/m·K |
| Specific Heat Capacity | 1200 | J/kg·K |

> **Note:** PETG has relatively low thermal conductivity (0.17 W/m·K), meaning heat moves slowly through the material. This is why temperature gradients build up across the part during printing.

---

## Boundary Conditions

| Boundary | Condition | Value |
|----------|-----------|-------|
| Filament top/side surfaces | Natural convection to air | h ≈ standard air convection |
| Filament bottom (contact with bed) | Conduction | Continuity across interface |
| Print bed bottom face | Fixed temperature | 22°C (ambient/room temp) |
| Print bed sides | Natural convection | h ≈ standard air convection |

**Heat transfer modes modelled:**
- ✅ Conduction (through solid material)
- ✅ Natural convection (to surrounding air)
- ❌ Radiation (excluded — negligible below 300°C for polymers)

---

## Mesh

| Setting | Value |
|---------|-------|
| Mesh Resolution | 3 |
| Minimum Edge Length | 2.5 × 10⁻³ m |
| Element Type | Hexahedral (auto) |

---

## How to Set This Up in COMSOL

1. Open **COMSOL Multiphysics** → New Model → select **3D** space dimension
2. Under **Physics**, add **Heat Transfer in Solids (ht)**
3. Under **Study**, select **Stationary** (steady-state)
4. In **Geometry**:
   - Add a **Block**: 50mm × 50mm × 30mm (print bed)
   - Add a second **Block**: 15mm × 10mm × 2mm (filament bead)
   - Position filament centered on the top face of the bed using **Move** operation
5. In **Materials**, create a custom PETG material and enter the properties above for both domains
6. In **Heat Transfer in Solids**:
   - Apply **Temperature** boundary condition (22°C) to the bottom face of the bed
   - Apply **Heat Flux** (convective) to all exposed surfaces: use h = 10 W/m²·K, T_ext = 22°C
   - Apply **Temperature** (235°C) to the filament top surface to represent hot extrudate
7. In **Mesh**, set to **Fine** or manually set maximum element size to 2.5e-3 m
8. Click **Compute** → add **Temperature** plot under Results

---

## Results

| Location | Temperature |
|----------|-------------|
| Maximum | **80°C** |
| Minimum | **22°C** |

### Interpretation

The temperature distribution shows:
- The **filament retains significant heat** (up to 80°C at the top surface) because PETG is a poor thermal conductor
- The **print bed acts as a heat sink** — temperature drops sharply away from the filament toward the bed base
- The gradient from 80°C → 22°C across ~32mm is relatively steep, confirming that most heat loss occurs through the top surface via convection rather than through the bed via conduction

This equilibrium state tells us that if printing were to pause indefinitely, the system would settle at these temperatures — which defines the "baseline" thermal environment for each new layer deposited.

---

## Connection to Transient Analysis

The steady-state result is passed as the **initial temperature condition** into the Time Dependent study. This ensures the transient simulation starts from a physically realistic thermal state rather than assuming everything begins at room temperature.
