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

<img src="https://github.com/StefanatouGerasimina/BankCustomer_ChurnPrediction/blob/main/result_images/feature_correlation.png" width="400" height="350">

Feature correlation matrix provides a comprehensive view of the relationships between variables in our dataset.  By examining the matrix, we can can find which features strongly related and gain important information about the bank's customers.

In more detail, as we can see from the matrix above, the feature that are quite related to the label ("Exited"), are the Age, the Tenure and the IsActiveMember. While features related to each other, except from the label feature, is the Balance and the NumOfProducts.

First lets take a look to the Categorical Data:

### Customers & Region
<img src="https://github.com/StefanatouGerasimina/BankCustomer_ChurnPrediction/blob/main/result_images/customers_region_piechart.png" width="400" height="280">

The Region did not appear to have ane value for the label, but informationally we can see that the highest percentage of the customers came from France. While the other 50% appears to be almost equally devided to both Spain and Germany .

### Customers & Gender

<img src="https://github.com/StefanatouGerasimina/BankCustomer_ChurnPrediction/blob/main/result_images/customers_gender_piechart.png" width="400" height="280">

it seems that our data is almost equally divided in terms of gender.

### Customers & AgeRange

<img src="https://github.com/StefanatouGerasimina/BankCustomer_ChurnPrediction/blob/main/result_images/customers_age_piechart.png" width="400" height="280">

The bigest percentage of the customers dataset belongs to the Age range between 31 and 45. The smallest percentage of customers are underage while the next smallest category describes the customers in the age range of 61-100.


### Exited & AgeRange

<img src="https://github.com/StefanatouGerasimina/BankCustomer_ChurnPrediction/blob/main/result_images/exited_age.png" width="400" height="280">

The chart reveals a distinct pattern: the age category of 19-30 exhibits the lowest percentage of customers who have chosen to discontinue their relationship with the bank. Subsequently, the age groups of 0-18 and 61-100 also display relatively lower attrition rates. In contrast, the category spanning ages 46-60 ranks last in terms of customer retention. This diagram though, does not show any detail based on the total percentage of the customers. That's why we plot the diagram bellow.

### Exited & AgeRange based on total sum of customers

<img src="https://github.com/StefanatouGerasimina/BankCustomer_ChurnPrediction/blob/main/result_images/fprob_exited_age.png" width="400" height="280">

The figure suggests that the highest percentage of customers leaving the bank falls within the age category of 46-60, followed by the 61-100 age group, then the 31-45 age group, and finally the 0-18 and 19-30 age groups. However, when considering the overall percentage of customers leaving in our dataset, we observe a different pattern. The largest percentage of customers leaving the bank belongs to the 31-45 age group, with 9.32% of customers in this category leaving. Following closely behind is the 46-60 age group. This indicates a departure from the age distribution in the dataset.

## Smote Analysis

I chose to perform Synthetic Minority Over-sampling Technique (SMOTE) analysis in my research because it is a valuable method for addressing class imbalance in datasets. SMOTE works by generating synthetic instances of the minority class to balance the dataset, thereby improving the performance of machine learning models. By creating new data points that resemble existing minority class samples, SMOTE helps prevent models from being biased toward the majority class and enhances their ability to accurately classify rare events or minority class instances.


Before applying smote analysis, we need to standarize our data; And in order to do that, we need to split the categorical and the numerical features.

Categorical Features:
- Geography
- Gender

For these categorical features, we use LabelEncoder by sklearn preprocessing library, which is a way of converting categorical data to numerical values. For every feature and for each category within a categorical variable, you assign a unique integer label, in ascending order. For the geography variable we can have 3 possible values, while for hender only two. This means that for the Geography features the possible values will be 0,1,2 while for the gender 0 and 1.
For the numerical data, I used standar scaler, which in general transforms feature values to have a mean of 0 and a standard deviation of 1.
Other possible transformation whould be the one hot encoding one for the categorical data with the standar scaler for the numerical data.

As soon as the transforming and their combination is done, we move on to the smote analysis, to minimize the problem of the high difference between classes of the output label.

Before the smote analysis, the sum of values for each label where: 


{1: 2037, 0: 7963}


While after the smote analysis, we have a more balanced dataset:


{0: 6356, 1: 6356}


## Model Training & Evaluation


First of all, before applying any of the algorithms mentioned bellow, we split the dataset into train and test randomly.

### Logistic Regression

