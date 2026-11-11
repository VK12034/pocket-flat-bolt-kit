# Graph Report - pfbkg  (2026-11-11)

## Corpus Check
- Corpus is ~4,931 words - fits in a single context window. You may not need a graph.

## Summary
- 54 nodes · 100 edges · 7 communities (6 shown, 1 thin omitted)
- Extraction: 86% EXTRACTED · 14% INFERRED · 0% AMBIGUOUS · INFERRED: 14 edges (avg confidence: 0.88)

## Community Hubs (Navigation)
- Parts, Materials & Print Results
- Torque Path & Stress Evidence
- Model Checks & Printability
- Sourced Hardware & Parameters
- Key Selection & Unverified Items
- Kit Scope & Tire Levers
- Spoke Wrench

## God Nodes (most connected - your core abstractions)
1. `Fusion User Parameters (sourced, ESTIMATE, derived)` - 14 edges
2. `Research — Sizes, Torques, Standards` - 12 edges
3. `Planned Load Case (fixed 5 mm bore, F≈214 N at end A)` - 8 edges
4. `Prusament PETG Datasheet v1.1` - 7 edges
5. `Hand Calculation — ESTIMATE` - 7 edges
6. `Model Checks — PFBK v0.1` - 6 edges
7. `Structural Min Wall Check (1.87 mm, ray cast)` - 6 edges
8. `Pocket Flat & Bolt Kit (PFBK)` - 6 edges
9. `T_design = 20 N·m` - 6 edges
10. `Steepest Overhang Check (45.0°, 0 bridges)` - 5 edges

## Surprising Connections (you probably didn't know these)
- `Supports Check (re-slice with supports, 0 features)` --semantically_similar_to--> `Steepest Overhang Check (45.0°, 0 bridges)`  [INFERRED] [semantically similar]
  slicing/README.md → docs/checks.md
- `Slice Results (≈2 h 24 min, ≈71.3 g kit)` --references--> `Tire_Lever (body)`  [INFERRED]
  slicing/README.md → docs/checks.md
- `Could Not Verify (Shimano DM-TORQUE-01, ISO 2936, PETG Poisson, lever loads)` --references--> `Printed Hex Socket Rejection (SF ≈ 0.25-0.35)`  [INFERRED]
  research/sources.md → sim/hand_calculation.md
- `Print Settings (5 walls, 40% gyroid, supports off)` --shares_data_with--> `Key-Bore Bearing p_max = 6M/(d·Le²)`  [INFERRED]
  slicing/README.md → sim/hand_calculation.md
- `Structural Min Wall Check (1.87 mm, ray cast)` --references--> `FDM Design Rules (45° overhang, 0.8-1.2 mm wall, 0.2-0.5 mm clearance)`  [EXTRACTED]
  docs/checks.md → research/sources.md

## Hyperedges (group relationships)
- **PFBK Verification Evidence (CAD checks, hand calc, blocked FEA, slicing)** — docs_checks, sim_hand_calculation, sim_readme_static_stress_study, slicing_readme_supports_check, docs_checks_overhang_check [INFERRED 0.85]
- **20 N·m Design Torque Load Chain** — research_sources_wolf_tooth_6_bit, docs_scope_t_design, docs_scope_steel_l_key_architecture, sim_hand_calculation_key_bore_bearing, sim_readme_planned_load_case [INFERRED 0.95]
- **FDM Printability Rules Applied** — research_sources_fdm_design_rules, docs_checks_min_wall_check, docs_checks_overhang_check, docs_checks_diamond_bore_roofs, slicing_readme_print_settings, docs_scope_pivot_clear [INFERRED 0.85]

## Communities (7 total, 1 thin omitted)

### Community 0 - "Parts, Materials & Print Results"
Cohesion: 0.21
Nodes (12): Body_Bottom, Body_Top, Structural Min Wall Check (1.87 mm, ray cast), Packed Envelope and Model Mass (107.0×49.7×25.0 mm, 148.5 g), Tire_Lever (body), fdm_xy_comp (printer XY compensation hook), Jabil PETG TDS (cross-check), Prusament PETG Datasheet v1.1 (+4 more)

