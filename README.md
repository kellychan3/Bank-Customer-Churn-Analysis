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
<img width="1413" height="460" alt="image" src="https://github.com/user-attachments/assets/5c6936b2-96b1-416d-8ec6-dec22219eb66" />

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
<img width="554" height="432" alt="image" src="https://github.com/user-attachments/assets/78953661-3110-41fd-ba14-fa0634c9383b" />

Correlations:
<img width="1232" height="1304" alt="image" src="https://github.com/user-attachments/assets/1c87117e-86d5-4323-9d40-2c9e58b4b647" />
<img width="2989" height="2990" alt="image" src="https://github.com/user-attachments/assets/8bbc76f7-87a3-4ec5-a5c1-c858a6a07047" />

- Age positively correlates with churn (0.29).
- Active members less likely to churn (-0.16).
- Geography influences churn (Germany higher).
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
<img width="548" height="492" alt="image" src="https://github.com/user-attachments/assets/c94ec70f-1a1a-487f-a328-652e6770a939" />

- True Negative: 2520
- True Positive: 255
- False Negative: 428
- False Positive: 97

Classification Report:
<img width="630" height="211" alt="image" src="https://github.com/user-attachments/assets/e867901f-6287-44ee-82c5-34039386ba9d" />

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
