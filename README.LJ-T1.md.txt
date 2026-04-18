# LAMMPS Modification Guide for LJ-T1 Modified Interface Potential
==============================================
## Copyright and License
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Copyright (2026) MicroMechanics Team, Department of Applied Mechanics, School of Mathematics and Physics, University of Science and Technology Beijing.
This modification and its associated files are developed by the MicroMechanics Team and are provided exclusively for academic and research sharing. The purpose 
is to advance molecular dynamics simulations of two-dimensional materials and the study of surface/interface mechanics, particularly the development of interfacial
potentials. **Commercial use is strictly prohibited.**
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
This software is distributed under the Academic Free License v1.0 or similar, which permits use, modification, and distribution for non-commercial academic purposes only.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Overview
-----------------
This document describes the procedure for implementing the modified Lennard-Jones (LJ-T1) interface potential into the LAMMPS molecular dynamics software package. 
The LJ-T1 potential provides enhanced accuracy for layered transition metal dichalcogenides systems.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## References
--------------------
- **Potential Parameters**:  
Sulaiman N M, Weikun L, Yunhan Z, Douxing P. Lennard-Jones potential parameters and cut-off modifications for layered transition metal dichalcogenides[J]. Journal of 
Applied Mechanics, 2025, 92(10): 101010.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
- **Implementation Methodology**:  
Yakang Z, Wenqu L, Jinda W, Douxing P. Tensile and Fracture Behaviours in Layered Transition Metal Compounds: A Hybrid Model Using Modified Lennard-Jones and 
Stillinger-Weber Potentials. Physica Scripta, 2026, Doi: https://doi.org/10.1088/1402-4896/ae60b3.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Pre-compilation Preparation
----------------------------------
### Step 1: Repository Access
Visit the GitHub repository at:  
**https://github.com/Douasing/pdx.github.io**  
Carefully review the `README_LJ-T1.md` file for implementation details and important notes.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Step 2: File Download
Download the following four essential files for compilation:
1. `pair_lj_cut_mx2.cpp`
2. `pair_lj_cut_mx2.h` 
3. `style_pair_update.h`
4. `Makefile_update.list`
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Step 3: Source Code Modification
Navigate to your LAMMPS source directory (example path):  
`user/software/lammps-10Aug15/src`
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
**Recommended Version**: We strongly recommend using `lammps-10Aug15.tar` (August 10, 2015 release) for optimal stability in mechanical property simulations.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
**File Integration**:
- Copy `pair_lj_cut_mx2.cpp` and `pair_lj_cut_mx2.h` directly into the `src` directory
- Rename and replace existing files:
  - `style_pair_update.h` ¡ú `style_pair.h`
  - `Makefile_update.list` ¡ú `Makefile.list`
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
**Important**: Backup the original `style_pair.h` and `Makefile.list` files before replacement.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Compilation Procedure
### Step 4: Standard Compilation
Follow the conventional LAMMPS compilation process to generate the executable named `lmpmx2`.
## Usage in LAMMPS Input Scripts
### Basic Implementation
```lammps
pair_style     lj/cutmx2 r_cutoff
pair_coeff    n1*n2 m1*m2 lj/cutmx2 ¦Å_LJ ¦Ò_LJ C_FD
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
***Hybrid Potential Example (Bilayer MoO2)***
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
pair_style      hybrid sw lj/cutmx2 20
pair_coeff      * *  sw h-moo2.sw      O1  Mo1 O2  O3  Mo2 O4  O5  Mo3 O6  O7  Mo4 O8 O1  Mo1 O2  O3  Mo2 O4  O5  Mo3 O6  O7  Mo4 O8
pair_coeff      1*12 13*24  lj/cutmx2 0.0117 2.8563 2.2744
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
***Technical Support***
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
This implementation has been validated for mechanical property calculations in layered material systems by the MicroMechanics Team, USTB.
For  any difficulties or to report issues, please refer to the original publications or contact the PI of Micromechanics Team, Pan Douxing, directly via email 
at pandouxing¡°at¡±iamt.ac.cn. He will provide direct assistance.
==========================================================================================================
Good luck~