### Community 1 - "Torque Path & Stress Evidence"
Cohesion: 0.22
Nodes (9): T_design = 20 N·m, 5 N·m Torque Indicator (printed flexure + gap stop), Park Tool Torque Specifications and Concepts, Hand Calculation — ESTIMATE, Torque-Indicator Cantilever Beam Calc (SF 2.05, 3.37 mm deflection), Static Stress Study — NOT RUN (blocked), adsk.sim Simulations.get Returns None, Indicator Beam Second Case (51.6 N at push dot) (+1 more)

### Community 2 - "Model Checks & Printability"
Cohesion: 0.24
Nodes (9): Model Checks — PFBK v0.1, Fold/Unfold Key Sweep Check (52 states), Interference Check (packed kit, 12 bodies, 0 pairs), Steepest Overhang Check (45.0°, 0 bridges), STL vs CAD Volume Check, half_t (clamshell half thickness), pivot_clear = 0.4 mm (ESTIMATE), FDM Design Rules (45° overhang, 0.8-1.2 mm wall, 0.2-0.5 mm clearance) (+1 more)

### Community 3 - "Sourced Hardware & Parameters"
Cohesion: 0.48
Nodes (6): Fusion User Parameters (sourced, ESTIMATE, derived), Research — Sizes, Torques, Standards, DIN 934 / ISO 4032 M5 Hex Nut, Guillevin Metric L-Key Catalogue, ISO 4762 M5 Socket Head Screw, Wiha 01317 / King Tony 114325 T25 Torx Key

### Community 4 - "Key Selection & Unverified Items"
Cohesion: 0.40
Nodes (4): nu_petg = 0.38 (ESTIMATE Poisson's ratio), Pocket Tool Survey (Wolf Tooth, Topeak Hexus X, Lezyne V Pro 7, Park MT-10), Could Not Verify (Shimano DM-TORQUE-01, ISO 2936, PETG Poisson, lever loads), Wolf Tooth 6-Bit (20 N·m max)

### Community 5 - "Kit Scope & Tire Levers"
Cohesion: 0.50
Nodes (4): Scope — Pocket Flat & Bolt Kit (PFBK) v0.1, Pocket Flat & Bolt Kit (PFBK), Tire Levers (F6, nest on body faces), Tire Lever Commercial Precedents (Park TL-6.3, Silca Premio, Wera, Schwalbe)

## Knowledge Gaps
- **4 isolated node(s):** `Interference Check (packed kit, 12 bodies, 0 pairs)`, `STL vs CAD Volume Check`, `Jabil PETG TDS (cross-check)`, `adsk.sim Simulations.get Returns None`
  These have ≤1 connection - possible missing edges or undocumented components. (Counts symbols only; 5 node(s) total have ≤1 connection when file, concept and rationale nodes are included.)
- **1 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Fusion User Parameters (sourced, ESTIMATE, derived)` connect `Sourced Hardware & Parameters` to `Parts, Materials & Print Results`, `Torque Path & Stress Evidence`, `Model Checks & Printability`, `Key Selection & Unverified Items`, `Kit Scope & Tire Levers`, `Spoke Wrench`?**
  _High betweenness centrality (0.286) - this node is a cross-community bridge._
- **What connects `Interference Check (packed kit, 12 bodies, 0 pairs)`, `STL vs CAD Volume Check`, `Jabil PETG TDS (cross-check)` to the rest of the system?**
  _4 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Why does `Research — Sizes, Torques, Standards` connect `Sourced Hardware & Parameters` to `Parts, Materials & Print Results`, `Torque Path & Stress Evidence`, `Model Checks & Printability`, `Key Selection & Unverified Items`, `Kit Scope & Tire Levers`, `Spoke Wrench`?**
  _High betweenness centrality (0.210) - this node is a cross-community bridge._
- **Why does `Prusament PETG Datasheet v1.1` connect `Parts, Materials & Print Results` to `Torque Path & Stress Evidence`, `Sourced Hardware & Parameters`?**
  _High betweenness centrality (0.198) - this node is a cross-community bridge._