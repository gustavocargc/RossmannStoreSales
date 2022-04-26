# 💲 Sales Forecast - Dirk Rossmann GmbH

<p align="center">
   <img src="http://img.shields.io/static/v1?label=STATUS&message=Deploy%20in%20development%20on%20heroku%20cloud&color=RED&style=for-the-badge" height="35"/>
</p>

![image](https://user-images.githubusercontent.com/88887546/165095094-670c6eb8-0f83-4a6d-89a3-7c0d3d4b14ab.png)

## 📋 Project's Goal
Develop a Machine Learning solution for forecasting the sales of a drugstore chain with over 1,100 stores

## 📋 Languages and Tools
<p align="left">
<a href="https://jupyter.org/" target="_blank" rel="noreferrer"> <img src="https://github.com/devicons/devicon/blob/master/icons/jupyter/jupyter-original-wordmark.svg" alt="jupyter" width="40" height="40"/> <a href="https://jupyter.org/" target="_blank" rel="noreferrer">
<a href="https://www.python.org" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="40" height="40"/> <a href="https://pandas.pydata.org/" target="_blank" rel="noreferrer">
<img src="https://raw.githubusercontent.com/devicons/devicon/2ae2a900d2f041da66e950e4d48052658d850630/icons/pandas/pandas-original.svg" alt="pandas" width="40" height="40"/> </a> <a href="https://heroku.com" target="_blank" rel="noreferrer">
<img src="https://github.com/devicons/devicon/blob/master/icons/numpy/numpy-original.svg" alt="numpy" width="40" height="40"/> </a> <a href="https://numpy.org/" target="_blank" rel="noreferrer">
<a href="https://seaborn.pydata.org/" target="_blank" rel="noreferrer"> <img src="https://seaborn.pydata.org/_images/logo-mark-lightbg.svg" alt="seaborn" width="40" height="40"/> </a> 
<img src="https://upload.wikimedia.org/wikipedia/commons/0/05/Scikit_learn_logo_small.svg" alt="scikit_learn" width="40" height="40"/> </a> 
<img src="https://www.vectorlogo.zone/logos/heroku/heroku-icon.svg" alt="heroku" width="40" height="40"/> </a> <a href="https://www.heroku.com/" target="_blank" rel="noreferrer">
<img src="https://github.com/devicons/devicon/blob/master/icons/flask/flask-original.svg" alt="flask" width="40" height="40"/> </a> <a href="https://flask.palletsprojects.com/en/2.1.x/" target="_blank" rel="noreferrer">
<img src="https://github.com/devicons/devicon/blob/master/icons/github/github-original.svg" alt="GitHub" width="40" height="40"/> </a> <a href="https://github.com/" target="_blank" rel="noreferrer">
</p>

## 📋 Methodology
The solution was developed using the Cross Industry Standard Process for Data Mining (CRISP-DM)

  ![image](https://user-images.githubusercontent.com/88887546/164997082-a4bc2626-f312-48bb-b4bf-ac6cb37ca667.png)>

## Crisp Pipeline Explained ⤵️

### ✅ 1. Business Understanding

Dirk Rossmann GmbH is one of the largest drugstore chains in Europe, present in 7 countries on this continent. Store sales are influenced by many factors, including promotions, competition, school and state holidays, seasonality and location.

Currently, the revenue forecast for each of its 1,100 stores is made by each manager of these units, and forwarded to the corporate finance department, to consolidate, manage and trace out the working capital management strategy for the next 6 weeks.

As thousands of individual managers make their sales forecasts based on their unique circumstances, and often making use of very fragile techniques such as simple averaging or even personal expectations, forecasting results are inaccurate and unactionable.


Rossmann requires a reliable, actionable and data-driven solution to optimize working capital management.
### ✅ 2.	Data Understanding
In a multidisciplinary team involving the business areas and the data science team, for the first CRISP cycle, it was defined which features best explain Rossmann's sales behavior.

Daily sales per store for the last 31 months were collected, resulting in a dataset with 1,017,209 lines and 18 features, described below:


| Feature | Description |
|---|---|
|Store|a unique Id for each store|
|Day Of Week|day of the week of sale|
|Date|date of the week of sale|
|Sales|the turnover for any given day (this is what you are predicting)|  
|Customers|the number of customers on a given day|  
|Open|an indicator for whether the store was open: 0 = closed, 1 = open|  
|State Holiday|indicates a state holiday. Normally all stores, with few exceptions, are closed on state holidays. Note that all schools are closed on public holidays and weekends. a = public holiday, b = Easter holiday, c = Christmas, 0 = None|
|School Holiday|indicates if the (Store, Date) was affected by the closure of public schools|
|Store Type|differentiates between 4 different store models: a, b, c, d|
|Assortment|describes an assortment level: a = basic, b = extra, c = extended|
|Competition Distance|distance in meters to the nearest competitor store|
|Competition Open Since[Month]|gives the approximate month of the time the nearest competitor was opened|
|Competition Open Since[Year]|gives the approximate year of the time the nearest competitor was opened|
|Promo|indicates whether a store is running a promo on that day|
|Promo 2|Promo2 is a continuing and consecutive promotion for some stores: 0 = store is not participating, 1 = store is participating|
|Promo 2 Since[Week]|describes the week when the store started participating in Promo2|
|Promo 2 Since[Year]|describes the year when the store started participating in Promo2|
|Promo Interval|describes the consecutive intervals Promo2 is started, naming the months the promotion is started anew. E.g. "Feb,May,Aug,Nov" means each round starts in February, May, August, November of any given year for that store|
#### 2.1 Data Exploration Report
##### 2.1.1 Missing Values

The missing values presented significant percentages in some fields, being necessary to apply some assumptions, to recover a large volume of data.

| Feature | % Missing Values |
|---|---|
|Store|0,0%|
|Day of Week|0,0%|
|Date|0,0%|
|Sales|0,0%|
|Customers|0,0%|
|Open|0,0%|
|Promo|0,0%|
|State Holiday|0,0%|
|School Holiday|0,0%|
|Store Type|0,0%|
|Assortment|0,0%|
|Promo2|0,0%|
|Competition Distance|26,0%|
|Competition Open Since Month|31,8%|
|Competition Open Since Year|31,8%|
|Promo 2 Since Week|49,9%|
|Promo 2 Since Year|49,9%|
|Promo Interval|49,9%|


  - Missing values Assumptions

    -   Competition Distance:    
        - Stores with no nearby competitors or no competitors;
        - For these cases, I entered a distance of 200 thousand meters in the dataset, indicating to the model that the competitors are externally distant from this store, which would not happen if the option were for zero value.
    
    -   Competition Open Since Month:    
        -  Stores without competitors;
        - Inserted in this field the same month in which the sale was generated, the intention is to generate a zero value, when comparing the month of the sale with the month in which the competition was started.
        
     -   Competition Open Since Year:    
          - Stores without competitors;
          - Inserted in this field the same year in which the sale was generated, the intention is to generate a zero value, when we compare the year of sale with the year in which the competition was initiated. 

     -   Promo Since Week:    
          - Stores that did not join the promotion;
          - Inserted in this field the same week in which the sale was generated, the intention is to generate a zero value, when comparing the sale week with the week in which the promotion started. 

     -   Promo Since Year:    
          - Stores that did not join the promotion;
          - Inserted in this field the same year in which the sale was generated, the intention is to generate a zero value, when comparing the year of sale with the year in which the promotion started. 

     -   Promo Interval:    
          - From this feature, I derived the IS PROMO feature, indicating 0 = No Promotion 1 = Promotional Period and the MONTH_MAP, which contains the month the promotion occurs.

##### 2.1.2 Descriptive Statistical
Highlight in the target variable, zero sales and standard deviation indicating a non-linear behavior, probably the linear models will present low performance, and the positive Skew, concentrating sales in smaller values, characteristic behavior of a retailer.

![image](https://user-images.githubusercontent.com/88887546/165082019-38ef742e-3473-459c-80fb-75e637cfcf82.png)

![image](https://user-images.githubusercontent.com/88887546/165082374-ca49fdfc-6109-4a4a-849a-46c5ca4821ac.png)

##### 2.1.3 Feature Engineering
Created Features: Year | month |  day | week | week-year 
##### 2.1.4 Feature Engineering
Excludes the following data for the next steps of CRISP-DM:

  - sales equal and less than zero
  - closed stores (open = 0)

##### 2.1.5 Exploratory data Analysis
After Feature Filtering, the target variable has a normal distribution with positive skew and sales behavior as shown in the charts below:

![image](https://user-images.githubusercontent.com/88887546/165082703-eb136326-3c23-45ed-be9c-545390bbb278.png)

![image](https://user-images.githubusercontent.com/88887546/165083242-4861d1ec-bb37-4ac6-bd47-b9203c169459.png)

### ✅ 3.	Data Preparation
  - Rescaling: 

    - Robust Scaler -> Competition Distance | Competition Time Month
    > for features with significant amount of outliers
    - Min Max Scaler -> Promo Time Week | Year

  - Encoding:
    - One Hot Encoding -> State Holiday
    - lablel Encoding -> Store Type
    - Ordinal Encoding -> Assortment

- Nature Transformation:
    - Sine and cosine transformation -> Day of Week | Month | Day | Week of Year
    > to maintain the cyclical sense of the variables

- Log encoding:

    - I applied a logarithmic transformation in the target variable (sales), due to the high kurtosis, which could generate a bias and overfit the model. With the log encoding, the target variable is closer to a normal distribution.

![image](https://user-images.githubusercontent.com/88887546/165002314-edc2133e-9a9f-40ec-9c39-c69c3b6cddb3.png)

### ✅ 4. Modeling
The following models have been tested

#### 4.1. Single Performance

![image](https://user-images.githubusercontent.com/88887546/165002629-088f12da-3966-4e3f-a646-b0989d0078c1.png)


#### 4.2. Cross Validaton Performance

![image](https://user-images.githubusercontent.com/88887546/165002647-78bfdaa3-6a52-427e-ad77-c6e42228ac10.png)

#### 4.3. Final Model - Tuned

After analyzing the trade-off between model performance and computational cost, I evaluated that XGBoost Regressor has the best performance to keep up with Deployment.

![image](https://user-images.githubusercontent.com/88887546/165002685-62aedc04-bb6b-4615-bba5-f158d4dc16b7.png)

### ✅ 5. Evaluation

Error performance evaluation.

  - As Is - Average Model Error
  
![image](https://user-images.githubusercontent.com/88887546/165081478-69ef8fc3-9c3b-4aea-a691-4c8f43165f6e.png)

  - To Be - XGBoost Regressor Error
  
![image](https://user-images.githubusercontent.com/88887546/165081640-d67a044c-ea0e-4a05-aaa7-f1211daef2ea.png)

### ❗ 6. Deployment

Deploy in development on heroku cloud.

# 📋 Conclusion
After a complete CRISP-DS cycle, I chose XGBoost Regressor, after analyzing the trade-off between performance and computational cost presented by the tested algorithms.

XGBoost achieved a Mean Absolute Percentage Error (MAPE) of 11%, while the baseline, the traditional average model, achieved a MAPE of 45%. XGBoost also featured a Mean Absolute Error (MAE) of $1,065 ranging from +/- $179

The result of this solution in ML is an increase in reliability and assertiveness in the stores' sales forecast, resulting in a substantial improvement in the working capital management.

# 📋 Next Steps

   - Report model performance to business team
   - Report the insights to the business team
   - Finish the deployment
   - If necessary, run a new crisp cycle

# 📋 Get In Touch

<a href="https://www.linkedin.com/in/gustavocardoso-/" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/linked-in-alt.svg" alt="www.linkedin.com/in/gustavocardoso-" height="30" width="40" /></a>
 
