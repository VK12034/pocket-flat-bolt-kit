# Research — sizes, torques, standards (PFBK v0.1)

Every number used in the design traces to a row here, to the Fusion model, to a simulation result,
or is marked **ESTIMATE** in `docs/scope.md`. Retrieved 2026-11-10.

## 1. Bolt torque specs (target range for the kit)

Source: Park Tool, *Torque Specifications and Concepts* (page dated 2015-08-25; values are manufacturer
specs compiled by Park, "for reference only") — https://www.parktool.com/en-us/blog/repair-help/torque-specifications-and-concepts

| Bolt (roadside-relevant) | Range in Park's table (N·m) | Notable entries |
|---|---|---|
| Stem faceplate, 4-bolt | 5.4 – 16.3 | Thomson 5.4 · Race Face 6.2 · Time 6 · Deda 8 · FSA OS-115 8.8 · Control Tech 13.6–16.3 |
| Stem steerer clamp (threadless) | 5 – 10.1 | Time 5 · Thomson 5.4 · Race Face 6.2 · Deda 8 · FSA 8.8 · Syncros 10.1 |
| Front derailleur cable pinch | 4.5 – 7 | SRAM 4.5 · Campagnolo 5 · Shimano 5–6.8 · Mavic 5–7 |
| Rear derailleur cable pinch | 4 – 7 | SRAM 4–5 · Campagnolo 6 · Shimano 5–7 |
| Rim-brake caliper mount | 7.7 – 10 | Cane Creek 7.7–8.1 · Shimano 7.8–9.8 · Tektro 8–10 · Campagnolo 10 |
| Disc caliper body mount | 5.7 – 12.4 | Magura 5.7 · Shimano 6–8 · Tektro 6–8 · Avid 9–10.2 · Hayes 12.4 |
| Disc rotor M5 bolts | 2 – 6.2 | Shimano 2–4 · Magura 3.8 · Hayes 5.6 · Avid 6.2 |
| Seat rail binder | 5 – 33.9 | Syncros 5/bolt · Time 5 · Truvativ M6 6–7.1 · Shimano 20–30 · Control Tech 1-bolt 33.9 |
| Disc rotor lockring | 40 | Avid, Shimano (lockring tool, not hex) |

Not covered by Park's page: bottle-cage / accessory bolts.

## 2. Hex / Torx sizes carried by comparable pocket tools

| Tool | Hex sizes | Torx | Published max torque | Source |
|---|---|---|---|---|
| Wolf Tooth 6-Bit | 2, 2.5, 3, 4, 5, 6, 8 | T10, T25 | **20 N·m** for 4/5/6 mm & T25 bits; 40 N·m for 8 mm | https://backcountry.com/wolf-tooth-components-6-bit-hex-wrench-multi-tool |
| Topeak Hexus X | 2, 2.5, 3, 4, 5, 6, 8 | T15, T25 | not stated | https://www.topeak.com/global/en/product/1066-HEXUS-X |
| Lezyne V Pro 7 | 3, 4, 5, 6 | T10, T25 | not stated | https://smidgens.evo.com/en-ca/multi-tools/lezyne-v-pro-7-tool |
| Park MT-10 | 3, 4, 5, 8 | T25 | not stated; T25 "typically used on brake bolts, shifters, and disc rotors" | https://www.excelsports.com/park-tool-mt-10-multi-tool |

**Finding:** 4 mm, 5 mm and T25 appear in all four tools; 6 mm in three of four.

## 3. Steel key dimensions (purchased parts)

| Key | Size | Short-arm length | Source |
|---|---|---|---|
| Hex L-key 4 mm | 4 mm A/F | 11/16 in = 17.46 mm | Guillevin metric L-key catalogue — https://www.guillevin.com/cdn/shop/files/Technical-Specs-Detail-aa0816db-2b3b-4359-a5dc-ee2cc3d3ec26.pdf |
| Hex L-key 5 mm | 5 mm A/F | 13/16 in = 20.64 mm | same |
| Hex L-key 6 mm | 6 mm A/F | 15/16 in = 23.81 mm | same |
| Torx L-key T25 | Ø4.5 mm blade | 25 mm | Wiha 01317 listing — https://aio.lv/en/product--wiha-363-t25--10549460.md ; King Tony 114325 — https://toolsid.com/king-tony/t25-torx-key-mpn-114325.html |

The same Guillevin catalogue gives long arms of 100.8 / 111.1 / 123.0 mm. The kit uses shorter
embedded lengths, so **long arms must be cut to length**.
Hex across-corners = A/F × 2/√3 (geometry, not a sourced value).

## 4. Spoke nipple flats

Park Tool SW-0 / SW-1 / SW-2 (also SW-7.2 triple wrench): **3.23 mm (0.127 in), 3.30 mm (0.130 in), 3.45 mm (0.136 in)**.
https://www.parktool.com/en-us/product/triple-spoke-wrench-sw-7-2 · https://outset.bike/park-tool-sw-0-1-2-3-standard-nipple-spoke-wrenches/
Park advises measuring the nipple first. Retailers label the "Size 0/1/2" sections inconsistently, so go by mm.

