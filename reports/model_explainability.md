🔍 Model Explainability Report
German Credit Risk Prediction Project
1. Introduction

Machine Learning models can make accurate predictions, but accuracy alone does not explain why a prediction was made.

For a credit risk system, this is especially important.

Suppose a model predicts:

Customer → Bad Credit Risk

A bank should be able to understand:

Why did the model classify this customer as risky?

This project therefore includes Explainable AI (XAI) techniques to understand the model's decisions.

2. What is Explainable AI?

Explainable Artificial Intelligence refers to techniques that help humans understand how an AI or Machine Learning model reaches its predictions.

Instead of treating the model as a black box:

Customer Data
      ↓
   Model
      ↓
Bad Risk

we want:

Customer Data
      ↓
   Model
      ↓
Bad Risk
      ↓
Why?
├── Poor Credit History
├── Long Loan Duration
├── Large Credit Amount
└── Low Savings
3. Why Explainability Matters in Credit Risk

Credit decisions can have significant financial consequences.

A customer may ask:

Why was my loan classified as high risk?

Financial institutions also need to understand whether the model is relying on sensible information.

Explainability can help with:

Trust
Model validation
Risk management
Debugging
Regulatory requirements
Business decision-making

4. Black-Box Models

Some machine learning models are difficult to interpret directly.

Examples:

Random Forest
XGBoost
Neural Networks

These models may contain hundreds or thousands of learned relationships.

It can therefore be difficult to manually understand why a particular prediction was made.

5. Explainability Techniques

Two techniques will be used in this project:

Feature Importance
SHAP
6. Feature Importance

Feature importance measures how influential each feature is in a model.

For example:

Feature	Importance
Credit History	0.25
Checking Account	0.20
Duration	0.15
Credit Amount	0.12
Savings Account	0.10

This suggests that Credit History has a stronger influence on the model than some other features.

7. Global Feature Importance

Global feature importance answers:

Which features are generally important across the entire dataset?

For example:

Credit History
      ↓
Very Important

Loan Duration
      ↓
Important

Credit Amount
      ↓
Important

This helps the business understand which customer characteristics are most useful for risk prediction.

8. Limitations of Basic Feature Importance

Feature importance provides an overall view, but it does not explain individual predictions.

For example:

Customer A → Bad Risk

Feature importance cannot necessarily tell us:

Why was Customer A classified as bad risk?

For individual explanations, SHAP is more useful.

9. What is SHAP?

SHAP stands for:

SHapley Additive exPlanations

SHAP is based on concepts from cooperative game theory.

The basic idea is to determine how much each feature contributes to a prediction.

10. Simple Explanation of SHAP

Imagine a model predicts:

Bad Risk Probability = 80%

SHAP can explain how different features moved the prediction toward or away from the bad-risk outcome.

For example:

Baseline Risk
     ↓
50%
     ↓
Poor Credit History
     +15%
     ↓
Long Duration
     +10%
     ↓
Large Credit Amount
     +8%
     ↓
Strong Employment
     -3%
     ↓
Final Prediction
80%

The exact values will depend on the trained model.

11. SHAP Baseline

SHAP explanations begin from a baseline prediction.

The baseline represents the model's typical prediction across the dataset.

Individual features then contribute positively or negatively relative to that baseline.

Conceptually:

Baseline Prediction
       +
Feature Contributions
       =
Individual Prediction
12. Positive and Negative Contributions

A feature can push a prediction toward:

Bad Risk

or:

Good Risk

For example:

Poor Credit History
        ↓
Pushes toward Bad Risk

while:

Stable Employment
        ↓
Pushes toward Good Risk

13. Global SHAP Analysis

Global SHAP analysis helps identify which features have the greatest influence across the entire dataset.

A SHAP summary plot can show:

Feature
   ↓
Credit History      ███████████
Checking Account    █████████
Duration            ███████
Credit Amount       ██████
Savings Account     █████
Age                 ███

The actual ranking will be determined after model training.

14. Individual Prediction Explanation

SHAP can also explain one specific customer.

Example:

Customer ID: Example Customer

Prediction:
Bad Credit Risk

Important Factors:

Credit History
→ Increased Risk

Loan Duration
→ Increased Risk

Credit Amount
→ Increased Risk

Savings
→ Reduced Risk

This provides a human-readable explanation of the prediction.

15. SHAP for Tree-Based Models

SHAP provides specialized explainers for tree-based models.

Examples:

Random Forest
XGBoost
Decision Tree

A TreeExplainer can be used for suitable tree-based models.

Conceptually:

explainer = shap.TreeExplainer(model)

Then SHAP values can be calculated for the data.

16. SHAP Workflow

The explainability workflow is:

Trained Model
      ↓
Create SHAP Explainer
      ↓
Calculate SHAP Values
      ↓
Global Explanation
      ↓
Individual Explanation
      ↓
Interpret Model Behavior
17. Global vs Local Explainability

There are two major types of explanations.

Global Explainability

Explains the model as a whole.

Question:

Which features generally influence predictions?

Local Explainability

Explains one prediction.

Question:

Why did the model make this prediction for this customer?

Both are useful.

18. Example Global Interpretation

Suppose SHAP analysis shows:

1. Credit History
2. Checking Account
3. Loan Duration
4. Credit Amount
5. Savings Account

This suggests that the model relies heavily on previous financial behavior and current financial circumstances.

19. Example Local Interpretation

Suppose a customer receives:

Bad Risk Probability = 0.82

SHAP may show:

Poor Credit History      → +0.20
Long Loan Duration       → +0.12
Large Credit Amount      → +0.08
Low Savings              → +0.06
Stable Employment        → -0.03

This indicates which characteristics pushed the prediction toward bad risk.

20. Explainability and Trust

Explainability increases confidence in a model because analysts can investigate whether the model is using reasonable patterns.

For example, if the model predicts high risk because of:

Poor credit history
Long repayment period
Large loan amount

the reasoning is financially understandable.

21. Explainability and Model Debugging

Explainability can also identify problems.

Suppose the model heavily depends on an unexpected variable.

For example:

Telephone Ownership

If it becomes one of the strongest predictors without a reasonable business explanation, this may require investigation.

Potential causes include:

Data artifacts
Hidden correlations
Sampling issues
Leakage
Proxy variables
22. Feature Importance vs SHAP
Feature Importance	SHAP
Global view	Global + Local
Easier to understand	More detailed
Shows overall importance	Shows direction and magnitude
Model-dependent	More flexible
Limited individual explanation	Strong individual explanations
23. Important Limitation

Explainability does not automatically mean that the model is correct.

A model can be:

Explainable
Consistent
Wrong

Therefore, explainability should be combined with:

Good evaluation
Domain knowledge
Data validation
Error analysis