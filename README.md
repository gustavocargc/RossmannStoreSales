# Dirk Rossmann GmbH Sales Forecast
## Project's Goal
Develop a data-based solution for forecasting the sales of a drugstore chain with over 1,100 stores
## Methodology
The solution was developed using the Cross Industry Standard Process for Data Mining (CRISP-DM)


![image](https://user-images.githubusercontent.com/88887546/164997082-a4bc2626-f312-48bb-b4bf-ac6cb37ca667.png)



### 1. Business Understanding
Dirk Rossmann GmbH is one of the largest drugstore chains in Europe, present in 7 countries on this continent. Store sales are influenced by many factors, including promotions, competition, school and state holidays, seasonality and location.

Currently, the revenue forecast for each of its 1,100 stores is made by each manager of these units, and forwarded to the corporate finance department, to consolidate, manage and trace out the working capital management strategy for the next 6 weeks.

As thousands of individual managers make their sales forecasts based on their unique circumstances, and often making use of very fragile techniques such as simple averaging or even personal expectations, forecasting results are inaccurate and unactionable.

Rossmann requires a reliable, actionable and data-driven solution to optimize working capital management.
### 2.	Data Understanding
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
    
        - Assumptions: Stores with no nearby competitors or no competitors
        - For these cases, I entered a distance of 200 thousand meters in the dataset, indicating to the model that the competitors are externally distant from this store, which would not happen if the option were for zero value.