## 5. Tire levers (no published standard exists; commercial precedents)

| Lever | L × W × T (mm, per lever) | Source |
|---|---|---|
| Park TL-6.3 (steel core) | 145 × 25 × 6 | https://www.treefortbikes.com/Park-Tool-TL-63-Steel-Core-Tire-Levers |
| Silca Premio | 105 × 25 × 7 | https://bikerumor.com/2021/07/22/best-tire-levers-bicycle/ |
| Wera Bicycle Set 13 | 105 × 20 × 8 | https://www.rosebikes.com/p/wera-bicycle-set-13-tyre-lever-set-2705735 |
| Schwalbe | 98 × 25 × n/a | https://bikable.com/tools/tools-for-tyres-and-tubes/schwalbe-tire-levers-3-pack-white |

## 6. Material — Prusament PETG (datasheet v1.1, updated 2022-02-16)

| Property | Value | Test | Source |
|---|---|---|---|
| Tensile yield, printed, horizontal | **47 ± 2 MPa** | ISO 527-1 | Prusament PETG TDS (via search extract) — https://cdn.shopify.com/s/files/1/1745/6181/files/PETG_TechSheet_ENG.pdf |
| Tensile yield, printed, vertical (xz) | 50 ± 1 MPa | ISO 527-1 | same |
| Tensile modulus, printed, horizontal | **1.5 ± 0.1 GPa** | ISO 527-1 | same |
| Tensile modulus, printed, vertical (xz) | 1.6 ± 0.1 GPa | ISO 527-1 | same |
| Density | **1.27 g/cm³** | ISO 1183 | same |
| Test prints | Original Prusa i3 MK3, 0.20 mm FAST | | same |
| Cross-check (Jabil PETG) | E = 1655 MPa, yield 45 MPa | ASTM D638 XY | https://cdn.shopify.com/s/files/1/0789/2979/files/Jabil_PETg_TDS_05.pdf |

## 7. FDM design rules

| Rule | Value used | Sources |
|---|---|---|
| Max unsupported overhang | 45° | GrabCAD FDM guidelines https://grabcad.com/tutorials/fused-deposition-modeling-fdm-design-guidelines ; Makerverse FDM guide https://www.makerverse.com/resources/the-fused-deposition-modeling-fdm-design-guide/ |
| Min wall | 0.8–1.2 mm (2–3 × 0.4 mm nozzle) | Wevolver FDM tips https://www.wevolver.com/article/fdm-3d-printing-design-tips-best-practices-and-techniques-for-stronger-prints ; same guides |
| Clearance, moving parts | 0.2–0.5 mm (Xometry cites 0.5) | https://xometry.pro/en/?p=154421 ; Wevolver (above) |

## 8. Fasteners

| Part | Value | Source |
|---|---|---|
| ISO 4762 M5 socket head | head Ø 8.5 max, head height 5.0 max, 4 mm hex drive | https://cdefasteners.com/sites/default/files/product-specs/metsocketcap.pdf ; https://fasten.it/norms/norm/din_en_iso_4762 |
| M5 hex nut (DIN 934 / ISO 4032) | 8 mm A/F, 4.0 mm max height (supplier listing) | https://aspenfasteners.com/m5-0-8-din-934-iso-4032-metric-hex-finished-nuts-class-10-steel-plain |

## 9. Could NOT verify (do not treat as sourced)

- **Shimano dealer-manual torque chart (DM-TORQUE-01)**: si.shimano.com returned HTTP 403 (access denied). Shimano values above are *as reported by Park Tool*, not read from Shimano directly.
- **Park Tool torque PDF** (`torque.pdf`, metadata dated 2003): text could not be extracted. The HTML table was used.
- **ISO 2936 hex-key dimensions and proof torques**: the standard is paywalled. Short-arm lengths come from one supplier catalogue. The steel keys' own torque capacity is **not** verified. The kit relies on Wolf Tooth's 20 N·m published rating for comparable 4/5/6 mm and T25 bits.
- **ISO 4032 M5 nut height**: supplier says 4.0 mm (DIN 934). The ISO 4032 table was not seen. The design is insensitive to this value because the lever hex pocket is a through-hole.
- **ISO 1173 E6.3 tolerances**: not needed after the hex-socket drive was dropped (see rationale).
- **PETG Poisson's ratio**: not on any sheet retrieved. The simulation uses an ESTIMATE (see `docs/scope.md`).
- **Spoke nipple turning torque, tire-bead lever loads, spoke diameters**: no source found. The lever and spoke-wrench features are not simulated.
- **Tire-lever tip geometry**: no published drawing exists. Tip dimensions are ESTIMATES.
