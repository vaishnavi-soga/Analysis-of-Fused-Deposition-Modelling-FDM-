# FDM Material Comparison Guide

## Overview

The choice of filament material is arguably the most important decision in FDM printing. It determines the mechanical properties of the final part, what temperatures the printer must reach, whether you need a heated bed or enclosure, and what applications the part is suitable for.

This document provides a detailed comparison of the five material classes studied in this project.

---

## Quick Comparison Table

| Material | Strength | Flexibility | Heat Resistance | Ease of Printing | Cost | Biodegradable |
|----------|----------|-------------|-----------------|------------------|------|---------------|
| **PLA** | Medium | Low (brittle) | Low | ⭐⭐⭐⭐⭐ | $ | ✅ Yes |
| **ABS** | High | Medium | High | ⭐⭐⭐ | $ | ❌ No |
| **PETG** | Medium-High | Medium | Medium | ⭐⭐⭐⭐ | $$ | ❌ No |
| **Nylon** | Very High | High | High | ⭐⭐ | $$ | ❌ No |
| **Composites** | Extreme | Low | Very High | ⭐ | $$$$ | ❌ No |

---

## 1. PLA — Polylactic Acid

### What it is
PLA is a **biodegradable thermoplastic** derived from renewable resources like corn starch or sugarcane. It is the most widely used FDM material for beginners and prototyping.

### Properties
- Rigid and strong in compression
- **Brittle** — snaps rather than bending; poor impact resistance
- Low heat resistance (starts softening around 60°C)
- Not chemically resistant
- Available in the widest color range of any filament

### Printing Requirements
| Parameter | Value |
|-----------|-------|
| Extruder Temperature | 180–220°C |
| Bed Temperature | 20–60°C (or no heated bed) |
| Enclosure Required | No |
| Drying Required | Minimal |

### Strengths
- Easiest material to print — very forgiving of temperature and speed variations
- Minimal warping — good bed adhesion without a heated bed
- Produces sharp details and good surface finish
- Biodegradable — more environmentally friendly than petroleum-based plastics

### Weaknesses
- Poor impact resistance — not suitable for parts that will be dropped or stressed dynamically
- Low heat resistance — will deform in a hot car, near an oven, or in direct sunlight
- Not suitable for outdoor use long-term (UV degradation)
- Cannot be easily post-processed with acetone (unlike ABS)

### Best Applications
- Concept models and visual prototypes
- Architectural models
- Educational tools and hobby prints
- Parts that will not experience mechanical stress or heat

---

## 2. ABS — Acrylonitrile Butadiene Styrene

### What it is
ABS is a **petroleum-based thermoplastic** that has been widely used in injection molding for decades (LEGO bricks are made from ABS). It was one of the first materials available for FDM printing.

### Properties
- Tough and impact-resistant
- Significantly better heat resistance than PLA (softens ~105°C)
- Can be smoothed with acetone vapor for excellent surface finish
- More flexible than PLA — bends before breaking

### Printing Requirements
| Parameter | Value |
|-----------|-------|
| Extruder Temperature | 215–230°C |
| Bed Temperature | 80–110°C |
| Enclosure Required | Strongly recommended |
| Drying Required | Minimal |

### Strengths
- Strong functional parts that can withstand mechanical loads
- Heat resistant — suitable for engine bays, outdoor use, hot environments
- Acetone smoothing produces near-injection-molded surface quality
- Well-understood material with decades of use in manufacturing

### Weaknesses
- **Warping** — ABS shrinks significantly on cooling; without a heated enclosure, parts curl and delaminate
- Emits **fumes during printing** (styrene) — requires good ventilation
- More sensitive to print settings — requires higher temperatures and careful calibration
- Not biodegradable

### Best Applications
- Functional prototypes that will be mechanically tested
- Automotive parts and housings
- Electronic enclosures
- Parts that will be finished with acetone smoothing

---

## 3. PETG — Polyethylene Terephthalate Glycol ⭐

### What it is
PETG is a modified version of PET (the material used in plastic water bottles). The "G" stands for glycol modification, which improves clarity, reduces brittleness, and lowers the glass transition temperature slightly compared to standard PET.

### Properties
- Good balance of strength and flexibility
- Excellent chemical resistance (resists many solvents, oils, and acids)
- High transparency — can print clear parts
- Minimal warping during cooling
- FDA-approved grades available for food contact
- Absorbs moisture (hygroscopic)

### Printing Requirements
| Parameter | Value |
|-----------|-------|
| Extruder Temperature | 220–250°C |
| Bed Temperature | 70–85°C |
| Enclosure Required | No (but recommended for tall parts) |
| Drying Required | Yes — dry at 65°C for 4–6 hours before printing |

