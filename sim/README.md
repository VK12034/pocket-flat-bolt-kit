# Static stress study — STATUS: NOT RUN (blocked), hand calculation only

**Decision (2026-11-11):** v0.1 ships with the hand calculation as its only strength evidence. The FEA study is deferred to v0.2.

**The Fusion static stress study has not been run.** No safety factor in this repository comes from FEA.

## What was attempted (2026-11-11)
The study was to be built through Fusion's `adsk.sim` API: LinearStaticStress study, PETG material, fixed constraint and force load, mesh, solve.
`adsk.sim.Simulations.get(document)` returned `None`, with no error code, in every configuration tried:
1. Main design, Design workspace active.
2. Main design after activating the Simulation workspace (UI then reported `InternalValidationError : pCurrentSession`).
3. Read-only and transactional script contexts.
4. A fresh unsaved design containing only copies of the two body halves (the intended FEA model).
5. The same, after activating the Simulation workspace.
6. After executing Fusion's `CreateSimulationModelCommand`.
7. Starting `SimCreateSimCaseCommand` (New Simulation Study) by text command. This opened a modal dialog, which stopped all API calls.
8. **After the designer created "Study 1 - Static Stress" in the UI**, the document holds a `SimCaseProductType` product, but the
   Simulations product itself throws `InternalValidationError : res` on access and `Simulations.get` still returns `None`.
   This is a defect in the preview `adsk.sim` API in Fusion 2706.1.17, not a missing study. Setting the study up interactively was deferred to v0.2.

**Study 1 exists** in the simulation-only document, with the PETG material already assigned. Constraint, load, mesh and solve have not been applied.
That document's bodies were copied before the cosmetic top-face label engraving was removed from the top half; the difference is 0.4 mm deep
text far from the 5 mm bore, which does not change the load path.

The cause is a defect in this build's preview simulation API (item 8): the study exists but cannot be reached from scripts.

## Planned load case (ready to run once a study exists)
* **Model:** `Body_Top` + `Body_Bottom` only (bonded at the parting plane, which stands in for the two M5 screws). Keys, levers and fasteners are excluded.
* **Material:** PETG (Prusament, printed) — E 1.5 GPa, yield 47 MPa, ν 0.38 (ESTIMATE), ρ 1.27 g/cm³. Safety factor based on yield.
* **Constraint:** fixed on all faces of the **5 mm key bore**, the bore with the highest hand-calc bearing pressure. The steel key is ≈130× stiffer
  than PETG and is held by the bolt.
* **Load:** **20 N·m** (T_design) applied as a force on the far end faces (end A) in −Y.
  F = 20 000 N·mm / R, where R = distance from the 5 mm key axis to end A ≈ 93.5 mm, so **F ≈ 214 N**. The bending moment at the key is
  20 N·m wherever along the grip the hand pushes, so the bore bearing check does not depend on this choice.
* **Second case:** indicator beam, 51.6 N at the push dot (5 N·m at R = 96.8 mm). This checks the beam stress and the tip deflection against `ind_gap` = 3.4 mm.
* **Pass criterion:** minimum safety factor ≥ 2. If it comes out lower: raise `sf_target` (which lengthens the embedded key lengths) or raise
  `side_wall` / `half_t`, then rerun.

## Current evidence instead
`hand_calculation.md` (ESTIMATE): lowest bearing safety factor **2.01** (5 mm key), indicator beam **2.05**. Those numbers are at the
target by construction and ignore stress concentrations, so **a real study could come out below 2**. Treat the design as unverified until it runs.
