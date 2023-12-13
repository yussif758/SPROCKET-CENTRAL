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
### Data Quality Issues and Data Cleaning Process
These are some of the data quality issues I encountered while reviewing the datasets.

  |Datasets|Inacccuracy|Incompleteness|Inconsistency|Irrelevany|Validity|
  |--------|--------|------------|-----------|--------|--------|
  |Customer Demographic|DOB column had Inaccurate date format|Age, Job title, Job Category, Last name, and customer ID columns had Null  values| Gender column had inconsistent format|Deleted the default column|
  |Customer Address| | | State Column had inconsistent format| | |
  |Transaction| | Customer ID, Online order, and brand columns had null values| | |Pricelist column had incorrect date format|

Below are more in-depth descriptions of the data quality issues encountered in the datasets and some mitigation and recommendations. 
- Inaccuracy:

  Some dates in the DOB column in the "Customer Demographic" datasets were inaccurate and missing some values.

  Mitigation: After sorting the DOB column in ascending order, you'll notice an outlier. Filter out the outlier in the DOB.

   Recommendation: Create an age column using the DOB to help in analyzing the data.

- Incompleteness

  The age, Job title, Job Category, Last Name, and Customer ID columns, have empty values among the "Custoner Demographic" and "Transactions" datasets.

  Mitigation: Since the number of empty values is few, we can filter them out and proceed with our analysis.
- Inconsistency
- Irrelevancy
- Validity
