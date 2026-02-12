# One-at-a-Time (OAT) Sensitivity — Brightway2 + Parametric Excel

This repository contains a reproducible **Jupyter notebook workflow** to run **One-at-a-Time (OAT) sensitivity analysis** for a **consequential LCA (c-LCA)** model in **Brightway2**, driven by a **parametric Excel-based foreground**.

The notebook is designed to support:
- **Foreground database import** from Excel (`bw2io.ExcelImporter`)
- **Static LCA / contribution analysis** (LCIA per activity from a functional unit)
- **OAT sensitivity analysis** by perturbing parameters (e.g., +10%) and recalculating LCIA scores
- **Excel exports** of results for reporting and interpretation

> **Acknowledgements**  
> This workflow builds on previous work developed within the **ALIGNED project** and related workshops (Rebecca Belfoire, Christhel Andrade). Thanks to Lorie Hamelin for support during learning and implementation.

---

## What the notebook does

### 1) Import & setup in Brightway2
- Loads/activates required Brightway2 project context
- Imports one or more **foreground databases** from Excel using `bw2io.ExcelImporter`  
  (example files referenced in the notebook include marginal suppliers / biomass mix and Pyro-Phenol CHP foreground Excel sheets)

### 2) Static LCA and contribution analysis
- Computes baseline LCIA score for the main functional unit
- Iterates over exchanges/activities contributing to the functional unit and performs **LCIA per activity**
- Exports contribution results to Excel (multiple output files are produced, e.g. contribution exports)

### 3) OAT sensitivity analysis (parameter-driven)
- Selects a parameter group (e.g., `CHP_parameters` or `ActivityParameter`)
- Stores each parameter baseline value
- Perturbs the parameter (currently implemented as **+10%**, i.e., `original * 1.1`)
- Recomputes LCIA score after perturbation
- Exports parameter-wise OAT results and sensitivity ranking to Excel

---

## Repository contents
- `*.ipynb` : main notebook implementing import + contribution analysis + OAT
- `.gitignore` : ignores local/temporary files and (recommended) secrets
- `README.md` : documentation

---

## Requirements
Typical Python packages used in the notebook:
- `bw2data`, `bw2calc`, `bw2io`, `bw2analyzer`, `bw_processing`
- `pandas`, `numpy`, `scipy`, `matplotlib`
- (optional) `seaborn`
- Excel writer support: `xlsxwriter` or `openpyxl`

> Note: the notebook also references project-specific helper modules (e.g., `Harmonizer`, `Importer_parameters`, `lci_to_bw2`).  
> If these are not included in this repo, you must add them or adapt the notebook to run without them.

---

## Credentials / secrets (IMPORTANT)
Do **not** store ecoinvent usernames/passwords inside the notebook.

Use environment variables instead:

### Windows (PowerShell)
```powershell
setx ECOINVENT_USER "your_username"
setx ECOINVENT_PASS "your_password"


import os
EI_USER = os.getenv("ECOINVENT_USER")
EI_PASS = os.getenv("ECOINVENT_PASS")

Author

Dineshkumar Muniyappan
(Notebook date: 6 February 2026)

