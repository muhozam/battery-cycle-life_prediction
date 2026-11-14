# Battery Cycle-Life Prediction from Early-Cycle Data

Predicting LFP/graphite cell cycle life from the first 100 cycles, reproducing and extending
Severson et al., *Nature Energy* (2019). 124 A123 cells, fast-charging protocols (data.matr.io).

## Highlights
- Single-pass HDF5 parser (MATLAB v7.3) → cleaned per-cycle table + ΔQ(V) curves
- Severson features: ΔQ₁₀₀₋₁₀(V) statistics, capacity-fade slopes, IR, temperature
- Models: Elastic Net (baseline), Dense NN, Conv1D on ΔQ(V), MC-dropout uncertainty
- Correlation analysis with within-batch validation to separate physics from batch effects

## Results (test set, split by cell)
| Model | RMSE (cycles) | MAPE (cycles) |
|---|---|---|
| Elastic Net, full features | 109 | 9.7% |
| Conv1D on ΔQ(V) | 235 | 21.2% |
| Dense NN | 548 | 24.2% |

## Key findings
- ΔQ(V) variance tracks capacity fade consistently across all batches.
- Several pooled correlations (temperature, IR) are largely batch effects.
- With 124 cells, the linear model on physics-based features outperforms deep models.

## Run
Open the notebook in Colab (badge above), choose a T4 GPU runtime, and run all cells.
Data (~9 GB) downloads to Google Drive on the first run.

## Reference
Severson, K.A. et al. *Data-driven prediction of battery cycle life before capacity degradation.*
Nature Energy 4, 383–391 (2019).
