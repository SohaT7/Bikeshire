# Bikeshire
## Table of Contents
- [Overview of the Analysis](#overview-of-the-analysis)
    - [Purpose](#purpose)
    - [About the Dataset](#about-the-dataset)
    - [Tools Used](#tools-used)
    - [Description](#description)
        - [Queries in Cloud SQL](#Queries-in-Cloud-SQL)
        - [Data Visualizations in Vertex AI](#Data-Visualizations-in-Vertex-AI)
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

![query_nyc1](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/query_nyc1.png)

A Cloud Storage bucket is then created, wherein these CSV files are uploaded and renamed to 'start_stations' and 'end_stations'. A Cloud SQL instance is then created by visiting the Navigation menu > SQL > Create Instance > Choose MySQL. The Cloud Shell is opened in a new tab, and we connect to the SQL instance created earlier through the following command:

gcloud sql connect NAME_OF_INSTANCE --user=root --quiet

Once the mysql> prompt appears, a new database called 'bike' is created. Within this databse, two empty tables named 'nyc1' and 'nyc2' are created. In the Cloud Console, the two CSV files 'start_stations' and 'end_stations' are then imported (from the Cloud Storage bucket) into the 'nyc1' and 'nyc2' tables, respectively. In the Cloud Shell session, we confirm the two tables have been filled now. 'nyc1' contains 919 rows and 'nyc2' contains 967 rows. The records were grouped by (GROUP BY) the station names, hence why there are only 919 starting stations and 967 end stations out of around 59 million records. 

![nyc1](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/nyc1.png)
![nyc1_rows](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/nyc1_rows.png)
![nyc2](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/nyc2.png)
![nyc2_rows](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/nyc2_rows.png)

The header rows are deleted from the two tables.

![query_DELheaders](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/query_DELheaders.png)

The tables are now ready to query data from (results shared under the Results section).

#### Data Visualizations in Vertex AI
Queries were written in a Notebook on the original citibike_trips data (which has around 59 million records), and the reuslts then visualized. Vertex AI API (and the Notebook API) was enabled, and a notebook created by visiting User-Managed Notebooks > New Notebook > Python 3. To be able to run queries on a BigQuery dataset through the notebook, we first installed, and then imported and initialized the BigQuery Python Client library. BigQuery Client helps with the flow of messages to and from the BigQuery API.

A query is run on the Bigquery dataset and the results stored in a dataframe. The data is then pivoted to create charts.

![code_sql](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/code_sql.png)

![code_pivot](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/code_pivot.png)

<img style="width:60%" alt="acc_nn" src="">

## Results
### Cloud SQL Queries

![topStart](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/topStart.png)

![topStart_D](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/topStart_D.png)

![topEnd](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/topEnd.png)

![topEnd_D](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/topEnd_D.png)

![bottomStart_D](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/bottomStart_D.png)

![bottomEnd_D](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/bottomEnd_D.png)

![topUnion_D](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/topUnion_D.png)

![topUnion](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/topUnion.png)

![bottomUnion_D](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/bottomUnion_D.png)

![bottomUnion](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/bottomUnion.png)

### Data Visualizations 

![top10start](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/top10start.png)

![bottom10start](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/bottom10start.png)

![top10end](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/top10end.png)

![bottom30end](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/bottom30end.png)

![chart_usertype](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/chart_usertype.png)

![chart_usertype3](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/chart_usertype3.png)

![chart_usertype2](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/chart_usertype2.png)

![chart_gender](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/chart_gender.png)

![chart_gender2](https://github.com/SohaT7/Bikeshire/blob/main/Resources/Images/chart_gender2.png)

## Summary

## Contact Information
Email: st.sohatariq@gmail.com

 
