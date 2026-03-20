# Uncertainty-Aware Preferential Mixture-of-Experts (UA-PMoE) Reproduction

This repository contains the implementation and experimental results for the analysis of the **Pima Indians Diabetes** and **MIMIC-III Mortality** datasets using Preferential MoE with KL-regularisation and Conformal Prediction.

## 📁 Repository Structure

To run the notebooks successfully, please organise your files as follows:
```text
.
├── notebooks/
│   ├── pima_diabetes_prefmoe_kl_cp.ipynb   # Pima Diabetes Analysis
│   └── mimiciii_prefmoe_kl_cp.ipynb        # MIMIC-III Mortality Analysis
├── data/                                   # Not included — see Data Access below
│   ├── diabetes.csv                        # Pima Dataset
│   └── icu24h_mortality_imputed12.csv      # MIMIC-III Dataset
├── weights/                                # Not included — see note below
│   └── cell8a_cache.pkl                    # Pre-computed weights & CV results
├── requirements.txt                        # Python dependencies
└── README.md                               # This instructions file
```

## 📂 Data Access

The `data/` and `weights/` folders are **not included** in this repository.

- **Pima Indians Diabetes:** Download `diabetes.csv` from [Kaggle](https://www.kaggle.com/datasets/uciml/pima-indians-diabetes-database) and place it in `data/`.
- **MIMIC-III:** Access requires credentialed registration via [PhysioNet](https://physionet.org/content/mimiciii/1.4/). Once approved, place the processed file `icu24h_mortality_imputed12.csv` in `data/`.
- **Pre-computed weights:** `weights/cell8a_cache.pkl` can be downloaded from [Releases](../../releases) *(or contact the author)*.

> ⚠️ Redistribution of MIMIC-III data is prohibited under the PhysioNet Data Use Agreement.

## 🛠 Installation

1. **Environment:** It is recommended to use Python 3.8 or higher.
2. **Install Dependencies:** Open your terminal/command prompt in this folder and run:
```bash
pip install -r requirements.txt
```

## 🚀 Running the Experiments

### 1. Pima Diabetes

The notebook `notebooks/pima_diabetes_prefmoe_kl_cp.ipynb` reproduces the statistical significance and conformal safety analysis. It is optimised for local execution and typically runs in under 2 minutes.

### 2. MIMIC-III Mortality Analysis

The notebook `notebooks/mimiciii_prefmoe_kl_cp.ipynb` evaluates the CP-gating escalation reduction.

**Note on Efficiency:** Training the 5-seed × 5-fold cross-validation loop can be computationally expensive.

- **Default (Fast):** The notebook is set to `FORCE_RETRAIN = False`. It will automatically load the pre-computed results from `weights/cell8a_cache.pkl`.
- **Full Reproducibility:** To re-run the training from scratch, change the variable to `FORCE_RETRAIN = True` in the designated cell.

## 📊 Key Results Captured

- **Escalation Reduction:** Demonstrates the reduction in CP-gating escalation (32.8% → 3.8%) on the MIMIC-III dataset.
- **Safety Analysis:** Provides the coverage and soft-coverage metrics for both datasets.
- **Gating Weights:** Visualises how KL-regularization shifts routing distributions away from decision boundaries.
