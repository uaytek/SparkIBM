# Udacity DSND Capstone Data Analysis with Spark

## Installation
This project uses the following software and python libraries
- Pyspark-2.4.1
- Python 3.6
- NumPy
- Pandas

## File Description

Udacity_Sparkify .ipynb : Jupyter notebook 

## Project Overview
The goal of this project is to analyse users interaction data and predict which group of users are expected to churn - either downgrading from premium to free or cancel thier subscriptions.

Sparkify data consists of users interaction with music stream data. There are two user service levels, paid and free. Users can also upgrade and downgrade their service. Also, events such as playing a song, like or dislike a song, are all recorded. 

There is also an optional cloud deployment either on  Amazon Aws or IBM Watson in the project. Both cloud deployment was tried and IBM Watson was comparable easy for deployment. It does not require any default module installation like pandas, plotly, or no session termination in any code line. 

## Problem Statement
The first task to predict the churned group from data is data exploration to define the churn and to idenntify related features. Especially page data that gives info about the users visit has relevant information about the churn. 

Identifying category columns also helped for defining some features. Main focus definning features is the users main events in the system. So some questions should be answered like how many songs and in which hour they are listening in a day, how they interact with other users or pages, do they have any error in the system.

## Metric
The problem is to identify users who are about to churn, so we should prevent false negative results and focus on recall (true-positive). 

F1 score is also included as a metric, because precision can also be considered after identifying possible churn users. 

## Data Exploration
There are four categories; gender, level, auth and method used in data. gender and level added to feature list. Because auth and method gives info about the technical system, they were not included in feature list. 

The pages that visited by users gives many information of user events and definning features like thumpup - thumbdown, how much time spending on listening music. 

- About
- Add Friend
- Add to Playlist
- Cancel
- Cancellation Conf...
- Downgrade
- Error
- Help
- Home
- Login
- Logout
- NextSong
- Register
- Roll Advert
- Save Settings
- Settings
- Submit Downgrade
- Submit Registration
- Submit Upgrade
- Thumbs Down
- Thumbs Up 
- Upgrade

### Define Churn 
Cancellation Confirmation events defined the churn. This event can be define in page data. 1 as churned and 0 stayed users.

### Feature Engineering

After data exploration, the features selected for the model listed below. 

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
PySpark and SparkML libraries are used for  modelling, refinning and evaluating the solution. 

### Data transformation, data splitting  

Data was splitted 20% for trainning and 80% for testing, 
The transformer VectorAssembler is used for combining a given list of features into a single vector column so that decision tree can be used for modelling. 

StandardScaler is also used for normalizing this single vector. 

### Model Training

RandomForestClassifier, Naive Bayes and Logistic Regression are used for modelling.The initial recall and F1 Score is the highest on Random Forest. 

The next step is using coss validation to find the ideal hyper-parameters for Random Fores Classifier.The ideal paramneters are MaxDepth 5 and numTrees = 20. 

### Refinement 

CrossValidator method used for refinement. The best solution in this model for RandomForestClassifier is impurity = gini, naxDepth =	8,	numTrees = 20 and with this parameter F1 Score is %95.1.

## Result
Sparkify data has variance of user expereince like song play, thumbs-up, thumbs-down, error. Random Forest did a better job by splitting nodes in each tree considering a limited number of the features.

Navie Bayes produces better in categorial variables, whereas there are more numerical features in Sparkify data. That might be the reason that Navie Bayes has lower results than Random Forrest.

Logistic regression might be expected a better model because of a binary outcome churn and not churn, the data better modelled with both classification and regression on a Random Forest model

it is time to continue with the refined model on a larger dataset. This will raise the robustness of the model and improve customer management.

## Conclusion
 
Although Sparkify project implementation initially started on Amazon Aws,  there was a session termination on StandartScalar code execution. The same code works properly on IBM Watson and Udacity workspace. Some modules like pandas, plotly are also needed to install on Amazon Aws before starting the project. Whereas on IBM Watson, after adding an initial code lines for dataset connection, no nwed any module installation and all code executed without session termination.  

Sparkify data features are mostly system created like page info, time, user level, error; thus, not much effort needed to re-formatting its data or dealing with null values in feature. So, this project also shows that how application's logging processes should be taken into consideration to support machine learning algorithms during its development. 
 
 ### Future Improvements
 
- More features can be included like more user events such as Add Friend, Add a Playlist and location, status can also be included. 
- Different user agents can be analysed in its own data because they might have different user experience. 
- Artist and songs popularity can also be analysed. 
- Add a recommendation engine for users.
- Use larger data for better results
