####  US Immigration information

### Data Engineering Capstone Project

## Project Summary

This project will provide information on US immigration including questions like what are the most popular cities for immigration, the gender distribution of the immigrants, the visa type distribution of the immigrants,the average age per immigrant and the average temperature per month per city. Our dataset is from 3 different sources - the I94 immigration dataset of 2016, city temperature data from Kaggle and US city demographic data from OpenSoft. We defined our data model with 4 dimension tables: (Cities, immigrants, monthly average city temperature and time) and 1 fact table: Immigration. We use Spark for ETL jobs.

The project follows the follow steps:

Step 1: Scope the Project and Gather Data
Step 2: Explore and Assess the Data
Step 3: Define the Data Model
Step 4: Run ETL to Model the Data
Step 5: Complete Project Write Up

### Step 1: Scope the Project and Gather Data

#### Scope 
The goal of this project is to extract data from 3 different sources and create fact and dimension table to be able to do analysis on US immigration using factors of city monthly average temperature, city demographics and seasonality.

#### Describe and Gather Data 
I94 Immigration Data: This data comes from the US National Tourism and Trade Office. A data dictionary is included in the workspace. This is where the data comes from. There's a sample file so you can take a look at the data in csv format before reading it all in. You do not have to use the entire dataset, just use what you need to accomplish the goal you set at the beginning of the project.
World Temperature Data: This dataset came from Kaggle. You can read more about it here.
U.S. City Demographic Data: This data comes from OpenSoft. You can read more about it here.
Airport Code Table: This is a simple table of airport codes and corresponding cities. It comes from here.

### Step 2: Explore and Assess the Data
#### Explore the Data 
More than 3 million entries in the i94 df and 659 valid ports. The demo dataset have 49 valid states. UDF written for coversion to pyspark datetime format and validate state codes.
Temperature df has 8.6 million entries. UDF is written to map city full name to city port abbreviation


#### Cleaning Steps
Removed any missing values. Removed invalid states from US immigration dataset. Created staging data from i94 data.
Removed invalid ports, Only used temperatures from United States and mapped full name to city port abbrv. Create staging data from Temperature dataset.
Caculated the percentage of demographics column. Used a pivot for the Race column. Create staging data from Demographics dataset.


### Step 3: Define the Data Model
## Conceptual Data Model
The star schema is chosen as the data model because it is simple and yet effective. users can write simple queries by joing fact and dimension tables to analyze the data. Define Dimension tables and fact tables.

### Step 4: Build ETL Pipelines 
## Run Data Quality checks