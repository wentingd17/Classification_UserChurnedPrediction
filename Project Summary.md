# Prediction: Credit Card Churned
Wenting Deng

##Abstract
The goal of this project was to predict credit card holders who are likely to churn, in order to help the credit card company identify the targets they would like to reach out to with the 0% APR offers, thus to improve customer retentions. The data I worked with was a [Kaggle dataset](https://www.kaggle.com/sakshigoyal7/credit-card-customers). This dataset contains 10,127 unique customers, and the features include demographic information and the credit card usage information. This is an imbalanced data with 16% customers who have churned. The final model was built by using XGBoost, and it was able to achieve a 0.89 F2 score and a 0.99 AUC score.

##Design
In order to improve the credit card company's retention rate, the company needs to pay attentions to customers who are likely to churn in the near future. Sending them 0% APR offers of X months would be a good business solution. In this project, I'm focusing on building a classification model to predict the likelihood of being churned based on the customer portfolio data. The 0% APR of X months offer design is not covered in this project given the additional data are needed.

##Data
The data came from [Kaggle](https://www.kaggle.com/sakshigoyal7/credit-card-customers), which contains 10,127 unique customers and 23 original features. The features include demographic information such as gender, age, education, and number of dependents etc. And it also includes credit card usage information such as the current balance, credit limit, utilization ratio etc. The target variable is a binary feature "Attrition_Flag" which has "Existing Customer" and "Attrited Customer".

##Algorithms
**Feature Engineering**
1. Remove credit_limit and open_to_buy, because they can be represented by total_balance and utilization_ratio;
2. Create two additional binary features: inactive_12_month_flag (whether the customer was inactive in the past 12 months) and contacts_12_month_flag (whether we contacted the customer in past 12 months)
3. Convert categorical variables into dummies.

**Model Evaluation and Selection**
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

**Model Test by Demographic Segments**
Because this model uses demographic data, test the model by segments to evaluation demographic related bias would be important.

Test the model by gender groups as one example:

| Metrics | Male | Female |
| --- | --- | --- |
| F2 Score | 0.95 | 0.92 |
| Recall | 0.95 | 0.93 |
| Precision | 0.92 | 0.90 |

**Feature Importance**
Feature importance is calculate by information gain.

<img src="plots/feature importance.png" width=500>

**Tools**
* Numpy and Pandas for data manipulation
* Scikit-learn and XGBoost for model evaluation and selection
* Matplotlib and Seaborn for visualization

## Communication
In addition to the slides and visuals presented, it will be embedded on my analytic blog.
