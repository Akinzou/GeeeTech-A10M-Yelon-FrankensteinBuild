# Parts, hardware and printing

## Printed parts (`cad/step`, `cad/stl`)

| File | Part | Volume [cm³] |
|---|---|---|
| `carriage_body` | Carriage body: MGN12H mount, hotend clamp, Orbiter mount, ADXL mount, belt clamp tongue. Includes stiffening blocks and inserts for option 1 | 29.5 |
| `hotend_cover` | Hotend cover: BLTouch mount and both 5015 fan arms. Includes stiffening (front screw bosses, closed window, strip) | 47.2 |
| `fan_duct_right` | Right part-cooling duct, a10 snout, ears and diagonal | 5.44 |
| `fan_duct_left` | Left part-cooling duct (built separately, not a mirror) | 5.49 |
| `toolboard_mount` | Toolhead PCB mount | 1.64 |

All files are in the assembly coordinate frame of the CAD model:
- **+Z points down** (towards the bed);
- **−Y is the front** of the printer;
- the nozzle tip is at (271.48, −16.00, 78.23) mm.

Orient the parts in your slicer.

### Print settings (from the simulations)

- **Material:**
  - **ASA** (or ABS) for everything. The ducts end about 2.4 mm above the nozzle tip, and the cover sits next to the heater block.
  - Avoid PETG: it is the softest and heaviest, and it softens near the hotend.
  - **ASA-CF / ABS-CF** for the body and cover raise the first fan mode by about 12 Hz, but need a hardened nozzle. Don't use CF for the thin ducts: they are brittle and their channels come out rough.
- **Perimeters ≥ 4** (0.45 mm lines). Perimeters matter much more than infill: 2 perimeters drop the first fan mode into Klipper's test band. 15 % infill is enough. Use 4–5 perimeters around the insert holes.
- **Ducts:** see the orientation note in [design-changes.md](design-changes.md#23-duct-mounting-ears-and-diagonals). Keep the inside of the channel and the snout lip clean; that is where the jet is formed.

## Hardware

Taken from the complete fastener model. All screws are ISO 4762 / DIN 912 socket head. Nuts are ISO 4032.

| Qty | Item | Where |
|---|---|---|
| 4 | M3×22 screw | 5015 fan + duct ear → cover fan sleeves (no washer) |
| 8 | M3×10 screw | Cover → body (4 original + 2 front, stiffening option 1); Orbiter → body (2, with nuts) |
| 6 | M3×8 screw | Toolhead PCB (2), BLTouch (2), ADXL345 (2), all with nuts |
| 5 | M3×6 screw | MGN12H carriage (4, heads from the front, fit them before the hotend); toolboard mount → body (1) |
| 2 | M3×20 screw | Hotend heatsink, from the back. **Assumption:** the model hole is about Ø3.2, so check your hotend's thread |
| 8 | M3 nut | PCB, Orbiter, BLTouch, ADXL (2 each) |
| 11 | M3×5.7 heat-set insert | Cover fan sleeves (4), cover → body (6), toolboard mount (1) |

The fasteners weigh about 36 g. Moving mass of the complete head, as modelled, is about 357 g in ASA, plus the 50 g MGN12H carriage.

Bought components (not included):
- **Hotend:** Bambu Lab P1S/X1-style hotend with its 25 mm fan.
- **Extruder:** Orbiter v2.0 with LDO 36STH17 motor.
- **Part cooling:** 2× 5015 radial blower (about 30 g each assumed; a lighter fan helps).
- **Probe:** BLTouch (Smart V3.1).
- **Accelerometer:** ADXL345 board, 15.24 mm hole spacing.
- **Toolhead PCB:** 36 × 10 × 27 mm, 2× Ø3 holes 30 mm apart.
- **Linear rail:** MGN12H rail and carriage; 20 × 20 mm M3 pattern on the back of the body.

## After assembly

1. `PID_CALIBRATE HEATER=extruder TARGET=<your temp>` with the part fan at your usual speed (e.g. `M106 S255`). The aimed jets cool the nozzle tip more than the original ducts did.
2. `TEST_RESONANCES AXIS=X FREQ_END=250` with the head in the middle of X. The model predicts:
   - the main peak at about 70–76 Hz;
   - a small second peak at about 150–170 Hz.
3. Start with a lower part-fan percentage than you used with the original ducts. The jet at the nozzle is much stronger.
