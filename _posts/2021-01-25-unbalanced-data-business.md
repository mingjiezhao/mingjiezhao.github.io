---
layout: post
title: Handling Unbalanced Data Classification with Business-driven Perspectives
subtitle:  
tags: [Data Analysis]
comments: true
---
I think one critical skill that data scientists should gain is the capability to change a real business problem into a data science question. Knowing all the machine learning (ML) techniques is one important thing; while knowing how to utilize business insights into ML modeling is another. So far I have performed a few data science projects with unbalanced datasets and I'd like to share with you some tactics I learned with best practices. 

I have noticed that many online resources (blogs, tutorials) about unbalanced data analysis mostly focus on the technical tricks including sampling, parameters tuning, and choice of ML models. Therefore, in this blog I would talk more from a DS production perspective, focus on how business knowledge would help the modeling. I hope you could enjoy reading! 

## 1. Imbalanced data modeling in business inustry
Imbalanced dataset is not uncommon in the business world. Usually the imbalance occurs when modeling low probability events with a large target population. Some examples are like fraud detection, identification of defective products, insurance claims, etc. The majority of the imbalance is **intrinsic** which is caused by the nature of the dataset (i.e. a naturally low probability event like fraud). However, some dataset can have **extrinsic** imbalance due to limitations when collecting the data. 

Without having business knowledge, data scientists usually develop machine learning models which aim to optimize F1 score, ROC AUC curves, confusion matrix, precision and recall. However, when dealing with business question in reality, business background knowledge including cost and/or revenue could be a game changer. Balancing **False Positives (Type 1 Error) and False Negatives (Type 2 Error)** can be very complicated considering factors and limitations such as time, cost etc. However, utilizing business knowledge could help dealing with the imbalanced data modeling.





## 2. Handing imbalance in model development process
Usually we could consider the ML model development has the following steps:
![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/imbalanced_data/model_process.PNG?raw=true){: .center-block :}


Actually, business-driven perspectives can be applied to all the steps. In the following sections I will present how to use business knowledge to create a better ML model. 

### 1. Data Preparation
Before performing models, we need to have a good understanding of the data structure. Data manipulation and feature engineering are critical to the modeling steps. For imbalanced data, we could consider **potential segmentation** for the data. This includes segmentation to:
* Response variable

If one class of the response variable is the majority and other classes are all minority, you could consider combining the classes of minority. For example, when predicting number of severe tornado in one month, you may see most of the data entries have 0 tornado, a minority of the data entries have 1, 2, or 3 tornadoes. In this case, you may change the response variable to a binary one by predicting if there will be any severe tornado or not.
* Independent variables

Explore the data population and see what caused the imbalance. For example, you may see that younger employees have higher chance to leave the company compared to older employees. In this case you could try segmentation of your population, which may help with the imbalanced situation.

In addition to segmentation, another technique to do in the data preparation stage is **sampling**. You probably already learned about **under sampling, over sampling** and some other methods like **SMOTE (Synthetic Minority Over-sampling Technique)**. When sampling the data, having Business knowledge could be helpful. Using binary classification as an example, knowing the costs of having **False Negatives (FN)** and **False Positives (FP)** could help determine the sampling weights. 

For example:
* suppose in original data, ratio of positive and negative is 1:100
* suppose cost of FP: $10, cost of FN: $100
* when perform undersampling, we could use a weight of positive and negative equals to 1:10

### 2. Model tuning
Some ML method libraries provide weights related parameters to tune with. For example in Python, a commonly used one is class_weight from Random Forest classifier. We could again use cost data to set the weights by penalizing classification mistakes. Similar to the idea of choosing sampling weights, we want to tune the modeling with realistic considerations of reducing costs and/or increase potential revenue.
### 3. Model evaluation
For imbalanced data, using Recall vs. Precision curve is better than ROC AUC curve when compare model performance (Reference 1):
![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/imbalanced_data/ref1.PNG?raw=true){: .center-block :}

In addition, I would highly recommend analyzing the **confusion matrix**, by applying the ideas of **Expected Value Analysis**. Again, I am using a binary classification as an example. Handling both FP and FN at the same time is always difficult, but performing Expected Value Analysis can change this trade-off situation to an optimization question. Below is an example of using business knowledge to evaluate the model:   

#### Example analysis of malfunctioning cameras
* Problem description:

