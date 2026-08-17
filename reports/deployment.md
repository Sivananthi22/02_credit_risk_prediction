🚀 Model Deployment Report
German Credit Risk Prediction Project
1. Introduction

Machine Learning does not end when a model is trained and evaluated.

A model becomes useful when it can be used to make predictions on new, unseen data.

This process is called:

Model Deployment

In this project, the trained credit risk model will be deployed as an interactive web application.

The application will allow a user to enter customer information and receive:

Credit risk prediction
Risk probability
Model explanation
2. What is Model Deployment?

Model deployment is the process of making a trained Machine Learning model available for real-world use.

The development process looks like:

Data
 ↓
Training
 ↓
Evaluation
 ↓
Best Model
 ↓
Deployment
 ↓
Real-World Predictions

3. Why Deployment is Important

A model inside a Jupyter Notebook is useful for experimentation, but it is not convenient for non-technical users.

For example, a bank employee should not need to open Python and run:

model.predict(customer_data)

Instead, they should be able to use a simple application.

For example:

Customer Information
        ↓
[ Predict Credit Risk ]
        ↓
Bad Credit Risk
Probability: 78%
4. Deployment Technology

The planned application will use:

Streamlit

Streamlit is a Python framework for creating interactive data science and machine learning applications.

It allows us to build a web interface without requiring extensive frontend development.

5. Why Streamlit?

Streamlit is suitable for this project because it:

Works directly with Python
Is easy to develop
Integrates well with Machine Learning models
Supports interactive inputs
Is suitable for demonstrations and prototypes
Can be deployed online
6. Deployment Architecture

The application will follow this architecture:

                 User
                  ↓
          Streamlit Application
                  ↓
       Customer Input Information
                  ↓
        Data Preprocessing Pipeline
                  ↓
          Trained ML Model
                  ↓
          Risk Probability
                  ↓
       Good / Bad Risk Prediction
                  ↓
         Explainable Prediction
7. User Input

The application will collect information about the customer.

Potential inputs include:

Checking Account Status
Loan Duration
Credit History
Loan Purpose
Credit Amount
Savings Account
Employment Duration
Installment Rate
Personal Status
Other Debtors
Present Residence
Property
Age
Other Installment Plans
Housing
Number of Credits
Job
Number of Dependents
Telephone
Foreign Worker Status

For numerical variables:

Age
[ 35 ]
Credit Amount
[ 5000 ]
Buttons
[ Predict Credit Risk ]
9. Prediction Workflow

When the user clicks the prediction button:

User Input
    ↓
Create DataFrame
    ↓
Apply Encoders
    ↓
Apply Scaler
    ↓
Pass Data to Model
    ↓
Generate Prediction
    ↓
Generate Probability
    ↓
Display Result
10. Why the Preprocessing Pipeline Must Be Reused

The model was trained using transformed data.

For example:

Categorical Data
      ↓
Encoding
      ↓
Numerical Data
      ↓
Scaling
      ↓
Model

The same transformations must be applied to new user data.

Otherwise, the model may receive data in a format different from what it learned during training.

11. Example

Suppose during training:

Housing = Own

was encoded as:

Own → 1

The application must apply the same encoding when a user selects:

Housing = Own

It must not create a different mapping.

12. Saving the Model

After selecting the final model, it should be saved to disk.

Possible file:

models/credit_risk_model.pkl

Python's joblib library can be used.

Example:

import joblib

joblib.dump(
    model,
    '../models/credit_risk_model.pkl'
)

14. Why Feature Order Matters

Suppose the model was trained using:

Age
Duration
Credit Amount

in a particular order.

If the application sends:

Credit Amount
Age
Duration

the model may interpret the values incorrectly.

Therefore, the feature order must remain consistent.

15. Prediction

The trained model can generate a class prediction.

Conceptually:

prediction = model.predict(input_data)

Possible output:

0

or:

1

where:

0 → Good Credit Risk
1 → Bad Credit Risk
16. Probability Prediction

Many classification models can also provide probabilities.

Example:

probability = model.predict_proba(input_data)

Possible output:

Good Risk = 0.22
Bad Risk = 0.78

The application can display:

Bad Risk Probability: 78%
17. Risk Categories

The application can provide a simple interpretation.

Example:

Probability < 30%
→ Low Risk

30% – 60%
→ Moderate Risk

> 60%
→ High Risk

These thresholds are illustrative and should not be treated as official financial decision thresholds.

In a real banking system, risk thresholds would need to be established using validated business, regulatory, and financial criteria.

18. Explainable Prediction

The application can also display the most influential factors.

For example:

Prediction: Bad Risk

Important Factors:

1. Poor Credit History
2. Long Loan Duration
3. High Credit Amount
4. Low Savings

This makes the application more useful than simply returning:

Bad Risk