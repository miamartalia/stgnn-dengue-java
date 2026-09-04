# A Spatio-Temporal Graph Neural Network for District-Level Dengue Incidence Rate Forecasting in Java, Indonesia

This repository contains the code accompanying the paper *"A Spatio-Temporal Graph
Neural Network for District-Level Dengue Incidence Rate Forecasting in Java,
Indonesia"* (submitted to *Machine Learning and Knowledge Extraction*, MDPI).

The proposed model (STGNN) forecasts monthly Dengue Incidence Rate (DIR) across
119 districts in Java using a Spatial Graph Convolutional module, a Gated Temporal
Convolutional module, temporal attention pooling, and learnable node embeddings.
It is benchmarked against CatBoost, SVM, LSTM, and a stacking ensemble under a
matched-information evaluation protocol, with multi-seed training, ablations, and
district-level Wilcoxon signed-rank tests (Holm-corrected).

## Repository structure

```
.
├── notebooks/
│   ├── Model_STGNN.ipynb      # Proposed STGNN: graph construction, training,
│   │                          # evaluation, ablation, statistical tests, figures
│   └── Model_Baseline.ipynb   # Baselines: CatBoost, SVM, LSTM, stacking ensemble
├── data/                      # Data placeholder + schema (restricted data NOT included)
│   └── README.md
├── outputs/                   # Regenerated model artifacts, tables, figures (not committed)
│   └── README.md
├── requirements.txt
├── LICENSE                    # MIT (code only)
└── README.md
```

## Data availability

The dengue case surveillance data (Kemenkes RI) is **restricted and is not included**
in this repository. All case counts have been removed from the notebooks and their
outputs. The climate data were obtained from the Copernicus Climate Data Store
(ERA5-Land), population data from Statistics Indonesia (BPS), and
administrative boundaries from the Humanitarian Data Exchange (HDX).
Access and preprocessing details are provided in [`data/README.md`](data/README.md).

## Reproducibility

- **Fixed seeds:** all experiments use five seeds - `42, 123, 456, 789, 2024`.
- **Determinism:** random seeds are set for Python, NumPy, PyTorch (CPU/CUDA), and
  the data loaders; splits are chronological to avoid temporal leakage; the feature
  scaler is fit on the training split only.
- Running each notebook end-to-end regenerates every table and figure reported in
  the paper (into `outputs/`), once the restricted `df_final.csv` is placed in
  `data/data_preprocessed/`.

## Environment setup

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter lab                      # or jupyter notebook
```


## Model configuration (STGNN)

| Parameter | Value | Parameter | Value |
|---|---|---|---|
| Look-back window | 12 months | Node features | 6 |
| GCN hidden | 32 | Learning rate | 5×10⁻⁴ |
| TCN hidden | 64 | Weight decay | 1×10⁻⁴ |
| MLP hidden | 64 | Batch size | 16 |
| Kernel size | 3 | Optimizer | Adam |
| Dilation | 1 | Max epochs | 500 |
| Dropout | 0.1 | Early-stop patience | 60 |
| Node embedding dim | 6 | LR scheduler | ReduceLROnPlateau (×0.5, patience 20) |

Graph construction: Haversine-KNN-Gaussian (K = 5, σ = 25 km).

## Citation

If you use this code or repository in your work, please cite the associated paper:

> Martalia, A. M., et al. *A Spatio-Temporal Graph Neural Network for District-Level Dengue Incidence Rate Forecasting in Java, Indonesia.*

The citation information will be updated once the article DOI is assigned.

## License

Source code is released under the MIT License (see [`LICENSE`](LICENSE)). The license
covers code only; the restricted surveillance data is not part of this repository.
