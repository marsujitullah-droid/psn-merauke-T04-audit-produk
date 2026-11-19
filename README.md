# Accuracy and Ecosystem Bias of Global Deforestation Products in the Merauke PSN Area (T04)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24362575.svg)](https://doi.org/10.5281/zenodo.24362575)

Code, blind visual-interpretation app and data for the study *"Accuracy and Ecosystem Bias of Machine-Learning-Based Global Deforestation Products for Monitoring Land Clearing in the Merauke National Strategic Project, Indonesia: A Stratified-Sampling Assessment with Blind Visual Interpretation"*.

> **Ringkasan (ID):** Repositori ini berisi notebook, aplikasi interpretasi visual buta, titik sampel berlabel, dan tabel hasil untuk penilaian akurasi Hansen GFC, JRC TMF, RADD, dan Dynamic World dalam mendeteksi pembukaan lahan 2024–2025 di Kabupaten Merauke. Semua tabel dan gambar tersedia dalam versi Indonesia (_ID) dan Inggris (_EN).

## Study design

| Item | Value |
|---|---|
| Study area | Merauke Regency (FAO GAUL), excluding permanent water and built-up land |
| Products assessed | Hansen GFC v1.13, JRC TMF 2025, RADD, Dynamic World (2024–2025 clearing) |
| Sampling | 300 points, stratified by number of products flagging clearing (0–4); allocation 60/80/60/50/50 |
| Reference data | Blind visual interpretation of Sentinel-2 chips (2023, 2024, 2025, 2025/26) in a Colab ipywidgets app |
| Estimation | Stehman (2014) stratified estimator; 95% CI by within-stratum bootstrap (2,000 replicates) |
| Outputs | OA, UA, PA, F1, cleared area, PA by ecosystem, inter-product kappa, interpreter consistency |

## Main results

| Product | User's accuracy | Producer's accuracy | F1 | Mapped area (ha) |
|---|---|---|---|---|
| **Hansen GFC** | 0.874 [0.761–0.973] | 0.787 [0.655–0.936] | **0.828** [0.732–0.921] | 32,019 |
| JRC TMF | 0.559 [0.407–0.787] | 0.301 [0.218–0.409] | 0.391 [0.299–0.498] | 16,584 |
| RADD | 0.983 [0.955–1.000] | 0.374 [0.285–0.499] | 0.542 [0.441–0.664] | 16,384 |
| Dynamic World | 0.196 [0.151–0.251] | 0.536 [0.413–0.674] | 0.288 [0.230–0.353] | 86,727 |
| *Reference estimate* | | | | *31,549 [24,629–39,179]* |

- 300 points interpreted; 280 used (20 undeterminable). 155 cleared, 117 no change, 7 already open in 2023, 1 natural change.
- Only Hansen's mapped area falls within the reference 95% CI; TMF and RADD ≈ 0.5×, Dynamic World 2.75×.
- In open forest and savanna, TMF and RADD detected 0 of 10 cleared points; Hansen detected 10 of 10 (small sample, indicative).
- Inter-product kappa 0.14–0.55; interpreter consistency on 30 re-labelled points: 83.3% (5 classes), 90.0% (binary), binary kappa 0.80.
- Caveat: 0 of 53 points in stratum 0 were cleared (one-sided 95% upper bound 5.5%), so clearing missed by all products is not captured by the CI.

## How to run

1. Open `notebooks/T04_notebook.ipynb` in Google Colab and set `GEE_PROJECT` to your Earth Engine project.
2. **Part A** (automatic, ~30–45 min): builds strata, draws 300 points and writes image chips to Google Drive.
3. **Part B** (manual, 2–3 h, resumable): label every point in the app, then re-label 30 points for consistency.
4. **Part C** (automatic, ~5 min): accuracy, area, ecosystem bias and figures; writes `T04_hasil.zip`.

## Repository structure

```
notebooks/T04_notebook.ipynb   full pipeline + interpretation app (Colab + Earth Engine)
data/                          sample points, interpretation labels, re-labels
results/tables/                result tables (_ID / _EN) and T04_hasil_ringkas.json
results/figures/               figures (_ID / _EN)
docs/diagrams/                 flowchart, context diagram, level-1 DFD, use case (ID & EN)
```

## License

Code: MIT (`LICENSE`). Data, results and figures: CC BY 4.0.
