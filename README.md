# Independent Bias Audit of PARHAF
## Towards More Representative Synthetic Clinical Datasets for France and Europe

**Author:** Laurent Poyet
**Date:** April 2026
**License:** CC-BY 4.0

---

## What is this?

A systematic, quantitative bias audit of [PARHAF](https://huggingface.co/datasets/HealthDataHub/PARHAF) — the first large-scale open corpus of French synthetic clinical reports (4,259 patients, 20 specialties, ~6,190 documents).

I compare demographic, clinical, and linguistic distributions against official French national hospital statistics (PMSI/ATIH 2023, DREES 2024) using standard statistical tests, NLP analysis, and predictive modeling.

**Paper:** Tannier et al. (2026), arXiv:2603.20494

---

## Key Findings

| Finding | Metric |
|---------|--------|
| Oncology ~2× over-represented | χ² p < 0.001, Cohen's w = 0.80 |
| Near-deterministic specialty → ICD mapping | NMI = 0.585 |
| Specialty predictable from text alone | Logistic Regression F1 = 98.9% |
| Age distribution: medium deviation | Cohen's w = 0.31 |
| Sex distribution: minor deviation | Cohen's w = 0.14 |
| Text readability: realistic | French Flesch scores match clinical expectations |

**Overall bias score: 2.6 / 5** — significant deviations from national benchmarks.
**Overall fidelity score: 3.6 / 5** — moderate realism, good text quality.

---

## Repository Structure

```
notebooks/
    PARHAF_Bias_Audit_...ipynb    # Main analysis notebook (39 cells)
PARHAF_Bias_Audit_.../data/       # Exported scorecards & summary (JSON, CSV)
requirements.txt                   # Python dependencies
```

---

## Quick Start

### Run locally

```bash
pip install -r requirements.txt
jupyter notebook notebooks/PARHAF_Bias_Audit_Towards_Representative_Synthetic_Clinical_Datasets.ipynb
```

### Run on Google Colab

Upload the `.ipynb` to Colab and run all cells. Cell 3 auto-detects Colab, installs dependencies, and mounts Google Drive for exports. No GPU needed — everything is CPU-only.

---

## Methods

- **Chi-squared goodness-of-fit** tests against PMSI/ATIH population benchmarks
- **Cohen's w** effect sizes for practical significance
- **Jensen-Shannon Divergence** and **Earth Mover's Distance** for distributional comparisons
- **Bias-corrected Cramér's V** (Bergsma, 2013) for categorical associations
- **Kruskal-Wallis** with η² for numerical-categorical relationships
- **TF-IDF** distinctive vocabulary analysis per specialty
- **LDA** topic modeling (k=8) for unsupervised thematic analysis
- **Logistic Regression** specialty prediction (text + demographics)
- **Coefficient-based feature importance** with leakage detection
- **Normalized Mutual Information** causation chain analysis
- **French Flesch readability** (De Landsheere, 1963)

---

## Requirements

- Python 3.10+
- See `requirements.txt` for full dependency list
- Key packages: datasets, pandas, numpy, scikit-learn, scipy, matplotlib, seaborn, plotly, nltk

---

## Exported Outputs

After running the notebook, the following files are generated:

| File | Contents |
|------|----------|
| `audit_summary.json` | All key metrics in structured JSON |
| `bias_scorecard.csv` | 9-dimension bias scorecard |
| `fidelity_scorecard.csv` | 8-dimension fidelity scorecard |
| `specialty_comparison.csv` | PARHAF vs. PMSI specialty distribution |

---

## Citation

```bibtex
@misc{poyet2026parhaf_audit,
  author = {Poyet, Laurent},
  title = {Independent Bias Audit of PARHAF: Towards Representative Synthetic Clinical Datasets},
  year = {2026},
  url = {https://github.com/LaurentAIA/PARHAF_Bias_Audit_Towards_Representative_Synthetic_Clinical_Datasets}
}
```

---

## Disclaimer

This is an independent analysis. It is not affiliated with or endorsed by the Health Data Hub or the PARHAF authors. The goal is to provide a transparent, quantitative reference for downstream users of the dataset.
