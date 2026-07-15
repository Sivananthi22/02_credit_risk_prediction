# 🛠️ Data Preprocessing Report

## German Credit Risk Prediction Project

---

# 1. Introduction

Data preprocessing is one of the most important stages in the Machine Learning lifecycle.

Raw data is rarely in a form that can be directly used for model training. Therefore, preprocessing techniques are applied to convert the data into a clean, structured, and machine-readable format.

The primary objectives of preprocessing are:

* Prepare data for machine learning algorithms
* Convert categorical information into numerical form
* Prevent data leakage
* Improve model performance
* Ensure fair model evaluation

---

# 2. Why Data Preprocessing is Important

Machine learning algorithms work primarily with numerical data.

However, real-world datasets usually contain:

* Text values
* Categorical information
* Different feature scales
* Imbalanced data
* Missing values
* Outliers

Without proper preprocessing:

* Models may fail to train.
* Performance may decrease.
* Evaluation results may become misleading.

Therefore, preprocessing is a critical step before model development.

---

# 3. Dataset State Before Preprocessing

After Exploratory Data Analysis, the German Credit dataset showed:

### Dataset Characteristics

| Property              | Observation      |
| --------------------- | ---------------- |
| Missing Values        | None             |
| Numerical Variables   | Present          |
| Categorical Variables | Present          |
| Outliers              | Present          |
| Class Imbalance       | Moderate         |
| Feature Scales        | Different ranges |

---

# 4. Separating Features and Target Variable

Machine learning models require:

### Input Variables (Features)

Represented by:

```python
X
```

### Output Variable (Target)

Represented by:

```python
y
```

---

## Features (X)

Features contain customer information such as:

* Age
* Credit Amount
* Loan Duration
* Credit History
* Employment Status
* Savings Information

---

## Target Variable (y)

The target variable is:

```text
risk
```

Encoding:

| Value | Meaning          |
| ----- | ---------------- |
| 0     | Good Credit Risk |
| 1     | Bad Credit Risk  |

---

## Why Separate Features and Target?

The objective of supervised learning is:

```text
Learn patterns from X
↓
Predict y
```

Therefore, the target variable must be separated before training.

---

# 5. Feature Type Identification

The dataset contains two major feature types.

---

# Numerical Variables

Examples:

* Age
* Credit Amount
* Duration
* Number of Credits

Characteristics:

* Quantitative values
* Mathematical operations can be performed

Examples:

```text
Age = 35
Credit Amount = 5000
```

---

# Categorical Variables

Examples:

* Housing
* Credit History
* Purpose
* Savings Account Status

Characteristics:

* Represent categories
* Cannot be directly used by machine learning models

Examples:

```text
Housing = Own
Purpose = Car
```

---

# Why Identify Feature Types?

Different preprocessing techniques are applied to different data types.

| Feature Type | Processing Technique |
| ------------ | -------------------- |
| Numerical    | Scaling              |
| Categorical  | Encoding             |

---

# 6. Encoding Categorical Variables

---

# What is Encoding?

Encoding is the process of converting text categories into numerical values.

Machine learning algorithms cannot directly understand:

```text
A11
A12
A13
```

Therefore, these values must be transformed.

---

# Label Encoding

Label Encoding assigns an integer value to each category.

Example:

| Category | Encoded Value |
| -------- | ------------- |
| A11      | 0             |
| A12      | 1             |
| A13      | 2             |

---

# Why Label Encoding Was Chosen

The German Credit dataset contains many coded categorical values.

Examples:

```text
A11
A32
A43
```

Label Encoding:

✅ Simple
✅ Memory efficient
✅ Suitable for tree-based models

---

# Potential Limitation

Label Encoding introduces artificial ordering.

Example:

```text
A11 → 0
A12 → 1
A13 → 2
```

This does not necessarily imply:

```text
A13 > A12 > A11
```

However, tree-based models usually handle this issue well.

---

# 7. Train-Test Split

---

# Why Split the Dataset?

The objective of Machine Learning is not only to memorize training data but also to perform well on unseen data.

Therefore, the dataset is divided into:

### Training Set

Used to learn patterns.

### Testing Set

Used to evaluate model performance.

---

# Dataset Split Used

```text
Training Data → 80%
Testing Data → 20%
```

---

# Why 80/20?

This is one of the most commonly used splitting strategies because it provides:

* Sufficient training data
* Reliable evaluation data

---

# 8. Stratified Sampling

---

# What is Stratification?

