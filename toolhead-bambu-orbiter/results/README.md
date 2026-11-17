# Result files

These are the numbers behind every table and figure in `../docs`.

| Path | Content |
|---|---|
| `figures_data.json` | Values shown in the figures, already scaled to the typical-fan operating point (CFD) |
| `cfd/<case>.result.json` | Bed test, raw at 1.5 L/s per fan: ring and sector speeds 1 mm above the bed, bed / sock / nozzle wall shear, sock pressure, downward velocity, fan-outlet pressures |
| `cfd/<case>.result_free.json` | Free-air test: metrics on planes 0.2–12 mm below the tip, `scale_U` = operating-point scale |
| `cfd/fan_operating_points.json` | Fan operating points on each duct |
| `cfd/a10_snout_params.json` | Parameters of the final a10 snout profile |
| `fea/<run>/summary.json` | Frequencies, probe mode shapes, FRFs (belt → ADXL / nozzle; fan imbalance), model metadata (materials, masses, screws) |
| `fea/<run>/energy.json` | Kinetic and strain energy per part, per mode |

CFD case names:

| Case | Description |
|---|---|
| `base` | Original duct |
| `v3` | 45° visor |
| `v4d` / `v4e` | Visor with the outlet narrowed to 13 / 10 mm |
| `n55n` | 55° snout |
| `a05` / `a10` / `a10h3` | Aimed snout, screening runs at 350 iterations |
| `a10F` | Final a10, 700 iterations |
| `*_free` | Free-air test |

FEA run names:

| Prefix | Study |
|---|---|
| `a_w<perimeters>_i<infill>` | Print settings |
| `b_<material>` | Material |
| `c_*` | Joints and fan mass |
| `s1` / `s2` / `s12` | Stiffening options |
| `h_*` | Real hardware masses |
| `f_*` | Final design |

