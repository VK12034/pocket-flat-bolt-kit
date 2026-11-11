# Hand calculation — ESTIMATE (not a simulation result)

These closed-form numbers sized the design. They are **labelled estimates**. They are not the Fusion static stress study (see
`sim/README.md` for that study's status).

## Load case
* Design torque **T = 20 N·m**, Wolf Tooth's published maximum for 4/5/6 mm and T25 bits on a pocket tool. It is above the highest in-scope
  Park Tool spec, 16.3 N·m (Control Tech stem faceplate).
* Material: Prusament PETG, printed horizontal: yield **47 MPa**, E **1.5 GPa** (TDS v1.1, ISO 527-1).
* Steel key ≈ 130× stiffer than PETG (library steel E vs 1.5 GPa), so the key is treated as rigid. The plastic only carries bearing along the
  embedded long arm.

## 1. Key-bore bearing (the most loaded printed region)
Rigid peg in an elastic socket under moment M with a linear pressure distribution: **p_max = 6·M / (d·Le²)**.
`Le` (embedded length) was chosen with this formula so that p_max ≤ yield / 2.

| Key | d (mm) | Le (mm) | p_max (MPa) | SF vs 47 MPa |
|---|---|---|---|---|
| 4 mm hex | 4.0 | 36 | 23.15 | 2.03 |
| 5 mm hex | 5.0 | 32 | **23.44** | **2.01 (lowest)** |
| 6 mm hex | 6.0 | 30 | 22.22 | 2.12 |
| T25 | 4.5 | 34 | 23.07 | 2.04 |

**Limits of this model:** it ignores stress concentration at the bore mouth and at the slot corners. It assumes uniform contact
across the key width, isotropic solid PETG (5 walls ≈ 2.1 mm make the bore region solid), and no creep. A real FE study is expected to show
higher local peaks than this average-pressure model.

## 2. Torque-indicator beam at the 5 N·m set-point
Cantilever, load F at `ind_a` from the root: F = 5 N·m / R = 5000 / 96.84 mm = **51.6 N**. Section 6.8 × 13 mm, I = 340.6 mm⁴.

* σ_max = F·a·(t/2)/I = **22.9 MPa → SF 2.05**
* Tip deflection = F·a³/(3EI) + F·a²/(2EI)·inset = **3.37 mm** → `ind_gap` = 3.4 mm (rounded up), so the gap closes at ≈ 5 N·m
* Once the gap closes the beam bottoms out on the body, so extra force goes into the body and beam stress stays near this value.

## 3. Why a printed hex socket was rejected
A 1/4 in (6.35 mm A/F) bit driven through PETG flats with 15 mm of engagement, half-flat contact model:
T = 3·p·L·(w/2)² → p ≈ 130 MPa at 20 N·m (≈ 200 MPa with a triangular distribution), against a 47 MPa yield. SF ≈ 0.25–0.35.
**The design therefore uses steel L-keys and never transmits torque through printed hex flats.**
