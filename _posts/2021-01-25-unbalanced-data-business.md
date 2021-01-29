---
layout: post
title: Handling Imbalanced Data Classification with Business-Driven Perspectives
subtitle:  
tags: [Data Analysis]
comments: true
---
I think one critical skill that data scientists should gain is the capability to translate a real business problem into a data science question. Knowing all the machine learning (ML) techniques is one important thing; while knowing how to inject business insights into ML modeling is another. So far I have performed a few data science projects with imbalanced datasets and I'd like to share with you some tactics I learned with best practices. 

I have noticed that many online resources (blogs, tutorials) about imbalanced data analysis mostly focus on  technical tricks including sampling, parameters tuning, and choice of ML models. Therefore, in this blog I would talk more from a DS production perspective, and focus on how business knowledge would help the modeling. I hope you would enjoy reading it! 

## 1. Imbalanced data modeling in the business world
Imbalanced dataset is not uncommon in the business world. Usually the imbalance occurs when modeling low probability events in a large target population. Some examples include fraud detection, identification of defective products, insurance claims, etc. The majority of the imbalance is **intrinsic** which is caused by the nature of the events (i.e. a naturally low probability event like fraud). However, some dataset can have **extrinsic** imbalance due to limitations when collecting the data. For instance, if data-collecting equipment is limited to work during the daytime, then the data observations that collected at night would be much less, even though the events happen with a constant frequency during the day. 

Without having business knowledge, data scientists usually develop machine learning models that aim to optimize F1 score, ROC- AUC, confusion matrix, precision and recall. However, when dealing with business questions in reality, business background knowledge including cost and/or revenue could be a game-changer. Balancing **False Positives (Type 1 Error) and False Negatives (Type 2 Error)** can be very complicated considering factors and limitations such as time, cost, etc. However, utilizing business knowledge could help to deal with the imbalanced data modeling.

## 2. Handing imbalance in model development process
Usually we could develop ML models with the following steps:
![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/imbalanced_data/model_process.PNG?raw=true){: .center-block :}


Actually, business-driven perspectives can be applied to all the steps. In the following sections I will present how to use business knowledge to create a better ML model with imbalanced data. 

### 2.1 Data Preparation
Before training models, we need to have a good understanding of the data structure. Data manipulation and feature engineering are critical to model development. For imbalanced data, we could consider **potential segmentation**. This includes segmentation for:
* 1) Response variable

If one class of the response variable is the majority and other classes are all minority, we could consider combining the classes of the minority. For example, when predicting the number of severe tornadoes in one month, we may see most of the data entries have 0 tornadoes, a minority of the data entries have 1, 2, or 3 tornadoes. In this case, we may change the response variable from a multi-class categorical variable to a binary variable by predicting if there will be any severe tornado or not.
* 2) Independent variables

Explore the data population and figure out what caused the imbalance. For example, if younger employees have higher probability to leave the company compared to older employees, we could try to segment the employees based on age.

In addition to segmentation, another technique to pre-process the data is to perform **sampling** methods. You probably already know **under sampling, over sampling** and some other methods like **SMOTE (Synthetic Minority Over-Sampling Technique)**. When sampling the data, having business knowledge such as the costs of **False Negatives (FN)** and **False Positives (FP)** could help determine the **sampling weights**. Basically, the higher weight would be given to the minority class and the lower weight to the majority class.

For example:
* suppose in original data, the ratio of positive and negative is 1:100
* suppose the cost of FP: $10, cost of FN: $100
* when performing under sampling, we could use a weight of positive and negative equals to 1:10 to represent the costs

### 2.2 Model Tuning
Some ML method libraries provide weights related parameters to tune with. For example in Python, a commonly used parameter is 'class_weight' for Random Forest classifier. By setting 'class_weight='balanced', the model uses the values of y to automatically adjust weights inversely proportional to class frequencies. Alternatively, we could again use the cost data to set the weights by penalizing classification mistakes from the model. Similar to the idea of choosing sampling weights, we want to tune the modeling with realistic considerations of reducing costs and/or increase potential revenue.
### 2.3 Model Evaluation
For imbalanced data, using Precision-Recall (PR) Curves is better than ROC AUC curve when comparing model performance (Reference 1):
![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/imbalanced_data/ref1.png?raw=truE){: .center-block :}

