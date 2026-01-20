# HR Analytics: Employee Attrition Pipeline on AWS

## 📌 Project Overview
This project implements a cloud-native **Data Engineering pipeline on AWS** to analyze employee attrition. By leveraging a serverless "Lakehouse" architecture, the system ingests raw HR data, transforms it for analytics, and visualizes key attrition drivers (e.g., Age, Monthly Income, Job Role) to help HR departments retain top talent.

The entire workflow is built using **AWS Managed Services**, ensuring scalability, cost-efficiency, and zero infrastructure management.

## 🏗 Architecture & Methodology
The pipeline follows a modern data flow, moving data from raw storage to a consumption layer using AWS services:


<img width="1024" height="559" alt="Archi_HR" src="https://github.com/user-attachments/assets/fc893d57-1b40-4ee2-9b65-847e5db1fb48" />



### 1. Ingestion (Data Lake)
* **Amazon S3:** Acts as the centralized Data Lake. Raw HR datasets (CSV format) are uploaded here to a "Raw" bucket. This ensures a single source of truth for all downstream analytics[cite: 5244].

### 2. Processing & Cataloging (ETL)
* **AWS Glue Crawlers:** Automatically scans the S3 buckets to infer the schema (column names, data types) and populates the **AWS Glue Data Catalog**.
* **AWS Glue ETL Jobs:** Serverless Apache Spark jobs (written in Python) clean the data, handle null values, and standardize formats before writing the processed data back to a "Curated" S3 bucket.

### 3. Analytics & Visualization
* **Amazon Athena:** Provides serverless SQL querying capabilities directly against the S3 data. This allows for ad-hoc analysis without loading data into a traditional database.
* **Amazon QuickSight:** Connects to Athena as a data source to build interactive, auto-updating dashboards.

## 📈 Dashboard & Insights

<img width="1476" height="911" alt="Code_Generated_Image" src="https://github.com/user-attachments/assets/729a69d6-c1a9-4fcb-b360-930d21d21e81" />


The **Amazon QuickSight** dashboard allows stakeholders to visualize and drill down into attrition metrics:
* **Attrition Overview:** Tracks the overall attrition rate and total employee count.
* **Demographic Heatmaps:** Visualizes attrition spikes in specific segments, such as the **25-35 Age Group** or specific **Marital Statuses**.
* **Income Analysis:** A scatter plot correlating **Monthly Income** vs. **Attrition**, helping identify if salary discrepancies drive turnover.
* **Role-Based Risk:** Bar charts identifying "High Risk" job roles (e.g., Sales Representatives often show higher attrition than Research Directors).

## 🛠 Tech Stack
* **Cloud Provider:** Amazon Web Services (AWS)
* **Storage:** Amazon S3 (Simple Storage Service)
* **ETL:** AWS Glue (Crawlers, Jobs, Data Catalog)
* **Query Engine:** Amazon Athena (Serverless SQL)
* **Visualization:** Amazon QuickSight
* **Security:** AWS IAM (Roles & Policies)

## 📊 Key Data Attributes
The analysis is based on 35+ attributes for each employee, including:
* **Personal:** Age, Gender, Marital Status, Education Field.
* **Employment:** Department, Job Role, Job Level, OverTime status.
* **Compensation:** Monthly Income, Percent Salary Hike, Stock Option Level.
* **Satisfaction:** Job Satisfaction, Environment Satisfaction, Work-Life Balance.

## 🚀 Key Features
* **Serverless Architecture:** The pipeline is fully managed (S3, Glue, Athena), meaning no servers to provision or patch.
* **Schema Evolution:** Glue Crawlers automatically detect changes in source data (e.g., if a new column is added) and update the Data Catalog without breaking the pipeline.
* **Cost-Effective:** Utilizing S3 for storage and Athena for on-demand querying minimizes costs compared to running a dedicated data warehouse 24/7.
