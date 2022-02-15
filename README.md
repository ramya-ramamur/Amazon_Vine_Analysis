Analysis on Amazon's vine review program using PySpark and AWS RDS with PostgreSQL

# Amazon_Vine_Analysis

# Overview
The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. This project analyzes Amazon Vine program and determines if there is a bias toward favorable reviews from Vine members.

The analysis uses PySpark to perform the ETL (extract, transform, and load) process to extract the dataset, transform the data, connect to an AWS RDS instance, load the transformed data into PostgreSQL server (pgAdmin). 

After the ETL process, analysis was done to answer the following questions:
* How many Vine reviews and non-Vine reviews were there?
* How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars?
* What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars?

# Resources
* **Data Source:** From [Amazon Review Datasets](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt),  [the Books_v1_02.tsv.gz](https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Books_v1_02.tsv.gz) dataset was chosen.
* **Software:** Google Colab Notebook, PostgreSQL 11.9, pgAdmin 4, AWS

# Results

#### ETL (extract, transform, and load) 
Originally created in Google Colab for PySpark to run, these dataframes were then loaded to AWS RDS using a a connection from PySpark to PostgreSQL. See 

**Table1: customers_table**

