# BankCustomer_ChurnPrediction


It is the dataset of a U.S. bank customer for getting the information that , this particular customer will leave bank or not. You can find it from Kaggle here: https://www.kaggle.com/datasets/shantanudhakadd/bank-customer-churn-prediction.

**Features:**

- CreditScore: Credit Score of customer.
- Geography: Location of customer.
- Gender: Gender whether male or female.
- Age: Age of Customer.
- Tenure: From how many years customer is in bank.
- Balance: Average balance of customer.
- NumOfProducts: Number of bank product facilities customer is using

**Features and types**

<img src="https://github.com/StefanatouGerasimina/BankCustomer_ChurnPrediction/blob/main/result_images/features_types.png" width="200" height="180">

As I can see from the array above, the continuous values are indeed of int or float type. Only the features that describe a category such as the Geography location and the gender, are of type object. Therefore, no data transformation is needed yet.


## Exploratory Data Analysis (EDA)

### Feature Corellation Analysis

<img src="https://github.com/StefanatouGerasimina/BankCustomer_ChurnPrediction/blob/main/result_images/feature_correlation.png" width="200" height="200">

Feature correlation matrix provides a comprehensive view of the relationships between variables in our dataset.  By examining the matrix, we can can find which features strongly related and gain important information about the bank's customers.

In more detail, as we can see from the matrix above, the feature that are quite related to the label ("Exited"), are the Age, the Tenure and the IsActiveMember. While features related to each other, except from the label feature, is the Balance and the NumOfProducts.

First lets take a look to the Categorical Data:

### Customers & Region

### Customers & Gender

### Customers & AgeRange

### Exited & AgeRange

### Exited & AgeRange based on total sum of customers

## Smote Analysis


## Model Training & Evaluation

### Logistic Regression

### Random Forest

### XGBoost
