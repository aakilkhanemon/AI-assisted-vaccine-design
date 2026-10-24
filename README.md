# AI-Driven Kinetic and Structural Validation Framework for Mpox Subunit Vaccines

[![bioRxiv](https://img.shields.io/badge/bioRxiv-2026.10.04.756542-b31b1b.svg)](https://doi.org/10.64898/2026.10.04.756542)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python: 3.10](https://img.shields.io/badge/Python-3.10-brightgreen.svg)](https://www.python.org/)
[![Zenodo](https://img.shields.io/badge/Zenodo-10.5281%2Fzenodo.22865532-blue.svg)](https://doi.org/10.5281/zenodo.22865532)

<p align="center">
  <img src="assets/graphical_abstract.png" alt="Graphical Abstract" width="100%">
</p>

Official implementation and validation codebase for:  
**"AI-Driven Design of Next-Generation Immunoinformatics Multi-Epitope Subunit Vaccine Targeting the Most Virulent Mpox Proteome: A Structural and Kinetic Validation Framework"**  
*Mohammed Emon, Noimul Hasan Siddiqque, Md. Enamul Haque* (bioRxiv preprint doi: [10.64898/2026.10.04.756542](https://doi.org/10.64898/2026.10.04.756542)).

---

## Key Highlights

- **Latent-Space Naturalness (ESM-2):** Structural verification across synthetic linker junctions (EAAAK, AAY, GPGPG) to prevent misfolding and aberrant intracellular proteolysis.
- **Deep-Learning Immunopeptidomics (MHCflurry 2.0):** Deconvolved intracellular antigen processing (cleavage and TAP transport) from HLA Class I groove binding affinity, prioritizing candidates in the optimal presentation tier (FLADKKMTL, KD = 15.07 nM, 0.002% presentation percentile rank).
- **Immune Synapse Mechanics (Graph Neural Networks):** Modeled ternary TCR–pMHC physical interactions using geometric graphs with AlphaFold-PAE weighted edges, resolving residue-level edge-attention dynamics across CDR3 loops.
- **Translational Kinetics & Expression Vector Mapping:** Ensured high-level heterologous expression via ViennaRNA minimum free energy (MFE) simulation, validating an open 5' initiation terminal (ΔG = -11.6 kcal/mol) and in-frame insertion into pET-28a(+).

---

## Directory Architecture

```text
├── assets/                  # High-resolution graphical abstracts and workflow diagrams
├── data/                    # FASTA sequences, HLA matrices, and 3D PDB/PAE coordinates
├── notebooks/               # Step-by-step Colab-compatible demonstration notebooks
│   ├── 01_immunopeptidomics_mhcflurry.ipynb
│   ├── 02_mrna_kinetics_and_cloning.ipynb
│   └── 03_tcr_pmhc_synapse_gnns.ipynb
├── src/                     # Core reusable validation modules
│   ├── immunopeptidomics.py
│   ├── mrna_kinetics.py
│   ├── in_silico_cloning.py
│   └── synapse_gnn.py
├── results/                 # Exported composite figures and TSV matrices
├── environment.yml          # Exact Conda dependencies pinned for reproducibility
├── CITATION.cff             # Standard academic citation metadata
└── README.md
```

---

## Interactive Demonstration Notebooks

Run the validation pipelines interactively via Google Colab:

| Notebook | Focus Area | Runtime | Badges |
| :--- | :--- | :--- | :--- |
| **01: Deep Immunopeptidomics** | MHCflurry Class I presentation and bivariate affinity/cleavage plots | CPU (~3 min) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/aakilkhanemon/AI-assisted-vaccine-design/blob/main/notebooks/01_immunopeptidomics_mhcflurry.ipynb) |
| **02: mRNA Kinetics & Vector Mapping** | ViennaRNA MFE base-pair density and pET-28a(+) plasmid generation | CPU (~2 min) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/aakilkhanemon/AI-assisted-vaccine-design/blob/main/notebooks/02_mrna_kinetics_and_cloning.ipynb) |
| **03: TCR-pMHC GNN Dynamics** | Geometric graph attention modeling of the ternary synapse | T4 GPU (~5 min) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/aakilkhanemon/AI-assisted-vaccine-design/blob/main/notebooks/03_tcr_pmhc_synapse_gnns.ipynb) |

---

## Local Installation

To reproduce all analyses locally, build a Python 3.10 environment:

```bash
git clone [https://github.com/aakilkhanemon/AI-assisted-vaccine-design.git](https://github.com/aakilkhanemon/AI-assisted-vaccine-design.git)
cd AI-assisted-vaccine-design

# Create and activate environment
conda env create -f environment.yml
conda activate mpxv-ai-vaccine

# Download MHCflurry presentation models
mhcflurry-downloads fetch models_class1_presentation
```

---

## Reproducing Primary Manuscript Figures

### Figure: mRNA Secondary Profiling & In Silico Cloning
```bash
python -m src.mrna_kinetics \
  --input data/constructs/candidate_3_optimized_mRNA.fasta \
  --out results/Figure_4_mRNA_and_Plasmid.png
```

### Figure: Deep Learning Antigen Presentation Screening
```bash
python -m src.immunopeptidomics \
  --epitopes data/immunopeptidomics/screened_epitopes.json \
  --alleles data/immunopeptidomics/target_hla_alleles.txt \
  --out-tsv results/candidate_3_immunopeptidomics.tsv \
  --out-fig results/Figure_5_Immunopeptidomics.png
```

### Figure: Synaptic Topology and Attention Decomposition (GNN)
```bash
python -m src.synapse_gnn \
  --pdb data/structural_models/TCR_pMHC_FLADKKMTL.pdb \
  --pae data/structural_models/TCR_pMHC_FLADKKMTL_pae.json \
  --out results/Figure_GNN_Synapse.png
```

---

## Citation

If you build upon this pipeline or utilize our design matrices, please cite:

```bibtex
@article{Emon2026MpoxVaccine,
  author = {Emon, Mohammed and Siddiqque, Noimul Hasan and Haque, Md. Enamul},
  title = {AI-Driven Design of Next-Generation Immunoinformatics Multi-Epitope Subunit Vaccine Targeting the Most Virulent Mpox Proteome: A Structural and Kinetic Validation Framework},
  journal = {bioRxiv},
  year = {2026},
  doi = {10.64898/2026.10.04.756542},
  url = {[https://doi.org/10.64898/2026.10.04.756542](https://doi.org/10.64898/2026.10.04.756542)}
}
```
