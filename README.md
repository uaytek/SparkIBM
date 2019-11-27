# Udacity DSND Capstone Data Analysis with Spark
Sparkify Project
Analysis of medium_sparkify_event_data.json dataset using IBM Cloud services. 

## Installation
This project uses the following software and python libraries
- Pyspark-2.4.1
- Python 3.6
- NumPy
- Pandas

## Project Overview
Sparkify data consist of users interaction with music stream data. There are two user service levels, paid and free. Users can also upgrade and downgrade their service. Also, events such as playing a song, like or diskike a song, are all recorded. 

The goal of this project is then to analyse users interaction data and predict which group of users are expected to churn - either downgrading from premium to free or cancel thier subscriptions altogether.

### Data Exploration
Learn the data and find cleaning items and identify features

### Define Churn 
Determine which feature or feature value can be user to defin churn

### Feature Engineering
Clean data, prepare features with right types for machine learnings

### Data transformation, data splitting and model training

Split data into training, and test data and Transform feature engineered data.  Build a machine learning model to train using training data and evaluate it. 

## File Description
Sparkify.ipynb : Jputer notebook used for this project

s3n://udacity-dsnd/sparkify/mini_sparkify_event_data.json :128 MB. Data 

The project was started to develop on EMR cluster, but there is no success building the model because of a specific error in StandardScaler code. The same code copied to IBM Watson Studio, there was no problem in any code line.

IBM_Watson_Sparkify.ipynb : Jputer notebook in IBM Watson Studio

# Conclusion
 F1 Score is %92.8. on the test dataset using the Random Forest algorithm. T
