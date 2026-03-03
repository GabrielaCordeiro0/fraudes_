# 💳 Credit Card Fraud Detection using Machine Learning

## 📌 Executive Summary

Fraud detection in financial systems is a high-impact risk management problem.

This project builds and compares multiple machine learning models to detect fraudulent credit card transactions using a highly imbalanced real-world dataset.

Instead of optimizing for accuracy, the focus is on:

- Maximizing fraud detection (Recall)
- Controlling false alarms (Precision)
- Understanding model trade-offs
- Evaluating business impact of classification errors

---

## 📊 Business Problem

Fraudulent transactions represent less than 0.2% of total transactions, but generate disproportionate financial losses.

A model optimized only for accuracy can achieve over 99% accuracy while failing to detect fraud.

Two types of errors must be balanced:

- **False Negative (FN):** Fraud not detected → direct financial loss  
- **False Positive (FP):** Legitimate transaction blocked → customer friction & operational cost  

Therefore, this project prioritizes:

- Precision  
- Recall  
- F1-score  
- Confusion Matrix  
- Threshold behavior  

---

## 📦 Dataset

Source:  
https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud

Dataset characteristics:

- 284,807 transactions
- 492 fraud cases (~0.17%)
- Highly imbalanced binary classification
- Features anonymized via PCA (V1–V28)
- Includes `Time`, `Amount`, and `Class` (target)

---

## ⚙️ Methodology

### 1️⃣ Data Processing

- Data ingestion using PySpark
- Conversion to Pandas for modeling
- Missing value verification
- Class distribution analysis
- Stratified train/test split (80/20)

Stratification ensures fraud proportion consistency across datasets.

---

### 2️⃣ Handling Class Imbalance

Because fraud cases are extremely rare, specific strategies were applied:

- Logistic Regression with `class_weight='balanced'`
- Tree-based models evaluated under original distribution
- Evaluation focused on Recall and Precision rather than Accuracy

---

### 3️⃣ Model Comparison

Three models were evaluated:

#### 🔹 Logistic Regression
- Interpretable baseline model
- Class weighting to handle imbalance
- Fast and stable performance

#### 🔹 Random Forest
- Captures nonlinear patterns
- Robust to outliers
- Learns feature interactions

#### 🔹 LightGBM
- Gradient boosting framework
- Optimized for large-scale tabular data
- Efficient and production-oriented

The goal was not only performance comparison but understanding trade-offs between fraud detection and false alerts.

---

## 📊 Evaluation Strategy

Due to severe class imbalance, performance was evaluated using:

- Confusion Matrix
- Precision
- Recall
- F1-score

Accuracy was intentionally not used as a primary metric.

### Example Result (Logistic Regression)

Confusion Matrix:
[[56814 50]
[ 10 88]]

Precision (Fraud): 0.63
Recall (Fraud): 0.89
F1-score: 0.74

### Interpretation

- 89% of fraud cases detected
- 63% of flagged transactions are truly fraud
- Balanced trade-off between detection and false alerts

---

## 📈 Model Selection Insight

- Logistic Regression provides strong baseline performance.
- Random Forest improves nonlinear detection capacity.
- LightGBM offers scalability and competitive predictive power.

Final model choice depends on:

- Operational tolerance for false positives
- Financial impact of missed fraud
- Deployment constraints

---

## 🧠 Key Takeaways

- Accuracy is misleading in highly imbalanced fraud problems.
- Recall is critical when fraud cost is high.
- Class imbalance requires explicit modeling strategy.
- Model evaluation must reflect business trade-offs.
- Simple models can perform competitively when properly adjusted.

---

## 🚀 How to Run

1. Install dependencies:



2. Run the notebook or script.

---

## 📁 Project Structure

---

## 👩‍💻 Author

Machine Learning applied with a business-impact orientation.
