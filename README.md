# Prediciting Kickstarter Project Status (Success vs. Failed)


## 1. Problem Identification 

Kickstarter is a crowdfunding website for groups or individuals looking to raise funds to start a personl or professional project. Project ideas range from technology and consumer gadgets, to brick and mortar restaurants, or music, plays and productions. The definition of a successful project is to reach and/or exceed the goal amount within the 60 days that Kickstarer allows per campaign. With vested community interest in the projects, my goal is to understand what factors could indicate a successful project, and whether or not this data can help new teams make their projects more likely to succeed. 






## 2. Data Collection, Organization, and Definitions 

The data is obtained from Kaggle, titled "Kickstarter Projects" from Mickaël Mouillé. It is mentioned that the original dataset is pulled directly from the Kickstarter platfrom. For this project, we only looked at the 2016 dataset and did not include the 2018 data. 

* The dataset started with 17 columns, many of them misaligned, and majority type object. 
     * My first task was to figure out which columns were misaglied and why. The culprit became clear that any projects with multiple categories selected, extended an extra column by the amount of additional selected cateogry. 

* I first realigned the columns so that the data is consistend, and then deleted the "category" column, relying on the "main category" feature for modeling. 
    * This decision is because some projects fit multip sub categories, but only 1 main cateogry. The "category" column also had too many unique values. 

* Rows with missing data in the "State" (dependent variable) were removed, and other missing/NaN values were addressed. 

* Columns were further reduced for data that did not make sense to include in the model, such as ID, project name, etc. 

* Datatypes were adjusted for numeric columns 

![dataframe head](https://github.com/belindaleebl/kickstarter/blob/master/Images/data.head.PNG?raw=true)

## 3. Exploratory Data Analysis  

<p>&nbsp;</p>

* Early visualizations show that the project state "successful" has many more "backers" than any other project state. 
* Successful projects also tend to have much smaller goal amounts. 
* Successful projects tended to be listed as technology, games, or design, with these three also having the highest pledge amounts 
* These three categories also happen to be the top three failed categories as well and thus we're not sure if we can make any inferences from the early visualizations. 

<p>&nbsp;</p>
<p>&nbsp;</p>

![Project State vs. Backers](https://github.com/belindaleebl/kickstarter/blob/master/Images/project_state_backers.PNG?raw=true)
![Project State vs. Goals](https://github.com/belindaleebl/kickstarter/blob/master/Images/goal_state.PNG?raw=true)

## 4. Data Preprocessing

* Created dummies for the non numerical features. 
* Separated the independent and dependent variable, then created training and testing data, making sure to stratify so that the training and testing data have similar population profile. 

## 5. Model

<p>&nbsp;</p>

* DecisionTree Classifier 
     * Performed GridSearchCV for best max_depth parameter of 9
     * Checked for overfitting and concluded the metrics were aligned and most likely not overfit. 
     * Feature importance showed only 3 features heavily influenced model (backers, usd_pledged, and goal)
     * Used SMOTE to addres data imbalance
<p>&nbsp;</p>

* RandomForest Classifier 
    * RandomizedSearchCV to find best n_estimators 
    * Feature importance showed same three heavy influlencers as DecisionTree 
    * Used BalancedRandomForest Classifier 
<p>&nbsp;</p>

* Binary DecisionTree and RandomForrest 
    * Changed dependent variable to binary (Successful or Other) 
    
<p>&nbsp;</p>
     
![DecisionTree Feature Importance](https://github.com/belindaleebl/kickstarter/blob/master/Images/decision_tree_feature_importance.PNG?raw=true)

## 6. Metrics and Documentation 

* DecisionTree 
    * The precision and recall score for the "successful" state was always high, around 0.97, even after balancing the data, but the scores for predicing other states are much lower. This prompted me to consider binary classification 
<p>&nbsp;</p>

* RandomForrest 
     * Showed similar trend as decision tree, where the precision and recall score for "successful" state is high, while other values were lower. 
     * Showed similar but slightly lower metrics compared to DecisionTree at 0.8 and 0.85 for weighted average on the precision and recall. 
<p>&nbsp;</p>

* Binary classification scored the highest for both DecisionTree and Randomforest, with weighted averages for Precision and Recall at 0.98   
<p>&nbsp;</p>



## Recommendations and Areas of Improvement 

Overall I'd recommend using the binary RandomForest classifier for the highest score. The scores for both binary classifiers are so similar, but the the binary RandomForest score 0.01 point higher on precison for not successful projects. Since our goal is to predict whether a project is successful and what factors could increase success, all other states of project could be lumped together. 


1. We understand that successful projects are typically determined by three features, the number of backers, the orinal goal amount, and the amount of money pledged. Potential Kickstarter project can now consider arranging their intial project to a small goal amount or encourage larger amount of pledges for smaller upfront payment to increase their chances of success. 
<p>&nbsp;</p>

2. As a pledger, we can also understand better a project's likely outcome, and choose to pledge when we feel that the project is more likely to succeed. 
<p>&nbsp;</p>

3. For future improvement, we can perform A/B testing to understand where the cutoff numbers might be, for exmaple, how many backers is "enough" to be successful. What should be the ideal goal amount. 


```python

```
