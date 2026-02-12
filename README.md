## Description
This repository contains a reproducible workflow to run **One-at-a-Time (OAT) sensitivity analysis** for an LCA model using a **parametric Excel sheet** as input.

The script reads parameter names and baseline values from Excel, applies a user-defined perturbation (e.g., +10% / −10% or custom ranges), updates the model accordingly, and recomputes the **LCIA score** (Brightway2). Results are exported as tables (CSV/Excel) that include:
- baseline score vs. perturbed score
- absolute and relative score change
- ranked list of the most sensitive parameters
- (optional) method-wise results if multiple LCIA methods are used

### Typical use cases
- Identify dominant parameters affecting LCIA results
- Validate parameter linking between Excel and functional-unit driving exchanges
- Support uncertainty screening before Monte Carlo or global sensitivity analysis

### Notes
This repo does **not** include proprietary databases (e.g., ecoinvent exports) or confidential project datasets. Instead, it provides an input template and expects the user to configure local Brightway2 databases/projects.
