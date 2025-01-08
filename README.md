# Hands-on Airbyte, Apache Airflow, PostgreSQL and BigQuery

This repository for course Data Ingestion using Airbyte in Data Engineering Mini Bootcamp. 
In this course use tech stack : 
- Data Ingestion : Airbyte
- Workflow Orchestions : Apache Airflow
- Data Platform : OLTP(PostgreSQL) & OLAP(BigQuery)

## Prerequisite
1) Already installed docker and docker compose
2) Already have service account key json file for Google BigQuery
3) Already installed postgresql in local
4) Already installed vscode or other IDE

## Table of Content
1) Install Airbyte OSS in local
2) Define source connection in Airbyte
3) Define destination connection in Airbyte
4) Configure connection in Airbyte
5) Create Airbyte Connection in Airflow Web Server
6) Create airflow dags for trigger Airbyte job

### Install Airbyte OSS in local
please refer to this [docs](https://docs.airbyte.com/using-airbyte/getting-started/oss-quickstart#part-1-install-abctl)

### Define source connection in Airbyte (CSV)
- Click New Connection
- In Define source, choose setup new source
- Input csv in search text box then click File
- Input dataset name and choose file format csv 
- For Storage Provider choose HTTPS : Public Web and input URL : https://storage.googleapis.com/raw_data_alterra_batch2_2024/customer.csv 
- Click set up source

### Define source connection in Airbyte (Postgres)
- Click New Connection
- In Define source, choose setup new source
- Input postgres in search text box then click File
- Input source name
- Input host : host.docker.internal if postgres db installed in local computer not in docker
- Input port : 5432
- Input DB name
- Input User and password
- For Update Method, choose option Scan Changes with User Defined Cursor
- Click set up source 

### Define destination connection in Airbyte
- In Define destination, choose setup new destination
- Input BigQuery in search text box then click BigQuery
- Input destination name
- Input project id, dataset location and default dataset id based in dataset destination
- For loading method, choose Batch Standard Inserts. If file size is big from data source then choose second option GCS Staging
- Copy Paste Service Account that already created before
- Click Setup destination

### Configure connection in Airbyte
- In Connection, input connection name
- In Configuration, Choose schedule type manual(because airbyte job will trigger by airflow)
- Click Setup connection
- Click Sync Now

### Create Airbyte Connection in Airflow Web Server
- Click Admin --> Connections
- Input connection id
- Choose connection type : Airbyte
- Input host : host.docker.internal
- Inport port : 8000
- Click Test
- Click Save

### Create airflow dags for trigger Airbyte job
- Go to Airbyte UI then copy connection id for each connection. e.g : b1016cab-07de-499c-84f2-abfc1abdf819