Stratification ensures that class distributions remain similar in both training and testing datasets.

Original Dataset:

| Class     | Percentage |
| --------- | ---------- |
| Good Risk | 70%        |
| Bad Risk  | 30%        |

After splitting:

Training and testing sets should maintain approximately the same proportions.

---

# Why Stratification is Important

Without stratification:

The testing dataset may accidentally contain:

* Too many good customers
* Too many bad customers

This could produce misleading evaluation results.

---

# Benefits

✅ Fair evaluation
✅ Stable model performance estimates
✅ Reduced sampling bias

---

# 9. Feature Scaling

---

# What is Feature Scaling?

Different variables often have completely different numerical ranges.

Example:

| Variable      | Example Value |
| ------------- | ------------- |
| Age           | 35            |
| Credit Amount | 15000         |

The difference in scale may cause some algorithms to assign excessive importance to larger variables.

---

# Why Scaling is Needed

Some machine learning algorithms depend heavily on distances.

Examples:

* Logistic Regression
* K-Nearest Neighbors
* Support Vector Machines
* Neural Networks

Without scaling:

Large numerical variables may dominate smaller variables.

---

# Standardization

Standardization transforms variables so that:

### Mean = 0

### Standard Deviation = 1

Formula:

```text
Z = (X − μ) / σ
```

Where:

* X = Original value
* μ = Mean
* σ = Standard deviation

---

# Example

Suppose:

```text
Age = 40
Mean Age = 35
Standard Deviation = 5
```

Then:

```text
Z = (40 − 35) / 5

Z = 1
```

This means:

The customer's age is one standard deviation above the average.

---

# Why StandardScaler Was Chosen

StandardScaler:

✅ Works well with normally distributed variables
✅ Widely used in machine learning pipelines
✅ Improves convergence of optimization algorithms

---

# Important Rule: Preventing Data Leakage

The scaler is fitted only on training data.

---

## Correct Procedure

```text
Fit → Training Data
Transform → Training Data
Transform → Testing Data
```

---

## Incorrect Procedure

```text
Fit → Entire Dataset
```

This introduces information from the test dataset into training.

This problem is called:

# Data Leakage

---

# 10. Data Leakage

---

# Definition

Data leakage occurs when information unavailable during real-world prediction is accidentally used during training.

This leads to:

* Unrealistically high performance
* Poor real-world generalization

---

# Why It is Dangerous

A model may appear highly accurate during testing but fail when deployed.

Preventing data leakage is one of the most important responsibilities of a data scientist.

---

# 11. Saving Processed Data

After preprocessing, multiple datasets are stored.

---

## Training Data

```text
X_train.csv
y_train.csv
```

---

## Testing Data

```text
X_test.csv
y_test.csv
```

---

## Scaled Data

```text
X_train_scaled.csv
X_test_scaled.csv
```

---

# Why Save Processed Data?

Benefits:

✅ Reproducibility
✅ Faster experimentation
✅ Cleaner notebooks
✅ Easier deployment

---

# 12. Preprocessing Pipeline Summary

The preprocessing workflow can be summarized as:

```text
Raw Dataset
      ↓
Separate Features and Target
      ↓
Identify Data Types
      ↓
Encode Categorical Variables
      ↓
Train-Test Split
      ↓
Apply Stratification
      ↓
Scale Numerical Variables
      ↓
Save Processed Data
```

---

# 13. Final Dataset Ready for Modeling

After preprocessing:

✅ Dataset contains only numerical values.

✅ Training and testing data are separated.

✅ Numerical variables are standardized.

✅ Data leakage has been prevented.

The dataset is now ready for machine learning model development.

---

# 14. Next Steps

The next phase of the project involves:

## Model Development

Models to be implemented:

1. Logistic Regression
2. Decision Tree
3. Random Forest
4. XGBoost

---

## Evaluation Metrics

* Accuracy
* Precision
* Recall
* F1 Score
* ROC-AUC

---

## Explainability

* Feature Importance
* SHAP Analysis

---

# 15. Conclusion

Data preprocessing transformed the raw German Credit dataset into a structured machine-learning-ready dataset.

Key achievements:

✅ Encoded categorical variables
✅ Performed train-test splitting
✅ Maintained class distribution using stratification
✅ Standardized numerical variables
✅ Prevented data leakage
✅ Prepared data for model training

Proper preprocessing significantly increases the reliability and effectiveness of machine learning models and forms the foundation of a robust credit risk prediction system.
