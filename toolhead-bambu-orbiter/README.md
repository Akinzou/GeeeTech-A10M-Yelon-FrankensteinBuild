# A10M direct-drive toolhead: Bambu-style hotend + Orbiter v2, simulation-driven

A direct-drive toolhead for the **Geeetech A10M** (bed-slinger, X axis on an MGN12H rail). It carries:
- a Bambu Lab P1S/X1-style hotend;
- an Orbiter v2.0 extruder;
- two 5015 part-cooling blowers;
- a BLTouch;
- an ADXL345 for Klipper input shaping.

The printed parts of an existing design were reworked with **CFD of the part-cooling air** and **modal FEA of the whole head**.
This folder holds the printable parts, the full write-ups of both studies (methods, results and limitations) and the result
files behind every number.

![Toolhead](docs/img/render_assembly_front_right.png)

> **Status:** designed and simulated, **not yet printed or measured.** All numbers are model predictions. Measurements are welcome
> (see [How to check it on your printer](#how-to-check-it-on-your-printer)).

## What changed and what the models predict

| | Original | This version |
|---|---|---|
| Part-cooling ducts | Jets hit the silicone sock and land 12–15 mm from the nozzle | **"a10" snout aimed 1 mm below the nozzle tip** from both sides |
| Air speed 1 mm below the tip, no bed (thin walls, bridges), r < 3 mm | 4.7 m/s | **10.5 m/s** |
| Air speed 1 mm above the bed, r 0–8 mm | 2.4–4.7 m/s | **3.4–6.7 m/s (+43 %)** |
| Duct mounting | Press fit on the fan + hot glue | **Screwed with the fan** (3.2 mm ears, ear-to-ear diagonal) |
| First "fan" vibration mode (ASA) | 135 Hz, at the edge of Klipper's test band, 33 % of the main peak in the ADXL | **156 Hz, 11 %** (ASA-CF: 168 Hz) |
| Main belt mode (what input shaping targets) | 71 Hz | 73 Hz |
| Cover-to-body joint | 4× M3 at the rear | **6× M3** plus a closed window and a strip (stiffening) |
| Heat-set insert holes | 4.4–5.5 mm deep (too shallow for M3×5.7) | 6.5 mm |

What the cooling numbers mean:
- **Free air:** the jets meet just under the nozzle and the air goes **down**.
  - The original ducts also aim below the tip, but the air there is about half as fast.
  - The intermediate "visor" and "snout" variants looked better with a bed, but in free air their jets crossed 5–8 mm below the nozzle and air rose under the tip.
- **Trade-off:** surfaces further than about 10–15 mm from the nozzle get less air. Each fan delivers about half the flow, because the narrow outlet has about 9× the resistance.

| Free air, section through the nozzle | Simulated ADXL response |
|---|---|
| ![](docs/img/cfd_free_section.png) | ![](docs/img/fea_frf_adxl_x.png) |

## Documentation

| | |
|---|---|
| [docs/airflow-cfd.md](docs/airflow-cfd.md) | Part-cooling CFD: OpenFOAM model, fan operating point, bed and free-air tests, design history from the original through the visor, narrowed and snout variants to a10, limitations |
| [docs/vibration-fea.md](docs/vibration-fea.md) | Modal FEA: deformable printed parts and fan housings, real masses, screw joints, belt and rail. Covers print settings, materials, joints and fan imbalance |
| [docs/cover-stiffening.md](docs/cover-stiffening.md) | Where the cover moves, stiffening options 1 / 2 / 1+2, results with every screw modelled, final design |
| [docs/design-changes.md](docs/design-changes.md) | Every change against the original design: ducts, ears and diagonals, stiffening, insert holes |
| [docs/assembly.md](docs/assembly.md) | Printed parts, print settings, hardware list, what to do after assembly |

## Folder layout

```
cad/step, cad/stl   printed parts (assembly coordinates: +Z down, -Y = front)
docs/               write-ups and figures
results/            result files behind every number in docs (CFD metrics, FEA modes / FRFs / energy splits)
```

## Printing (short version)

- **ASA or ABS. Avoid PETG:** it softens next to the hotend and is the worst choice in the vibration model.
- CF-filled ASA or ABS for the body and cover adds about 12 Hz to the first fan mode, but needs a hardened nozzle.
- **At least 4 perimeters.** With 2 perimeters the first fan mode falls into Klipper's test band. Infill hardly matters.
- Hardware: M3 socket head screws, M3 nuts and 11 M3×5.7 heat-set inserts. See [docs/assembly.md](docs/assembly.md).

## How to check it on your printer

```
PID_CALIBRATE HEATER=extruder TARGET=<temp>     ; with the part fan at your usual speed (e.g. M106 S255)
TEST_RESONANCES AXIS=X FREQ_END=250             ; head in the middle of X
```

The model predicts:
- the main peak at about 70–76 Hz;
- a small second peak at about 150–170 Hz.

The default `FREQ_END` (135 Hz) cuts the second peak off. If you measure this toolhead, please open an issue with the graph.

## Tools

- Fusion 360 for the CAD.
- **CFD:** OpenFOAM v2412 (snappyHexMesh, simpleFoam, k-ω SST).
- **FEA:** gmsh 4.8 and CalculiX 2.20.
- **Post-processing:** Python (numpy, scipy, matplotlib).
- Everything ran locally in Docker.

## Third-party parts

The hotend, extruder, motor, fans, BLTouch, accelerometer board and linear rail are bought parts. Their CAD models were used only
as context, as obstacles in the CFD and as masses in the FEA. They are **not** included in this repository. Only the printed parts
designed for this toolhead are.

## License

[CC BY-SA 4.0](../LICENSE), like the rest of this repository.
