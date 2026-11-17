# Parts and hardware

## Printed (`cad/step`, `cad/stl`)

`carriage_body`, `hotend_cover`, `fan_duct_right`, `fan_duct_left`, `toolboard_mount`.

- **Material:** ASA or ABS, at least 4 perimeters, about 15 % infill. ASA-CF for the body and cover needs a hardened nozzle; not for the thin ducts.
- **Coordinates:** the files are in assembly coordinates (+Z down, −Y = front).

## Hardware

| Qty | Item | Where |
|---|---|---|
| 4 | M3×22 | Fan + duct ear → cover |
| 8 | M3×10 | Cover → body (6), Orbiter (2, with nuts) |
| 6 | M3×8 | PCB, BLTouch, ADXL (2 each, with nuts) |
| 5 | M3×6 | MGN12H carriage (4), toolboard mount (1) |
| 2 | M3×20 | Hotend heatsink from the back (check your thread) |
| 8 | M3 nut | |
| 11 | M3×5.7 heat-set insert | Fan sleeves (4), cover → body (6), toolboard mount (1) |

**Bought parts:**
- Bambu P1S/X1-style hotend;
- Orbiter v2.0 + LDO 36STH17;
- 2× 5015;
- BLTouch;
- ADXL345;
- toolhead PCB;
- MGN12H.

## After assembly

- `PID_CALIBRATE HEATER=extruder TARGET=<temp>` with the part fan on.
- `TEST_RESONANCES AXIS=X FREQ_END=250`. Expect the main peak at about 73 Hz and a small one at about 150–170 Hz.
- Start with a lower part-fan % than before.
