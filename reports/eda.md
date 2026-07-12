# 📊 Exploratory Data Analysis (EDA) Report

## German Credit Risk Prediction Project

---

# 1. Introduction

Exploratory Data Analysis (EDA) is performed to better understand the dataset before developing machine learning models.

The primary objectives of this analysis are:

* Understand feature distributions
* Identify outliers and anomalies
* Explore relationships between variables and credit risk
* Detect class imbalance
* Determine preprocessing requirements
* Generate business insights for financial decision-making

---

# 2. Dataset Overview

### Dataset Name

Statlog (German Credit Data)

### Number of Records

1000 customers

### Number of Features

20 predictor variables + 1 target variable

### Problem Type

Binary Classification

### Target Variable

| Value | Meaning          |
| ----- | ---------------- |
| 0     | Good Credit Risk |
| 1     | Bad Credit Risk  |

---

# 3. Feature Classification

The dataset contains both numerical and categorical variables.

## Numerical Features

* Duration
* Credit Amount
* Installment Rate
* Present Residence
* Age
* Number of Credits
* People Liable

## Categorical Features

* Status of Checking Account
* Credit History
* Purpose
* Savings Account
* Employment Duration
* Personal Status and Sex
* Other Debtors
* Property
* Housing
* Job
* Telephone
* Foreign Worker
* Other Installment Plans

---

# 4. Target Variable Analysis

The target variable represents customer credit risk.

### Distribution

| Credit Risk | Approximate Percentage |
| ----------- | ---------------------- |
| Good Risk   | 70%                    |
| Bad Risk    | 30%                    |

### Observation

The dataset exhibits moderate class imbalance.

### Business Interpretation

Most customers are considered low-risk borrowers. However, approximately one-third of customers represent higher risk and require careful evaluation before loan approval.

### Implications

During model development:

* Stratified train-test splitting should be used.
* Evaluation metrics beyond accuracy should be considered.
* Techniques such as SMOTE may be explored if necessary.

---

# 5. Age Analysis

### Distribution Findings

* Majority of customers are between 25 and 45 years old.
* Very few elderly customers exist.

### Business Insight

Banks tend to issue loans primarily to working-age individuals with stable income sources.

### Potential Impact on Risk

Younger customers may have limited financial history, while older customers may demonstrate more stable repayment behavior.

---

# 6. Credit Amount Analysis

### Distribution Findings

* Highly right-skewed distribution.
* Most customers request moderate loan amounts.
* A small number of customers request significantly larger loans.

### Outlier Detection

Several extreme values were observed.

### Business Insight

Large loan amounts generally carry increased financial risk due to larger repayment obligations.

### Modeling Implications

The variable may require:

* Log transformation
* Scaling
* Outlier treatment

---

# 7. Loan Duration Analysis

### Distribution Findings

* Most loans are short-term.
* Some customers have significantly longer repayment periods.

### Business Insight

Longer repayment periods often increase uncertainty and default probability.

### Potential Risk Indicator

Loan duration may become one of the most important predictive features.

---

# 8. Outlier Analysis

Boxplots were used to identify extreme observations.

## Observations

### Age

Contains a few higher-age observations.

### Duration

Contains several long-duration loans.

### Credit Amount

Contains significant outliers.

### Business Interpretation

Extreme observations are common in financial datasets and often represent high-value customers or higher-risk loan applicants.

### Modeling Consideration

Outliers should not be removed without proper business justification.

---

# 9. Relationship Between Features and Credit Risk

## Age vs Risk

The relationship between age and credit risk appears moderate.

Possible interpretation:

* Younger individuals may have limited credit history.
* Older individuals may exhibit more financial stability.

---

## Duration vs Risk

Customers with longer loan durations appear more likely to belong to the bad-risk category.

### Business Insight

Long repayment periods increase exposure to financial uncertainty.

---

## Credit Amount vs Risk

Higher loan amounts may be associated with greater default risk.

### Business Insight

Larger financial obligations may increase repayment difficulty.

---

# 10. Categorical Feature Analysis

Several categorical variables appear to have strong relationships with credit risk.

## Potentially Important Features

### Status of Checking Account

Customers with poor account status may exhibit higher risk.

### Credit History

Past financial behavior is often one of the strongest indicators of future repayment capability.

### Savings Account

Higher savings balances may indicate greater financial stability.

### Employment Duration

Longer employment generally reflects stable income.

### Housing Status

Property ownership may positively influence repayment capability.

---

# 11. Correlation Analysis

Correlation analysis was performed among numerical variables.

### Observations

* Credit Amount and Duration may exhibit moderate relationships.
* Age appears to have weak correlation with other numerical variables.
* Target variable correlations are relatively low.

### Interpretation

Weak linear relationships suggest that machine learning models capable of learning nonlinear patterns may perform better.

Examples:

* Random Forest
* XGBoost
* Gradient Boosting Models

---

# 12. Important Findings

## Key Insights

### Dataset Quality

✅ No missing values.

### Class Distribution

⚠ Moderate class imbalance exists.

### Feature Types

✅ Combination of numerical and categorical variables.

### Outliers

⚠ Present in financial variables.

### Strong Candidate Predictors

* Credit History
* Duration
* Credit Amount
* Savings Account
* Checking Account Status
* Employment Duration

---

# 13. Preprocessing Requirements

Based on EDA findings, the following preprocessing steps are recommended.

## Encoding

Categorical variables must be converted into numerical representations.

Possible techniques:

* Label Encoding
* One-Hot Encoding

---

## Feature Scaling

Numerical variables may require scaling:

* Credit Amount
* Duration
* Age

Techniques:

* StandardScaler
* MinMaxScaler

---

## Class Imbalance Handling

Potential techniques:

* Stratified Sampling
* SMOTE
* Class Weight Adjustment

---

# 14. Next Steps

The next phase of the project includes:

1. Data Preprocessing
2. Feature Engineering
3. Train-Test Split
4. Building Machine Learning Models
5. Model Evaluation
6. Explainability Analysis using SHAP
7. Deployment using Streamlit

---

# 15. Conclusion

The German Credit dataset represents a realistic financial dataset suitable for credit risk assessment.

EDA revealed:

✅ Clean dataset
✅ Moderate class imbalance
✅ Presence of outliers
✅ Several potentially strong predictors of credit risk

These findings provide a solid foundation for developing robust machine learning models for predicting customer credit risk.
