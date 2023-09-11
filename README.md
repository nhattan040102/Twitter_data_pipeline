# A streaming ETL pipeline for RealTime Tweet Collection, Analysis and Reporting

![Pipeline-Diagram](https://github.com/AlphanAksoyoglu/tweeter-etl-pipeline/blob/main/tweet_collector.png?raw=true)

## Description

A basic ETL pipeline concept project which collects realtime tweets from the Twitter API mentioning or from six selected world leaders. Assigns a sentiment score to these tweets and posts the best scoring and worst scoring tweet per hour to a Slack channel via Slack Bot.

### Tech Stack
- Python 3.8 (See requirements.txt's for libraries)
- MongoDB
- Postgres SQL
- Docker
- Twitter API
- Slack (Slackbot)


## The Pipeline 

The pipeline consists of 5 components:

### Tweet Collector

A python script that uses the Tweepy library to listen to Twitter API streams in real time. If one of the listened tweets mention one of the chosen world leaders it is caught pre-processed (we are only interested in the original tweet text and get the original from retweets) and stored in MongoDB

### MongoDB

MongoDB is our Data Lake, where we dump the collected tweets through the Tweet Collector. ETL Job reads from MongoDB and Tweet Collector writes to it 

### Postgres SQL

The Postgres SQL is our Data Warehouse. Where we store sentiment analysed and timestamped tweets. ETL Job writes to Postgres and Slackbot reads from it 

### ETL Job

A python script that reads the tweets at MongoDB, performs a sentiment analysis on them, then writes them to Postgres SQL DB with a timestamp

### Slackbot

A python script that reads the highest and lowest ranking tweet in the Postgres SQL DB
placed in the DB every hour and posts them to the selected Slack channel
