# Model checks — PFBK v0.1

All values below come from the Fusion model (API measurements), not from estimates. Run on 2026-11-11.

| Check | Method | Result | Limit / target | Pass |
|---|---|---|---|---|
| Interference, packed kit (12 bodies) | `Design.analyzeInterference`, coincident faces excluded | **0** pairs | 0 | ✅ |
| Fold / unfold, 4 keys | Each key rotated about its long-arm axis −90°…+90° in 15° steps, interference vs both body halves at every step (52 states) | **0** interference at all 52 | 0 | ✅ |
| Keys locked when levers fitted | Key rotated ±15° / ±30° with levers on, interference vs levers | 26.6 mm³ at ±15°, 186–242 mm³ at ±30° → blocked before 15° | keys must not swing out | ✅ |
| Deployed reach beyond body face | Key bounding box at ±90° minus half_t | 6 mm 14.3 · 4 mm 9.0 · T25 16.3 · 5 mm 11.7 mm | > 0 | ✅ |
| Structural min wall — Body_Top / Body_Bottom | Ray cast inward from sampled points on every face (≈1000 rays/part), engraved-letter ridges excluded | **1.87 mm** | ≥ 1.2 mm (`min_wall`, cited FDM range 0.8–1.2) | ✅ |
| Min wall — Tire_Lever | `lever_tip_t` by construction; sampled 2.35 mm elsewhere | **1.5 mm** at bead tip | ≥ 1.2 mm | ✅ |
| Steepest overhang (print orientation) | Sampled face normals vs build direction | **45.0°**, 0 faces > 45°, **0 bridges** | ≤ 45° | ✅ |
| Flat print base | Largest planar face on the bed | 3564 mm² (each half) · 2493 mm² (lever) | flat face present | ✅ |
| STL ↔ CAD volume | Mesh signed volume vs B-rep volume | 25.757 vs 25.760 cm³ (halves) · 14.115 vs 14.114 cm³ (lever) | match | ✅ |
| Engraved-letter ridges (cosmetic) | Same ray cast, letter-to-letter only | 0.13 mm | — | ⚠️ cosmetic: thin letter ridges may fuse; does not affect strength |

## Packed envelope and model mass

* Envelope (levers fitted): **107.0 × 49.7 × 25.0 mm**
* Model mass at 100 % solid density (PETG 1.27 g/cm³, steel library density): body halves 32.7 g each, levers 17.9 g each,
  keys 13.3 / 5.8 / 7.4 / 9.0 g (6 / 4 / T25 / 5 mm), M5×16 screws 4.7 g each, nuts 1.1 g each, **total 148.5 g**.
  Printed mass is lower (see slicing).

## Problems found and fixed during checking

1. **Bore roofs were 2–3 mm flat bridges** (a 90° overhang). Bores were redrawn as elongated diamonds with 45° roofs, keeping the same
   inradius so the keys still rotate. That raised the apex to r·√2, so `half_t` is now an expression,
   `ceil((max bore/2 · √2 + min_wall)·2)/2` = 6.5 mm (was 6.0).
2. **0.107 mm sliver** where the "5Nm" engraving ran into the indicator-beam edge fillet. Replaced it with Ø2 mm engraved push dots on
   the beam centre-line (≥1.4 mm from every edge) and moved the label text to the main face.
3. **Screw length vs. thicker body.** The design keeps a standard M5×16 and adds `nut_recess` = body_t + nut − screw = 1 mm
   hex pockets, so the screw ends flush and the nut cannot spin.
4. **Lever tip taper missing.** A failed script had been rolled back silently. The wall check caught it (6 mm at the tip), and the
   taper was re-applied and re-verified.
5. **Label detached from the engrave cut** after a text edit. The engraving was rebuilt and verified by face count.

Screenshots: `01_packed_iso.png`, `02_keys_deployed_iso.png`, `03_keys_deployed_end.png`, `04_levers_off_top.png`.
