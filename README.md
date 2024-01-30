# SPROCKET-CENTRAL
## Background
Sprocket Central Pty Ltd is a long-standing KPMG client specializing in high-quality bikes and accessible cycling accessories for riders.
Their marketing team is looking to boost business by analyzing their existing customer dataset to determine customer trends and behavior. 
Using the existing 3 datasets (Customer demographic, customer address, and transactions) as a labeled dataset, please recommend which 1000 new customers should be targeted to drive the most value for the organization. 
## Data Source 
[Dataset](https://cdn-assets.theforage.com/vinternship_modules/kpmg_data_analytics/KPMG_VI_New_raw_data_update_final.xlsx) used for this analysis was provided by Sprocket Central Pty Ltd.
## Tools
- Excel - Data Cleaning and Analysis
- Tableau - Creating Dashboard

 
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

  Some dates in the DOB column in the "Customer Demographic" datasets were inaccurate and missing some values.

  Mitigation: After sorting the DOB column in ascending order, you'll notice an outlier. Filter out the outlier in the DOB.

   Recommendation: Create an age column using the DOB to help in analyzing the data.

- Incompleteness:

  The age, Job title, Job Category, Last Name, and Customer ID columns, had empty values among the "Customer Demographic" and "Transactions" datasets.

  Mitigation: Since the number of empty values were few, filter them out and proceed with our analysis. Because the can skew the result of our analysis.

- Inconsistency:

  There were cases of inconsistent values and data type in the state and gender columns. Some of the state names and genders were represented with abbreviations while others had extended values.

  Mitigation: To ensure consistentcy, change the the abbreviations to extended values to get a consistent column. For instance, by using the "find and replace" in excel. Change "M or F" to "Male or Female" and "VIC" to "Victoria". 
- Irrelevancy:

  Deleted the default column in the "Customer Demographic" dataset because it was irrelevant/ had no impact no my analysis.
- Validity: 

  The pricelist column had incorrect date format.

#### Calculations and Transformation
Create additional columns to allow for further and easy analysis.

- Age column in the Customer Demographic dataset with the formula ```=(NOW()-DOB)/365```

- Profit column in the Transactions dataset with the formula ```=list_price - standard_cost```

  Join some the columns from the "Customer demographic" to "Transactions" datasets with the help of "VLOOKUP" for further.

  These are some of the excel functions that helped me:

  ```=VLOOKUP(C2,'Cleaned CustomerDemographic'!$A$1:$N$3998,4,FALSE)```

  ```=VLOOKUP(C2,'Cleaned CustomerDemographic'!$A$1:$N$3998,5,FALSE)```

  ```=VLOOKUP(C2,'Cleaned CustomerDemographic'!$A$1:$N$3998,13,FALSE)```
  
### MODEL DEVELOPMENT
#### RFM Analysis
In order to identify the top 1000 customers SPROCKET-CENTRAL should target, I used the RFM analysis method. This is a segmentation type that allows businesses to rank and segment customers based on the recency, frequency and monetary value of a transaction. Based on the data, the customers were segmented in 5 categories according to their RFM values.

To derive the RFM values of each customer, first we have to calculate the R(recency), F(frenquency) and the M(Monetary) scores of each customer using the PERCENTRANK function.
Create a pivot table named RFM table from the "Transactions" dataset using the customer_id, recency, product_id and profit columns.

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

#### Customer Segmentation

Group customers based on their RFM scores.
  
  |RFM score|Customer Segmentation|
  |------|-----|
  |10 - 8|Top customer|
  |7 - 6|Loyal customer|
  |5| Almost loyal customer|
  |4 - 2|Regular customer|
  |1| Needs attention|

Now, sort the customers from highest to lowest based on their RFM score. After that we can now select the top 1000 customers.

## Key Findings/ Customer Behaviour
