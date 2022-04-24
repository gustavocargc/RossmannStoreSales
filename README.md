# Sales Forecast - Dirk Rossmann GmbH    
## Project's Goal
Develop a Machine Learning solution for forecasting the sales of a drugstore chain with over 1,100 stores
## Methodology
The solution was developed using the Cross Industry Standard Process for Data Mining (CRISP-DM)

  ![image](https://user-images.githubusercontent.com/88887546/164997082-a4bc2626-f312-48bb-b4bf-ac6cb37ca667.png)>


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

![image](https://user-images.githubusercontent.com/88887546/165001440-c0ce2b80-a197-4b8c-98ce-4625a25f58d4.png)

![image](https://user-images.githubusercontent.com/88887546/165001413-e14ae1a6-b472-4453-9455-16d64350af89.png)

##### 2.1.3 Feature Engineering
Created Features: Year | month |  day | week | week-year 
##### 2.1.4 Feature Engineering
Excludes the following data for the next steps of CRISP-DM:

  - sales equal and less than zero
  - closed stores (open = 0)

##### 2.1.5 Exploratory data Analysis
After Feature Filtering, the target variable has a normal distribution with positive skew and sales behavior as shown in the charts below:

![image](https://user-images.githubusercontent.com/88887546/165001258-ee794716-7947-4ee5-8e4a-6451e2cb0d57.png)

![image](https://user-images.githubusercontent.com/88887546/165001262-62716bf4-e27e-4ab4-8fdd-49d8c05279b3.png)

### 3.	Data Preparation
I applied a Robust Scaler to the outliered features, as I will test linear models that are sensitive to outliers.

For the other features Min Max Scaler was applied

  - Robust Scaler
    - Competition Distance
    - Competition Time Month

  - Min Max Scaler
    - Promo Time Week
    - Year



