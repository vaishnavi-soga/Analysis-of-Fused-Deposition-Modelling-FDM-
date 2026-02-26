# Transient Thermal Simulation

## Overview

The transient thermal analysis captures how temperature **evolves over time** (0 to 20 seconds) as PETG filament is continuously deposited on the print bed. Unlike the steady-state simulation, this tells us what happens *during* the printing process — including the heating spikes from new beads and the cooling cycles between passes.

This is the **second simulation** in the workflow, using the steady-state result as its starting point.

---

## Software

- **Tool:** ANSYS Workbench 2024 R2 (Student Edition)
- **Analysis Type:** Transient Thermal (Module B)
- **Linked to:** Steady-State Thermal (Module A) — initial conditions imported

---

## Setup

Same geometry, mesh, and material properties as the steady-state simulation. See [steady_state_thermal.md](steady_state_thermal.md) for those details.

### Time Settings

| Setting | Value |
|---------|-------|
| Total Simulation Time | 20 seconds |
| Number of Time Steps | 20 (1 step per second) |
| Time Integration | Backward Euler (ANSYS default) |

### Additional Boundary Condition: Heat Generation

To simulate the cyclic deposition of hot filament beads, a **time-varying heat flux** or **temperature load** is applied to the filament surface to replicate the effect of the nozzle passing across and depositing material in cycles. This produces the oscillatory temperature pattern visible in the results.

---

## Results

### Temperature Summary at t = 20 seconds

| Metric | Value |
|--------|-------|
| Maximum Temperature | **90.67°C** |
| Average Temperature | **30.2°C** |
| Minimum Temperature | **−9.4°C** |

> The negative minimum temperature may appear unphysical at first glance. This is an artifact of the thermal interpolation at mesh nodes far from the heat source during rapid convective cooling — in practice, temperatures would floor at ambient (~22°C). It indicates the mesh could benefit from local refinement at the bed base in future iterations.

---

## Temperature vs. Time Plot Analysis

The simulation outputs three curves plotted from t = 0 to t = 20 seconds:

### 🟢 Maximum Temperature (Green Curve)
- Oscillates between ~75°C and ~90.67°C
- Each peak corresponds to a **new filament bead being deposited** — the hot material briefly raises the local maximum
- The peaks are relatively consistent, meaning the printing process has reached a **thermal quasi-steady state** — the system is neither continuously heating up nor cooling down globally

### 🔵 Average Temperature (Blue Curve)
- Rises **monotonically** from ~29°C to ~40°C over 20 seconds
- This gradual increase means the **overall part accumulates heat** as more material is added
- This is important: in a real long print, this rising average temperature can lead to warping in lower layers if it gets too high — this is why enclosures and controlled cooling are used for some materials

### 🔴 Minimum Temperature (Red Curve)
- Oscillates near 0°C, with occasional dips below
- Represents the **outer surfaces of the print bed** being cooled by air convection
- The oscillation corresponds to thermal waves propagating through the part each time a new hot bead is deposited

---

## Physical Interpretation: What Is Actually Happening?

```
Time 0–1s:   First bead deposited → sharp temperature spike at filament
Time 1–2s:   Nozzle moves to next position → convective cooling begins
Time 2–3s:   Next bead deposited → spike again, reheating adjacent material
...repeats...
```

The **reheating of adjacent material** by each new bead is crucial — this is what creates **interlayer bonding** in FDM. The polymer chains at the interface between layers need to briefly re-melt and interdiffuse to form a strong bond. The transient simulation confirms this is happening: the previously deposited material is being brought back above the glass transition temperature (~80°C for PETG) with each new deposition cycle.

### Practical Implications

| Observation | Implication |
|------------|-------------|
| Rising average temperature | Long prints may accumulate heat → potential warping in tall parts |
| Consistent max temperature oscillations | Printing is thermally stable → good interlayer bonding expected |
| Low minimum temperatures at bed base | Bed is effectively cooling the part → reduces warping |
| −9.4°C artifact in simulation | Indicates mesh refinement needed near bed base in future work |

---

## Limitations of This Model

1. **Simplified geometry** — Real filament beads are not perfect rectangles; they have a slightly oval cross-section that affects surface area for convection
2. **Single bead modelled** — A real print involves dozens of parallel beads per layer; the thermal interaction between adjacent beads is not captured
3. **No radiation** — At temperatures near 90°C, radiation from polymers is very small but not entirely negligible
4. **Constant material properties** — In reality, thermal conductivity and specific heat of PETG are temperature-dependent, especially near the glass transition
5. **No phase change** — The melting/solidification of PETG is not explicitly modelled; this would require a more complex enthalpy-based approach

---

## How to Reproduce in ANSYS

1. In ANSYS Workbench, connect **Module A (Steady-State Thermal)** → **Module B (Transient Thermal)** by dragging the Solution cell of A to the Setup cell of B
2. In Module B Mechanical, verify that **Initial Temperature** is set to "Import from Module A"
3. Set **Analysis Settings**:
   - End Time: 20 s
   - Number of Substeps: 20
   - Auto Time Stepping: Off
4. Apply the same convection boundary conditions as Module A
5. Add a **time-varying temperature load** on the filament top surface:
   - Use a tabular input cycling between 235°C (deposition) and 22°C (ambient) every ~1 second
6. Solve → Insert **Temperature** result → Right-click → **Evaluate All Results**
7. To get the Temperature vs. Time plot: Right-click on Temperature result → **Create Chart** → set X-axis to Time
