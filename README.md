# PANI–PPY Supercapacitor Explainable Machine Learning

Data and analysis code associated with the study:

**“Polymer-specific response windows and descriptor coupling in polyaniline and polypyrrole supercapacitor electrodes mapped by explainable machine learning.”**

This repository contains the literature-derived dataset, missing-data imputation workflows, correlation analysis, machine-learning models, SHAP interpretation, and polymer-resolved two-dimensional partial-dependence analyses used to investigate the gravimetric capacitance of chemically polymerized polyaniline (PANI) and polypyrrole (PPY) supercapacitor electrodes.

## Study overview

The curated dataset contains **917 gravimetric capacitance records**:

- 541 PANI records
- 376 PPY records
- Capacitance range: 18–954 F g⁻¹

The prediction target is gravimetric capacitance in F g⁻¹. A combined PANI–PPY model is trained, followed by polymer-resolved evaluation and interpretation to identify shared and polymer-specific response patterns.

The analysis includes:

- Missing-data imputation using predictive mean matching (PMM) and classification and regression trees (CART)
- Numerical and mixed-type descriptor correlation analysis
- Gradient boosting machine (GBM)
- XGBoost
- LightGBM
- CatBoost
- Global and polymer-resolved SHAP analysis
- Support-masked two-dimensional partial-dependence analysis
- Response-scale quantification of pairwise non-additivity using the root-mean-square interaction (RMSI)

## Dataset descriptors

The model uses 15 input descriptors organized into five groups.

| Group | Descriptors |
|---|---|
| Synthesis | Monomer, dopant, template, oxidant, oxidant-to-monomer ratio (OMR) |
| Textural | Specific surface area (SSA) |
| Electrode composition | Active-material ratio (AMR), binder ratio (BR), conductive-additive ratio (CR) |
| Electrolyte | Electrolyte class, ACN, molarity |
| Electrochemical testing | Cell configuration, potential window (PW), current density (CD) |

The prediction target is:

- `Capacitance`: gravimetric capacitance in F g⁻¹

## Repository contents

| Path | Description |
|---|---|
| [`Data/Initial dataset.xlsx`](Data/Initial%20dataset.xlsx) | Initially compiled literature dataset, including electrolyte identity and publication references |
| [`Data/Curated dataset.xlsx`](Data/Curated%20dataset.xlsx) | Dataset retained after data screening and curation |
| [`Data/Correlation.ipynb`](Data/Correlation.ipynb) | Pearson, Spearman, Kendall, and mixed-type association analyses |
| [`Data/Correlation_Matrices.xlsx`](Data/Correlation_Matrices.xlsx) | Calculated descriptor-correlation matrices |
| [`Imputation/PMM/`](Imputation/PMM) | Predictive mean matching code and five imputed datasets |
| [`Imputation/CART/`](Imputation/CART) | CART imputation code and five imputed datasets |
| [`Algorithms/GBM.ipynb`](Algorithms/GBM.ipynb) | GBM optimization, evaluation, SHAP analysis, and supported 2D-PDP interactions |
| [`Algorithms/XGBoost.ipynb`](Algorithms/XGBoost.ipynb) | XGBoost optimization and evaluation |
| [`Algorithms/LightGBM.ipynb`](Algorithms/LightGBM.ipynb) | LightGBM optimization and evaluation |
| [`Algorithms/CatBoost.ipynb`](Algorithms/CatBoost.ipynb) | CatBoost optimization and evaluation |

`DatasetIPMM3.xlsx` is the imputed dataset used by the machine-learning notebooks.

## Missing-data imputation

Missing numerical values were imputed in R using multiple imputation by chained equations (`mice`). Two methods were examined:

- Predictive mean matching (PMM)
- Classification and regression trees (CART)

Five completed datasets were generated with each method using 20 MICE iterations. The imputation workflow preserves observed values and constrains imputed AMR, BR, and CR values so that the electrode-composition fractions sum to 100%.

The PMM and CART scripts contain user-specific input and output paths. These paths must be updated before the scripts are run on another system.

## Machine-learning workflow

Four tree-based regression algorithms are included:

1. Gradient boosting machine
2. XGBoost
3. LightGBM
4. CatBoost
