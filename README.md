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
The dataset used contained the churn target and the following customer details and factors affecting churn that were used in the modeling process:  
* State where customer lives.  
* account length - number of days customer has used the telecommunication company.    
* international plan - Has customer subscribed to international calling plan?  
* voice mail plan - Does customer have an active voicemail service?  
* Number of voicemail messages customer currently has.  
* Daytime Usage, Evening Usage, Night Usage and International Usage each having total number of minutes and total number of calls.  
* Number of times customer contacted customer service.  
* churn - Is customer expected to churn or not? 


## **Data Preprocessing**
First noted the categorical and numeric columns separately and split the data into training and test sets with 70:30 ratio.  
Next was checking for duplicated and missing values in both training and test sets and there were none.  
For both the training and test set separately, I handled numeric data using normalization and categric data using one hot encoding then combined the two back together.  
Also checked for class imbalance and balanced the classes using SMOTE.  

## **Modeling and Evaluation**
### **Objective 1 : Building the Classifier**
#### **Logistic Regression Model**
Trained a baseline model for logistic regression with only random state of 42 as the parameter. This model had no overfitting and underfitting according to log loss. It also had a 76% recall and a 76% accuracy.  
Also tuned the previous logistic regression model with saga for solver, elasticnet for penalty and l1-ratio of 0.5 to control and balance L1 and L2 regularization. This model had a 77% recall and a 77% accuracy.   
#### **Decision Tree Classifier**
Trained a baseline decision tree classifier with only random state of 42 as the parameter. This model had a 77% recall and a 91% accuracy.  
Tuned the above decision tree classifier with the best hyperparameters from a grid search cross-validation. This model had a 81% recall and a 94% accuracy.  
>From the above model training and testing, the best model so far according to both recall and accuracy is the tuned decision tree classifier.

### **Objective 2 : Identify Features that Highly Influence Churn**
The best model so far being the tuned decision tree classifier, its highest feature importance values were displayed.
These highest values indicate strongest influence features(factors) on churn.   
The features influencing churn greatly are `total anytime minutes`, `customer service calls` and `international plan_yes`.  

### **Objective 3 : Best Recall Score i.e Minimize False Negatives(Missing a churning customer)**
Evaluated all the models created using accuracy, recall, precision scores and f1-score and created a table(dataframe) with these results.  
From the created table(dataframe), the recall score increased as model building continued and the model with less false negative classification was the tuned decision tree with recall score of 81%. 

### **Objective 4 : Best Accuracy Score i.e Highly Accurate Model**
From the same table(dataframe), the accuracy score also increased as model building continued and the highly accurate model was the tuned decision tree with an accuracy of 94%. 

## **Recommendations**
1. A classifier that predicts churn well was created and can hence be used for early identification of churn cases. I recommend deploying this model in real-time systems so that churns are flagged immediately.
2. Factors(features) that highly influence churn are such as customer service calls, total anytime minutes and international plan. I recommend focusing churn prevention strategies on these high impact factors. 
3. Since high recall reduces false negatives i.e chance of missing a churn, I recommend prioritizing recall as a key performance metric when tuning future models.

## **Conclusion**
This project successfully addressed the business problem of customer churn at SyriaTel by developing a strong and highly accurate predictive model. Through model building and evaluation, the study identified key churn drivers and achieved strong performance particularly in recall and accuracy.  
The insights provided provide SyriaTel with the ability of early identification of customer churns and to implement prevention strategies preventing the churn. This can therefore reduce revenue loss and support the business's growth in the telecommunications industry.