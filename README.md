# data-science-learning-notes

Capstone_SpaceX Falcon 9 First Stage Landing Prediction 

## Introduction

According to the historical recode of SpaceX Falcon 9 Landing plan, we can design and validate models to predict Falcon 9 landing probability through collected data and methodology.

First of all, I collected data to identified variables and selected necessary attributes for modeling preparation using Python libraries.

Ø   Using correlation method to validate the numerical variables.
Ø   Plotting their relationship through scatter and checking whether they are linear or non-linear
Ø   Check the relationship between pay load mass (kg) and Launch sites
Ø   Compared three variables (Success rate, Flight Number, and Pay Load Mass) with orbit types
Ø   Plotting the yearly trend of the launch success

Secondly, I sued Folium to identify the launch site locations in the map with markers to show the success indicators.

Finally, I built four machine learning models to validate the best hyperplane in model prediction through accuracy scores and confusion matrix. There are the machine learning models I chose to validate: 

- Logistic Regression
- SVM
- Decision Tree
- KNN
  
## Features

·      Data Wrangling
·      SQL
·      EDA processes
·      Data Visualization
·      Dashboard
·      Machine Learning models with validations:
-       Best score
-       Best parameters
-       Accuracy score
-       Precision
-       Recall
-       F-1 score 
## Requirements

     The libraries I used in Python:
·      pandas
·      numpy
·      requests
·      datetime
·      sys
·      BeautifulSoup
·      unicodedata
·      re
·      csv,sqlite3
·      prettytable
·      seaborn
·      matplotlib.pyplot
·      folium
·      from folium.plugins import MarkerCluster
·      from folium.plugins import MousePosition
·      from folium.features import DivIcon
·      dash
·      from dash import html, dcc
·      from dash.dependencies import Input, Output
·      plotly.express
·      from sklearn import preprocessing
·      from sklearn.preprocessing import StandardScaler
·      from sklearn.model_selection import train_test_split
·      from sklearn.linear_model import LogisticRegression
·      from sklearn.svm import SVC
·      from sklearn.tree import DecisionTreeClassifier
·      from sklearn.neighbors import KNeighborsClassifier
·      from sklearn.model_selection import GridSearchCV
 
## Usage
 
python train.py
 
#### Description: 

This is the assignment for self-learning in IBM Data Science Professional Certification through IBM Skills NetWork Lab to help me understand how to use data methodology with Python to clean and prepare data. Then, I can use the cleaned data to build a prediction model through machine learning methods. The class chose four machine learning models which were logistic regression, SVM, decision tree, and KNN with confusion matrix and the accuracy scores. 
 
## Methodology 

1. Data Collection
2. Data Cleaning
3. Feature Engineering
4.  Model Training
5. Hyperparameter Tuning 6. Evaluation

## Results

Decision Tree achieved the highest accuracy score of 0.875 on the test dataset.
 
 
## Acknowledgement
 
This project was completed as part of the IBM Data Science Professional Certificate on Coursera.
 
The project includes original work by the author, including data collection, data preparation, exploratory data analysis, visualization, machine learning model development, evaluation, and interpretation of results.
 
During the development process, ChatGPT was used as a learning and productivity assistant to support debugging, code review, concept clarification, and documentation improvement. All generated suggestions were reviewed, validated, and adapted by the author before implementation.
 
The project reflects the author's understanding, analysis, and final conclusions.
