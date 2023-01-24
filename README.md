# Bikeshire
## Table of Contents
- [Overview of the Analysis](#overview-of-the-analysis)
    - [Purpose](#purpose)
    - [About the Dataset](#about-the-dataset)
    - [Tools Used](#tools-used)
    - [Description](#description)
        - [Model Comparison](#Model-Comparison)
        - [Building Models](#Building-Models)
        - [Compiling Models](#Compiling-Models)
        - [Model Architectures](#Model-Architectures)
        - [Model Metrics](#Model-Metrics)
- [Results](#results) 
    - [Deep Neural Network (DNN)](#Deep-Neural-Network)
    - [Convolutional Neural Network (CNN)](#Convolutional-Neural-Network)
    - [Deep Convolutional Neural Network (DCNN)](#Deep-Convolutional-Neural-Network)
    - [Making an Example Prediction](#Making-an-Example-Prediction)
- [Summary](#summary)
- [Contact Information](#contact-information)

## Overview of the Analysis
### Purpose:


### About the Dataset:
The dataset is the NYC Citibike dataset taken from the public datasets available in BigQuery. The "citibike_trips" table used herein can be found under the "new_york_citibike" dataset on BigQuery, to be exact. The "citibike_trips" contains nearly 59 million records (58,937,715).
The schema for it can be seen below:

![]()

### Tools Used:
* Google Cloud Platform (GCP) - Vertex AI, BigQuery, Cloud Shell, Cloud Storage Buckets
* APIs - Vertex AI API, Notebooks API, Cloud SQL Admin API
* Python 
* SQL
* My SQL

### Description:
The Cloud Shell was activated and the project configured therein. In BigQuery, the "new_york_citibike" dataset was then starred, which contains two tables: citibike_stations and citibike_trips. 

#### Queries in Cloud SQL
Queries written and run on the data in citibike_trips extract starting stations and end stations, and the results are then saved as CSV files locally. 

![query_]()

A Cloud Storage bucket is then created, wherein these CSV files are uploaded and renamed to 'start_stations' and 'end_stations'. A Cloud SQL instance is then created by visiting the Navigation menu > SQL > Create Instance > Choose MySQL. The Cloud Shell is opened in a new tab, and we connect to the SQL instance created earlier through the following command:

gcloud sql connect NAME_OF_INSTANCE --user=root --quiet

Once the mysql> prompt appears, a new database called 'bike' is created. Within this databse, two empty tables named 'nyc1' and 'nyc2' are created. In the Cloud Console, the two CSV files 'start_stations' and 'end_stations' are then imported (from the Cloud Storage bucket) into the 'nyc1' and 'nyc2' tables, respectively. In the Cloud Shell session, we confirm the two tables have been filled now. 'nyc1' contains 919 rows and 'nyc2' contains 967 rows. The records were grouped by (GROUP BY) the station names, hence why there are only 919 starting stations and 967 end stations out of around 59 million records. 

![nyc1_top3]()
![nyc1_rows]()
![nyc2_top3]()
![nyc2_rows]()

The header rows are deleted from the two tables.

![code_DELheaders]()

The tables are now ready to query data from (results shared under the Results section).

#### Data Visualizations in Vertex AI (Writing Queries in Notebook and Visualizing the Results)
Queries were written in a Notebook on the original citibike_trips data (which has around 59 million records), and the reuslts then visualized. Vertex AI API (and the Notebook API) was enabled, and a notebook created by visiting User-Managed Notebooks > New Notebook > Python 3. To be able to run queries on a BigQuery dataset through the notebook, we first installed and then imported the BigQuery Python Client library. 

![install]()
![import]()

The BigQuery Client is then initialized. BigQuery Client helps with the flow of messages to and from the BigQuery API.

![initialize]()

A query is run on the Bigquery dataset and the results stored in a dataframe. The data is then pivoted to create charts.

![code_query]()
![code_df]()

<img style="width:60%" alt="acc_nn" src="">

## Results
### Cloud SQL Queries

### Data Visualizations 

### Making an Example Prediction:


## Summary

## Contact Information
Email: st.sohatariq@gmail.com

 
