# 🏦 Bank Customer Churn Data Analysis


**Table of Contents**

- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Model Building](#model-building)
- [Model Evaluation](#model-evaluation)
- [Conclusion](#conclusion)


## Project Overview

Predicting customer churn is crucial for banks to retain clients and optimize marketing strategies. This project builds an **Artificial Neural Network (ANN)** model to identify customers likely to leave the bank using demographics, account activity, and financial information.

## Dataset

The dataset Churn_Modelling.csv contains 10,000 customer records with 13 features, including demographic data, account activity, and financial status. The target variable Exited indicates whether a customer has left the bank (1) or remains (0).
<img width="1413" height="460" alt="image" src="https://github.com/user-attachments/assets/5c6936b2-96b1-416d-8ec6-dec22219eb66" />

**Feature Description**:
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
**Target distribution**: 20% churned, 80% stayed → imbalanced dataset.
<img width="554" height="432" alt="image" src="https://github.com/user-attachments/assets/78953661-3110-41fd-ba14-fa0634c9383b" />

**Correlations**:
<img width="1232" height="1304" alt="image" src="https://github.com/user-attachments/assets/1c87117e-86d5-4323-9d40-2c9e58b4b647" />
<img width="2989" height="2990" alt="image" src="https://github.com/user-attachments/assets/8bbc76f7-87a3-4ec5-a5c1-c858a6a07047" />

- Age positively correlates with churn (0.29).
- Active members less likely to churn (-0.16).
- Geography influences churn (Germany higher).


## Model Building
**Base Model**: The base model was designed as a simple feedforward neural network to establish a performance baseline.
- Input layer: 12 features
- Architecture:
  - Dense(32, ReLU) → BatchNormalization → Dropout(0.3)
  - Dense(16, ReLU) → BatchNormalization → Dropout(0.3)
  - Dense(8, ReLU) → BatchNormalization
  - Output: Dense(1, Sigmoid)
- Optimizer: Adam (lr=0.001)
- Loss Function: Binary Crossentropyy
- EarlyStopping: Patience = 10
- Test Accuracy: 0.8600

**Optimized Model**: To improve performance, hyperparameter tuning was conducted using KerasTuner (Random Search).
- Tuned Parameters:
  - units_input: 16–64
  - units_hidden: 8–48
  - learning_rate: 1e-4 – 1e-2 (log scale)
- Best Configuration:
  - Dense(64, ReLU) → BatchNormalization → Dropout(0.3)
  - Dense(48, ReLU) → BatchNormalization → Dropout(0.3)
  - Output: Dense(1, Sigmoid)
  - Learning Rate: 0.000707
- Final Test Accuracy: 0.8570

-> The optimized model achieved similar accuracy to the baseline while using a more refined architecture and lower learning rate, indicating stable and efficient training.
  
## Model Evaluation
**Test Accuracy**: 86%

**Confusion Matrix**:
- True Negative (TN): 2456 — correctly predicted as staying
- True Positive (TP): 372 — correctly predicted as churn
- False Negative (FN): 311 — missed churn cases
- False Positive (FP): 161 — false churn predictions
<img width="643" height="491" alt="image" src="https://github.com/user-attachments/assets/c4225251-eca2-4ee9-b490-866cd215cc34" />

**Classification Report**:
- The model shows strong performance for non-churn customers (high recall and precision).
- Churn detection improved compared to the initial model but still shows moderate recall, indicating some missed churn cases.
- Class imbalance remains a factor — churners are underrepresented in the dataset.
<img width="656" height="202" alt="image" src="https://github.com/user-attachments/assets/e2888b55-7cea-4b10-b9ad-f807ebc4b9c6" />


## Conclusion
The optimized ANN achieved 86% test accuracy, showing solid predictive performance overall.
While it effectively identifies customers likely to stay, recall for churners (54%) suggests further improvement could be made through techniques like class rebalancing (SMOTE, weighting) or ensemble methods.
