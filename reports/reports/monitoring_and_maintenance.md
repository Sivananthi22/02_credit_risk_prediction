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

16. Why Logging is Important

Logs help developers:

Debug problems
Investigate failures
Understand system behavior
Track model versions
Monitor application health
17. What Should NOT Be Logged?

Sensitive customer information should not be unnecessarily stored in logs.

Avoid logging sensitive personal or financial information unless there is a legitimate, protected operational requirement.

Instead of:

Customer:
Name = John Smith
Credit Amount = 15000

prefer:

Prediction completed
Model Version = v1
Prediction = Bad Risk

where appropriate.

18. Model Versioning

Every production model should have a version.

For example:

credit_risk_model_v1.pkl

Later:

credit_risk_model_v2.pkl

This makes it possible to identify which model generated a prediction.

19. Why Model Versioning Matters

Suppose a prediction was generated on:

August 18

and the model was updated on:

August 20

Without versioning, it may be difficult to determine which model generated the original prediction.

Versioning provides traceability.

20. Model Registry Concept

In larger ML systems, models can be managed through a Model Registry.

A registry can store:

Model version
Training date
Evaluation metrics
Model status
Deployment status

Example:

Version	Accuracy	Recall	Status
v1	0.78	0.72	Archived
v2	0.81	0.78	Production
v3	0.83	0.80	Testing
21. Model Retraining

When model performance decreases significantly, retraining may be necessary.

The process is:

New Data
 ↓
Data Validation
 ↓
EDA
 ↓
Preprocessing
 ↓
Model Training
 ↓
Evaluation
 ↓
Compare With Current Model
 ↓
Deploy If Better

22. When Should a Model Be Retrained?

Retraining can be triggered by:

Performance Degradation

For example:

Recall falls from 78% to 65%
Data Drift

Significant changes in input distributions.

Concept Drift

Relationship between features and risk changes.

Scheduled Retraining

For example:

Retrain every 3 months

The exact schedule depends on the business environment.

23. Retraining Strategy

A safe retraining process should not immediately replace the production model.

Instead:

Current Production Model
          ↓
Collect New Data
          ↓
Train Candidate Model
          ↓
Evaluate Candidate
          ↓
Compare
     ↙          ↘
Better          Worse
 ↓                ↓
Deploy          Keep Current
24. Model Validation Before Deployment

A new model should pass validation checks before being deployed.

Checks may include:

Accuracy
Recall
Precision
F1
ROC-AUC
Data quality
Fairness
Stability
25. Model Rollback

Sometimes a newly deployed model may perform poorly.

Therefore, the previous model should be retained.

Example:

Production:
v2


New:
v3

If v3 fails:

Rollback
v3 → v2

This reduces operational risk.

26. Monitoring Dashboard

A production ML system can have a dashboard displaying:

-----------------------------------------
     Credit Risk Model Monitoring
-----------------------------------------


Model Version: v2


Predictions:
Good Risk     71%
Bad Risk      29%


Recall:
78%


Precision:
74%


F1 Score:
76%


Data Drift:
Low


Model Status:
Healthy
-----------------------------------------

This allows data scientists and engineers to quickly identify problems.

27. Alerting

Automated alerts can be configured when important thresholds are exceeded.

Example:

IF recall < 70%
    → Alert

or:

IF missing_value_rate > 5%
    → Alert

or:

IF data_drift_score > threshold
    → Alert
28. Health Checks

The deployed application should also have basic health checks.

For example:

Application Running?
        ↓
Model Loaded?
        ↓
Preprocessing Available?
        ↓
Prediction Working?

If one component fails, the problem should be detected quickly.

29. Monitoring Architecture

The overall architecture can be represented as:

                   User
                     ↓
              Streamlit App
                     ↓
              ML Prediction
                     ↓
        ┌────────────┴────────────┐
        ↓                         ↓
   Prediction                 Application
    Logging                    Logging
        ↓                         ↓
        └────────────┬────────────┘
                     ↓
               Monitoring
                     ↓
             Drift Detection
                     ↓
             Model Evaluation
                     ↓
              Retraining
                     ↓
              New Model
30. MLOps Lifecycle

The complete lifecycle is:

Plan
 ↓
Collect Data
 ↓
Prepare Data
 ↓
Train Model
 ↓
Evaluate Model
 ↓
Deploy
 ↓
Monitor
 ↓
Detect Drift
 ↓
Retrain
 ↓
Evaluate New Model
 ↓
Deploy Updated Model

This cycle continues throughout the model's lifetime.