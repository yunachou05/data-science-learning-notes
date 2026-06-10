# data-science-learning-notes

Capstone_SpaceX Falcon 9 First Stage Landing Prediction 

## Introduction

According to the historical recode of SpaceX Falcon 9 Landing plan, we can design and validate models to predict Falcon 9 landing probability through collected data and methodology.

First of all, I collected data to identified variables and selected necessary attributes for modeling preparation using Python libraries.

 - Using correlation method to validate the numerical variables.
 - Plotting their relationship through scatter and checking whether they are linear or non-linear
 - Check the relationship between pay load mass (kg) and Launch sites
 - Compared three variables (Success rate, Flight Number, and Pay Load Mass) with orbit types
 - Plotting the yearly trend of the launch success

Secondly, I sued Folium to identify the launch site locations in the map with markers to show the success indicators.

Finally, I built four machine learning models to validate the best hyperplane in model prediction through accuracy scores and confusion matrix. There are the machine learning models I chose to validate: 

- Logistic Regression
- SVM
- Decision Tree
- KNN
  
## Features

- Data Wrangling
- SQL
- EDA processes
- Data Visualization
- Dashboard
- Machine Learning models with validations:
  1. Best score
  2. Best parameters
  3. Accuracy score
  4. Precision
  5. Recall
  6. F-1 score 
## Requirements

### Python Libraries

The following Python libraries were used throughout this project:

#### Data Processing and Analysis
- pandas
- numpy
- datetime
- re
- unicodedata
- csv
- sqlite3

#### Web Scraping and Data Collection
- requests
- BeautifulSoup (`bs4`)

#### System Utilities
- sys
- prettytable

#### Data Visualization
- seaborn
- matplotlib.pyplot
- folium
  - `MarkerCluster`
  - `MousePosition`
  - `DivIcon`

#### Dashboard Development
- dash
- `html`
- `dcc`
- `Input`
- `Output`
- plotly.express

#### Machine Learning
- sklearn.preprocessing
  - `StandardScaler`
- sklearn.model_selection
  - `train_test_split`
  - `GridSearchCV`
- sklearn.linear_model
  - `LogisticRegression`
- sklearn.svm
  - `SVC`
- sklearn.tree
  - `DecisionTreeClassifier`
- sklearn.neighbors
  - `KNeighborsClassifier`

---

### Installation

Install the required packages using:

```bash
pip install pandas numpy requests beautifulsoup4 prettytable seaborn matplotlib folium dash plotly scikit-learn
```

---
 
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

## Project Report
[view project report](https://github.com/yunachou05/data-science-learning-notes/blob/main/Capstone_SpaceX%20Falcon%209%20First%20Stage%20Landing%20Prediction_v.3%20.pdf)
 
 
## Acknowledgement

This project was completed as part of the IBM Data Science Professional Certificate on Coursera.

All analysis, code implementation, visualizations, interpretations, and project decisions in this repository were completed by the author.

During the development process, ChatGPT was used as a learning and productivity assistant to support debugging, code review, concept clarification, and documentation improvement. All generated suggestions were reviewed, validated, and adapted by the author before implementation.

The project reflects the author's understanding, analysis, and final conclusions.