From the plot above, we can see that although a and b have the same ROC curves, PR curve of b is much better than that of a, indicating that the model used in a does not have good performance with imbalanced data of a.
In addition, I would highly recommend analyzing the **confusion matrix**, by calculating the **expected loss**. Handling both FP and FN at the same time is always difficult, but analyzing expected loss can turn this trade-off situation into an optimization question. Below is a binary classification example of using business knowledge to evaluate the model:  

#### Example analysis of malfunctioning cameras
* Problem description:

Project goal: Fault detection of cameras

Binary response variable:  1 malfunctioning with fault, 0 without fault

Imbalanced dataset: 1% of cameras are malfunctioning (Response variable= 1)
* Business background:

50k cameras produced daily, test capacity is 1k cameras

Test cost per camera: $10, 

Loss when failed to detect: $200
* Model performance

Recall=0.1, so the model can correctly detect 100 malfunctioning cameras out of 1000 predictions
#### How does the business information affect modeling?
As stated above, we could answer this question by calculating the **expected loss**, which is the goal that we want to minimize. The table below calculates the expected loss from 3 scenarios:
![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/imbalanced_data/camera_table.PNG?raw=true){: .center-block :}

It can be seen that model could save 100k-90k = **10k** in this situation. When comparing performance with different ML models, we should focus on maximizing the saving by **reducing the expected loss**.  
#### What else can we learn from the given business information?
It is worth noticing that the test capacity is **1k** cameras. With the model results, only the cameras predicted as positive will be tested. So the test capacity actually determines the upper limit of **FP+TP**, a.k.a the number of predicted positive by the model. It makes sense to choose models with < = 1k predicted positives, because we are limited to test at most 1k cameras. If the model predicted more than 1K positives, we will not have the ability to test all the predicted cameras. 
### 2.4 Model Output
Personally, I think delivering model output is the stage that needs the most cooperation efforts with business partners, especially when the data science model leads to a product. The final output of the model should meet the business goals that we want to achieve. 
In general, the business background can affect the model outputs and post-processing mainly on the following: 
* Output format

Depends on who the model users will be, requirements of the output format could vary. In terms of classification, the common formats to deliver the model output would be the **class label** and **the probability** of being assigned to a certain label. Sometimes the model users only need to know which label is given, but in some situations knowing the probability is necessary, especially the results need to be ranked. 
* Rank of the results

Limited by time, resources and cost, it makes more sense to deliver model results ranked by priority. Again, this is where DS and business partners should have a discussion on 1) what are the **limitations** and 2) what is the **priority**.
#### Example analysis of membership marketing
* Problem description:

Project goal: Reach out to customers who has potential to buy the VIP membership

Binary response variable: 1 potential customer, 0 not a potential customer

Imbalanced dataset: 10% of customers are willing to make the purchase (Response variable= 1)
* Business background:

The amount of revenue brought by different customers varies if they join the membership, so the model output should be ranked to maximize the revenue. 
* **Who to reach out first?**

Suppose we have an example model output for the following 3 customers, how do we rank them based on predicted probability and business knowledge?
![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/imbalanced_data/customers.PNG?raw=true){: .center-block :}

Since the goal is to maximize the revenue, we could calculate the expected revenue based on the modeling results. Here one EDA I would suggest is **heat map** plot. In this example, the expected potential revenue is calculated by probability given by model times the revenue bought by the customers. Below is the python code to create a heat map based on toy data of revenue.
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
![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/imbalanced_data/heatmap.PNG?raw=true){: .center-block :}
From this heat map plot, we can clearly see that though customer A has the highest probability to join the VIP club, and customer C has the most potential revenue to bring, we want to reach out to customer B first!
* **Further thoughts**

Obviously the example presented here is simplified from the real business problem. In reality, it may need a lot more consideration when plotting the heat map and ranking the model outputs. For example, if cost is different when reaching out to clients, then this cost should be another factor to be involved in the expected revenue analysis. 
## 3. Summary
Modeling imbalanced dataset is never an easy task. But luckily in the business world we may inject business insights to help the model development process in multiple ways. In addition to all the technical tactics you already tried to improve the model performance, I hope this blog is useful from a different perspective. Thanks for reading! 

**Reference**
[1] Lever et al. (2016) Nat Methods: Graphical representation of classifier performance avoids setting an exact threshold on results but may be insensitive to important aspects of the data.