# A10M toolhead: Bambu-style hotend + Orbiter v2

[![Rotatable 3D airflow model, click to open](docs/img/cfd_3d_preview.png)](https://akinzou.github.io/GeeeTech-A10M-Yelon-FrankensteinBuild/)

**[▶ Rotatable 3D airflow model](https://akinzou.github.io/GeeeTech-A10M-Yelon-FrankensteinBuild/)**. Each fan's jet can be toggled in
the legend. Download for offline use: [with bed](docs/interactive/cfd_a10_3d_with_bed.html) /
[free air](docs/interactive/cfd_a10_3d_free_air.html).

A direct-drive toolhead for the Geeetech A10M. It carries a Bambu P1S/X1-style hotend, an Orbiter v2.0, 2× 5015, a BLTouch and an
ADXL345, on an MGN12H X rail. It has been designed and simulated, but **not printed or measured yet**.

## Contents

- [Results](#results)
- [Downloads](#downloads)
- [Printing and hardware](#printing-and-hardware)
- [Photos](#photos)
- Details:
  - [airflow (CFD)](docs/airflow-cfd.md)
  - [vibration (FEA)](docs/vibration-fea.md)
  - [cover stiffening](docs/cover-stiffening.md)
  - [design changes](docs/design-changes.md)
  - [parts and hardware](docs/assembly.md)

## Results

| | Stock | This version |
|---|---|---|
| Air 1 mm below the nozzle, nothing under it (thin walls, bridges) | 4.7 m/s | **10.5 m/s** |
| Air 1 mm above the bed, within 8 mm of the nozzle | 2.4–4.7 m/s | **3.4–6.7 m/s** |
| Jet hitting the silicone sock | yes | **no** |
| First fan vibration mode (ASA) | 135 Hz, visible to the ADXL (33 %) | **156 Hz, 11 %** (ASA-CF: 168 Hz) |
| Main X belt mode (what input shaping targets) | 71 Hz | 73 Hz |
| Duct mounting | press fit + hot glue | **screwed with the fan** |

The cost of the aimed jets is that each fan delivers about half its former flow. Surfaces more than 10–15 mm from the nozzle get
less air.

| Free air through the nozzle: stock → final | Simulated ADXL response |
|---|---|
| ![](docs/img/cfd_free_section.png) | ![](docs/img/fea_frf_adxl_x.png) |

## Downloads

- STEP and STL in [`cad/`](cad/): `carriage_body`, `hotend_cover`, `fan_duct_left`, `fan_duct_right`, `toolboard_mount`.
- They are in assembly coordinates (+Z down, −Y = front). Orient them in your slicer.

## Printing and hardware

- **Material:** ASA or ABS. Avoid PETG. ASA-CF for the body and cover adds about 12 Hz but needs a hardened nozzle.
- **Perimeters:** at least 4; they matter far more than infill.
- **Hardware:** 11× M3×5.7 heat-set inserts, M3 socket screws and nuts. The full list is in [docs/assembly.md](docs/assembly.md).
- **After assembly:**
  - re-run `PID_CALIBRATE` with the part fan on;
  - run `TEST_RESONANCES AXIS=X FREQ_END=250`. Expect the main peak at about 73 Hz and a small one at about 150–170 Hz.

## Photos

| | |
|---|---|
| ![](docs/img/render_assembly_front_right.png) | ![](docs/img/render_assembly_front_left.png) |
| ![](docs/img/render_assembly_front.png) | ![](docs/img/render_assembly_back.png) |
| ![](docs/img/render_assembly_bottom.png) | ![](docs/img/render_printed_hardware.png) |
| ![](docs/img/render_printed_front_right.png) | ![](docs/img/render_printed_bottom.png) |
| ![](docs/img/render_duct_right.png) | ![](docs/img/render_duct_left.png) |
| ![](docs/img/duct_brace_right.png) | ![](docs/img/duct_brace_left.png) |
| ![](docs/img/stiff_cover_iso_before.png) stock cover | ![](docs/img/stiff_cover_iso_after.png) stiffened cover |
| ![](docs/img/stiff_right_before.png) stock, right side | ![](docs/img/stiff_right_after.png) stiffened, right side |
| ![](docs/img/stiff_bottom_after.png) stiffened, from below | ![](docs/img/fea_modes_f_s12_ASA.png) vibration modes |

Licence: [CC BY-SA 4.0](../LICENSE).
