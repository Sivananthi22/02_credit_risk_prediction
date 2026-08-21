🧩 Feature Engineering
German Credit Risk Prediction Project
1. Introduction

Feature engineering is the process of creating, transforming, selecting, or improving input variables so that Machine Learning models can learn useful patterns more effectively.

In simple terms:

Feature engineering converts raw information into useful signals for a Machine Learning model.

For example, a raw variable might be:

duration = 48 months

A more meaningful feature could be:

long_term_loan = 1

This can help a model understand that the loan has a relatively long repayment period.

2. Why Feature Engineering Matters

A Machine Learning model is only as useful as the information provided to it.

Consider:

Raw Data
   ↓
Features
   ↓
Machine Learning Model
   ↓
Prediction

If the features do not represent important patterns in the data, even a sophisticated model may perform poorly.

Good feature engineering can:

Improve predictive performance
Capture hidden relationships
Reduce unnecessary complexity
Improve model interpretability
Help models learn domain-specific patterns

3. Feature Engineering vs Data Preprocessing

These two concepts are related but different.

Data Preprocessing

Prepares existing data for Machine Learning.

Examples:

Encoding
Scaling
Missing-value handling
Train-test splitting
Feature Engineering

Creates or transforms features to make them more informative.

Examples:

Creating loan categories
Creating income-to-loan ratios
Grouping age
Creating financial stability indicators
4. Feature Engineering in Credit Risk

Credit risk depends on several aspects of a customer's financial situation.

Important concepts include:

Ability to repay
Financial stability
Previous credit behavior
Loan size
Loan duration
Existing financial obligations

Feature engineering can help represent these concepts more explicitly.

5. Existing Features

The German Credit dataset contains features such as:

Age
Credit Amount
Duration
Credit History
Checking Account
Savings Account
Employment Duration
Housing
Number of Credits

These are already useful predictors.

However, relationships between them may contain additional information.

6. Feature Engineering Strategy

Feature engineering should be based on:

Domain knowledge
EDA findings
Model behavior
Business logic

It should not simply involve creating as many features as possible.

Too many unnecessary features can:

Increase complexity
Introduce noise
Increase overfitting
Reduce interpretability
7. Loan Duration Categories

The original feature:

duration

contains the number of months.

We can create:

loan_duration_category

For example:

Short
Medium
Long

A possible categorization:

≤ 12 months → Short
13–36 months → Medium
> 36 months → Long

The exact thresholds should be justified using EDA and domain knowledge.


8. Why Create Duration Categories?

A numerical model sees:

12
24
36
48
60

A categorical feature allows us to explicitly represent:

Short
Medium
Long

This can make certain nonlinear relationships easier for some models to learn.

9. Credit Amount Categories

The original:

credit_amount

can potentially be transformed into categories.

For example:

Low
Medium
High

However, categories should not automatically replace the original numerical feature.

We can initially retain:

credit_amount

and create an additional feature.

10. Age Groups

Age is currently numerical.

We could create:

age_group

For example:

Young
Adult
Middle-aged
Older

Possible implementation:

df['age_group'] = pd.cut(
    df['age'],
    bins=[0, 25, 35, 50, 100],
    labels=[
        'young',
        'adult',
        'middle_aged',
        'older'
    ]
)

The exact bins should be evaluated carefully.

11. Why Age Groups Can Help

The relationship between age and credit risk may not be linear.

For example:

Age
 ↓
Risk

may behave differently across age ranges.

Age grouping can expose possible nonlinear patterns.

However, tree-based models can already learn many nonlinear relationships, so this feature should be validated experimentally.

12. Credit History Grouping

Credit history is likely to be one of the most important variables.

It represents previous financial behavior.

We can investigate whether categories can be grouped into broader concepts such as:

Good History
Poor History
No/Weak History

This can simplify interpretation.

However, we should preserve the original information unless EDA shows that grouping is beneficial.

13. Financial Stability Features

Financial stability is an important concept in credit risk.

Possible indicators include:

Checking account status
Savings account status
Employment duration
Housing status

These can potentially be combined into a broader concept such as:

financial_stability_score
14. Example Financial Stability Score

A simple experimental score could assign points for indicators such as:

Stable checking account → +1
Strong savings → +1
Long employment → +1
Own housing → +1

Then:

0 → Low Stability
1–2 → Moderate Stability
3–4 → High Stability

This is only an example.

In a real financial system, such scoring rules would need strong domain validation.

15. Loan Burden Features

Loan duration and credit amount together may provide more information than either feature independently.

For example:

credit_amount
+
duration

can represent the size and length of the financial obligation.

One possible derived feature is:

credit_amount_per_month

For example:

df['credit_amount_per_month'] = (
    df['credit_amount'] / df['duration']
)

This is a simplified indicator of monthly loan burden.

It should not be interpreted as the actual monthly repayment because interest and repayment structure are not represented.

16. Why Interaction Features Matter

Consider two customers:

Customer A
Credit Amount = 5000
Duration = 12
Customer B
Credit Amount = 5000
Duration = 60

Both have the same loan amount.

But their repayment periods are very different.

Feature engineering can help the model capture relationships between:

Loan Amount
+
Loan Duration
17. Existing Credit Burden

The dataset contains:

number_credits

This represents the number of existing credits.

