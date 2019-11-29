# Udacity DSND Capstone Data Analysis with Spark

## Installation
This project uses the following software and python libraries
- Pyspark-2.4.1
- Python 3.6
- NumPy
- Pandas

## Project Overview
Sparkify data consist of users interaction with music stream data. There are two user service levels, paid and free. Users can also upgrade and downgrade their service. Also, events such as playing a song, like or diskike a song, are all recorded. 

The goal of this project is then to analyse users interaction data and predict which group of users are expected to churn - either downgrading from premium to free or cancel thier subscriptions.

## Problem Statement
The first task to predict the churned group from data is data exploration to define the churn and to idenntify the features. Especially page data that gives info about the users visit has relevant information about the churn. 

Identifying category columns also helped for defining some features. Main focus definning features is the users main events in the system. So some questions should be answered like how many songs and in which hour they are listening in a day, how they interact with other users or pages, do they have any error in the system.

## Metric
The problem is to identify users who are about to churn, so we should prevent false negative results and focus on recall (true-positive). 

F1 score is also included as a metric, because precision can also be considered after identifying possible churn users. 

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
Cancellation Confirmation events defined the churn. This event can be define in page data. 1 as churned and 0 stayed users.

### Feature Engineering

The features are listed below. 

1. userId - initial id of the user
2. gender - user's gender
3. songs_total - total songs of events per day for the user
4. thumbs_up - total of thumbs up for each users
5. thumbs_down - total of thumbs down for each users
6. downgrade_total - total numbers of downgrade
7. error count - total number errors the user had 
8. hour - last login hour
9. day - last login date
10. month - last login date
11. year - last login year

## Implementation
PySpark and SparkML libraries to model, refine and evaluate the solution. 

### Data transformation, data splitting  

Data was splitted 20% for trainning and 80% for testing, 
The transformer VectorAssembler is used to combine a given list of columns into a single vector column so that decision tree can be used for modelling. 

StandardScaler is also used normalizing the single vector. 

### Model Training

RandomForestClassifier is used for modelling. Because the initial recall and F1 Score is high no other models used. 

The next step is using coss validation to find the ideal hyper-parameters for Random Fores Classifier.The ideal paramneters are MaxDepth 5 and numTrees = 20. 

### Refinement 

CrossValidator method used for refinement. The best solution in this model for RandomForestClassifier is impurity = gini, naxDepth =	8,	numTrees = 20 and with this parameter F1 Score is %95.1.

## File Description

Udacity_Sparkify .ipynb : Jupyter notebook 

# Conclusion
 Initial F1 Score and recall is %86.6. After refinement, the scores  Recall and F1 score improved to %%93.3 
 
 ## Future Improvements
 
- More features can be included like more user events such as Add Friend, Add a Playlist and location, status can also be included. 
- Different user agents can be analysed in its own data because they might have different user experience. 
- Artist and songs popularity can also be analysed. 
- Add a recommendation engine for users.
- Use larger data for better results
