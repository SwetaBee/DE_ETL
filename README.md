####  US Immigration information

### Data Engineering Capstone Project

## Project Summary

This project will provide information on US immigration like the most popular cities for immigration, the gender distribution of the immigrants, the average age per immigrants and so on. As more and more immigrants move to the US, officals want to reliably access information about their immigration, weather of the destination, demographics of destination. Also it is important to keep track of immigrants and data like their visa type, visa expire date, entry method to the US. Our dataset is from 3 different sources - the I94 immigration dataset of 2016, city temperature data from Kaggle and US city demographic data from OpenSoft. We defined our data model with 4 dimension tables: (Cities, immigrants, average temperature and time) and 1 fact table: Immigration. We use Spark for ETL jobs.

***The project includes the following steps:***
* Step 1: Scope the Project and Gather Data
* Step 2: Explore and Assess the Data
* Step 3: Define the Data Model
* Step 4: Run ETL to Model the Data
* Step 5: Complete Project Write Up

### Step 1: Scope the Project and Gather Data

#### Scope 
The goal of this project is to extract data from 3 different sources and create fact and dimension table to be able to do analysis on US immigration using factors of city monthly average temperature, city demographics and how things change with time. Finally perform some data quality checks.

#### Describe and Gather Data 
***I94 Immigration Data:*** This data comes from the US National Tourism and Trade Office. A data dictionary is included in the workspace. This is where the data comes from. There's a sample file so you can take a look at the data in csv format before reading it all in. You do not have to use the entire dataset, just use what you need to accomplish the goal you set at the beginning of the project.(https://travel.trade.gov/research/reports/i94/historical/2016.html)

***World Temperature Data:*** This dataset came from Kaggle. (https://www.kaggle.com/berkeleyearth/climate-change-earth-surface-temperature-data)

***U.S. City Demographic Data:*** This data comes from OpenSoft. (https://public.opendatasoft.com/explore/dataset/us-cities-demographics/export/)

***Airport Code Table:*** This is a simple table of airport codes and corresponding cities.(https://datahub.io/core/airport-codes#data)


### Step 2: Explore and Assess the Data

#### Explore the Data 
More than 3 million entries in the i94 df and 659 valid ports. The demo dataset have 49 valid states. UDF written for coversion to pyspark datetime format and validate state codes.
Temperature df has 8.6 million entries. UDF is written to map city full name to city port abbreviation


#### Cleaning Steps
Removed any missing values. Removed invalid states from US immigration dataset. Created staging data from i94 data.
Removed invalid ports, Only used temperatures from United States and mapped full name to city port abbrv. Create staging data from Temperature dataset.
Calculated the percentage of demographics column. Used a pivot for the Race column. Create staging data from Demographics dataset.


### Step 3: Define the Data Model
#### 3.1 Conceptual Data Model
Here we have chosen the star schema for the data modeling part.BY joining fact and dimension tables, we can query to analyze the data. The tables are in the ipynb file.

#### 3.2 Mapping Out Data Pipelines
List of steps necessary to pipeline the data into the data model:

1. Clean the data which includes remove nulls, invalid data types, duplicates, etc
2. Create staging tables for df_immigration_processed, df_temp_processed and df_demo_processed
3. Create dimension tables for df_immigration_dim, df_demographics_dim, df_temperature_dim and df_time_dim
4. Finally Create fact table df_immigration_fact with information on immigration count, mapping cicid in df_immigration_dim, airport_code in df_demographics_dim and State Code df_temperature_dim and arrdate in df_time_dim

### Step 4: Build ETL Pipelines 
## Run Data Quality checks
 My Data Quality checks on the fact and dimension tables were able to query correctly.
 
#### Step 5: Complete Project Write Up

I chose Spark for this project because it is known for processing large amount of data (with less compute time), scale easily with additional worker nodes and integrate appropriately with cloud storage like S3 and data warehouse like Redshift.Spark can also handle different file formats.

The data should be updated monthly in order to handle the files.

Answers:

1. ***If the data was increased by 100x ?***  We can store data in Amazon S3 bucket and scale up larger instances of EC2. Spark would still be the best pltform to use because it can handle ladrge datasets.

2. ***If the data populates a dashboard that must be updated on a daily basis by 7am every day?***  We can use Airflow to schedule and run the ETL during night.

3. ***If the database needed to be accessed by 100+ people?***  We can use data warehouse like Redshiift in the cloud, to hold larger capacity to serve more users, and support workload management and accessiblity for large number of users. We can also use parquet files in HDFS.