### Strengths
- **Best warping resistance** of any commonly used FDM material — much better than ABS
- **Strong interlayer bonding** — layers fuse well together → good mechanical properties in Z-direction
- No toxic fumes at standard printing temperatures
- Excellent chemical resistance — suitable for chemical containers and lab equipment
- FDA-approved variants available

### Weaknesses
- **Hygroscopic** — must be stored in airtight containers and dried before printing
- **Stringing** — tends to leave thin strings between travel moves; requires careful retraction calibration
- Softer surface — more prone to scratching than ABS
- Higher nozzle temperature than PLA — requires a printer capable of 250°C+

### Best Applications
- Waterproof containers and enclosures
- Snap-fit components (good flex/snap ratio)
- Medical device components
- Food-safe applications (FDA-approved grades)
- Parts requiring transparency
- Outdoor applications (good UV resistance compared to PLA)

---

## 4. Nylon (Polyamide)

### What it is
Nylon is a family of synthetic polyamides widely used in engineering applications. In FDM, Nylon 12 and Nylon 6 are most common.

### Properties
- Extremely strong and tough
- **Partially flexible** — absorbs impact energy through deformation
- High heat resistance
- Very low friction coefficient — ideal for moving parts
- Highly hygroscopic — must be extremely well dried

### Printing Requirements
| Parameter | Value |
|-----------|-------|
| Extruder Temperature | 240–260°C |
| Bed Temperature | 70–90°C |
| Enclosure Required | Yes |
| Drying Required | Critical — 8–12 hours at 70°C before printing |

### Strengths
- Outstanding wear resistance — gears, bearings, and sliding parts last much longer
- Excellent fatigue resistance — handles repeated cyclic loading
- High impact strength — tough in real-world use
- Good chemical resistance

### Weaknesses
- Very difficult to print without an enclosure — warps significantly
- Absorbs moisture extremely quickly — even mid-print, ambient humidity can ruin a print
- Requires precise calibration
- More expensive than PLA/ABS/PETG

### Best Applications
- Functional mechanical parts: gears, hinges, bushings
- Wear-resistant components
- Living hinges and flexible clips
- Industrial tooling and fixtures

---

## 5. Composites (Carbon Fiber, Kevlar, Fiberglass)

### What it is
Composite filaments embed short chopped fibers (carbon fiber, Kevlar aramid, or fiberglass) into a thermoplastic matrix (usually Nylon or PLA). Continuous fiber composites (like Markforged) embed uncut continuous fiber strands for even higher performance.

### Properties
- **Extremely high stiffness-to-weight ratio** (especially carbon fiber)
- Very high strength in the fiber direction
- Reduced elongation at break compared to unfilled matrix
- Carbon fiber is also electrically conductive and thermally conductive

### Printing Requirements
| Parameter | Value |
|-----------|-------|
| Extruder Temperature | 200–300°C (depends on matrix) |
| Special Nozzle Required | Yes — hardened steel (carbon fiber rapidly abrades brass nozzles) |
| Compatible Printers | Industrial FDM systems (Markforged, Stratasys, etc.) |
| Cost | $$$$ |

### Strengths
- Highest specific stiffness available in FDM
- Lightweight structural parts that rival aluminum in some applications
- Used in aerospace, motorsports, and high-performance applications

### Weaknesses
- Very expensive — both the printer and the filament
- Requires specialized (hardened) nozzles — standard brass nozzles wear out in hours
- Short-fiber composites are anisotropic — strong in one direction, weaker in others
- Limited to industrial machines for best results

### Best Applications
- Aerospace components and brackets
- Racing car structural parts (Formula 1 hydraulic pipe supports, NACA ducts)
- High-performance tooling, jigs, and fixtures
- Drone frames and unmanned vehicle structures

---

## Material Selection Guide

```
What does your part need?
│
├── Looks good, low stress → PLA
│
├── Withstands heat / impact → ABS
│
├── Chemical resistance / waterproof / food safe → PETG ⭐
│
├── Moving parts / wear resistance / high fatigue → Nylon
│
└── Maximum stiffness + lightweight → Composite (Carbon Fiber)
```

---

## References

- Material property data from manufacturer datasheets and:
- Cano-Vicent, A. et al. *Fused deposition modelling: Current status, methodology, applications and future prospects*. DOI: 10.1016/j.addma.2021.102378
- Yan, C. et al. *PETG: Applications in Modern Medicine*. ISSN 2666-1381
