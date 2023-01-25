# Bikeshire
## Table of Contents
- [Overview of the Analysis](#overview-of-the-analysis)
    - [Purpose](#purpose)
    - [About the Dataset](#about-the-dataset)
    - [Tools Used](#tools-used)
    - [Description](#description)
        - [Queries in Cloud SQL](#Queries-in-Cloud-SQL)
        - [Queries and Data Visualizations in Vertex AI](#Queries-and-Data-Visualizations-in-Vertex-AI)
- [Results](#results) 
    - [Cloud SQL Queries](#Cloud-SQL-Queries)
    - [Data Visualizations](#Data-Visualizations)
- [Summary](#summary)
- [Contact Information](#contact-information)

## Overview of the Analysis
### Purpose:


### About the Dataset:
The dataset is the NYC Citibike dataset taken from the public datasets available in BigQuery. The "citibike_trips" table used herein can be found under the "new_york_citibike" dataset on BigQuery, to be exact. The "citibike_trips" contains nearly 59 million records (58,937,715).

### Tools Used:
* Google Cloud Platform (GCP) - Vertex AI, BigQuery, Cloud Shell, Cloud Storage Buckets
* APIs - Vertex AI API, Notebooks API, Cloud SQL Admin API
* Python 
* SQL
* My SQL

### Description:
The Cloud Shell was activated and the project configured therein. In BigQuery, the "new_york_citibike" dataset was then starred, which contains two tables: citibike_stations and citibike_trips. 

#### Queries in Cloud SQL
Queries written and run on the data in citibike_trips extract number of users for each starting stations and end stations (GROUP BY, ORDER BY), and the results are then saved as CSV files locally. 

<img style="width:100%" alt="query_nyc1" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/query_nyc1.png">

A Cloud Storage bucket is then created, wherein these CSV files are uploaded and renamed to 'start_stations' and 'end_stations'. A Cloud SQL instance is then created by visiting the Navigation menu > SQL > Create Instance > Choose MySQL. The Cloud Shell is opened in a new tab, and we connect to the SQL instance created earlier through the following command:

gcloud sql connect NAME_OF_INSTANCE --user=root --quiet

Once the mysql> prompt appears, a new database called 'bike' is created. Within this databse, two empty tables named 'nyc1' and 'nyc2' are created. In the Cloud Console, the two CSV files 'start_stations' and 'end_stations' are then imported (from the Cloud Storage bucket) into the 'nyc1' and 'nyc2' tables, respectively. In the Cloud Shell session, we confirm the two tables have been filled now. 'nyc1' contains 919 rows and 'nyc2' contains 967 rows. The records were grouped by (GROUP BY) the station names, hence why there are only 919 starting stations and 967 end stations out of around 59 million records. 

<img style="width:60%" alt="nyc1" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/nyc1.png">
<img style="width:60%" alt="nyc1_rows" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/nyc1_rows.png">
<img style="width:60%" alt="nyc2" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/nyc2.png">
<img style="width:60%" alt="nyc2_rows" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/nyc2_rows.png">

The header rows are deleted from the two tables.

<img style="width:60%" alt="query_DELheaders" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/query_DELheaders.png">

The tables are now ready to query data from (results shared under the Results section).

#### Queries and Data Visualizations in Vertex AI
Queries were written in a Notebook on the original citibike_trips data (which has around 59 million records), and the reuslts then visualized. Vertex AI API (and the Notebook API) was enabled, and a notebook created by visiting User-Managed Notebooks > New Notebook > Python 3. To be able to run queries on a BigQuery dataset through the notebook, we first installed, and then imported and initialized the BigQuery Python Client library. BigQuery Client helps with the flow of messages to and from the BigQuery API.

Queries are run on the Bigquery dataset and the results stored in a dataframe. The data is then pivoted to create charts. The following query produces the top 10 starting stations and arranges them in a descending order as per their number of users. It returns the results in the form of a dataframe and then creates a stacked bar chart using the results. 

<img style="width:60%" alt="code_sql" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/code_sql.png">

<img style="width:100%" alt="code_pivot" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/code_pivot.png">

## Results
### Cloud SQL Queries
Queries run on Cloud SQL (shown below) included:
* Top starting stations (where number of users is greater than 250000), arranged in a descending alphabetical order (i.e. by station name)
* Top starting stations (where number of users is greater than 250000), arranged in a descending order by number of users
* Top end stations (where number of users is greater than 250000), arranged in a descending alphabetical order (i.e. by station name)
* Top end stations (where number of users is greater than 250000), arranged in a descending order by number of users

<img style="width:100%" alt="topStart" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/topStart.png">

<img style="width:100%" alt="topStart_D" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/topStart_D.png">

<img style="width:100%" alt="topEnd" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/topEnd.png">

<img style="width:100%" alt="topEnd_D" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/topEnd_D.png">

Queries were also run for (shown below):
* Bottom starting stations (where number of users is less than 100), arranged in a descending order by number of users
* Bottom end stations (where number of users is less than 100), arranged in a descending order by number of users

<img style="width:100%" alt="bottomStart_D" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/bottomStart_D.png">

<img style="width:100%" alt="bottomEnd_D" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/bottomEnd_D.png">

In the following queries:
* Results for top starting stations and top end staions (where number of users is greater than 250000) were combined using the SQL command UNION, and the results arranged in a descending order by number of users
* Results for bottom starting stations and bottom end staions (where number of users is less than 100) were combined using the SQL command UNION, and the results arranged in a descending order by number of users
* Results for top starting stations and top end staions (where number of users is greater than 250000) were combined using the SQL command UNION, and the results arranged in a descending alphabetical order (i.e. by station name)
* Results for bottom starting stations and bottom end staions (where number of users is less than 100) were combined using the SQL command UNION, and the results arranged in a descending alphabetical order (i.e. by station name)

<img style="width:60%" alt="topUnion_D" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/topUnion_D.png">

<img style="width:60%" alt="topUnion" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/topUnion.png">

<img style="width:60%" alt="bottomUnion_D" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/bottomUnion_D.png">

<img style="width:60%" alt="bottomUnion" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/bottomUnion.png">

### Data Visualizations 

<img style="width:100%" alt="top10start" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/top10start.png">

<img style="width:100%" alt="bottom10start" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/bottom10start.png">

<img style="width:100%" alt="top10end" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/top10end.png">

<img style="width:100%" alt="bottom30end" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/bottom30end.png">

<img style="width:100%" alt="chart_usertype" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/chart_usertype.png">

<img style="width:100%" alt="chart_usertype3" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/chart_usertype3.png">

<img style="width:100%" alt="chart_usertype2" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/chart_usertype2.png">

<img style="width:100%" alt="chart_gender" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/chart_gender.png">

<img style="width:100%" alt="chart_gender2" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/chart_gender2.png">

## Summary

## Contact Information
Email: st.sohatariq@gmail.com

 
