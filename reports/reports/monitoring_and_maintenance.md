📊 Monitoring & Maintenance Report
German Credit Risk Prediction Project
1. Introduction

Building and deploying a Machine Learning model is not the end of a Machine Learning project.

Once a model is deployed, it operates on new data that may be different from the data used during training.

Therefore, the model needs to be continuously monitored.

The complete lifecycle is:

Data
 ↓
Training
 ↓
Evaluation
 ↓
Deployment
 ↓
Monitoring
 ↓
Retraining
 ↓
Redeployment

This process is an important part of MLOps (Machine Learning Operations).

2. What is MLOps?

MLOps is a set of practices used to manage Machine Learning systems throughout their lifecycle.

It combines:

Machine Learning
Software Engineering
DevOps
Data Engineering
Monitoring

The goal is to make ML systems:

Reliable
Reproducible
Maintainable
Scalable
3. Why Monitoring is Important

A model may perform well when it is initially deployed.

However, its performance can decrease over time.

For example, customer behavior may change.

During training:

Average Credit Amount
= 5,000

Several months later:

Average Credit Amount
= 15,000

The model is now receiving data that differs from the data it learned from.

This can reduce prediction quality.

4. What Should Be Monitored?

A Machine Learning system should monitor several components.

1. Data

Monitor the incoming customer data.

2. Model Predictions

Monitor what the model predicts.

3. Model Performance

Monitor accuracy, recall, precision, etc., when actual outcomes become available.

4. System Performance

Monitor application health and response time.

5. Data Monitoring

Data monitoring checks whether incoming data behaves as expected.

Important properties include:

Data types
Missing values
Value ranges
Category distributions
Statistical distributions
6. Missing Value Monitoring

Suppose the training data contained:

Missing Values = 0%

but the deployed system starts receiving:

Missing Values = 15%

This could indicate a problem with the data pipeline.

Therefore, missing-value rates should be monitored.

7. Data Range Monitoring

Some features should have reasonable ranges.

For example:

Age

should not normally contain:

Age = -10

Similarly:

Credit Amount

should not contain invalid negative values unless specifically allowed by the business definition.

8. Categorical Value Monitoring

Categorical variables may contain unexpected categories.

For example:

Housing:
Own
Rent
Free

If a new category appears:

Housing:
Mortgage

the application may not know how to encode it.

This should be detected before it causes prediction failures.

9. Data Drift

Data drift occurs when the statistical distribution of incoming data changes over time.

Example:

Training Data
Average Age = 35
Production Data
Average Age = 48

This may indicate that the customer population has changed.

10. Concept Drift

Concept drift is different from data drift.

Concept drift occurs when the relationship between features and the target changes.

For example:

During training:

Long Loan Duration
        ↓
Higher Risk

Later, market conditions change and the relationship becomes weaker.

The model may therefore become less accurate even if the feature distributions remain similar.

11. Data Drift vs Concept Drift
Type	Meaning
Data Drift	Input data distribution changes
Concept Drift	Relationship between inputs and target changes

Both can affect model performance.

12. Model Performance Monitoring

When actual customer outcomes become available, model performance can be measured.

Important metrics include:

Accuracy
Precision
Recall
F1 Score
ROC-AUC

For this project, special attention should be given to:

Recall for Bad Credit Risk

because failing to identify a risky borrower can cause financial losses.

13. Prediction Monitoring

Even before actual outcomes are available, prediction distributions can be monitored.

For example:

Normal
Good Risk = 70%
Bad Risk = 30%

Suddenly:

Good Risk = 95%
Bad Risk = 5%

This unexpected change may indicate:

Data drift
Preprocessing problems
Model problems
Changes in customer population
14. Prediction Probability Monitoring

The model may output probabilities such as:

Good Risk = 0.30
Bad Risk = 0.70

Monitoring probability distributions can reveal changes in model confidence.

For example:

Average Bad-Risk Probability
Training = 0.30


Production = 0.75

This should be investigated.

15. Logging

Logging records important events during application execution.

For example:

2026-08-18 10:15:23
Prediction completed

Logs can record:

Prediction timestamp
Model version
Processing status
Errors
Response time
Prediction result