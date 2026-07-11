# 📊 Data Understanding Report – German Credit Risk Prediction

## 1. Project Overview

### Project Title

**Credit Risk Assessment Using Machine Learning**

### Objective

The objective of this project is to develop a machine learning model that can predict whether a customer represents a **good credit risk** or a **bad credit risk** based on demographic and financial attributes.

Credit risk prediction helps financial institutions make informed lending decisions and reduce potential losses caused by loan defaults.

---

# 2. Dataset Information

### Dataset Name

**Statlog (German Credit Data)**

### Source

UCI Machine Learning Repository

### Dataset Link

https://archive.ics.uci.edu/dataset/144/statlog+german+credit+data

### Dataset Characteristics

* Number of Records: **1000**
* Number of Features: **20**
* Target Variable: **Risk**
* Type of Problem: **Binary Classification**

---

# 3. Dataset Structure

The original dataset file (`german.data`) does not contain column names. Therefore, descriptive feature names were manually assigned.

## Features

| Feature                 | Description                                |
| ----------------------- | ------------------------------------------ |
| status_checking_account | Status of existing checking account        |
| duration                | Loan duration in months                    |
| credit_history          | Previous credit history of the customer    |
| purpose                 | Purpose of the loan                        |
| credit_amount           | Amount of credit requested                 |
| savings_account         | Savings account status                     |
| employment_duration     | Length of employment                       |
| installment_rate        | Installment rate as a percentage of income |
| personal_status_sex     | Personal status and gender                 |
| other_debtors           | Presence of other debtors or guarantors    |
| present_residence       | Number of years at current residence       |
| property                | Property ownership status                  |
| age                     | Customer age                               |
| other_installment_plans | Other installment plans                    |
| housing                 | Housing status                             |
| number_credits          | Number of existing credits                 |
| job                     | Employment category                        |
| people_liable           | Number of dependents                       |
| telephone               | Telephone ownership                        |
| foreign_worker          | Whether customer is a foreign worker       |
| risk                    | Target variable                            |

---

# 4. Target Variable

The target variable indicates customer credit risk.

### Original Encoding

| Value | Meaning          |
| ----- | ---------------- |
| 1     | Good Credit Risk |
| 2     | Bad Credit Risk  |

For machine learning purposes, the target variable was transformed into:

| Value | Meaning          |
| ----- | ---------------- |
| 0     | Good Credit Risk |
| 1     | Bad Credit Risk  |

This transformation simplifies model training and evaluation.

---

# 5. Data Loading Process

The dataset was loaded using Pandas.

```python
df = pd.read_csv(
    '../data/raw/german.data',
    sep=' ',
    header=None,
    names=columns
)
```

### Shape of Dataset

Expected Output:

```python
(1000, 21)
```

This indicates:

* 1000 customer records
* 20 predictor variables
* 1 target variable

---

# 6. Initial Data Inspection

Several exploratory functions were used:

```python
df.head()
df.info()
df.describe()
df.isnull().sum()
```

These functions help understand:

* Dataset dimensions
* Data types
* Statistical summaries
* Missing values

---

# 7. Missing Value Analysis

The German Credit dataset does not contain missing values.

### Result

```python
df.isnull().sum()
```

Output:

```python
0 missing values
```

This simplifies preprocessing since no imputation techniques are required.

---

# 8. Data Types

The dataset contains both:

### Numerical Features

* duration
* credit_amount
* age
* installment_rate
* present_residence
* number_credits
* people_liable

### Categorical Features

* status_checking_account
* credit_history
* purpose
* savings_account
* employment_duration
* housing
* job
* foreign_worker
* telephone
* etc.

Because machine learning algorithms require numerical input, categorical variables will need to be encoded during preprocessing.

---

# 9. Target Distribution

The distribution of credit risk is:

| Class     | Approximate Count |
| --------- | ----------------- |
| Good Risk | 700               |
| Bad Risk  | 300               |

### Visualization

```python
sns.countplot(data=df, x='risk')
plt.title('Credit Risk Distribution')
plt.show()
```

### Observation

The dataset exhibits a moderate class imbalance:

* Good Risk: ~70%
* Bad Risk: ~30%

This imbalance should be considered during model development and evaluation.

---

# 10. Importance of This Dataset

This dataset is widely used in:

* Credit Scoring Systems 💳
* Banking Analytics 🏦
* Financial Risk Assessment 📈
* Machine Learning Education 🤖

The project closely resembles real-world applications where banks assess loan applicants before granting credit.

---

# 11. Planned Workflow

## Phase 1 ✅

Data Understanding

## Phase 2

Exploratory Data Analysis (EDA)

## Phase 3

Data Preprocessing

* Encoding categorical variables
* Feature engineering
* Scaling numerical features

## Phase 4

Model Development

* Logistic Regression
* Decision Tree
* Random Forest
* XGBoost

## Phase 5

Model Evaluation

* Accuracy
* Precision
* Recall
* F1 Score
* ROC-AUC

## Phase 6

Model Explainability

* Feature Importance
* SHAP Analysis

## Phase 7

Deployment

* Streamlit Web Application

---

# 12. Conclusion

The German Credit dataset provides a realistic financial dataset for building a credit risk prediction system. The initial analysis indicates clean data, moderate class imbalance, and a combination of numerical and categorical features suitable for implementing a complete end-to-end machine learning pipeline.
