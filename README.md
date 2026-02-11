# 🍷 Wine Quality Prediction — Classification & Regression

## 📌 Project Overview

This project explores wine quality prediction using machine learning from two perspectives:

1. **Multi-class Classification**
   Predict whether a wine is:

   * Low quality
   * Medium quality
   * High quality

2. **Regression**
   Predict the **actual quality score** (0–10 scale) based on chemical properties.

This project builds on earlier foundational models and focuses on:

* Multi-class learning
* Class imbalance challenges
* Model comparison
* Regression fundamentals

---

## 📊 Dataset

**Source:** UCI Wine Quality Dataset
**Link:** https://archive.ics.uci.edu/dataset/186/wine+quality

* winequality-red.csv
* winequality-white.csv

Both datasets were merged into a single dataset for analysis.

**Total Samples:** 6,497
**Features:** 11 chemical attributes
Examples:

* Fixed acidity
* Volatile acidity
* Citric acid
* Residual sugar
* Alcohol
* pH

**Target Variable:**

* Classification: quality_label (Low / Medium / High)
* Regression: quality (numeric score)

---

## 🧠 Problem 1 — Multi-Class Classification

### Goal

Predict the quality category of wine using chemical properties.

### Class Distribution

* Medium: 4,974
* High: 1,277
* Low: 246

This shows a **class imbalance**, which makes prediction harder.

---

## ⚙️ Models Used

### 1️⃣ Logistic Regression

Baseline model for multi-class classification.

* Initial accuracy: ~0.77
* Struggled with imbalanced data
* Improved recall for minority classes when using:

```
class_weight='balanced'
```

Trade-off observed:

* Better detection of rare classes
* Reduced accuracy for dominant class

---

### 2️⃣ Random Forest Classifier (Best Performer)

* Accuracy: ~0.85
* More stable across classes
* Handled imbalance better than Logistic Regression
* Provided stronger overall performance

---

## 📉 Evaluation Metrics Used

* Precision
* Recall
* F1-score
* Confusion Matrix

Key learning:

> Accuracy alone is not enough when classes are imbalanced.

Recall became important for detecting rare classes.

---

## 📈 Problem 2 — Regression

### Goal

Predict the **actual wine quality score** using chemical properties.

### Model Used

* Linear Regression

### Results

* MAE: 0.56
* RMSE: 0.73
* R² Score: 0.26

### Interpretation

* The model predicts wine quality within ~0.5 points on average.
* R² ≈ 0.26 is expected because wine quality is subjective and influenced by human perception.

---

## 🔍 Key Challenges Faced

* Class imbalance affected classification performance
* Logistic Regression required higher iterations to converge
* Categorical column (`type`) had to be removed for regression model

These are common real-world ML problems.

---

## 🧪 Exploratory Data Analysis

Performed:

* Class distribution visualization
* Correlation heatmap
* Feature boxplots
* Statistical summaries

These helped understand:

* Feature relationships
* Class imbalance
* Feature spread across wine types

---

## 🧠 Key Learnings

This project strengthened understanding of:

* Multi-class classification
* Handling imbalanced datasets
* Model comparison techniques
* Confusion matrix interpretation
* Regression metrics:

  * MAE
  * RMSE
  * R² Score
* Real-world data preparation challenges

---

## 🏁 Conclusion

* Random Forest performed best for classification tasks.
* Linear Regression provided a reasonable baseline for quality score prediction.
* The dataset demonstrates the complexity of predicting subjective outcomes using numerical features.

This project bridges the gap between:

* Category prediction
* Numeric prediction

And serves as a strong step toward more advanced ML problems.

---

## 📂 Project Structure

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

## 🚀 Future Improvements

There are several ways this project can be further enhanced:

* Apply feature scaling before training Logistic Regression to improve convergence and performance
* Experiment with additional models such as Support Vector Machines (SVM)
* Perform hyperparameter tuning (Grid Search / Random Search) to optimize model performance
* Use cross-validation to ensure model stability and reduce overfitting
* Explore more advanced ensemble methods for better classification accuracy

These improvements can help build more robust and generalizable models.

---

## 📌 Conclusion

This project demonstrates a complete machine learning workflow for solving a multi-class classification problem and a regression problem using real-world structured data.

Key observations:

* Random Forest slightly outperformed Logistic Regression in classification tasks, showing the importance of testing multiple models.
* Class imbalance had a noticeable impact on performance, especially for minority classes.
* Linear Regression provided a reasonable baseline for predicting wine quality scores, though the subjective nature of quality limits prediction accuracy.

Overall, this project highlights how different models behave on the same dataset and reinforces the importance of proper evaluation, preprocessing, and model comparison in practical machine learning.

