# Uplift Modeling Project

Uplift modeling pipeline for estimating individual treatment effects (CATE) from A/B test data. The goal is to identify users who benefit most from a marketing campaign and optimize targeting.

## Data

- Binary treatment/target, ~2:1 control/treatment split
- Weak but statistically significant average treatment effect
- Balanced groups (no propensity correction needed)

## Approach

### Part 1 - Model comparison

Three meta-learner approaches compared using `causalml` with RandomForest base learner:

- **T-Learner** — simple two-model baseline
- **X-Learner** — used for unequal group sizes, selected as the best model
- **R-Learner** — doubly-robust approach

Primary metric: **uplift@30%** (targeting quality for the top 30% of users).

### Part 2 — Tuning

X-Learner improved via OHE, feature engineering, and hyperparameter tuning. All metrics improved over the baseline.

## Setup

```bash
uv sync
```

Copy `.env_template` to `.env` and fill in the values:

```bash
cp .env_template .env
```

Start MLflow tracking server:

```bash
bash run_mlflow.sh
```

Run the notebook:

```bash
uv run jupyter notebook final_project.ipynb
```

## Tech Stack

- **Python 3.10**, **uv** package manager
- **causalml**, **sklift** — uplift modeling
- **scikit-learn** — base learners (RandomForest)
- **Optuna** — hyperparameter tuning
- **MLflow** — experiment tracking
- **pandas**, **numpy** — data processing
- **matplotlib**, **seaborn** — visualization
