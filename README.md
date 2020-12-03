# We-Rate-Dogs-Analysis
# Wrangle Report Summary
### Pre-requesite Python packages
* pandas
* requests
* os
* numpy
* tweepy
* json
* wptools
* time
* matplotlib
### Introduction
The purpose of this notebook is to demonstrate initial steps to clean data from the WeRateDogs database in order to perform insightful analysis.

Below, I describe the steps taken to produce the data clean up and visualizations in wrangly_act.ipynb. There are 3 steps to the data wrangle process.

* Gather
* Assess
* Clean
## Gather
Files Required:

* twitter_arch.csv: The WeRateDogs Twitter archive of data prior to August 1st, 2017.
* image_predictions.tsv: An image prediction file containing information on dog breeds that is hosted in Udacity's servers.
* tweet_json.txt: File downloaded programmatically using the Tweepy API to fetch the favorite/retweet counts for each tweet_id in twitter_arch.csv
Assess
The following steps were used to assess the data in the 3 files mentioned above:

* Initial visual analysis (i.e looking for anything suspicious in the data by inspecting samples)
* Data information using pandas dataframes (Ex: null values, duplicates, incorrect data types)
* Advanced data quality/tidiness analysis using pandas. (Ex: Irrelevant data exclusion)
As a result, several issues were found. These can be classified in 2 groups: Quality and Tidiness issues.

_**Note**_: This process was not exhaustive. I limited the amount of issues to 10 but there are potentially many more data issues left to fix.

### Quality
**twitter_arch**
* retweeted_status_id is NaN in 2175 rows, this should be 0 instead.
* Remove 112 retweets.
* Remove images associated to retweets.
* Incorrect data type for retweeted_status_id and retweet_status_user_id. It should be an integer instead of a float.
* There are 745 records where the dog's name is "N/A" or "Null" or "None".
* Source has html, this should be removed to show a more readable source.
* The following columns should be datetime instead of string: timestamp, retweet_status_timestamp.
* Remove the in_reply_to_status_id, in_reply_to_user_id, retweeted_status_id, retweeted_status_user_id since we won't do any analysis on those columns.
**image_pred**
* 66 duplicate images.
* There are some tweets missing images.
### Tidiness
* The dog statuses are in 4 different columns when they could just be in 1.
* The twitter_arch and tweet_json tables can be merged.
## Clean
The quality issues mentioned above were manually and programmatically fixed. Joins between all 3 tables were used to determined only the relevant data and exclude unnessary data (i.e duplicates, retweets, tweets missing images, irrelevant columns).

As a standard, for each issue there is Coding and Testing section. An assessment of the existing data is taken prior to coding the changes and is used to compare with the resulting data in the testing section.
