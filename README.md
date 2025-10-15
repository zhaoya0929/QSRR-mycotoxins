# uhplc-qsrr-mycotoxin
Machine-learning assisted UHPLC–Orbitrap pseudo-targeted workflow for mycotoxin screening.  
Quantitative structure–retention relationship (QSRR) model with nested CV, OOF calibration, PI80/PI95, and applicability diagnostics.

## 1. Environment
- Python **3.10**
- RDKit **2023.09**
- scikit-learn **1.3**
- NumPy **1.26**, SciPy **1.11**, pandas **2.1**, Matplotlib **3.8**

**Install (conda recommended):**
```bash
conda create -n qsrr python=3.10 -y
conda activate qsrr
conda install -c conda-forge rdkit=2023.09 -y
pip install numpy==1.26 scipy==1.11 pandas==2.1 scikit-learn==1.3 matplotlib==3.8
````

## 2. Quick start

### 2.1 Prepare inputs

* `inhouse.csv` with columns: `compound_name, smiles, ion_mode, adduct, rt` (optional `t0`)
* `theory.csv` with columns: `compound_name, smiles, ion_mode, adduct`

### 2.2 Configure

Edit the header **Quick Config** in `qsrr_pipeline.py`:

```python
INHOUSE_PATH = r"<path>/inhouse.csv"
THEORY_PATH  = r"<path>/theory.csv"
OUTDIR       = r"<path>/qsrr_outputs"
```

### 2.3 Run

```bash
python qsrr_pipeline.py
```

### 2.4 Outputs (in `OUTDIR/`)

* **Metrics:** `metrics_POS.csv`, `metrics_NEG.csv`, `metrics_POOLED.csv`, `metrics_MACRO.csv`, `metrics_summary.csv`
* **OOF tables:** `oof_POS.csv`, `oof_NEG.csv`（以及 `oof_POOLED.csv`）
* **Predictions:** `predicted_rt_theory.csv`, `predicted_rt_inhouse.csv`
* **Figures**（`figures/`）: parity, `abs_error`, `ecdf`, `williams`, `error_vs_ood` / `error_vs_tanimoto`, boxplots
* **Diagnostics**（`analysis/`）: `williams_*.csv`, `ad_*_summary_*.csv`

## 3. Data availability

Raw LC–MS files are restricted; **de-identified feature tables** sufficient to reproduce all metrics and figures are included.

## 4. Code and archive

Repository: **(https://github.com/zhaoya0929/QSRR-mycotoxins)** (commit **b6b2ad**); archive: **Zenodo DOI 10.5281/zenodo.17359685**.