Project goal: Fault detection of cameras

Response variable: binary – 1 malfunctioning with fault, 0 without fault

Imbalanced dataset: 1% of cameras are malfunctioning (Response variable= 1)
* Business background:

50k cameras produced daily, test capacity is 1k cameras

Test cost per camera: $10, Loss if failed to detect: $200
* Model performance

Recall=0.1, so the model can correctly detect 100 cameras out of 1000 predictions
#### How does the business information affect modeling?
We could answer this question by calculating the **expected loss**, which is the goal that we want to minimize. The table below calculates the expected loss from 3 scenarios:
![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/imbalanced_data/customers.PNG?raw=true){: .center-block :}

It can be seen that model could save 100k-90k = **10k** in this situation. When comparing performance with different ML models, this saving is the goal we want to optimize by **reducing the expected loss**.  
#### What else can we learn from the business information?
It worth noticing that the test capacity is **1k** cameras. This actually determines the upper limit of **FP+TP**, a.k.a the number of predicted positive by the model. It makes sense to choose models with < = 1k predicted positives, because we are limited to test at most 1k cameras. If the model predicted more than 1K positives, we will not have the ability to test all the predicted cameras. 
### 3. Model Output
Personally, I think delivering model output is the stage that needs the most cooperation efforts with business partners, especially when the data science model leads to be a product. The final output of the model should meet the business goals that we want to achieve. 
In general, the business background can affect the model outputs and post-processing mainly on the following: 
* Output format

Depends on who the model users will be, requirements of the output format could vary. In terms of classification, the common formats to delivery the model output would be the class label and the probability of with a certain label. Sometimes the model users only need to know which label is given, but in some situations knowing the probability is necessary, especially the results need to be ranked. 
* Rank of the results

Limited by time, resources and cost, it makes more sense to deliver model results ranked by priority. Again, this is where DS and business partners should have a discussion on 1) what are the **limitations** and 2) what is the **priority**.
#### Example analysis of membership marketing
* Problem description:

Project goal: Reach out to customers who has potential to buy the VIP membership

Response variable: binary – 1 potential customer, 0 not a potential customer

Imbalanced dataset: 10% of customers are willing to make the purchase (Response variable= 1)
* Business background:

The amount of revenue brought by different customers varies if they join the membership, so the model output should be ranked to maximize the revenue. 
* Who to reach out first?
Suppose we have an example model output for the following 3 customers, how do we rank them based on predicted probability and business knowledge?
![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/imbalanced_data/heatmap.PNG?raw=true){: .center-block :}

Since we have a goal to achieve (maximize the revenue), we could perform the expected value analysis based on the modeling results, one EDA I would suggest is **heat map** plot. In this example, the expected potential revenue is calculated by probability given by model times the revenue bought by the customers. Here's an example of creating a heat map based on some toy data of revenue.
```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
prob = np.arange(0.1, 1.1, 0.1)
col_prob = ['10%','20%','30%','40%','50%','60%','70%','80%','90%','100%',]
revenue = np.arange(100, 1100, 100)
df = pd.DataFrame(np.outer(prob, revenue), columns=col_prob)
df.index = revenue.copy()
a4_dims = (11.7, 8.27)
fig, ax = plt.subplots(figsize=a4_dims)
ax = sns.heatmap(df.astype('int32'),
                cmap='coolwarm',
                annot=True,
                fmt="d",
                annot_kws={'size':12},
                cbar_kws={'label':'Potential Revenue'},
                square=True)
plt.title('Expected Potential Revenue from New VIP Members')
ax.set(xlabel='Prob. of Purchasing VIP Membership', ylabel='Revenue bought by Customers')
```
![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/COVID-19/Musk_test/theory.jpg?raw=true){: .center-block :}
From the heat map plot, we can see clearly that though customer A has highest probability to join the VIP club, customer C has the most potential revenue to bring, we want to reach out to customer B first!
* Further thoughts

Obviously the example presented here is simplified from the real business problem. In reality, it may needs a lot more consideration when drawing the heat map and rank the model outputs. For example, if cost is different when reach out to different clients, then this cost should be another factor to be involved in the analysis. 
## 5. Summary

References:
1. Graphical representation of classifier performance avoids setting an exact threshold on results but may be insensitive to important aspects of the data. (from Lever et al. (2016) Nat Methods)