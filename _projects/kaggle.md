---
layout: page
title: Kaggle Challenges
description: collection of Kaggle challenges I have participated in.
img: assets/img/tree.jpg  # Photo by <a href="https://unsplash.com/@sallybrad2016?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Preethi Viswanathan</a> on <a href="https://unsplash.com/photos/brown-tree-branch-covered-with-white-snow-h5fsy4E4FMY?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Unsplash</a>
importance: 1
category: personal
related_publications: false
giscus_comments: false
redirect:
---

I have participated in four Kaggle challenges so far. My participation in the challenge [Predict Future Sales](https://www.kaggle.com/competitions/competitive-data-science-predict-future-sales) was part of the Data Mining course and is described in the [Data Mining](/projects/DataMining) project. The challenge [G2Net-Hackathon](https://www.kaggle.com/competitions/g2net-hackathon) is described in the [Gravitational Wave Hackathon](/projects/GW_hackathon) project. The other two challenges are described below.

## [Titanic - Machine Learning from Disaster](https://www.kaggle.com/competitions/titanic)

The Titanic challenge is a classic challenge for introducing beginners to the Kaggle platform. The challenge is to predict which passengers survived the Titanic shipwreck. The dataset contains the following information for each passenger:
<!-- PassengerId,Pclass,Name,Sex,Age,SibSp,Parch,Ticket,Fare,Cabin,Embarked -->
- PassengerId: a unique identifier for each passenger
- Pclass: the class of the ticket (1st, 2nd, or 3rd)
- Name: the name of the passenger
- Sex: the sex of the passenger
- Age: the age of the passenger
- SibSp: the number of siblings/spouses aboard
- Parch: the number of parents/children aboard
- Ticket: the ticket number
- Fare: the ticket fare
- Cabin: the cabin number
- Embarked: the port of embarkation (C = Cherbourg, Q = Queenstown, S = Southampton)

The training dataset contains the information for 891 passengers, and the test dataset contains the information for 418 passengers. The test dataset does not contain the information about the survival of the passengers. The goal is to predict the survival of the passengers in the test dataset (0 = not survived, 1 = survived).

My goal for this challenge was to get familiar with the Kaggle platform and to practice on some decision tree algorithms. I used the following algorithms:
- Logistic Regression (LogReg)
- Light Gradient Boosting Machine (LightGBM)
- eXtreme Gradient Boosting (XGBoost)

For the data preprocessing, I dropped the columns for the passenger ID, name, ticket, and cabin. I mapped the sex and embarked columns to numerical values and filled the missing values in the age and fare columns with the mean values. For the samples that still had missing values, I dropped them from the training and test datasets. These decisions were made based on the exploratory data analysis I performed on the dataset, as well as practical considerations, since my goal for this challenge was to practice on some decision tree algorithms and get familiar with the Kaggle platform, rather than to achieve the best possible prediction.

I trained the algorithms on the training dataset and created a submission file for the test dataset. The submission file contained the passenger ID and the predicted survival. I made several submissions to the Kaggle platform for the different algorithms I used (for some of them I submitted multiple times). The scores I achieved are shown in the table below:

| Algorithm | Score |
|-----------|-------|
| LogReg    | 0.76794 |
| LightGBM  | 0.77511 |
| XGBoost   | 0.77751 |

The scores are based on the accuracy of the predictions. The best score I achieved was 0.77751 with the XGBoost algorithm. This score is on the top 30% of the leaderboard, which is not bad for the simple approach I used. The code for this challenge, with instructions on how to run it,can be found in the [Titanic](https://github.com/johnkou97/Titanic) repository.

## [Spaceship Titanic](https://www.kaggle.com/competitions/spaceship-titanic)

