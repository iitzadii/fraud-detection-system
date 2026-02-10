# Fraud Detection System

An end-to-end machine learning project for detecting fraudulent financial transactions using real-world transactional data. The project focuses on data preprocessing, feature engineering, handling class imbalance, model evaluation, and business-oriented decision making.

---

## Project Overview

Financial fraud detection is a highly imbalanced classification problem where identifying fraudulent transactions is critical while minimizing false alarms. This project builds and evaluates multiple machine learning models to proactively detect fraud and selects an optimal model based on precision–recall trade-offs and generalization performance.

The final solution uses **Gradient Boosted Trees (LightGBM)** to capture complex, non-linear fraud patterns in large-scale transactional data.

---

## Dataset

- Format: CSV  
- Size: ~1.6 million rows  
- Nature: Simulated financial transaction data over 30 days  

Due to GitHub file size limitations, the dataset is **not included** in this repository.

### Dataset Source
Add your dataset link here: [Fraud.csv]([url](https://drive.usercontent.google.com/download?id=1VNpyNkGxHdskfdTNRSjjyNa5qC9u0JyV&export=download&authuser=0))


After downloading, place the file in a `data/` directory:
```data/Fraud.csv```

## Data Preprocessing & Feature Engineering

Key preprocessing steps include:

- Handling missing values in balance-related fields
- Removing non-informative identifier columns
- Reducing multicollinearity using engineered balance-change features
- Creating temporal features (hour, day) from transaction timestamps
- Encoding categorical transaction types
- Preserving fraud-related outliers as meaningful signals

## Class Imbalance Handling

Fraud represents a very small fraction of total transactions. To address this:

- Class weights were applied during model training
- Accuracy was avoided as a primary metric
- Precision, recall, and F1-score were used for evaluation
- Probability threshold tuning was applied to control business trade-offs

## Models Evaluated

The following models were implemented and compared:

- Logistic Regression (baseline, interpretable)
- Decision Tree Classifier (non-linear, rule-based)
- Gradient Boosted Trees (LightGBM)

Logistic Regression was retained as a baseline reference, while tree-based models showed significantly better performance on non-linear fraud patterns.

## Final Model: LightGBM

LightGBM was selected as the final model due to:

- Strong performance on large-scale tabular data
- Ability to capture complex feature interactions
- Robust handling of class imbalance
- Superior precision–recall balance
- Minimal overfitting (validated via train–test comparison)

### Final Performance (Fraud Class)

| Metric     | Value |
|------------|-------|
| Precision  | ~0.81 |
| Recall     | ~0.85 |
| F1-score   | ~0.83 |

A probability threshold of **0.6** was selected to balance fraud detection effectiveness and operational feasibility.

## Key Fraud Indicators

Feature importance analysis highlights the following key predictors:

- Temporal patterns (hour, day)
- Sudden balance changes in origin and destination accounts
- Transaction amount
- Transaction types such as `TRANSFER` and `CASH_OUT`

These patterns align with real-world fraud behavior, such as rapid fund transfers and account draining.

## Business Recommendations

Based on model insights:

- Apply additional verification for high-risk transactions
- Monitor large balance-draining transfers, especially during off-peak hours
- Use model probabilities as dynamic risk scores
- Combine ML predictions with existing rule-based systems

## Model Monitoring & Validation

To ensure long-term effectiveness:

- Track precision, recall, and alert volume over time
- Monitor data and prediction drift
- Periodically retrain the model with recent data
- Evaluate impact using A/B testing or controlled rollouts

## Tech Stack

- Python
- Pandas, NumPy
- Scikit-learn
- LightGBM
- Matplotlib, Seaborn

## Repository Structure
├── notebooks/
│   └── fraud_detection.ipynb
├── data/
│   └── (dataset not included)
├── README.md
└── requirements.txt
