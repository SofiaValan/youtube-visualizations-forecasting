# YouTube Subscribers & Visualization Hours Prediction

## The Context

In this project, I will analyze the data from a YouTube channel focused on Chemistry classes for all levels. This YouTube channel has been actived since March 2021, publishing more than 120 videos until the current date. You can check the YouTube channel [here](https://www.youtube.com/channel/UCzQTrA_c1BgRNLewVyt2UFw).

The data sources I will include in this project are the following ones:

* Video statistics with a daily granularity from YouTube: subscribers, views, likes/dislikes, comments, visualization hours...

* Other interesting metrics based on the country or the subscription origin, for example.

* Google Ads data, available only for the videos that were part of the paid campaigns. This data will be displayed per day and per video. Some of the metrics will be: impressions, clicks, CTR, CPV...

## The Goals

The main question I want to answer with this project is determinating when the channel will be ready for monetization. In order to monetizate a channel on YouTube, you need two requirement:

* Gain 1000 subscribers 
* Get at least 4,000 organic visualization hours in one year

I will answer to this question creating a time series prediction based on statistics methodologies.

With this project, I want to achieve other secondary goals: 

* Performing an Exploratory Data Analysis to understand better the data and discover new trends that are difficult to see in the YouTube Analytics platform.
* Determinating if stopping the campaigns in Google Ads affects in any negative or positive way to the organic growth of the channel.

## Steps Involved on This Project

The steps I will follow to develop this project will be:

* Connect to the YouTube & Google Ads API to get the data with Python
* Do some basic transformations on the data before pushing it to the data warehouse
* Upload the cleaned tables to Google BigQuery (GBQ) from the Python script
* Automate this process, so I can have the most recent data updated on GBQ
* Create some views with SQL in GBQ depending on different granularities
* Perform an exploratory data analysis with Python
* Develop different time series models to predict the subscribers and the visualization hours over time
* Evaluate the results & set up improvements

### Step 1: Connecting to the YouTube API

As I said, the first step on this project is connecting to the YouTube API to gather the basic video metrics on a daily basis. In order to do this, I created a new project inside Google Cloud Platform, extract the data from the different YouTube APIs and then push it in to Google BigQuery.

The main metrics I have extracted are:

* Basic metrics: views, likes , comments, dislikes, shares, subscribersLost, subscribersGained.
* Video performance metrics: estimatedMinutesWatched, averageViewDuration, averageViewPercentage. 
* Annotations performance: annotationImpressions, annotationClicks, annotationClickThroughRate.
* Card performance: cardImpressions, cardClicks, cardClickRate.

You can find the specific definition of all those metrics [in the YouTube API website](https://developers.google.com/youtube/analytics/metrics).

The tables I have extracted from this API are:

* Daily metrics by video
* Daily metrics by country
* Daily metrics by country & video. This is only available for those videos that were added in to paid campaigns in Google Ads.

### Step 2: Connecting to the Google Ads API

The second step is to extract the data from a second data source: Google Ads. As some videos were added to branding campaigns to get more visibility, this could have an impact over the number of subscribers and visualization hours.

The main metrics that I have extracted are:

* Basic metrics: impressions, clicks, CTR, cost, CPV (cost per visualization)
* Interaction metrics: likes gained, shares gained, subscribers gained, visualization hours gained, engagement rate.
* Performance metrics: video quantile reproduction (25%, 50%, 75%, 100%)

### Step 3: The Exploratory Data Analysis

In this step, I am going to answer some questions that can be useful to understand better the data before running any Machine Learning model.

Some of the questions selected are:

* How our target audiences behave? Is there any correlation between them?
* Based on our target variables, what are the videos that performed the best? What characteristics have those videos?
* Which periods of time bring us more subscribers and visualization hours? Yearly, monthly, weekly.
* How Google Ads helped to accomplish our target goals?
* Did the videos promoted had better performance based on the target variables?
* After the paid campaigns were stopped, did the performance of the videos get worse? What happened after three months?
