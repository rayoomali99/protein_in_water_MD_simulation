# 🧬 Protein-in-Water Molecular Dynamics Simulation (Hemoglobin Fragment)

This project demonstrates a **basic Molecular Dynamics (MD) simulation** of a small *hemoglobin peptide fragment (13 residues)* in a solvated water environment using **GROMACS**.

---

## 🎯 Objective
To simulate a small protein fragment in water, observe its structural stability, and validate the MD workflow using minimal computational resources (Intel i5 CPU, 4 GB RAM, no GPU).

---

## ⚙️ Tools & Environment

| Tool / Software | Purpose |
|-----------------|----------|
| GROMACS         | Molecular Dynamics simulation |
| ChimeraX / VMD  | Visualization & analysis |
| Windows 11 (HP Envy x360) | Working environment |

---

## 🧪 Workflow Overview

### Step 1 – Protein Preparation  
- Imported peptide (hemoglobin fragment)  
- Generated topology using GROMACS force field  
- Added hydrogens and processed structure  
- Saved as `protein_processed.gro`

### Step 2 – System Setup  
- Defined simulation box  
- Solvated with **SPC/E** water model  
- Neutralized with Na⁺ and Cl⁻ ions  

### Step 3 – Energy Minimization  
- Removed steric clashes and optimized geometry using `minim.mdp`

### Step 4 – Equilibration  
- NVT (constant volume) and NPT (constant pressure) equilibrations performed  
- Stabilized system temperature and pressure  

### Step 5 – Production MD  
- Ran 5 ns simulation using `md.mdp`  
- Output: `mds.gro`, `mds.xtc`, `mds.edr`

---

## 💻 Commands Used
All commands were executed as listed in `command.txt`:

```bash
gmx pdb2gmx -f protein.pdb -o protein_processed.gro -water spce
gmx editconf -f protein_processed.gro -o protein_box.gro -c -d 1.0 -bt cubic
gmx solvate -cp protein_box.gro -cs spc216.gro -p topol.top -o protein_solv.gro
gmx grompp -f ions.mdp -c protein_solv.gro -p topol.top -o ions.tpr
gmx genion -s ions.tpr -o protein_solv_ions.gro -p topol.top -pname NA -nname CL -neutral
gmx grompp -f minim.mdp -c protein_solv_ions.gro -p topol.top -o em.tpr
gmx mdrun -v -deffnm em

---
##📁 Repository Structure
Protein_in_Water_MD/
│
├── protein.pdb               # Original peptide structure
├── protein_processed.gro     # Processed structure
├── protein_box.gro           # Box definition
├── protein_solv.gro          # Solvated structure
├── protein_solv_ions.gro     # Neutralized system
├── topol.top                 # Topology file
│
├── nvt.mdp, npt.mdp, md.mdp  # Simulation parameter files
├── command.txt               # All GROMACS commands used
│
├── em.gro, nvt.gro, npt.gro, mds.gro  # Simulation outputs

---
##📊 Results & Observations
Simulation ran for 5 ns successfully without instability.

The peptide maintained its α-helix conformation throughout the trajectory.

RMSD stabilized after initial equilibration, confirming structural stability.

Visualization in VMD and ChimeraX showed realistic solvation and hydrogen bonding behavior.

---
##🧩 Conclusion
This molecular dynamics simulation demonstrated that a small hemoglobin fragment remains stable in a solvated environment, validating the setup and workflow for future, larger MD studies.

---
##👩‍🔬 Author

Reem Mohamednur
Bioengineer | Research Intern
📍 Riyadh, Saudi Arabia

✨ “Even the smallest protein can tell the biggest molecular story.” 🌙
