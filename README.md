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

## ETL (extract, transform, and load) 
Originally created in Google Colab for PySpark to run, these dataframes were then loaded to AWS RDS using a a connection from PySpark to PostgreSQL. See [Amazon_Reviews_ETL.pynb](https://github.com/ramya-ramamur/Amazon_Vine_Analysis/blob/main/Amazon_Reviews_ETL.ipynb) for complete code. 

**Table1: customers_table**

<img width="1120" alt="Screen Shot 2022-02-14 at 9 42 35 PM" src="https://user-images.githubusercontent.com/75961057/153999725-7a97568f-15f1-432d-b611-d99b59e680ab.png">

**Table2: products_table**

<img width="863" alt="Screen Shot 2022-02-14 at 9 43 36 PM" src="https://user-images.githubusercontent.com/75961057/153999865-e6d6b716-633d-4c40-bd90-16cac3e5937a.png">

**Table3: review_id_table**

<img width="1249" alt="Screen Shot 2022-02-14 at 9 45 27 PM" src="https://user-images.githubusercontent.com/75961057/154000017-2182dba0-7e24-49e3-8df1-0b2f5435abed.png">

**Table4: vine_table**

<img width="1004" alt="Screen Shot 2022-02-14 at 9 46 58 PM" src="https://user-images.githubusercontent.com/75961057/154000162-bdc1a006-e44a-4663-b3a5-1ff842829303.png">


## Analysis with vine_table

Using the extracted vine_table, an analysis was performed on the Amazon Vine program to determine if there is a bias toward favorable reviews from Vine members.
See [Vine_Review_Analysis.pynb](https://github.com/ramya-ramamur/Amazon_Vine_Analysis/blob/main/Vine_Review_Analysis.ipynb) for complete code.

* Paid Reviews Dataframe

<img width="1221" alt="Screen Shot 2022-02-14 at 9 52 29 PM" src="https://user-images.githubusercontent.com/75961057/154000821-51ac9b47-b624-4e14-a493-7e5db249fd38.png">

* Unpaid Reviews Dataframe
<img width="1185" alt="Screen Shot 2022-02-14 at 9 54 15 PM" src="https://user-images.githubusercontent.com/75961057/154001051-2dbad201-7713-47dd-b16c-79bfc20259ec.png">

### Total Reviews: Paid vs Unpaid

<img width="594" alt="Screen Shot 2022-02-14 at 9 55 37 PM" src="https://user-images.githubusercontent.com/75961057/154001201-e54abb89-ed94-46b7-af86-9e17ae79ebf1.png">

### 5-star Vine Reviews: Paid vs Unpaid

<img width="795" alt="Screen Shot 2022-02-14 at 9 57 04 PM" src="https://user-images.githubusercontent.com/75961057/154001385-de352254-6586-4ddc-b2d4-1b66a7aef092.png">

### Percentage of 5-star Vine Reviews: Paid vs Unpaid

<img width="1268" alt="Screen Shot 2022-02-14 at 9 58 07 PM" src="https://user-images.githubusercontent.com/75961057/154001501-45ee8a87-d800-4998-ad27-dc4162f24d8f.png">

# Summary
The analysis first filtered by total_votes count is equal to or greater than 20 and then by the number of helpful_votes divided by total_votes is equal to or greater than 50%. From the resulting dataframe, Paid and Unpaid Reviews dataframes were filtered. 

We see that there are 0 fields for Paid Reviews and 403,807 Unpaid Reviews. Under Unpaid Reviews, there are 242,889 5-star reviews which amounts to a total of 60.15% of Unpaid Reviews. 

What these numbers seems to suggest is that there is not strong bias toward five-star reviews from paid Amazon Vine reviewers. We can assume that Vine customers are more critical when submitting their review. We should do furthur analysis and include all of the data rather than filtering it to a percentage of helpful vs. total votes as we did for this analysis. 
