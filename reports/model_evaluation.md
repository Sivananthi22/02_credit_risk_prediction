📈 Model Evaluation Report
German Credit Risk Prediction Project
1. Introduction

Model evaluation is the process of measuring how well a trained machine learning model performs on unseen data.

In this project, the goal is not simply to find the model with the highest accuracy.

The main objective is to determine:

How reliably can the model identify customers who represent bad credit risk?

This is particularly important because incorrectly approving a high-risk customer can result in financial losses for a bank.

2. Why Model Evaluation is Important

A machine learning model can perform extremely well on training data but poorly on new data.

Therefore, evaluation helps us determine whether the model:

Generalizes to unseen data
Correctly identifies risky customers
Produces reliable predictions
Is suitable for the business problem

3. Training Performance vs Testing Performance

Two important concepts are:

Training Performance

Measures how well the model performs on data it has already seen.

Testing Performance

Measures how well the model performs on unseen data.

The testing performance is more important when estimating real-world performance.

4. Generalization

Generalization refers to the ability of a model to perform well on new, unseen observations.

A good machine learning model should learn general patterns rather than memorize the training dataset.

The desired behavior is:

Training Data
     ↓
Learn General Patterns
     ↓
Unseen Data
     ↓
Good Predictions
5. Overfitting

Overfitting occurs when a model learns the training data too closely.

Example:

Training Accuracy = 99%
Testing Accuracy = 70%

This suggests that the model may have memorized the training data instead of learning general patterns.

6. Underfitting

Underfitting occurs when the model is too simple to learn the important patterns in the data.

Example:

Training Accuracy = 65%
Testing Accuracy = 63%

The model may not have enough complexity to represent the underlying relationships.

7. Desired Model Behavior

A good model should achieve:

Strong training performance
Strong testing performance
Small generalization gap

For example:

Training Accuracy = 84%
Testing Accuracy = 82%

is generally more desirable than:

Training Accuracy = 99%
Testing Accuracy = 70%
8. Confusion Matrix

The confusion matrix is one of the most important tools for evaluating classification models.

For binary classification:


	Predicted Good	Predicted Bad
Actual Good	True Negative	False Positive
Actual Bad	False Negative	True Positive
9. True Positive

A True Positive occurs when:

Actual = Bad Risk
Prediction = Bad Risk

The model correctly identifies a risky customer.

This is important because the bank can take appropriate precautions.

10. True Negative

A True Negative occurs when:

Actual = Good Risk
Prediction = Good Risk

The model correctly identifies a low-risk customer.

11. False Positive

A False Positive occurs when:

Actual = Good Risk
Prediction = Bad Risk

The model incorrectly identifies a good customer as risky.

Business Impact

The bank may reject a customer who could have successfully repaid the loan.

12. False Negative

A False Negative occurs when:

Actual = Bad Risk
Prediction = Good Risk

This is particularly important in credit risk prediction.

Business Impact

The bank may approve a risky customer and potentially suffer a financial loss.

Therefore, reducing False Negatives can be an important business objective.

13. Accuracy

Accuracy measures the proportion of correct predictions.

Accuracy =
(TP + TN) / (TP + TN + FP + FN)

Example:

If the model correctly classifies 180 out of 200 customers:

Accuracy = 90%
14. Limitation of Accuracy

Accuracy can be misleading when classes are imbalanced.

Suppose:

Good Risk = 700
Bad Risk = 300

A model that predicts every customer as Good Risk would achieve:

Accuracy = 70%

but it would identify:

0% of Bad Risk customers

Therefore, accuracy alone is not sufficient.

15. Precision

Precision measures how many customers predicted as bad risk were actually bad risk.

Precision =
TP / (TP + FP)
Business Question

When the model says a customer is risky, how often is it correct?

High precision means fewer good customers are incorrectly classified as risky.

16. Recall

Recall measures how many actual bad-risk customers were correctly identified.

Recall =
TP / (TP + FN)
Business Question

Of all truly risky customers, how many did the model identify?

Recall is especially important for credit risk because missing a risky borrower can cause financial losses.

17. F1 Score

F1 Score combines Precision and Recall.

F1 Score =
2 × (Precision × Recall) /
(Precision + Recall)

F1 Score is useful when both false positives and false negatives matter.

A higher F1 Score indicates a better balance between Precision and Recall.

18. ROC Curve

The ROC curve shows the relationship between:

True Positive Rate
False Positive Rate

at different classification thresholds.

The ROC curve helps determine how effectively a model separates:

Good Risk

from:

Bad Risk
19. ROC-AUC

ROC-AUC represents the area under the ROC curve.

General interpretation:

ROC-AUC	Interpretation
0.50	Random
0.60–0.70	Weak
0.70–0.80	Acceptable
0.80–0.90	Strong
0.90–1.00	Excellent

These ranges are guidelines rather than strict rules.

20. Precision-Recall Relationship

There is often a trade-off between Precision and Recall.

Increasing the threshold may:

Increase Precision
Decrease Recall

Decreasing the threshold may:

Increase Recall
Decrease Precision

Therefore, the appropriate threshold depends on the business objective.

21. Credit Risk Perspective

For this project, the cost of different errors is not equal.

Consider:

False Positive

A good customer is incorrectly classified as risky.

Potential consequence:

Loan may be rejected
False Negative

A risky customer is incorrectly classified as good.

Potential consequence:

Loan may be approved
↓
Customer defaults
↓
Financial loss

Therefore, False Negatives may carry greater business risk.

22. Model Evaluation Strategy

The following models will be evaluated:

Logistic Regression
Decision Tree
Random Forest
XGBoost

Each model will be tested using the same test dataset.

23. Evaluation Metrics

The following metrics will be recorded:

Accuracy
Precision
Recall
F1 Score
ROC-AUC
24. Model Comparison

A comparison table will be created.

Model	Accuracy	Precision	Recall	F1 Score	ROC-AUC
Logistic Regression	-	-	-	-	-
Decision Tree	-	-	-	-	-
Random Forest	-	-	-	-	-
XGBoost	-	-	-	-	-

The actual values will be filled after model evaluation.