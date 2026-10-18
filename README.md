# CSET485 – AI and Society · Assignment 1
## Stress-testing a credit-approval model on the German Credit Data

| | |
|---|---|
| Enrollment number (last 4 digits) | 0095 |
| Dataset (last digit 5) | German Credit Data — UCI Statlog |
| Random seed (last 3 digits 095) | `random_state = 95` |
| Split | 70 % train (700) / 30 % test (300), stratified on the outcome |

### How to reproduce every number in the report
```bash
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute --inplace CSET485_A1_GermanCredit_0095.ipynb
# or open the notebook and choose Kernel → Restart & Run All
```
The notebook downloads `german.data` from the UCI repository. If the download fails it uses the identical copy in
`data/german.data` and checks it against the published properties (1,000 rows, 700/300 class split, credit-amount total 3,271,258 DM).

All reported values are written to `results/results.json`, all tables to `results/*.csv`, and all charts to `figures/`.
Running the notebook twice from a clean folder produces byte-identical results files.

### Notebook map → report sections
| Notebook section | Report section | Main outputs |
|---|---|---|
| 0–1 Setup, loading, preprocessing | Data preprocessing | `outliers.csv`, `scaling.csv` |
| 2 Part 1 | Part 1 — OLS vs logistic, thresholds, mismatch | `p1_confusion.csv`, `fig1_threshold_scatter.png` |
| 3 Part 2.1 | Simpson's-paradox hunt (age × sex) | `p21_coefficients.csv`, `fig2_simpson.png` |
| 4 Part 2.2 | Omitted-variable bias (drop `duration`) | `p22_ovb_key.csv`, `p22_ovb_all.csv`, `fig3_ovb.png` |
| 5 Part 2.3 | Adversarial subset (confident errors) | `p23_*.csv`, `fig4_adversarial.png` |
| 6 Part 2.4 | Fairness sweep (DP, EO, PP; age ≤ 25 vs > 25) | `p24_sweep.csv`, `p24_tradeoff_pairs.csv`, `fig5_tradeoff.png`, `fig6_metrics_vs_threshold.png` |

### Key modelling choices
* Outcome: `approve = 1` for UCI class 1 (good risk), `0` for class 2 (bad risk).
* No missing values; "unknown/none" categories kept as their own levels.
* 13 categorical attributes one-hot encoded (reference level dropped); 7 numeric features z-scored with training mean/SD;
  `credit_amount` log-transformed; IQR outliers flagged but kept.
* Model A: statsmodels OLS (linear probability model). Model B: statsmodels Logit (unpenalised MLE).

### Data licence
Hofmann, H. (1994). *Statlog (German Credit Data)*. UCI Machine Learning Repository, CC BY 4.0.

Tested with Python 3.13, numpy 2.x, pandas 3.0, scipy 1.18, statsmodels 0.15, scikit-learn 1.9, matplotlib 3.11.
