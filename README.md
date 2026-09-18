# MD-tensile-simulation-of-homogeneous-supra-nano-structured-copper-by-Lammps
This dataset accompanies the manuscript “Atomistic Direct Quantitative Evidence of Plastic Deformation Mechanisms and Delocalization in Supra-nano Structured Copper”. It provides one Voronoi-constructed copper model with an average grain size of 2.48 nm, the LAMMPS input file for tensile simulation, and the interatomic potential file for copper used by that input file.

## Files

| File | Description |
| --- | --- |
| `HSNS_2.48nm.data` | LAMMPS atomic configuration for the 2.48 nm model. The file contains 1,560,728 Cu atoms; its header identifies it as a Voronoi polycrystal with 2304 grains. |
| `in.tension.lmp` | LAMMPS input for energy minimization, equilibration, and tensile loading of the model. |
| `Cu_mishin1.eam.alloy` | The Cu embedded-atom method (EAM) potential file used by the input. |

The manuscript also considers models with average grain sizes of 4.96, 7.61, and 9.93 nm. Their atomic configurations are not included here. They follow the same Voronoi-based construction approach, with the number and spacing of seed points adjusted for the target grain size. 

## Running the simulation

Keep the three files in the same directory. The input reads `HSNS_2.48nm.data` and loads `Cu_mishin1.eam.alloy` using `pair_style eam/alloy`. From that directory, run:

```bash
lmp -in in.tension.lmp
```

Use a LAMMPS executable that supports `compute voronoi/atom` (the VORONOI package). The input uses `units metal`, periodic boundaries in all three directions, and a 0.002 ps timestep. It minimizes the structure, equilibrates it at 300 K for 10,000 steps, then applies tensile deformation along the z direction at an engineering strain rate of 2 × 10^8 s⁻¹ to a target engineering strain of 0.12. 

The input writes LAMMPS data files, trajectory dumps, stress–strain data, radial distribution function data, mean-squared-displacement data, restart files, and the standard LAMMPS log. These are outputs generated during execution and are not included in this dataset. The run requires enough memory and storage for a model containing more than 1.5 million atoms. 

## Potential provenance

The header of the supplied `Cu_mishin1.eam.alloy` file identifies it as a Cu EAM potential in LAMMPS setfl format from Mishin et al., *Physical Review B* **63**, 224106 (2001), converted by C. A. Becker from files provided by Y. Mishin on **4 February 2009**. The [NIST Interatomic Potentials Repository entry](https://www.ctcms.nist.gov/potentials/testing/entry/2001--Mishin-Y-Mehl-M-J-Papaconstantopoulos-D-A-et-al--Cu-1/) identifies this as the **EAM1** Cu potential and lists the current LAMMPS-compatible file under the name `Cu01.eam.alloy`. This record supplies the original `Cu_mishin1.eam.alloy` file used for the simulations; a shared provenance does not by itself establish byte-for-byte identity between differently named files.

The authors of the accompanying manuscript did not develop or modify the potential. It is supplied to support reproducibility. Users of the potential should cite both the original publication and the NIST repository:

> Y. Mishin, M. J. Mehl, D. A. Papaconstantopoulos, A. F. Voter, and J. D. Kress, “Structural stability and lattice defects in copper: Ab initio, tight-binding, and embedded-atom calculations,” *Physical Review B* **63**, 224106 (2001). [https://doi.org/10.1103/PhysRevB.63.224106](https://doi.org/10.1103/PhysRevB.63.224106)

The provenance statement does not assign a new license to this third-party potential.
