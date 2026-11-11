# Slicing results — PFBK v0.1

**Slicer:** Bambu Studio 02.06.00.51 command line (a PrusaSlicer-lineage slicer). PrusaSlicer itself is not installed on the build machine.
**Printer:** Bambu Lab X1 Carbon, 0.4 mm nozzle, the printer configured in the designer's Bambu Studio.
**Filament profile:** Bambu PETG Basic @BBL X1C (profile density 1.25 g/cm³, nozzle 255 °C, plate 70 °C).
**Plate:** Textured PEI. **ASSUMPTION:** the Cool Plate default is rejected for PETG; change it if you use a different plate.

## Settings (base: "0.20mm Standard @BBL X1C")
| Setting | Value | Why |
|---|---|---|
| Layer height | 0.20 mm | profile default |
| Walls | **5** (0.42 / 0.45 mm lines ≈ 2.1 mm) | thicker than the 1.87 mm min structural wall, so bore regions print solid, matching the solid-material stress assumption (design choice) |
| Sparse infill | **40 % gyroid** | design choice for a hand tool; not from a cited source |
| Supports | **off** | max overhang in the model is 45.0° with 0 bridges (see `docs/checks.md`) |
| Orientation | parting face / flat face on the bed (STLs are exported this way) | flat base, 45° bore roofs face up |

## Results (slicer estimates, one copy each)
| Part | Qty | Print time | Filament | Supports needed? |
|---|---|---|---|---|
| Body top | 1 | 46 min 25 s (2785 s) | 23.68 g | **No.** Re-sliced with tree supports enabled: 0 support features, +0.000 g |
| Body bottom | 1 | 47 min 44 s (2864 s) | 23.71 g | **No.** Supports enabled: 0 support features, +0.002 g (noise) |
| Tire lever | **2** | 24 min 35 s each (1475 s) | 11.96 g each | **No.** Supports enabled: 0 support features |
| **Kit total** | 4 parts | **≈ 2 h 23 min** (8599 s) sliced one at a time | **≈ 71.3 g** | none |

Grams use the profile density of 1.25 g/cm³. At the 1.27 g/cm³ Prusament datasheet value the kit total is about 72.4 g.
Printing all four parts on one plate will save per-plate heat-up and calibration time; that was not sliced.

Files per part: `x1c_petg.gcode.3mf` (sliced project with G-code), `slice_result.json` (slicer report),
`supports_check.json` (same part re-sliced with supports enabled, to show none are generated).
`profiles/` holds the flattened printer, process and filament presets used.
