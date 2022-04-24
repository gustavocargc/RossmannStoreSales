# Sales Forecast
## Project's Goal
Develop a data-based solution for forecasting the sales of a drugstore chain with over 1,100 stores
## Methodology
The solution was developed using the Cross Industry Standard Process for Data Mining (CRISP-DM)
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
