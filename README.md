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

### Logistic Regression

### Random Forest

### XGBoost
