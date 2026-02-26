# Contributing & Extending This Project

This repository is primarily an academic project. However, if you are a student, researcher, or engineer who wants to build on this work, here is how to do so effectively.

---

## Suggested Extensions

### 1. Add More Materials to the Simulation
The ANSYS setup in this project uses PETG. You could repeat the simulation for:
- **ABS** — Higher extrusion temperature, more warping; compare stress distributions
- **PLA** — Lower temperature; compare how much faster it cools
- **Nylon** — Much higher temperature; more significant thermal gradients

To do this: change the material properties in ANSYS Engineering Data to match the new material (density, thermal conductivity, specific heat), re-run the simulation, and compare the Temperature vs. Time plots.

### 2. Add Multi-Bead / Multi-Layer Simulation
The current model simulates a single rectangular bead. A more realistic model would:
- Simulate 4–6 parallel beads to capture inter-bead heat transfer
- Add a second layer on top of the first to see how reheating affects bond quality
- This would require a more complex geometry and possibly a parametric APDL script

### 3. Mechanical Simulation (Static Structural)
Using the thermal results as input (via **thermal-structural coupling** in ANSYS), you could:
- Apply a load to the printed part
- See how thermal residual stresses combine with mechanical stresses
- Predict where warping or failure is most likely

### 4. Experimental Validation
If you have access to an FDM printer and a thermal camera:
- Print a PETG calibration part while recording thermal images
- Compare the measured temperature profiles with the simulation results
- Quantify the error and discuss sources of discrepancy

---

## How to Structure New Additions

If you add a new simulation, create a new `.md` file in the `simulation/` folder following this format:

```
# [Simulation Name]

## Overview
[What does this simulation analyze?]

## Setup
[Geometry, material, boundary conditions, mesh]

## Results
[Tables and key numbers]

## Interpretation
[What do the results mean physically?]

## Limitations
[What was simplified or excluded?]
```

---

## Citing This Work

If you use this repository in your own work, please cite it as:

```
Rajamani, A., Sogalad, V., Vasu, R., & Narasimharaju, A. (2024).
Analysis of Fused Deposition Modelling (FDM).
Arizona State University, Modern Manufacturing.
GitHub: [repository URL]
```
