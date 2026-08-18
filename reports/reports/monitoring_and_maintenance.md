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
