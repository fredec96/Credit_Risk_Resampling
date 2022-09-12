# Credit Risk Resampling

## Overview of the Analysis


Accurately predicting un-healthy prospective loans is essential for deciding whether to give out a loan. It can save a lender from giving out loans who's owners will fail to repay. In this analysis, supervised learning was used to predict whether a potential loan should be considered healthy or un-healthy. Supervised learning contains three stages: Model, Fit, and Predict. Two logistic regression models were used for this analysis, with two slightly different data sources being used to fit the model.

The provided dataset contained information for 75036 healthy loans and 2500 un-healthy loans, each loan included data that can be used to predict whether or not the loan can be considered healthy. The information for each loan was categorized into: loan size, interest rate, borrower income, debt to income, number of accounts, derogatory marks, and total debt. See below for original data example. 

![Original Data](Resources/data.png)


Healthy loans far outnumber risky loans, which can pose a challenge when training a machine learning model. With too few instances of un-healthy loans to learn from, the model may struggle to identify un-healthy loans. Due to this challenge two different techniques were used. 

First, the model was trained with the original data as shown above.

Second, the data was altered using RandomOverSampler from Imbalanced Learn to create an equal amount of health an-unhealthy loans. After oversampling the data contained more instances of un-healthy loans, with 56271 instances of healthy loans, and the same amount of un-healthy loans. It was theorized that having an equal amount of both healthy and unhealthy loans would allow the model to. 

Accurately identifying the `1` (high-risk loan) is the most important part of this model because they are the loans the lender is trying to weed out and avoid. If an un-healthy loan is miscategorized as a healthy loan and approved, the lendor is at high risk for losing money due to the likeliehood the creditor will default. Ideally the model accurately predicts every loan, but there is a safer way for a model to fail. It's far safer for a lender to have a model that leans towards falsely predicting safe loans as un-safe (represented by the `1` high risk precision score) than it if the model leaned towards falsely predict un-safe loans as safe, (represented by the `1` high risk Recall score).

## Results

* Balanced Accuracy
    * Machine Learning Model 1, Original Data: The balanced accuracy score for this model was 0.95 which can be interpretted as a fairly strong score, however the precision and recall scores will provide deeper insight into the circumstances that created the balanced accuracy score.
    
    * Machine Learning Model 2, Over Sampled Data: Using the oversampled data the balanced accuracy score improved to 0.99 up from 0.95 using the original data

![Balanced Accuracy Scores Compared](Resources/balanced_accuracy.png)


* Precision 
    * Machine Learning Model 1, Original Data: The precision score for the `1` (high-risk loan) of 0.85 was the lowest score in the classification report, which we can understand by looking at the confusion matrix and seeing that the model predicted 665 instances of `1` (high-risk loan), but 102 of those instances were false positives and actually a `0` (healthy loan).
    
    * Machine Learning Model 2, Over Sampled Data: We can see that the precision value did slightly decrease from 0.85 to 0.84 using the oversampled data due to 14 additional instances of healthy loans being classified as high-risk.


* Recall 
  * Machine Learning Model 1, Original Data: The recal score for the `1` (high-risk loan) of was 0.91 which we can understand by looking at the confusion matrix and seeing that the model predicted 665 instances of `1` (high-risk loan), but miscategorized 56 un-healthy loans as healthy loans.  
  
  * Machine Learning Model 2, Over Sampled Data: Recall was improved to an impressive score of 0.99 with only 4 instances of high-risk loans being classified as healthy loans. 

![Classification Reports Compared](Resources/classification_report.png)


![Confusion Matrix Compared](Resources/confusion_matrix.png)

## Summary

Overall the model trained on the oversampled data performs very well and has better results than the model trained on the original data, as seen in the classification reports and balanced accuracy scores. For that reason the model trained on the over sampled data is the model I would recommend a lender use. The model trained on the original data outperformed the over sample in only one category, precision. But as I stated previously, erring on the side of caution is not necessarily a bad thing to see when testing a model, and the change from the original model is minimal. 




