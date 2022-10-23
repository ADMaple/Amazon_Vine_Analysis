# Amazon_Vine_Analysis

## Overview
The purpose is to analyze Amazon reviews written by members of the paid Amazon Vine program. The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. Companies like SellBy pay a small fee to Amazon and provide products to Amazon Vine members, who are then required to publish a review. To do this I had use PySpark to perform the ETL process to extract the dataset, transform the data, connect to an AWS RDS instance, and load the transformed data into pgAdmin. Then use PySpark to determine if there is any bias toward favorable reviews from Vine members in the Outdoor products dataset.

Deliverable 1: Perform ETL on Amazon Product Reviews

Deliverable 2: Determine Bias of Vine Reviews

## Resources

-Data Source: https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Outdoors_v1_00.tsv.gz

-Software: AWS (RDS, S3), ProgreSQL, Google Colab, PySpark

## Analysis of Data
The raw data set is uploaded to an S3 bucket in Amazon RDS. The Postgresql tables are already formatted to match the data frames that will be generated.

**Customer DataFrame**

![Customer_df](https://user-images.githubusercontent.com/108022219/197396668-6f153186-0f49-4799-a25f-0bebb709dc4a.png)

This shows the customer id and count.

**Product DataFrame**

![product_df](https://user-images.githubusercontent.com/108022219/197395018-19942c8c-54f0-4638-8d85-581f90e944f6.png)

This shows the product by id and title. 

**Reviews DataFrame**

![review_id_df](https://user-images.githubusercontent.com/108022219/197395019-e4c95110-06d4-4c6f-aff3-0e8e1a9f7b8d.png)

This shows how the customer id and product information are linked to the reviews by id and review dates.

The review data is then filtered into a table to only include reviews with 20 or more votes.
Then review data filtered into a table to only include those that recieved a 50% or above "Helpful" vote.
The vine dataframe is created which shows the customer, product, and review data all in one dataframe.
       The data is then separated into two groups:
            - Paid reviews
            - Unpaid reviews
            
![vine_df](https://user-images.githubusercontent.com/108022219/197395947-df095c92-9783-4e6a-836e-3b8f6b1ce408.png)

## Results of Data
From the dataframes created previously I was able to find the percentage of paid and unpaid 5-star reviews.

**Paid Reviews**

![Paid_reviews](https://user-images.githubusercontent.com/108022219/197395945-b1b0ff3d-f0d5-4985-b15a-4dc92ce52c53.png)

There are a total of 107 paid reviews, with 56 of those reviews being 5 star. The paid 5 star reviews make up 52%


**Unpaid Reveiws**

![Unpaid_reviews](https://user-images.githubusercontent.com/108022219/197395946-af6c46b7-48fc-4a19-9583-4a27ee5a39f4.png)

There are a total of 39,869 unpaid reviews, with 21,005 of those reviews being 5 star. The unpaid 5 star reviews make up 53%

## Summary 
Evaluation of reviews from the outdoor products results in a somewhat surprising conclusion.. The number of paid 5-star reviews is outnumbered by unpaid 5-star reviews by a factor of nearly 300:1. An overwhelming number of unpaid reviews are 5 stars, and comprise 53% of the total unpaid population. Of the 107 paid reviews, only 56 were 5 stars, comprising only 52% of the total paid review population. The conclusion drawn from the assessment is that consumers need no additional incentive to report a good experience with a product. This is proven by the overwhelming ratio of unpaid 5-star reviews to paid (incentivized) reviews. Note that this conclusion is drawn without the consideration of any omitted variables that could dictate the skew of the population towards the unpaid side.
