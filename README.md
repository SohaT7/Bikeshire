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
    - [Vertex AI Queries and Data Visualizations](#Vertex-AI-Queries-and-Data-Visualizations)
- [Summary](#summary)
- [Contact Information](#contact-information)

## Overview of the Analysis
### Purpose:
This project runs queries on the 59 million records in the BigQuery public dataset New York Citibike, in addition to making data visualizations, using Cloud SQL (MySQL), Vertex AI, Cloud Shell, and Cloud Storage buckets in Google Cloud Platform (GCP).

### About the Dataset:
The dataset is the NYC Citibike dataset taken from the public datasets available in BigQuery. The "citibike_trips" table used herein can be found under the "new_york_citibike" dataset on BigQuery, to be exact. The "citibike_trips" contains nearly 59 million records (58,937,715).

### Tools Used:
* Google Cloud Platform (GCP) - Vertex AI, BigQuery, Cloud Shell, Cloud Storage Buckets
* APIs - Vertex AI API, Notebooks API, Cloud SQL Admin API
* Python 
* SQL
* My SQL

### Description:
The Cloud Shell was activated and the project configured therein. In BigQuery, the "new_york_citibike" dataset was then starred, which contains two tables: citibike_stations and citibike_trips. The latter, containing around 59 million records was used in this project.

The project is divided into two parts:
* The first part writes and runs queries in Cloud SQL (MySQL), and makes use of Cloud Shell and Cloud Storage buckets.
* The second part writes queries and visualizes data in a Vertex AI notebook, and makes use of BigQuery Client to send and receive messages from the BigQuery API.

In sum total, the project answers the following questions from the data:

* Top Starting Stations (in general, and where users are greater than 250000 only)
* Top End Stations (in general, and where users are greater than 250000 only)
* Bottom Starting Stations (in general, and where users are less than 100 only)
* Bottom End Stations (in general, and where users are less than 100 only)
* Number of users for each Usertype (Customer or Subscriber) by years
* Number of users with a specific Gender by years

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
Queries were written in a Notebook on the original citibike_trips data (which has around 59 million records), and the reuslts then visualized. Vertex AI API (and the Notebook API) was enabled, and a notebook created by visiting User-Managed Notebooks > New Notebook > Python 3. To be able to run queries on a BigQuery dataset through the notebook, we first installed, and then imported and initialized the BigQuery Python Client library. BigQuery Client helps with the flow of messages to and from the BigQuery API. Queries are then run on the Bigquery dataset and the results stored in a dataframe. The data is then pivoted to create charts. 

## Results
### Cloud SQL Queries
Queries run on Cloud SQL (shown below) included:
* Top starting stations (where number of users are greater than 250000), arranged in a descending alphabetical order (i.e. by station name)
* Top starting stations (where number of users are greater than 250000), arranged in a descending order by number of users
* Top end stations (where number of users are greater than 250000), arranged in a descending alphabetical order (i.e. by station name)
* Top end stations (where number of users are greater than 250000), arranged in a descending order by number of users

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

### Vertex AI Queries and Data Visualizations 
BigQuery Client was used to run queries on the dataset in BigQuery via a Notebook. The results were dispalyed in the form of a dataframe, and the data pivoted to create charts. Queries and charts were created for the following:
* Top 10 starting and end stations
* Bottom 10 starting and bottom 30 end stations
* Usertype by year 
* Gender by year

The following query produces the top 10 starting stations and arranges them in a descending order as per their number of users. It returns the results in the form of a dataframe and then creates a stacked bar chart using the results. 

<img style="width:60%" alt="code_sql" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/code_sql.png">

<img style="width:100%" alt="code_pivot" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/code_pivot.png">

<img style="width:100%" alt="top10start" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/top10start.png">

A bar chart for the bottom 10 starting stations is given below:

<img style="width:100%" alt="bottom10start" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/bottom10start.png">

Following are the bar charts for the top 10 end stations and the bottom 30 end stations:

<img style="width:100%" alt="top10end" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/top10end.png">

<img style="width:100%" alt="bottom30end" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/bottom30end.png">

A query run to find the number of users for each usertype (i.e. customer and subscriber) is given below, followed by variations of bar charts displaying the results:

<img style="width:60%" alt="query_usertype" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/query_usertype.png">

<img style="width:100%" alt="chart_usertype" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/chart_usertype.png">

<img style="width:100%" alt="chart_usertype3" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/chart_usertype3.png">

<img style="width:100%" alt="chart_usertype2" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/chart_usertype2.png">

Subscribers form the larger chunk of users, being almost 40%-100% higher than the number of Customers. Sharper increases can be observed from 2013-2014 and from 2016-2017 for Subscribers. For Customers, there is a very small increase from 2013-2014 and a relatively larger increase from 2016-2017. There is a slight decrease in number of Customers from 2015 to 2016. 2017-2018 shows a decline in both the number of Customers as well as Subscribers.

Lastly, a query was run to find out the number of users that fall into different categories of gender, and how those numbers have changed over the years:

<img style="width:60%" alt="query_gender" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/query_gender.png">

The different car charts visulaizing gender of users by years are shown below:

<img style="width:100%" alt="chart_gender" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/chart_gender.png">

<img style="width:100%" alt="chart_gender2" src="https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/chart_gender2.png">

There has been an increase in number of users for all gender categories up until 2017, whereafter there has been a decline. Relatively sharper increases can be observed from 2013-2014 and 2016-2017, with an almost leveling during the 2015-2016 year in between. Male gender consists of the largest chunk of users, followed by females, and then the 'unknown' category. 

## Summary
The top starting and end stations have been queried in general but also with a specific conditional of number of users being greater than 250000 applied to them. Similarly for bottom starting and end stations, where the conditional spcified that the number of users should be less than 100. The results are given above. The number of users by Usertype and Gender were also queried, in order to compare how the ratios of users falling in each category within Usertype and Gender have changed over the years.

## Contact Information
Email: st.sohatariq@gmail.com

 
