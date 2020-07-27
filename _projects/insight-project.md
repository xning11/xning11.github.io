---
title: "Unrolling User Referrals - A Model for Predicting User Referrals in Online Education"
categories:
  - data science
  - machine learning
tags:
  - classification
  - supervised-learning
  - feature-engineering
last_modified_at: 2019-10-26
---

The E-learning industry has grown rapidly over the last decade and this trend is expected to continue thanks to increasing acceptance of remote learning courses and advances in E-learning technology. Hence new customer acquisition is a key performance driver for any company in this space, with referrals one of the common strategies currently used. 

As a Data Science Fellow at Insight, I consulted with an E-learning company (which we will call "Company X") to evaluate their user referral program and provide practical insights for acquiring new customers and accelerating their business growth in the coming months.

Company X connects learners and teachers via online classrooms. Users can share their experiences via social media, email, or referral link in various places throughout the platform (e.g., for sharing a specific class, a class comment/feedback, or recommending a teacher). Company X is interested in understanding and predicting which user details, prompts, and events/experiences are the most important in nudging users towards sharing their experiences on the platform and making a referral to potential customers. By better understanding these factors, they can prioritize product features, operations, and user acquisition efforts to target these areas.

Essentially, the client company needs a model to identify important features for predicting user referrals on their platform. I worked with the team to tackle this problem in the following manner:

1. Queried across 10+ datasets using SQL and reviewed all relevant data at the user level.
2. Extracted and engineered 30+ features that could be strong indicators for predicting user referrals.
3. Built a supervised learning model with referral as the main response variable.

Below I elaborate on each of these steps in detail. 

## Data Overview

(*Due to the protection of privacy, I will not present the details of client's data, i.e., providing data visualization, feature exploration, and estimated results. Instead, I will focus on the ideation and the approach to solve the data and model problems of this project.*)

As a startup company, Company X launched its referral program to expand user coverage. After users (i.e. parents) register online, they can enroll their children in courses that are conducted via live chat. A referral can happen at any stage, either before class enrollment, during class meetings, or after course completion. Once a referral is sent out by an existing user, the referred user gets a certain amount of credit upon signup to use towards their first class. When the referred user takes the class, the person who referred them will get also get a certain amount of credit. 

The data provided by Company X contain a granular level of user information (i.e, tracking clicks, logs, site activities, and class activities of each user). Users, in this case, include parents, learners, and teachers. I focused on parents’ data because they represent the largest proportion of users on the platform and they are the largest source of referrals on the platform. 

However, after a quick sanitary check of the data, I found that only a small portion of parents on the platform have enrolled in at least one class. In other words, many registered parents have not explored the platform to a deeper extent, leading to lower feature coverage in the following model development. Moreover, only a small number of registered users have referred another user to sign up. Using such an imbalanced sample would severely bias the predictive analysis. To lessen the issue, I restricted the sample to the most active parents who have enrolled in at least one class with full completion. It then gave me a relatively larger percentage of users who have referred one or more new users. 

## Feature Engineering

To approach the project, I made some granularity versus aggregation tradeoff in order to deliver applicable solutions that target user-level decision-making within 3 weeks. Specifically, I aggregated multiple activities for each user into a single record per user and generated features using feature statistics, such as mean, minimum, maximum, and value range of features. The idea is to look for features that serve as good proxies for describing how users may interact on the platform. For example, children may enjoy different class sizes, formats,  and course topics, and their parents may send a referral to potential users about these learning experiences. Parents’ first enrollment experience and their acquisition channel may also affect how they would share and refer potential users, if at all. 

After exploring and determining which features should be considered for the purpose of this project, I focused on 30+ features that cover a wide range of information including user retention, total spending, demographics, acquisition channel, and class subjects, formats, and schedules. Overall, the data look good for my client — their products are attractive and worth sharing, though it takes time for users to discover it. 

## Model Specifications

For this project, I used logistic regression for the predictive model. While logistic regression is a simpler model than other machine learning methods, it provides a clear interpretation of the feature importance in terms of the effect magnitude and direction on the predicted probability of user referral. It is also what my client preferred to use for this project. 

I first ran the logistic regression using all 30 features as a baseline model. It gave me a model performance of 82% accuracy. To evaluate the model performance, I used a stratified train-test-split of the dataset and ran the model again to alleviate potential overfitting. The model has an 85% accuracy on the test set. Furthermore, given that some of the features that aggregated at the user level present some degree of correlation, I ran the logistic regression combined with recursive feature elimination and 5-fold cross-validation (RFECV) to prune my model of redundancy and less informative features. Doing this allows my model to adapt to new feature entrances as the company thus their database grows. The RFECV logistic regression yielded the 6 best-fitting features for the final model without lowering the model performance on the test sets. 

To validate my results, I also ran this analysis using a 5-fold CV random forest model. Random forest is less sensitive to imbalanced samples, and it works well in high dimensions, with categorical variables, and outliers. However, it lacks the interpretability of feature impact, which is an important factor to be considered in this project. The top 6~8 features selected by the random forest model are consistent with what I have found in the logistic regression. Though, two additional features were brought up in the random forest model that my earlier model ignored, which is the average price per enrollment and total spending per user.  

Based on my analysis, I offered my client a set of suggestions to boost their referral program by nudging specific users to refer, optimizing class formats, and providing a great initial enrollment experience for their users.  

## Summary

In this project, I used SQL to extract and engineer 30+ useful features across multiple tables using Mode Analytics. I built a supervised learning classification model to predict parent referrals and identify the influencing factors in the prediction using both the RFECV logistic regression and the random forest model. I then presented these findings to my client company and provided practical business insights for them to implement. It generated heated discussions about how they can upgrade their products and user experiences to improve quality user referrals and accelerate growth in the next quarter. I look forward to seeing their success. 
