<p align='center'>
 <img width="400" alt="Screenshot 2024-02-06 at 4 14 18 PM" src="https://github.com/yussif758/SPROCKET-CENTRAL/assets/135538081/c2fbaf0e-063a-4449-a9f0-c181c087f802">

## Table of content
- [Background](#Background)
- [Data Source](#Data-Source)
- [Tools](#Tools)
- [Data Exploration](#Data-Exploration)
- [Model Development](#Model-Development)
- [key Findings/Customer Behaviour](#Key-Findings/Customer-Behaviour)

## Background
Sprocket Central Pty Ltd is a long-standing KPMG client specializing in high-quality bikes and accessible cycling accessories for riders.
Their marketing team is looking to boost business by analyzing their existing customer dataset to determine customer trends and behavior. 
Using the existing 3 datasets (Customer demographic, customer address, and transactions) as a labeled dataset, please recommend which 1000 customers should be targeted to drive the most value for the organization. 
## Data Source 
[Dataset](https://cdn-assets.theforage.com/vinternship_modules/kpmg_data_analytics/KPMG_VI_New_raw_data_update_final.xlsx) used for this analysis was provided by Sprocket Central Pty Ltd.
## Tools
- Excel - Data Cleaning and Analysis
- Tableau - Dashboard

 
## Data Exploration
### Data Quality Assessment and Data Cleaning Process
These are some of the data quality issues I encountered while reviewing the datasets.

  |Datasets|Inacccuracy|Incompleteness|Inconsistency|Irrelevancy|Validity|
  |--------|--------|------------|-----------|--------|--------|
  |Customer Demographic|DOB column had Inaccurate date format|Age, Job title, Job Category, Last name, and customer ID columns had Null  values| Gender column had inconsistent format|Deleted the default column|
  |Customer Address| | | State Column had inconsistent format| | |
  |Transaction| | Customer ID, Online order, and brand columns had null values| | |Pricelist column had incorrect date format|

Below are more in-depth descriptions of the data quality issues encountered in the datasets and some mitigation and recommendations. 
- Inaccuracy:

Some dates in the "DOB" column in the "Customer Demographic" datasets were inaccurate and missing some values.

 Mitigation: After sorting the DOB column in ascending order, you'll notice an outlier. Filter out the outlier in the DOB.

 Recommendation: Create an age column using the DOB to help in analyzing the data.

- Incompleteness:

The age, job title, job category, last name, and customer ID columns had empty values among the "customer demographic" and "transactions" datasets.

Mitigation: Since the number of empty values was small, filter them out and proceed with our analysis. Because it can skew the result of our analysis.

- Inconsistency:

There were cases of inconsistent values and data types in the state and gender columns. Some of the state names and genders were represented with abbreviations, while others had extended values.

Mitigation: To ensure consistency, change the abbreviations to extended values to get a consistent column. For instance, by using "find and replace" in Excel, Change "male, female, or femal" to "M or F" and "VIC" to "victoria."

- Irrelevancy:

Deleted the default column in the "Customer Demographic" dataset because it was irrelevant/ had no impact no my analysis.

- Validity: 

The pricelist column had incorrect date format.

### Calculations and Transformation
Create additional columns to allow for further and easy analysis.

- Age column in the Customer Demographic dataset with the formula ```=(NOW()-DOB)/365```

- Profit column in the Transactions dataset with the formula ```=list_price - standard_cost```

I add some of the columns from the "customer demographic" to "transactions" datasets with the help of "VLOOKUP" for further analysis.
- These are some of the Excel functions that helped me:

  ```=VLOOKUP(C2,'Cleaned CustomerDemographic'!$A$1:$N$3998,4,FALSE)```

    ```=VLOOKUP(C2,'Cleaned CustomerDemographic'!$A$1:$N$3998,5,FALSE)```
    
    ```=VLOOKUP(C2,'Cleaned CustomerDemographic'!$A$1:$N$3998,13,FALSE)```
  
### MODEL DEVELOPMENT
### RFM Analysis
In order to identify the top 1000 customers SPROCKET-CENTRAL should target, I used the RFM analysis method. This is a segmentation type that allows you to rank and segment customers based on the RFM values of their transactions. I was able to divide the customers into five segments according to their RFM scores.

To derive the RFM values of each customer, first we have to calculate the R (recency), F (frenquency), and M (monetary) scores of each customer using the PERCENTRANK function.
Create a pivot table named RFM table from the "Transactions" dataset using the customer_id, recency, product_id, and profit columns.

- Recency: Talks about how recent your transaction is as compared to the current date. This is determined by substracting the last transaction date from the comparison(current) date.
  ```=Comparison date - Transaction_date```                                                                                                                                      

  Recency score = ```=(1-PERCENTRANK.INC($B$2:$B$3494,B2,1))*10```

- Frequency: Count of purchaces made during a period of time. Determined by the ```count of product_id```
                                                                                                                                                                               
  Frequency score = ```=PERCENTRANK.INC($C$2:$C$3494,C2,1)*10```

- Monetary: The sum of amount generated from purchases for a period of time.

  Monetary score = ```=PERCENTRANK.INC($D$2:$D$3494,D2,1)*10``` 

- RFM values: The RFM value is the summation of the scores. Customers are ranked from 1 to 10 based on their RFM scores.
  
  RFM value = Recency score + Frequency score + Monetary score 

  RFM score = ```=VLOOKUP(I3,$N$7:$O$18,2,FALSE)```

### Customer Segmentation

Group customers based on their RFM scores.
  
  |RFM score|Customer Segmentation|
  |------|-----|
  |10 - 8|Top customer|
  |7 - 6|Loyal customer|
  |5| Almost loyal customer|
  |4 - 2|Regular customer|
  |1| Needs attention|

- Based on their RFM score, sort customers from highest to lowest. We are then able to choose the top 1000 customers.

## Key Findings/ Customer Behaviour

For this study, the top 1000 customers were chosen from a total of 3494 customers. 

### Age Distribution

- The age distribution of the top 1000 customers is displayed in the chart below.
- It is evident that the majority of the customers fall within the 50-year-old category. Which indicates that they are 50 years old, or almost 50.
- Age groups between 80 and 100 years old appeared to have the fewest customers, according to the data. The age range of 80 to 100 years old comprises a small subset of the customers.


<img src="https://github.com/yussif758/SPROCKET-CENTRAL/assets/135538081/5edcbb9b-7f89-4c0a-b4cf-efc30332ce2c" width="850" height="450" >

### Gender Distribution 

- There were three distinct gender categories among the target customers. Three genders: male, female, and unknown.
- Female dominance is evident from the gender distribution chart.
- Males account for only 46.40% of the target consumers, with 50.20% of them being female.
- For the remaining 3.40% of customers, the gender is unknown.
<img src="https://github.com/yussif758/SPROCKET-CENTRAL/assets/135538081/10bb338f-e4ad-4fc7-b2df-8f09ec34be60" width="900" height="450" >

### Customer Segmentation
- The target customers consists of customers who belong to the "top" or "loyal" customer segment.
- The majority of the target customers are "top customers," making up 63.70% of the target customers.
- While 36.30% of the target customers are loyal customers. 
<img src="https://github.com/yussif758/SPROCKET-CENTRAL/assets/135538081/64ae3383-3f3f-4d97-b64c-ab6b2128ecda" width="900" height="450" >

### Job Distribution 
 
- Most of the customers are in the financial services and manufacturing industries.
- The financial services and manufacturing industries account for about 25% and 22%, respectively.
- With 1.91%, 2.86%, and 3.70% of customers, respectively, the industries with the fewest customers are telecommunications, agriculture, and entertainment.
<img src="https://github.com/yussif758/SPROCKET-CENTRAL/assets/135538081/05f5e7fb-4105-4645-a42e-d0b69c20f490" width="900" height="450" >

### Total Profit per Month 
- The line graph below displays the total profit from customer transactions per month.
- With a total of $430,687 generated, April had the greatest amount. Followed by $429,340 generated in September.
- January brought in the least amount of money from customer transactions, totaling $187,981.
- Following the company's greatest profit in April, we can see fluctuations in the monthly profit.
<img src="https://github.com/yussif758/SPROCKET-CENTRAL/assets/135538081/aa27d4ef-f43c-421a-9a94-17446346a554" width="900" height="450" >

###  Wealth Segment 
- Largest number of customers are classified as "Mass Customer" followed by "High Net Customer".
- "Affluent customers" accounted for the smallest percentage of customers (23.70%), while "mass customers" made up around 50.40% of the total.
<img src="https://github.com/yussif758/SPROCKET-CENTRAL/assets/135538081/3f94c2b1-6e97-44d1-9b43-fb737cfb50e8" width="900" height="450" >


## Customer Location

- The target customers are dispersed throughout three Australian states, namely New South Wales, Queensland, and Victoria.

<img src="https://github.com/yussif758/SPROCKET-CENTRAL/assets/135538081/928dd37c-06fa-4dfd-b19e-4b4423324db2" width="900" height="450" >

 

