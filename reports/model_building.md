🤖 Model Building Report
German Credit Risk Prediction Project
1. Introduction

After completing:

Data Understanding
Exploratory Data Analysis (EDA)
Data Preprocessing

the dataset is now ready for Machine Learning model development.

The objective of this phase is to train multiple classification models and determine which model performs best at predicting customer credit risk.

2. Machine Learning Objective

The objective is to learn a relationship between customer characteristics and credit risk.

The model receives information such as:

Credit history
Credit amount
Loan duration
Age
Employment duration
Savings account
Checking account
Housing
Other financial information

and predicts:

Good Credit Risk
        OR
Bad Credit Risk

3. Type of Machine Learning Problem

This project is a:

Supervised Learning Problem

because the dataset contains both:

Input features
Known target labels

The specific task is:

Binary Classification

because there are two possible outcomes:

0 → Good Credit Risk
1 → Bad Credit Risk
4. What is Model Training?

Model training is the process of allowing a machine learning algorithm to learn patterns from historical data.

The training process can be represented as:

Training Data
     ↓
Machine Learning Algorithm
     ↓
Learn Patterns
     ↓
Trained Model

The trained model can then be used to make predictions on previously unseen customers.

5. Training and Testing Data

During preprocessing, the dataset was divided into:

80% → Training Data
20% → Testing Data
Training Data

Used to teach the model.

Testing Data

Used to evaluate how well the model performs on unseen data.

This separation is important because a model should generalize beyond the examples it has already seen.

6. Why Multiple Models?

There is no single machine learning algorithm that is always the best.

Different algorithms learn patterns differently.

Therefore, several models will be trained and compared.

The models selected for this project are:

Logistic Regression
Decision Tree
Random Forest
XGBoost
7. Model 1 – Logistic Regression
What is Logistic Regression?

Logistic Regression is a statistical and machine learning algorithm commonly used for binary classification.

Despite its name, Logistic Regression is a classification algorithm, not a regression algorithm.

It estimates the probability that an observation belongs to a particular class.

For this project:

Customer Information
        ↓
Logistic Regression
        ↓
Probability of Bad Credit Risk
        ↓
Class Prediction

8. Logistic Regression Probability

Logistic Regression uses the logistic function to convert a linear combination of features into a probability.

The probability is represented between:

0 and 1

A threshold is then used to determine the final class.

For example:

Probability = 0.20
→ Good Risk

Probability = 0.80
→ Bad Risk

The default classification threshold is commonly:

0.5
9. Advantages of Logistic Regression

Advantages:

Simple
Fast
Easy to interpret
Provides probabilities
Good baseline model
10. Limitations of Logistic Regression

Limitations:

Assumes a linear relationship between features and log-odds
May not capture complex nonlinear relationships
Can be affected by multicollinearity

Therefore, it will mainly serve as a baseline model.

11. Model 2 – Decision Tree
What is a Decision Tree?

A Decision Tree makes predictions by repeatedly splitting the dataset according to feature conditions.

Conceptually:

Credit History?
       |
   ┌───┴────┐
  Good     Poor
   |         |
Loan      Checking
Amount?   Account?

The tree continues splitting until it reaches a final prediction.

12. Example

A simplified credit decision tree could work like:

Is credit history good?
        |
      No
        ↓
Is loan duration high?
        |
      Yes
        ↓
Bad Credit Risk

The actual trained tree will contain many more conditions.

13. Advantages of Decision Trees
Easy to understand
Can capture nonlinear relationships
Handles numerical and categorical patterns
Does not require feature scaling
14. Limitations of Decision Trees

A Decision Tree can easily overfit the training data.

Overfitting occurs when the model learns the training data too closely and performs poorly on unseen data.

To control this, parameters such as:

max_depth
min_samples_split
min_samples_leaf

can be used.

15. Model 3 – Random Forest
What is Random Forest?

Random Forest is an ensemble learning algorithm.

Instead of using one Decision Tree, Random Forest creates many Decision Trees.

Conceptually:

              Dataset
                 |
       ┌─────────┼─────────┐
       ↓         ↓         ↓
    Tree 1    Tree 2    Tree 3
       ↓         ↓         ↓
    Good       Bad       Good
       \         |         /
        \        |        /
         Final Prediction

The individual trees vote on the final classification.