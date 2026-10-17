# Closed-Cycle Gas Turbine: Air vs Helium

A MATLAB model that compares air and helium as the working fluid of a closed-cycle gas turbine. It finds the best pressure ratio for each gas and estimates how large, heavy and expensive the recuperator has to be. The results are compared with real closed-cycle plants: Oberhausen II, HTR-PM and current supercritical CO₂ projects.

The full write-up is in [`GT_Project_Report.pdf`](GT_Project_Report.pdf). Appendix A of the report explains the code block by block.

## The cycle

- Two compressors with an intercooler between them.
- A recuperator (a heat exchanger that preheats the gas before the heater).
- An external heater, then the turbine.
- A final cooler. The gas then returns to the compressor, so the loop is closed.

## Key results

| | Air | Helium |
|---|---:|---:|
| Pressure ratio at maximum efficiency | 7.40 | 4.28 |
| Maximum thermal efficiency | 38.24 % | 37.23 % |
| Pressure ratio at maximum volumetric net work | 13.63 | 6.56 |
| Maximum volumetric net work | 4725 kJ/m³ | 3275 kJ/m³ |
| Compromise pressure ratio (best trade-off) | 10.19 | 5.38 |
| Recuperator area, same effectiveness (ε = 0.9) | 90.0 m² | 48.4 m² |
| Recuperator cost estimate | 22,730 USD | 18,967 USD |

- **Air** gives about 44% more work per cubic metre of gas, so the machine can be smaller and simpler for the same power.
- **Helium** reaches almost the same efficiency at a much lower pressure ratio.
- **Helium needs about 46% less recuperator area and mass**, because it transfers heat much better. This is why helium suits compact, high-temperature systems such as gas-cooled nuclear reactors.

The recuperator area and cost are calculated for a 1 kW/K basis with an assumed heat-transfer coefficient, so only the comparison between the two gases is meaningful, not the absolute values.

![Thermal efficiency versus pressure ratio](figures/efficiency_vs_pressure_ratio.png)

![Volumetric net work versus pressure ratio](figures/volumetric_work_vs_pressure_ratio.png)

## How to run

1. Download or clone this repository.
2. Open `GTT.m` in MATLAB and press **Run**, or type `GTT` in the command window.
   - GNU Octave also works: run `GTT` from this folder.
3. The script draws six figures and prints the results in the command window.
4. Compare the printed results with [`expected_output.txt`](expected_output.txt).

- **Tested with:** MATLAB R2023b and GNU Octave 8.4. Both give identical results.
- **Toolboxes and data files:** none needed.
- **Live script:** `GT.mlx` contains the same code, with the figures and results already saved next to each section.

## Repository contents

| File | What it is |
|---|---|
| `GTT.m` | The model (MATLAB script) |
| `GT.mlx` | The same code as a MATLAB live script, with saved outputs |
| `GT_Project_Report.pdf` | Full report; Appendix A is a guide to the code |
| `expected_output.txt` | Text printed by the script, for checking a run |
| `figures/` | The six figures produced by the script (Figures 4.1 to 7.2 of the report) |

## Main assumptions

- **Fixed operating conditions:**
  - compressor inlet: 20 bar and 300 K
  - turbine inlet: 1100 K
  - intercooler outlet: 300 K
- **Gas properties:** air and helium are treated as ideal gases with constant properties.
- **Efficiencies:** the compressors and turbine have polytropic efficiencies of 0.89 and 0.88.
- **Pressure losses:**
  - 1% in the intercooler and the cooler
  - 2.5% on each side of the recuperator
  - 3% in the heater
- **Pressure ratio:** swept from 1.2 to 30 in 1,000 steps.
- **Recuperator cost:** from a correlation given by the course instructor as an estimate, so the costs are indicative.
- **Heat-transfer ratio:** helium transfers heat 1.86 times better than air, taken from *Gas Turbine Theory* (Saravanamuttoo et al.). The script also estimates this ratio itself (2.09) and uses the book value when the two differ by more than 10%. Appendix A.5 explains this.

## Limitations

- **Constant gas properties.** This is less accurate for air at high temperature.
- **No component design.** Recuperator size, mass and cost are screening estimates; the compressors and turbine are not designed.
- **The code is kept exactly as submitted for the course.** A few `fprintf` calls have no newline, so some headings run into the next line of the printed output. The numbers are not affected.

## Authors

- **Armin Aghazadeh**
- **Sadra Adib**

Gas Turbine Theory course project, School of Mechanical Engineering, University of Tehran, July 2026.

## How to cite

Use the "Cite this repository" button on GitHub (it reads [`CITATION.cff`](CITATION.cff)), or the DOI from the Zenodo record.

## License

- **Code:** MIT License, see [`LICENSE`](LICENSE).
- **Report and figures:** Creative Commons Attribution 4.0 (CC BY 4.0).
