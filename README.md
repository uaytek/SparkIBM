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

## Problem Statement
The first task  to predict the churned group from data is data exploration to define the churn and to idenntify the features. Especially page data that gives info about the users visit has relevant information about the churn. 

Identifying catefory columns also helped for defining some features. Main focus definning features is the users main events in the system. So some questions should be answered like how many songs and in which hour they are listening in a day, do they have interaction to system, do they have error during they are listenning music.

## Metric


## Data Exploration
There are Four categories; gender, level, auth and method used in data. gender and level added to feature list. Because auth and method gives info about the technical system, they were not included in list. 

he pages that visited by users gives many information of user events and definning features like thump  

|               About|
|          Add Friend|
|     Add to Playlist|
|              Cancel|
|Cancellation Conf...|
|           Downgrade|
|               Error|
|                Help|
|                Home|
|               Login|
|              Logout|
|            NextSong|
|            Register|
|         Roll Advert|
|       Save Settings|
|            Settings|
|    Submit Downgrade|
| Submit Registration|
|      Submit Upgrade|
|         Thumbs Down|
|           Thumbs Up|
|             Upgrade|
+--------------------+



### Define Churn 
Cancellation Confirmation events defined the churn. 1 as churned and 0 stayed users.

### Feature Engineering

All features are listed below. Label coulumn is the churn values. 
+------+-------+-------+----+---+-----+----+-----------+--------------+----------------+--------------+-----------+-----+
|userId|is_male|is_paid|hour|day|month|year|songs_total|thumbsup_Total|thumbsdown_total|downgradeTotal|error_count|label|
+------+-------+-------+----+---+-----+----+-----------+--------------+----------------+--------------+-----------+-----+
|   124|      0|      1|  15| 30|   11|2018|       4079|           171|              41|            41|          6|    0|
|    51|      1|      1|   7| 17|   10|2018|       2111|           100|              21|            23|          1|    1|
|    15|      1|      1|   4| 25|   11|2018|       1914|            81|              14|            28|          2|    0|
|    54|      0|      1|  19| 12|   11|2018|       2841|           163|              29|            39|          1|    1|
|   155|      0|      1|  11| 28|   11|2018|        820|            58|               3|            12|          3|    0|
+------+-------+-------+----+---+-----+----+-----------+--------------+----------------+--------------+-----------+-----+

## Implementation
PySpark and SparkML libraries to implement the solution. 

### Data transformation, data splitting  

Data was splitted 20% for trainning and 80% for testing, 
The transformer VectorAssembler is used to combine a given list of columns into a single vector column so that decision tree can be used for modelling. 

StandardScaler is also used normalizing the single vector. 


### Model Training

RandomForestClassifier is used for modelling. Because the initial recall and F1 Score is high no other models used. 

The next step is using coss validation to find the ideal hyper-parameters for Random Fores Classifier.The ideal paramneters are MaxDepth 5 and numTrees = 20. 

## File Description
The project was started to develop on EMR cluster, but there is no success building the model because of a specific error in StandardScaler code. The same code copied to UDACITY workspace and IBM Watson Studio, there was no problem in any code line.

Udacity_Sparkify.ipynb : Jputer notebook used for this project

s3n://udacity-dsnd/sparkify/mini_sparkify_event_data.json :128 MB. Data 

IBM_Watson_Sparkify.ipynb : Jupyter notebook in IBM Watson Studio

# Conclusion
 F1 Score is %92.8. on the test dataset using the Random Forest algorithm. T
