# 🏦 Bank Customer Churn Data Analysis


**Table of Contents**

- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Model Building](#model-building)
- [Model Evaluation](#model-evaluation)
- [Conclusion](#conclusion)


## Project Overview

Predicting customer churn is crucial for banks to retain clients and optimize marketing strategies. This project builds an Artificial Neural Network (ANN) model to identify customers likely to leave the bank using demographics, account activity, and financial information.

## Dataset

The dataset Churn_Modelling.csv contains 10,000 customer records with 13 features, including demographic data, account activity, and financial status. The target variable Exited indicates whether a customer has left the bank (1) or remains (0).

Feature Description:
- CustomerId: Unique identifier for each customer.
- Surname: Customer’s last name.
- CreditScore: Customer’s credit score (higher values indicate better creditworthiness).
- Geography: Country of residence.
- Gender: Customer’s gender.
- Age: Customer’s age.
- Tenure: Number of years the customer has been with the bank.
- Balance: Account balance of the customer.
- NumOfProducts: Number of bank products the customer holds (e.g., savings, credit card, loan).
- HasCrCard: Indicates whether the customer has a credit card (1 = Yes, 0 = No).
- IsActiveMember: Indicates whether the customer is actively using bank services (1 = Active, 0 = Inactive).
- EstimatedSalary: Estimated annual income of the customer.
- Exited: Target variable: 1 = Customer has left the bank, 0 = Customer remains.

## Exploratory Data Analysis
Target distribution: 20% churned, 80% stayed → imbalanced dataset.

Correlations:
- Age positively correlates with churn (0.29).
- Active members less likely to churn (-0.16).
- Geography influences churn (Germany higher).
- Boxplots & histograms highlight distributions and key predictors.
- Identified strong predictors: Age, Balance, Geography.

## Model Building
Architecture:
- Input layer: 12 features
- Hidden layers: 2 layers × 6 neurons, ReLU activation
- Output layer: 1 neuron, Sigmoid activation
- Optimizer: Adam
- Loss function: Binary cross-entropy
- Training: 100 epochs, batch size = 10

## Model Evaluation
Accuracy: 84% on test set

Confusion Matrix:
- True Negative: 2520
- True Positive: 255
- False Negative: 428
- False Positive: 97

Classification Report:
- Precision, Recall, F1-score per class
- Class 0 (stayed): high recall (0.96)
- Class 1 (churn): low recall (0.37)

Insights: Model identifies non-churn customers well but struggles with churn prediction due to class imbalance.

## Conclusion
ANN performs reasonably well with overall accuracy of 84%.
Dataset imbalance affects the model’s ability to detect churners.

Future improvements:
- Apply oversampling (SMOTE) or class weighting.
- Test other models (Random Forest, XGBoost).
- Hyperparameter tuning and feature engineering.
