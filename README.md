# Leukemia Risk Prediction Challenge

This repository contains a **survival analysis project** aimed at predicting overall survival risk in leukemia patients using clinical, molecular, and cytogenetic data.

## Dataset

The data is split into:

- `clinical_train.csv` / `clinical_test.csv`: Clinical measurements per patient (blood counts, blast percentage, etc.)
- `molecular_train.csv` / `molecular_test.csv`: Somatic mutations per patient
- `target_train.csv`: Survival information (`OS_YEARS`, `OS_STATUS`)

Each mutation includes:

- `GENE`: Affected gene
- `PROTEIN_CHANGE`: Mutation effect on protein
- `EFFECT`: High-level mutation classification (frameshift, PTD, ITD, etc.)
- `VAF`: Variant allele fraction
- Genomic coordinates: `CHR`, `START`, `END`

## Methods

- **Feature engineering**:
  - Clinical features (blood counts)
  - Molecular features:
    - Number of mutations (`N_MUT`)
    - Variant allele fraction (`MEAN_VAF`, `MAX_VAF`)
    - Number of high-impact mutations (`HIGH_IMPACT`)
    - Truncating mutations (`N_TRUNCATING`)
    - Earliest truncation position (`EARLIEST_TRUNC_POS`)
  - Cytogenetic features:
    - Losses, gains, structural changes
    - Complex karyotypes
    - Cytogenetic risk score (`CYTO_RISK_SCORE`)

- **Modeling**:
  - Cox Proportional Hazards Model (`CoxPHSurvivalAnalysis`)
  - Pipeline includes imputation, scaling (Robust + MinMax), and optional PCA
  - Performance measured with **IPCW-concordance index** across stratified K-folds

## Notebook

- `Leukemia_Risk_Prediction.ipynb`:
  - Loads data
  - Performs feature engineering
  - Fits survival model
  - Evaluates model with IPCW-C-index
  - Generates submission file

## Results
- Mean IPCW-C-index across folds: `0.7169`
- Feature importance table (`beta`, `hazard_ratio`) provided

## Requirements
pandas
numpy
scikit-learn
scikit-survival
matplotlib
seaborn