A customer with multiple existing credits may have a different risk profile from a customer with no previous credits.

Potential derived feature:

multiple_existing_credits

For example:

df['multiple_existing_credits'] = (
    df['number_credits'] > 1
).astype(int)
18. Dependents

The dataset contains:

people_liable

This represents the number of people financially dependent on the customer.

A potential feature could be:

has_dependents

Example:

df['has_dependents'] = (
    df['people_liable'] > 1
).astype(int)

Again, the threshold should be validated rather than assumed.

19. Employment Stability

Employment duration can potentially be transformed into a stability indicator.

For example:

short employment
medium employment
long employment

This may help the model capture the difference between:

Recently employed

and:

Long-term employment
20. Savings and Checking Account Interaction

A customer's checking account and savings account provide related financial information.

We can investigate whether their combination provides additional predictive information.

For example:

Strong Savings + Good Checking
        ↓
Potentially Stronger Financial Position

while:

Low Savings + Poor Checking
        ↓
Potentially Higher Financial Risk

This should be tested empirically.

21. Feature Interaction

Feature interaction occurs when the effect of one variable depends on another variable.

Example:

Credit Amount
      +
Duration
      ↓
Loan Burden

Another example:

Employment Stability
      +
Credit History
      ↓
Financial Stability

Tree-based algorithms such as Random Forest and XGBoost can naturally learn many interactions.

Therefore, manually creating interaction features is optional and should be validated.

22. Feature Transformation

Sometimes a variable's distribution can be transformed.

For example:

credit_amount

was observed during EDA to be right-skewed.

A logarithmic transformation can reduce skewness.

Example:

df['log_credit_amount'] = np.log1p(
    df['credit_amount']
)
23. Why log1p()?

log1p(x) calculates:

log(1 + x)

It is often safer than directly applying:

np.log(x)

when zero values may exist.

24. Should We Always Transform Skewed Features?

No.

Transformation should depend on the model.

For example:

Logistic Regression

May benefit from transformed numerical variables when distributions are highly skewed.

Decision Tree

Usually does not require such transformations.

Random Forest

Usually does not require them.

XGBoost

Generally handles skewed numerical features well.

Therefore, transformations should be evaluated experimentally.

25. Feature Selection

Feature engineering is also connected to feature selection.

Feature selection means identifying the most useful variables and removing unnecessary ones.

Possible techniques include:

Correlation analysis
Mutual information
Model-based importance
Recursive Feature Elimination
SHAP analysis
26. Why Feature Selection Matters

Too many irrelevant variables can:

Add noise
Increase model complexity
Increase training time
Increase overfitting risk

A smaller set of meaningful features can sometimes produce a simpler and more interpretable model.

27. Avoiding Data Leakage in Feature Engineering

This is extremely important.

Feature engineering must not use information that would be unavailable at prediction time.

For example, suppose we create:

customer_defaulted

using information that only became known after the loan was issued.

That feature cannot be used to predict whether the customer will default before the loan is approved.

This would be:

Data Leakage
28. Train-Test Considerations

Feature engineering should respect the train-test boundary.

For transformations that learn information from the data, such as:

Scaling
Imputation
Statistical encoding

the transformation should be fitted on training data only.

Then:

Training Data
      ↓
Fit Transformation
      ↓
Training + Testing

The testing set should not influence the learned transformation.

29. Feature Engineering Pipeline

A professional pipeline can look like:

Raw Data
   ↓
Data Validation
   ↓
Basic Cleaning
   ↓
Feature Creation
   ↓
Categorical Encoding
   ↓
Numerical Transformation
   ↓
Feature Selection
   ↓
Model Training
30. Feature Engineering Experiments

Instead of creating every possible feature, we can compare experiments.

Experiment 1

Original features only.

Experiment 2

Original features + duration categories.

Experiment 3

Original features + loan burden features.

Experiment 4

Original features + selected interaction features.

Then compare:

Accuracy
Precision
Recall
F1
ROC-AUC
31. Baseline vs Engineered Features

Suppose:

Experiment	Recall	F1	ROC-AUC
Original Features	0.70	0.68	0.76
Engineered Features	0.75	0.73	0.80

The engineered feature set appears more useful.

However, the improvement must be validated using proper cross-validation.

32. Feature Engineering and Interpretability

Good feature engineering can make models easier to explain.

For example:

Instead of only:

duration = 48

we could also have:

loan_duration_category = Long

This may make the business interpretation more intuitive.

33. Feature Engineering and Business Knowledge

Machine Learning should not be treated as purely mathematical.

Domain knowledge is extremely important.

For credit risk, we should think about:

Ability to repay
Existing obligations
Financial stability
Credit history
Loan size
Loan duration

Features should represent these concepts where possible.

34. Feature Audit

Before using engineered features, each feature should be reviewed.

Questions:

Is the feature available at prediction time?
Does it contain leakage?
Does it have meaningful business interpretation?
Does it improve model performance?
Does it create excessive complexity?
Is it fair and appropriate?
35. Recommended Features to Investigate

For this project, we can experiment with:

1. loan_duration_category
2. age_group
3. credit_amount_per_month
4. multiple_existing_credits
5. has_dependents
6. employment_stability
7. financial_stability_score
8. log_credit_amount

These should be treated as experimental features, not automatically included in the final model.