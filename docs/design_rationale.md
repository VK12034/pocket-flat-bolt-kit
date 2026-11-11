# Design rationale — Pocket Flat & Bolt Kit (PFBK) · **v0.1**

> **v0.1. Not meant to replace professional bike shop tools.** The static stress
> study has **not** been run (see §4). Every number is cited in `research/sources.md`, measured in the Fusion model, or labelled ESTIMATE.

**Use case.** Roadside flat tire or loose bolt, carried in a jersey pocket. One closed body: four steel keys swing out of a printed
clamshell, two tire levers clip onto its faces and lock the keys, and the levers carry the spoke wrench.

**Functions.** 4 / 5 / 6 mm hex and T25 Torx L-keys (4, 5 and T25 appear in all four surveyed pocket tools, 6 mm in three of four) ·
5 N·m go/no-go torque indicator · 2 tire levers · spoke-nipple wrench for 3.23 / 3.30 / 3.45 mm flats (Park SW-0/1/2).
Covered torque range **2–16.3 N·m** (Park Tool chart). **Design torque 20 N·m** = Wolf Tooth's published max for 4/5/6/T25 bits.
Out of scope: seat-rail binders above 20 N·m (Shimano 20–30, Control Tech 33.9 N·m), rotor lockrings (40 N·m), cranks.

**The decision that shaped everything: torque never goes through printed hex flats.** A PETG socket driving a 1/4 in bit at
20 N·m sees ≈130–200 MPa against a 47 MPa yield (hand calc, SF ≈ 0.3). Instead, standard steel L-keys sit in bores in the body. The steel
carries the torque, and the PETG only sees bearing along the embedded long arm: p_max = 6M/(d·Le²). Each embedded length `le*` is
a Fusion expression solved for p_max = yield/2 at 20 N·m. That one requirement sets the key lengths, then the body length (107 mm), and
through the fold-clearance rule the body width (49.6 mm). Change `T_design`, `sf_target` or a key size and the model resizes.

**Sizing sources (abridged).** Torques: Park Tool torque table (manufacturer values; Shimano's own PDF returned HTTP 403, so
Shimano values are as reported by Park). Keys: Guillevin catalogue (short arms 17.46 / 20.64 / 23.81 mm), Wiha/King Tony T25 (Ø4.5, 25 mm).
Material: Prusament PETG TDS v1.1 (yield 47 MPa, E 1.5 GPa, 1.27 g/cm³). Fasteners: ISO 4762 M5 (head Ø8.5 × 5), M5 nut 8 A/F.
Levers: Silca / Schwalbe 25 mm width, Park TL-6.3 6 mm thickness. FDM rules: 45° overhang, 0.8–1.2 mm minimum wall, 0.2–0.5 mm moving clearance.
**Pivot clearance 0.4 mm diametral**: the middle of the cited 0.2–0.5 mm range. The keys only rotate to deploy (no running fit), and the
bores are horizontal holes. The parameter is `pivot_clear`.

**Printability (measured in Fusion).** Each half prints parting-face-down. The bores are diamonds with 45° roofs, so the steepest overhang is
**45.0° with 0 bridges**. Structural minimum wall **1.87 mm** (≥ 1.2 mm). Packed interference **0**. The fold sweep of every key from −90° to +90°
gives **0** interference. With the levers fitted, the keys are blocked before 15° of swing. Grip edges are filleted with `grip_fillet` = 2 mm.

## 4. Simulation result — **not available**
The Fusion static stress study could not be created through the API (`adsk.sim.Simulations.get` returned nothing in 7 attempts; see
`sim/README.md`). **No FEA safety factor exists for v0.1.** The load case is fully specified and ready to run: fixed 5 mm key bore, 20 N·m as
≈214 N on the far end, PETG material. Hand-calculation ESTIMATES: lowest bore bearing SF **2.01** (5 mm key), indicator beam SF **2.05**.
These sit at the target by construction and ignore stress concentrations, so a real study may come in below 2.

**Print settings (Bambu Studio CLI, X1 Carbon 0.4, PETG Basic).** 0.20 mm layers, 5 walls, 40 % gyroid, no supports, textured PEI (assumed).
Body top 46 min 25 s / 23.68 g · body bottom 47 min 44 s / 23.71 g · lever 24 min 35 s / 11.96 g (×2) · **kit ≈ 2 h 23 min, 71.3 g PETG**.
Re-slicing every part with tree supports enabled generated **no** supports.

**Known limits.** (1) No FEA yet. (2) The steel keys' own torque capacity is not verified (ISO 2936 proof torques are paywalled).
(3) PETG Poisson's ratio 0.38 is an ESTIMATE. FDM parts are anisotropic and creep, and the indicator calibration (`ind_gap` 3.4 mm) is a hand
calculation that will drift with print settings, so check it against a real torque wrench. (4) A 5 N·m indicator over-torques Shimano rotor bolts (2–4 N·m).
(5) Spoke-slot widths differ by 0.07 mm, which is below typical FDM accuracy, so tune `fdm_xy_comp` with a test print. (6) Tire-lever bead loads and spoke-nipple
torques were not found, so those features are not analysed. (7) Envelope 107 × 50 × 25 mm, larger than commercial multi-tools, because PETG needs
long embedded key lengths. (8) Key long arms must be **cut** to 40.5 / 37.6 / 36.7 / 38.7 mm (4 / 5 / 6 mm / T25).

## Changelog
* **v0.1 (2026-11-11).** First complete model. During checking: bores changed from flat-roof octagons to 45° diamonds (removed
  bridges, `half_t` 6.0 → 6.5 mm as a derived expression); the "5Nm" engraving that made a 0.107 mm sliver became Ø2 mm push dots; a nut recess
  was added so a standard M5×16 ends flush; the lever tip taper, lost to a rolled-back script, was restored; the version label engraved on the top face was
  removed from the part at the designer's request. Static stress study blocked (see `sim/README.md`); the designer chose to ship v0.1 on the hand-calculation estimate and defer FEA to v0.2.
