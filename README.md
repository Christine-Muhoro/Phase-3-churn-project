# **SyriaTel Customer Churn Prediction**
## **Business Understanding**
### **Overview**
SyriaTel is a telecommunications company experiencing customer churn, where customers stop doing business with the company. Customer churn leads to significant revenue loss and reduced long-term profitability. Therefore, early identification of customer churns allows intervention with prevention of churn strategies.

This project aims to build a model that predicts churn and minimizes chances of missing a churn.

### **Objectives**
1. Develop a predictive model that classifies customers as likely to churn or not, allowing early churn prevention.
2. Identify factors(features) that highly influence a customer to churn.  
3. Minimize chance of missing a customer who will churn i.e False Negatives. Getting a Recall Score of 81%.  
4. Create a highly accurate model. Getting an Accuracy Score of 94%.  

## **Data Understanding**
The dataset used contains customer details, factors affecting churn and churn classification. The following are the columns contained in the dataset:
*Customer identification and Location* :   
* `state` -> state where customer lives.  
* `area code` -> telephone area code of customer's phone number.  
* `phone number` -> customer's phone number.  

`account length` -> number of days customr has used the telecommunication company.  
  
*Service Plans*   
* `international plan` -> Has customer subscribed to international calling plan?  
* `voice mail plan` -> Does customer have an active voicemail service?  
* ` Number vmail messages` -> Number of voicemail messages customer currently has.  

*Daytime Usage*, *Evening Usage*, *Night Usage*, *International Usage* each having:
* `total minutes` -> Total number of minutes used during a call at that specific day period.  
* `total calls` -> Total number of calls made at that specific day period.  
* `total charge` -> Total cost charged for the calls at that specific day period.  
`customer service calls` -> Number of times customer contacted customer service.  
  
`churn` -> Is cutomer expected to churn or not?  

### **Selecting Target and Features**
* `churn` is the target since it's what I'm predicting.  
* `phone number` is a unique identifier and `area code` gives little or weak geographical information i.e small area. Therefore these two don't affect customer churn.  
* ***total charge*** is derived from ***total minutes*** hence they are correlated. Since minutes will never change but charge rates may change and are the same for everyone, I'll not use ***total charge***.  
* The rest of the columns will be the features I'll use.  

## **Data Preprocessing**
First noted the categorical and numeric columns separately and split the data into training and test sets with 70:30 ratio.  
Next was checking for duplicated and missing values in both training and test sets and there were none.  
For both the training and test set separately, I handled numeric data using normalization and categric data using one hot encoding then combined the two back together.  
Also checked for class imbalance and balanced the classes using SMOTE.  

## **Objective 1 : Building the Classifier**
### Logistic Regression Model
Trained a baseline model for logistic regression with only random state of 42 as the parameter. This model had no overfitting and undeitting according to log loss. It also had a 76% recall and a 76% accuracy.  
Also tuned the previous logistic regression model with saga for solver, elasticnet for penalty and l1-ratio of 0.5 to control and balance L1 and L2 regularization. This model had a 77% recall and a 77% accuracy.   
### Decision Tree Classifier
Trained a baseline decision tree classifier with only random state of 42 as the parameter. This model had a 77% recall and a 91% accuracy.  
Tuned the above decision tree classifier with the best hyperparameters from a grid search cross-validation. This model had a 81% recall and a 94% accuracy.  
>From the above model training and testing, the best model so far according to both recall and accuracy is the tuned decision tree classifier.

## **Objective 2 : Features that Highly Influence Churn**
The best model so far being the tuned decision tree classifier, `feature_importances_` i.e feature importance values were taken. The highest values were used to indicate strongest influence features(factors) on churn.  
The features influencing churn greatly are `total anytime minutes`, `customer service calls` and `interational plan_yes`.  

## **Objective 3 : Best Recall Score i.e Minimize False Negatives(Missing a churning customer)**
Evaluated all the models created using accuracy, recall, precision scores and f1-score and created a table(dataframe) with these results.  
From the created table(dataframe), the recall score has been increasing as I create more models and the model with less false negative classification is the tuned decision tree with recall score of 81%. 

## **Objective 4 : Best Accuracy Score i.e Highly Accurate Model**
From the same created table(dataframe), the accuracy score has been increasing as I create more models and the highly accurate model is the tuned decision tree with an accuracy of 94%. 