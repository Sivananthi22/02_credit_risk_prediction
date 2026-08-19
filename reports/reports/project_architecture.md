🏗️ Project Architecture & Structure
German Credit Risk Prediction System
1. Introduction

This document explains the overall architecture, folder structure, components, and data flow of the German Credit Risk Prediction project.

The goal is to organize the project so that it is:

Easy to understand
Reproducible
Maintainable
Scalable
Suitable for GitHub
Suitable for future deployment

Instead of keeping all code inside notebooks, the project will gradually separate:

Data
Experiments
Source code
Models
Reports
Application code
2. Project Objective

The project aims to build an end-to-end Machine Learning system that predicts whether a customer represents:

0 → Good Credit Risk


1 → Bad Credit Risk

The system will eventually provide:

Risk prediction
Risk probability
Model explanation
Interactive web interface
3. High-Level Architecture

The overall architecture is:

                    ┌──────────────────┐
                    │   Raw Dataset    │
                    └────────┬─────────┘
                             ↓
                    ┌──────────────────┐
                    │ Data Understanding│
                    └────────┬─────────┘
                             ↓
                    ┌──────────────────┐
                    │       EDA        │
                    └────────┬─────────┘
                             ↓
                    ┌──────────────────┐
                    │  Preprocessing   │
                    └────────┬─────────┘
                             ↓
                    ┌──────────────────┐
                    │  Model Training  │
                    └────────┬─────────┘
                             ↓
                    ┌──────────────────┐
                    │ Model Evaluation │
                    └────────┬─────────┘
                             ↓
                    ┌──────────────────┐
                    │ Explainability   │
                    └────────┬─────────┘
                             ↓
                    ┌──────────────────┐
                    │ Model Deployment │
                    └────────┬─────────┘
                             ↓
                    ┌──────────────────┐
                    │    Monitoring    │
                    └──────────────────┘

4. Recommended Project Structure

The project should follow this structure:

02_credit-risk-prediction/
│
├── data/
│   ├── raw/
│   │   └── german.data
│   │
│   └── processed/
│       ├── german_credit.csv
│       ├── X_train.csv
│       ├── X_test.csv
│       ├── y_train.csv
│       ├── y_test.csv
│       ├── X_train_scaled.csv
│       └── X_test_scaled.csv
│
├── notebooks/
│   ├── 01_data_understanding.ipynb
│   ├── 02_eda.ipynb
│   ├── 03_preprocessing.ipynb
│   ├── 04_model_building.ipynb
│   └── 05_model_explainability.ipynb
│
├── src/
│   ├── __init__.py
│   ├── preprocessing.py
│   ├── train.py
│   ├── predict.py
│   └── utils.py
│
├── models/
│   ├── credit_risk_model.pkl
│   ├── scaler.pkl
│   └── encoders.pkl
│
├── reports/
│   ├── project_fundamentals.md
│   ├── data_understanding.md
│   ├── eda.md
│   ├── preprocessing.md
│   ├── model_building.md
│   ├── model_evaluation.md
│   ├── model_explainability.md
│   ├── deployment.md
│   └── monitoring_and_maintenance.md
│
├── app/
│   └── streamlit_app.py
│
├── tests/
│   └── test_prediction.py
│
├── requirements.txt
├── README.md
├── .gitignore
└── LICENSE
5. data/

The data directory contains datasets used by the project.

data/
├── raw/
└── processed/
6. data/raw/

The raw directory contains the original dataset exactly as downloaded.

Example:

data/raw/german.data

The raw dataset should generally not be modified.

This preserves the original source data and allows the preprocessing pipeline to be reproduced.

7. data/processed/

The processed directory contains datasets generated during preprocessing.

Examples:

german_credit.csv
X_train.csv
X_test.csv
y_train.csv
y_test.csv

These datasets are ready for analysis or model training.


8. Why Separate Raw and Processed Data?

Keeping raw and processed data separate is important.

The workflow becomes:

Raw Data
   ↓
Processing
   ↓
Processed Data

If something goes wrong during preprocessing, the original dataset remains unchanged.

This improves:

Reproducibility
Debugging
Data management
9. notebooks/

The notebooks directory contains experimental and analytical work.

The notebooks are organized according to the Machine Learning lifecycle.

01_data_understanding.ipynb

Purpose:

Load dataset
Assign column names
Inspect shape
Check data types
Check missing values
Analyze target
02_eda.ipynb

Purpose:

Explore distributions
Analyze relationships
Detect outliers
Generate visualizations
Identify business insights
03_preprocessing.ipynb

Purpose:

Separate X and y
Encode categorical variables
Split training and testing data
Scale numerical variables
Prepare model-ready data
04_model_building.ipynb

Purpose:

Train classification models
Compare models
Generate predictions
Evaluate performance
05_model_explainability.ipynb

Purpose:

Analyze feature importance
Generate SHAP explanations
Explain individual predictions

10. Why Use Multiple Notebooks?

Separating notebooks prevents one large notebook from becoming difficult to maintain.

Instead:

Notebook 1
    ↓
Notebook 2
    ↓
Notebook 3
    ↓
Notebook 4
    ↓
Notebook 5

Each notebook has a specific responsibility.

11. src/

The src directory contains reusable Python code.

This is an important step toward moving from an experimental project to a production-style project.

12. preprocessing.py

This file can contain reusable preprocessing functions.

For example:

def preprocess_data(data):
    ...

Instead of copying preprocessing code into multiple notebooks, the same function can be reused.

13. train.py

This file can contain model training logic.

Example responsibility:

Load Data
   ↓
Train Model
   ↓
Evaluate Model
   ↓
Save Model
14. predict.py

This file can contain prediction logic.

For example:

def predict_credit_risk(customer_data):
    ...

The Streamlit application can then call this function.