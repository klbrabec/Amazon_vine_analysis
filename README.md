# Amazon_vine_analysis
Week 17 Challenge

## Overview 
The purpose of this analysis is to review customer reviews for a category of products offered by Amazon.  This analysis will allow us to determine if there is any relationship between the participation in Amazon's Vine program and 5-star reviews given to a product. 

Data was pulled from the Amazon Review Datasets that are available here: https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt.  For this particular study, data from the Pet Products v1 dataset was reviewed.  

Data was pulled into a Google Colab notebook (https://github.com/klbrabec/Amazon_vine_analysis/blob/main/Amazon_Reviews_ETL.ipynb) and processed using Spark in preparation to be loaded into a database.   Data was originally loaded into a raw dataframe.  The original layout of the dataframe is below: 

![dataframelayout](https://github.com/klbrabec/Amazon_vine_analysis/blob/main/DATATYPES.JPG)

From the raw dataframe - data was broken out into four different tables for analysis.    Once the initial dataframe structures were created and the initial records pulled into those dataframes, the dataframes were processed to remove duplicate records.  The four separate dataframes included: 
-- Review Dataframe - Contains information related to reviews
-- Customer Dataframe - Contains information related to customers 
-- Product Dataframe - Contains information related to products 
-- Vine Dataframe - Contains information related to the Vine program 

This information was then loaded into a PostGres database in AWS for further analysis.    This particular analysis project focused only on the Vine program.  Information from the vine table in the PostGres database was downloaded as a .csv file that was analyzed in Pandas Python. 

## Results
Using Pandas, the .csv file was read in for processing and analysis.  (https://github.com/klbrabec/Amazon_vine_analysis/blob/main/Vine_Review_Analysis.ipynb)

Inital processing created a dataframe that contained only those records that had over 20 reviews.  This was done to provide records that had more votes indicating that the review was helpful as well as remove the risk of any future division by zero issues.  

That dataframe was further filtered to create a dataframe containing records where the percentage of helpful_votes compared to total_votes was equal to or greater than 50%.    From this dataframe, we were able to filter and compare the records.  

The total number of records in the dataset is: 38010

![TotalNumberofRecords](https://github.com/klbrabec/Amazon_vine_analysis/blob/main/TotalNumberReviews.JPG)

The total number of paid reviews in the dataset is: 170 

![TotalNumberPaidReviews](https://github.com/klbrabec/Amazon_vine_analysis/blob/main/TotalNumberPaidReviews.JPG)

The total number of paid five star reviews in the dataset is: 65 

![TotalNumberPaid5starReviews](https://github.com/klbrabec/Amazon_vine_analysis/blob/main/TotalNumberPaidFiveStarReviews.JPG)

The percentage of paid five star reviews is: 0.171008 

![percentagepaidfivestarreviews](https://github.com/klbrabec/Amazon_vine_analysis/blob/main/percentagepaidfivestarreviews.JPG) 

The total number of unpaid paid reviews in the dataset is: 37840

![TotalNumberUnPaidReviews](https://github.com/klbrabec/Amazon_vine_analysis/blob/main/TotalNumberUnpaidReviews.JPG)

The total number of unpaid five star reviews in the dataset is: 20612

![TotalNumberunPaidFiveStarReviews](https://github.com/klbrabec/Amazon_vine_analysis/blob/main/TotalNumberUnpaidFiveStarReviews.JPG)

The percentage of unpaid five star reviews in the dataset is: 54.227835

![PercentageunpaidFiveStarReviews](https://github.com/klbrabec/Amazon_vine_analysis/blob/main/percentageunpaidfivestarreviews.JPG) 

## Summary 
### Is there Bias? 
There does not appear to be a positivity bias for reviews that are entered through the Vine program.    The percentage of five star reviews for Vine program reviews is 0.171008.  If there was an incentive for people to leave five star reviews, it would be expected that this percentage would be much higher.  

### Additional Analysis
In order to prove this, it is recommended to do the same types of analysis for all star_ratings.  If there was bias that drives users to select a particular star rating, the percentages for Vine reviews would be substantially higher than the non Vine reviews.  
