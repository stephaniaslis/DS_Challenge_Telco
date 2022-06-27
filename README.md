# :heavy_check_mark:	Data Science Challenge 

This is the 1st Alura Data Science Challenge about Telco Churn classification. The goal is Churn prediction.

## Dataset
The dataset is in json format, and it is available in the following link:

https://raw.githubusercontent.com/stephaniaslis/DS_Challenge_Telco/main/Telco-Customer-Churn.json

## Data Cleaning
Data cleaning was made analysing the following steps:

- Useless columns
- Data kind definition
    - Null values
    - Missing Analysis (%)
        - Fill missings or not
- Duplicated column
- Duplicated rows
- Constant columns
- Feature Analysis
    - Outlier analysis
- Data export

The notebook is available here:

https://github.com/stephaniaslis/DS_Challenge_Telco/blob/3d93e2667009c74f946479027f15b232f9f06c18/Telco_Data_cleaning.ipynb

# EDA
The EDA was made using pandas profiling that generates an interactive report in html format:

![pandas_prof](https://user-images.githubusercontent.com/82055743/175558728-9ba552e9-dce1-4121-944d-c4d73b3c0408.png)

https://github.com/stephaniaslis/DS_Challenge_Telco/blob/main/report_telco.html

PS: The html is in localhost.

There was created reports to Churn 0 (negative Churn) and Churn 1 (positive Churn):

https://github.com/stephaniaslis/DS_Challenge_Telco/blob/main/report_telco_churn_0.html

https://github.com/stephaniaslis/DS_Challenge_Telco/blob/main/report_telco_churn_1.html

### Report conclusions in general
- The target (Churn) is imbalanced, the churn rate is 27%
- The gender distribution is almost 50% for male and female
- There are more customers:
    - under 65 years old
    - with phone service
    - without dependents
    - with montly contract
- Customer tenure is highly correlated with Account charges total

### Conclusions Churn = 0
- Mostly :
    - are under 65 years old
    - don't have dependents
    - have phone service
- Top 1 contract is month-to-month
- Customer tenure (average) : 37 months
- Account charges monthly (average): 61.30 US$
- Customer tenure is highly correlated with Account charges total

### Conclusions Churn = 1
- Mostly :
    - are under 65 years old
    - don´t have customer partner
    - don't have dependents
    - have phone service
    - have fiber optic internet
    - have internet Online Security
    - have internet OnlineBackup
    - have internet Device Protection
    - have internet TechSupport
    - have monthly contract
    - have Paperless Billing   
- Customer tenure (average) : 17 months
- Account charges monthly (average): 74.44 US$
- Customer tenure is highly correlated with Account charges total

The notebook is available here:

https://github.com/stephaniaslis/DS_Challenge_Telco/blob/3d93e2667009c74f946479027f15b232f9f06c18/Telco_EDA.ipynb

## Feature Selection
For feature selection, is used a majority voting method applying 3 selection proposals:

- Statistical test:
    - Anova for numeric features
    - Chi2 for categorical features
- RFECV
- Boruta

Features maintained by at least 2 selection proposals will be used in the modeling process.

The notebook is available here:

https://github.com/stephaniaslis/DS_Challenge_Telco/blob/3d93e2667009c74f946479027f15b232f9f06c18/Telco_feature_selection_.ipynb

## Model
This is a Churn prediction project, so the metric choosen to evaluate the model is Recall, because the risk of misidentifying false negatives is more serious than predicting false positives.

Firstofall, there was a train test split.

Smote were the balance method used for this dataset.

The models were ranked using pycaret:

![compare_model](https://user-images.githubusercontent.com/82055743/175561615-149d3401-3e29-4a32-a19a-896695ab92e1.png)

After that, the three best models were fitted and predictions were made with test dataset:

|   Model   | Accuracy | Recall  | Precision |
| --------- | -------- | ------- | --------- |
|  xgboost  |  0.7597  | 0.6346  |   0.541   |
|    ada    |  0.7564  | 0.7273  |   0.5306  |
| lightgbm  |  0.7725  | 0.6613  |   0.5613  |
| Baseline  |   0.73   |

The choosen model is AdaBoost because it is above the baseline and it has the best recall.

After that, the model was tuned using random grid search, tunnig the hyperparams:
- n_estimators
- learning_rate

### Model metrics:

|          | Accuracy | Recall  | Precision |
| -------- | -------- | ------- | --------- |
| Train    |  0.79    |   0.85  |   0.77    |
| Baseline |  0.73    |


Model confusion matrix:

![cm_model](https://user-images.githubusercontent.com/82055743/175562817-4cc9d996-a6d2-47bb-b2e4-70096c152f6e.png)

The most important feature in this model is customer tenure:

![feature_selection](https://user-images.githubusercontent.com/82055743/175562984-6d147115-95c8-4442-88b4-63ee1c428ae6.png)

### Test metrics

|          | Accuracy | Recall  | Precision |
| -------- | -------- | ------- | --------- |
| Test     |  0.75    |   0.77  |   0.52    |
| Baseline |  0.73    |

Test confusion matrix

![cm_test](https://user-images.githubusercontent.com/82055743/175563864-3a4664ca-d9a2-4d2f-9ba1-f95ef5771a51.png)

Classification report by class:

![class_report](https://user-images.githubusercontent.com/82055743/175564134-3b13e8ed-8e9a-45a7-849c-1a10a747f0b5.png)

Train and test comparison:

|          | Accuracy | Recall  | Precision |
| -------- | -------- | ------- | --------- |
| Train    |  0.79    |   0.85  |   0.77    |
| Test     |  0.75    |   0.77  |   0.52    |
| Baseline |  0.73    |

The notebook is available here:

https://github.com/stephaniaslis/DS_Challenge_Telco/blob/3d93e2667009c74f946479027f15b232f9f06c18/Telco_model.ipynb

## Conclusion
The accuracy is 0.75, considering that the test dataset is imbalanced (0.73 for class 0 and 0.27 for class 1) the model predicts a little bit better than the baseline.

As it shows the recall (sensitivity) in the test dataset is 0.77, wich means that in 100 predictions using this model 77 of positive class are correctly predicted and 23 are incorrectly.

Next steps: 
- colect more data to build a robuster model
- deployment




