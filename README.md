# Prediction: Credit Card Churned

## Abstract
The goal of this project was to predict credit card holders who are likely to churn, in order to help the credit card company identify the targets they would like to reach out to with the 0% APR offers, thus to improve customer retentions. The data I worked with was a [Kaggle dataset](https://www.kaggle.com/sakshigoyal7/credit-card-customers). This dataset contains 10,127 unique customers, and the features include demographic information and the credit card usage information. This is an imbalanced data with 16% customers who have churned. The final model was built by using XGBoost, and it was able to achieve a 0.89 F2 score and a 0.99 AUC score.

## Data
The data came from [Kaggle](https://www.kaggle.com/sakshigoyal7/credit-card-customers), which contains 10,127 unique customers and 23 original features. The features include demographic information such as gender, age, education, and number of dependents etc. And it also includes credit card usage information such as the current balance, credit limit, utilization ratio etc. The target variable is a binary feature "Attrition_Flag" which has "Existing Customer" and "Attrited Customer".

## Model Evaluation and Selection
The entire dataset of 10,127 observations were randomly split into a train, test and validation dataset by 60/20/20/. The 5-fold cross validation were leveraged for feature selection and model evaluation. And GridSearch was applied to help with hyper-parameters test, especially in Random Forest.
Link to the business needs, F2 score was chosen as the key performance metric. As we need the model to be sensitive to churned customers, and also we need to look at precision as we need to control the cost of the 0% APR offers.

**5-fold cross validation on the 3 models**
3 types of models were built: Logistic Regression, Random Forest and XGBoost

| Model| F2 Score | Recall | Precision |
| --- | --- | --- | --- |
| Logistic Regression | 0.73 | 0.83 | 0.49 |
| Random Forest | 0.89 | 0.91 | 0.83 |
| XGBoost | 0.90 | 0.91 | 0.87 |

XGBoost was selected as the final model based on F2 score.

**Testing on Validation Data**
| Metrics | Test | Validation |
| --- | --- | --- |
| F2 Score | 0.90 | 0.89 |
| Recall | 0.91 | 0.89 |
| Precision | 0.87 | 0.90 |

**Tools**
* Numpy and Pandas for data manipulation
* Scikit-learn and XGBoost for model evaluation and selection
* Matplotlib and Seaborn for visualization
