# Wine Quality Prediction — Classification & Regression

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML-orange?logo=scikit-learn&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)
![Dataset](https://img.shields.io/badge/Dataset-UCI%20Wine%20Quality-red)

---

## Overview

This project analyzes the Wine Quality dataset using both classification and regression approaches to evaluate how different modeling strategies perform under class imbalance and subjective labels.

The focus is not just prediction accuracy, but understanding trade-offs between model performance, interpretability, and real-world decision impact.
---
## Dataset

**Source:** UCI Wine Quality Dataset
**Link:** https://archive.ics.uci.edu/dataset/186/wine+quality

---

## Problem 1 — Classification

**Goal:** Predict wine quality as Low / Medium / High based on chemical properties.

### Class Distribution

| Label  | Count |
|--------|-------|
| Medium | 4,974 |
| High   | 1,277 |
| Low    |   246 |

The dataset is heavily skewed. Medium wines make up 77% of samples. Low quality wines — the most consequential class to detect — represent fewer than 4%.

---

### Logistic Regression

Trained with `class_weight='balanced'` and `StandardScaler` to handle convergence and class imbalance.

| Metric              | Value |
|---------------------|-------|
| Accuracy            | 0.54  |
| Recall — Low class  | 0.63  |

Accuracy dropped from a naive ~0.77 baseline, but recall on the Low class rose substantially. The model sacrifices some correctness on the dominant class to avoid missing rare cases.

---

### Random Forest

| Metric              | Value |
|---------------------|-------|
| Accuracy            | 0.85  |
| Recall — Low class  | 0.12  |

Random Forest achieves the highest overall accuracy, but recall for Low quality wines collapses to 0.12 — meaning it misses **88% of rare cases**. It performs well on the majority class and poorly where it matters most.

---

### Key Finding

> The "best" model depends on the cost of errors — not the highest accuracy.

This is the precision-recall tradeoff in practice. Accuracy rewards the model for getting Medium wines right, which is easy — there are thousands of them. Neither model is "best" without defining what the prediction will be used for. If the consequence of missing a low-quality wine is high (a QC system, a flagging tool), then a 54% accurate model with 0.63 recall outperforms an 85% accurate model with 0.12 recall.
---
## Error Analysis

- Most misclassifications occur between Medium and High classes — the boundary is genuinely ambiguous
- Low quality wines are frequently predicted as Medium due to class imbalance
- Borderline samples near class thresholds are the hardest to separate

Model errors are not random. They concentrate in overlapping regions of feature space where even human tasters likely disagree.

---

## Problem 2 — Regression

**Goal:** Predict the raw quality score (0–10) using the same chemical features.

### Model: Linear Regression

| Metric | Value |
|--------|-------|
| MAE    | 0.57  |
| RMSE   | 0.74  |
| R²     | 0.26  |

### Interpretation

The model predicts quality scores within ~0.57 points on average. An R² of 0.26 is low — but not surprising. Wine quality is a human judgment scored by tasters. Chemical measurements capture objective properties; they cannot fully encode subjective perception. The ceiling for any regression model on this dataset is constrained by the inherent noise in the labels themselves.

---
## Feature Insights

Correlation analysis reveals which chemical properties most influence quality:

| Feature | Correlation with Quality |
|---|---|
| Alcohol | +0.44 (strongest positive) |
| Volatile Acidity | -0.27 (strongest negative) |
| Density | -0.31 |
| Chlorides | -0.20 |

- Higher alcohol content is the single strongest predictor of quality
- Volatile acidity consistently pulls quality scores down
- No single feature dominates — the top correlation is only 0.44, which explains why regression R² is limited to 0.26
- Wine quality is determined by interactions between features, not any one measurement alone
---

## Evaluation Approach

Both problems use metrics beyond accuracy:

- **Classification:** Precision, Recall, F1-score, Confusion Matrix — because accuracy alone misleads on imbalanced data
- **Regression:** MAE, RMSE, R² — to measure both average error and explained variance

---

## Project Structure

```
data/
 ├── winequality-red.csv
 ├── winequality-white.csv

classification_model.ipynb
regression_model.ipynb
README.md
.gitignore
```

---

## Future Improvements

- [x] Apply feature scaling before training Logistic Regression
- [ ] Hyperparameter tuning (Grid Search / Random Search) on Random Forest
- [ ] Cross-validation to assess model stability across folds
- [ ] Experiment with SVM and gradient boosting classifiers
- [ ] Threshold tuning on classifier probabilities to optimize recall directly
