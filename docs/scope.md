# Scope — Pocket Flat & Bolt Kit (PFBK) — v0.1

> **v0.1. Not meant to replace professional bike shop tools.**

## Use case
A roadside kit for two problems: a **flat tire** and a **loose bolt**. It has to fit in a jersey pocket, so the whole kit
packs into one closed body. The levers clip on and also lock the keys.

## Functions

| # | Function | Addresses | Target torque (source: research §1) |
|---|---|---|---|
| F1 | 4 mm hex L-key (steel, swing-out) | stem faceplate / steerer, derailleur cable pinch, caliper mounts — **size varies by component, check yours** | 2 – 16.3 N·m covered |
| F2 | 5 mm hex L-key (steel, swing-out) | same family of clamp bolts | same |
| F3 | 6 mm hex L-key (steel, swing-out) | same family of clamp bolts | same |
| F4 | T25 Torx L-key (steel, swing-out) | disc rotor bolts, brake bolts, shifters (Park MT-10 note) | rotor bolts 2 – 6.2 N·m |
| F5 | 5 N·m torque indicator (printed flexure + gap stop) | carbon-friendly clamp bolts; Park lists 5 N·m (Syncros, Time) and 5.4 N·m (Thomson) | go / no-go at **5 N·m (design choice)** |
| F6 | 2 × tire lever (printed, nest on the body faces) | bead removal and refit | no load data found; not simulated |
| F7 | Spoke nipple wrench, 3 slots per lever | nipples 3.23 / 3.30 / 3.45 mm flats (Park SW-0/1/2) | no torque data found; not simulated |

**Why these four keys:** 4 mm, 5 mm and T25 appear in all four surveyed pocket tools; 6 mm in three of four (research §2).
2.5/3/8 mm were left out to keep one compact body.

**Design torque, T_design = 20 N·m.** This is Wolf Tooth's published maximum for 4/5/6 mm and T25 bits on a pocket tool. It sits above
the highest in-scope spec in Park's table, 16.3 N·m (Control Tech stem faceplate), so every in-scope bolt is covered.
This is also the load used in the stress study.

**Deliberately out of scope:** seat-rail binders above 20 N·m (Shimano 20–30, Control Tech 33.9), rotor lockrings (40 N·m),
and crank or bottom-bracket work. These need a full-size tool. The 5 N·m indicator is **not** for Shimano rotor
bolts (2–4 N·m). Stop by feel there.

## Key architecture decision (hand calculation, verified later by simulation)
A printed PETG hex socket driving a 1/4 in steel bit at 20 N·m gives roughly 130–200 MPa peak flat pressure
(ESTIMATE: half-flat contact model, 15 mm engagement), against a 47 MPa yield. **That fails.**
Instead, standard **steel L-keys** run inside the printed body. Torque reaches the short arm through steel, and the plastic
only sees bearing along the embedded long arm. A peg-in-socket estimate gives p_max = 6M/(d·Le²). The embedded length
is sized so that p_max = yield/2 = 23.5 MPa at 20 N·m.

## User parameters (all created in Fusion; names match exactly)

### Sourced inputs
| Name | Value | Source |
|---|---|---|
| T_design | 20 (N·m) | Wolf Tooth 6-Bit max torque |
| yield_petg | 47 (MPa) | Prusament PETG TDS, printed horizontal |
| E_petg | 1500 (MPa) | Prusament PETG TDS, printed horizontal |
| sf_target | 2 | user requirement |
| key4_af / key5_af / key6_af | 4 / 5 / 6 mm | key size by definition |
| t25_d | 4.5 mm | Wiha 01317 listing |
| key4_arm / key5_arm / key6_arm | 17.46 / 20.64 / 23.81 mm | Guillevin catalogue |
| t25_arm | 25 mm | Wiha 01317, King Tony 114325 |
| spoke_f0 / f1 / f2 | 3.23 / 3.30 / 3.45 mm | Park SW-0/1/2 |
| m5_head_d / m5_head_k | 8.5 / 5 mm | ISO 4762 M5 (supplier tables) |
| m5_nut_af | 8 mm | DIN 934 / ISO 4032 M5 (supplier) |
| lever_w | 25 mm | Silca Premio, Schwalbe |
| lever_t | 6 mm | Park TL-6.3; also must be ≥ m5_head_k so the levers sit flush over the screw heads |
| ind_torque | 5 (N·m) | design choice, informed by Park values of 5 / 5.4 N·m |

### ESTIMATES (design choices, labelled)
| Name | Value | Why |
|---|---|---|
| pivot_clear | 0.4 mm | Diametral clearance for keys rotating in bores and slots. Middle of the cited 0.2–0.5 mm FDM range: keys only rotate to deploy (no running fit), but horizontal bores sag slightly at the bridged roof |
| half_t | 6.5 mm (now DERIVED) | Changed during checking from a 6 mm estimate to the expression `ceil((max bore/2 · √2 + min_wall)·2)/2`, so the 45° diamond-bore apex keeps `min_wall` = 1.2 mm (cited) |
| end_wall | 2.5 mm | Outboard wall that traps each key's bend axially |
| side_wall | 2.5 mm | Wall outside the key bores |
| slot_web | 3 mm | Web between the two key slots at each end |
| bore_gap | 3 mm | Web between the blind ends of two keys sharing a line |
| fold_clear | 1.5 mm | Gap between a folded short arm tip and the neighbouring bore |
| m5_clear_d | 5.5 mm | M5 clearance hole |
| ind_root_w | 10 mm | Width of the indicator beam root |
| ind_push_inset | 4 mm | Push mark distance from the beam tip |
| grip_fillet | 2 mm | Fillet on gripped (top) edges |
| lever_tip_t / lever_tip_L | 1.5 / 15 mm | Thin bead tip (≥ min wall), taper length |
| spoke_slot_d | 5 mm | Spoke-wrench slot depth |
| hook_w / hook_d | 2.6 / 6 mm | Spoke hook notch |
| lever_fit | 0.1 mm | Slip fit of lever holes over screw head and nut |
| screw_dx | 25 mm | Screw offset from centre |
| fdm_xy_comp | 0 mm | Hook for printer XY compensation on the spoke slots. **Tune by test print** |
| nu_petg | 0.38 | Poisson's ratio. Not found in any source; typical-polymer ESTIMATE, simulation only |

### Derived (Fusion expressions)
Bore Ø = across-corners + pivot_clear. Embedded lengths le4/le5/le6/le_t25 come from the peg formula. Key line offset key_y
comes from the fold-clearance condition at each end. Body length is set by the longest key line. Indicator beam
thickness comes from the cantilever bending limit at yield/2. The indicator gap starts from the hand-calc deflection and is then
**replaced by the simulated deflection**. See `cad/parameters.csv` for the exported final values.