Logistic regression works by modeling the relationship between a binary dependent variable (in this case, whether a customer churns or not) and a set of independent predictor variables (such as customer demographics, transaction history, account status, etc.) using a logistic function. This function maps the input variables to the probability of the binary outcome, ensuring that the predicted probabilities are between 0 and 1. It's a good fit for customer churn prediction because it's designed for binary classification tasks and provides clear insights into the probability of a customer churning. Additionally, it handles both categorical and numerical features, making it versatile for the heterogeneous data often present in customer churn datasets. The simplicity of the model makes it interpretable, allowing banks to understand which factors influence customer churn, and it can serve as a foundation for more complex models or as a benchmark to evaluate their performance.

In this specific example I used Logistic regression with 100 number of epocs. 
The results were:

- Train Acc (Logistic Regression): 0.7082
- Test Acc (Logistic Regression): 0.7135
- Test Acc Oversampled (Logistic Regression): 0.7135

We can see a stability between train accuracy and test accuracy, which may hide a avoidance of the overfitting. Lets see ...

<img src="https://github.com/StefanatouGerasimina/BankCustomer_ChurnPrediction/blob/main/result_images/feature_correlation_matrix_lr.png" width="400" height="280">

From the confusion matrix above, We can see that the percentage of the customers that stayed found to stay at a high propability rate, While the model seems to not doing good for the exited class, as there is a high percentage of variables found as 1 when they were truly 0.

- True Negatives (TN): 1158 (correctly labeled as about to leave/exit the bank)
- False Positives (FP): 449 (falsly labeled as about to stay in the bank)
- False Negatives (FN): 124 (falsy labeled as about to leave/exit the bank)
- True Positives (TP): 269 (corectly labeled as about to stay in the bank)

As we can see from the above mention bullet points, we have a rate of 449 false positives, which means that the model did found 449 people as "about to stay" where they ere actually belloging to the class of 0 ("about to exit the bank/ exited").

### Random Forest

Random Forest combines the strength of multiple decision trees to make accurate and robust predictions. Each tree in the forest is constructed using a random subset of the data and features, reducing the risk of overfitting and improving generalization to new data. This ensemble approach allows Random Forest to capture complex relationships and interactions between various customer attributes that might influence churn. Furthermore, it can handle both categorical and numerical features, making it suitable for customer churn prediction, which often involves diverse data types. With its inherent feature importance analysis, Random Forest can also provide insights into which factors are most influential in driving customer churn. Overall, Random Forest's ability to handle noisy and high-dimensional data while providing interpretable results makes it a well-suited choice for predicting and understanding customer churn in a business context.

The results seems to be a litle better than the logistic regression, for both train and test accuracy:

- Train Acc (Random Forest): 0.7629
- Test Acc (Random Forest): 0.7620
- Test Acc Oversampled (Random Forest): 0.7620

We can see the results of the confusion matrix here:

<img src="https://github.com/StefanatouGerasimina/BankCustomer_ChurnPrediction/blob/main/result_images/feature_correlation_matrix_rf.png" width="400" height="280">

- True Negatives (TN): 1246
- False Positives (FP): 361
- False Negatives (FN): 115
- True Positives (TP): 278

From the results mentioned above, both true negative and false positive performed much better than the logistic regression. The True Negatives are higher and the false Positives, lower.


### XGBoost

XGBoost, or Extreme Gradient Boosting, is an exceptionally effective and popular machine learning algorithm for churn prediction tasks. Its widespread adoption is attributed to its outstanding predictive performance and robustness. XGBoost is particularly well-suited for churn prediction due to several key strengths. It excels at handling imbalanced datasets, which are common in churn analysis, by assigning higher penalties to misclassifying the minority class, making it sensitive to capturing churn cases. Additionally, XGBoost employs an ensemble of decision trees, sequentially correcting errors made by the preceding trees, which allows it to capture intricate patterns and relationships in complex customer data. Its support for handling both numerical and categorical features, its inherent feature selection capabilities, and the flexibility to fine-tune hyperparameters make it a versatile choice for optimizing churn prediction models. Furthermore, XGBoost's efficiency in training and prediction enables it to scale well to large datasets, which is essential in real-world business applications. Altogether, XGBoost's exceptional predictive power and adaptability make it a compelling choice for addressing the critical task of customer churn prediction.

The results of the xgboost clasifier are:

- Train Acc (Logistic Regression): 0.9607
- Test Acc (Logistic Regression): 0.8535
- Test Acc Oversampled (Logistic Regression): 0.8535

The results seem a lot better and much higher for bith train ans test cases, than the resukts of the previous algorithms.

<img src="https://github.com/StefanatouGerasimina/BankCustomer_ChurnPrediction/blob/main/result_images/feature_correlation_matrix_xgb.png" width="400" height="280">

- True Negatives (TN): 1481
- False Positives (FP): 126
- False Negatives (FN): 167
- True Positives (TP): 226
