# Leishmania NTPDase1 Molecular Dynamics Pipeline

Molecular dynamics simulation and analysis pipeline for hinge-region mutations in *Leishmania* NTPDase1.

**Companion code for:** *Conserved Hinge-Region Mutations Produce Geometry-Specific Structural Effects in Leishmania NTPDase1: A Cross-Species Computational Target Validation Study* (Szolc, 2026)

## Overview

This repository contains the complete workflow used to run and analyse four independent 25 ns all-atom molecular dynamics simulations of wild-type and hinge-mutant NTPDase1 from *Leishmania infantum* and *Leishmania major*.

## Systems

- *L. infantum* wild type
- *L. infantum* hinge mutant (P40A, S43A, P44A, Y49F)
- *L. major* wild type
- *L. major* hinge mutant (same four substitutions)
- 
 ## Input Structures

The `structures/` folder contains the four AlphaFold-predicted PDB files used as simulation input:

- `WildtypeInfactum.pdb` — L. infantum wild-type NTPDase1
- `4MUTInfactum.pdb` — L. infantum hinge mutant (P40A, S43A, P44A, Y49F)
- `WtLmajopr.pdb` — L. major wild-type NTPDase1
- `Lmajor4mutataions.pdb` — L. major hinge mutant (same substitutions)

## Simulation Protocol

| Parameter | Value |
|-----------|-------|
| Force field | AMBER14 |
| Water model | TIP3P |
| Temperature | 310 K |
| Pressure | 1 atm |
| Timestep | 2 fs |
| Water box padding | 0.8 nm |
| Electrostatics | PME, 1.0 nm cutoff |
| Langevin friction | 1.0 ps⁻¹ |
| Equilibration | 100 ps NPT |
| Production | 25 ns per system |
| Frame save interval | 100 ps |

## Notebooks

- `NTPDase1_MD_Simulation.ipynb` — runs the full simulation pipeline including PDBFixer preparation, automatic disulfide bond detection, solvation, minimisation, equilibration and 25 ns production
- `NTPDase1_MD_Analysis.ipynb` — analyses the trajectories: RMSD, per-residue Cα RMSF, statistical testing, percentage change calculations

## Requirements

- Google Colab Pro+ recommended (A100 GPU, High RAM)
- Python packages: OpenMM 8.5+, PDBFixer, MDTraj, MDAnalysis, NumPy, Pandas, SciPy, Matplotlib

## Usage

1. Upload four input PDB files to `/content/drive/MyDrive/NTPDase1_MD/`
2. Open `NTPDase1_MD_Simulation.ipynb` in Colab
3. Connect to A100 GPU runtime with High RAM
4. Run cells sequentially — each simulation takes approximately 10-12 hours
5. When all simulations complete, run `NTPDase1_MD_Analysis.ipynb`

## Technical Notes

Several technical challenges were encountered and resolved during development:

- NumPy 2.0 compatibility with OpenMM's XTC module (bypassed via module blocking)
- Ambiguous cysteine templates requiring explicit disulfide bond detection based on SG-SG distance
- Google Drive sync limitations for large trajectory files
- Session disconnection handling via CheckpointReporter for crash recovery

## Author

Daniel Szolc  
MSci Pharmaceutical Science  


## License

MIT
