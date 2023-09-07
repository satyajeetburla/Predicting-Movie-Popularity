# Predicting Movie Popularity (Based on Current Economic Condition)
The Custom Datasets for this project can be found at : https://drive.google.com/drive/folders/1C9GLIN1Ko-3EpNrTlxRltXr2M79hweCT?usp=sharing
﻿<a name="br1"></a> 

Predicting Movie

Popularity



<a name="br2"></a> 

Outline

**1. Introduction & Background**

**2. Data Cleaning**

**3. Exploratory Data Analysis**

**4. Model Overview**

**5. Model Results**

**6. Challenges Faced**

**7. Next Steps & Future Directions**



<a name="br3"></a> 

Introduction & Background

We were inspired by the well publicized theory that film is a reflection of society…..

“The idea that horror films reflect, or even caricature, society's collective anxieties is nothing new. ''Invasion of the Body

*Snatchers'' is frequently read as a critique of McCarthy-era pod people. Godzilla? A Japanese reaction to the*

devastation of the bomb. And the vampires haunting us of late? A coded response to the trauma of AIDS.”

— The New York Times, Oct. 2000

“Films reflect the tastes and values of the period in which they are made. We can trace the changing status of women,

*evolving ideas about masculinity, war, crime, journalism, the C.I.A. or anything else by Hollywood treatments over the*

decades. So when historians look back at this glut of superhero flicks, what will they say about us?”

— The New York Times, July 2018

This idea has been expressed for years in many ways, but we wanted to see if this theory would hold up to

analytical scrutiny, and if the theory was strong enough that a machine learning model could be created to

predict which type of movie would do best (top release) in certain economic climates



<a name="br4"></a> 

Introduction & Background

● To analytically study this idea, we first collated two different datasets:

○

Movie Dataset: Top and Bottom Box Office Movies in the U.S. from 1975-2022, their genre and

runtime from IMDB

○ Financial Dataset: Unemployment rate, S&P 500 return, GDP Movement (positive movement

representing improvement of consumer spending power, negative meaning the opposite) from

FRED

● Next we cleaned the data and joined the datasets

● We then ran exploratory data analysis to see if the concepts would hold up to high level examination

● Finally we built a few different models, trained them on a training dataset (~90% of the data), and

tested them on the test dataset (~10% of the data)

● The findings of our project could help the movie industry make better decisions on movie production

to achieve higher revenue and profit, even during recessions. It could also help movies engage

viewers by acting as a truer reflection of societal experiences



<a name="br5"></a> 

Data Cleaning

● The financial dataset was significantly easier to clean and collate. The data was all publically

available from FRED (Federal Reserve Economic Data) and was provided either quarterly or monthly

○ We needed the data weekly, so we duplicated the monthly / quarterly data within the dataframe

to ensure we had a row to represent the financials of each week

● The movie dataset was challenging to collate and clean for a few reasons:

○ The information provided on box office top films was full of blanks

○ The information provided about the best and worst box office movies were separate and held

different data points

○ We had to one-hot encode the movie genres so that they could be used as a feature in the ML

model

○ We had to align “box office weeks” with calendar weeks



<a name="br6"></a> 

Exploratory Data Analysis

●

●

First we wanted to understand the trend of

U.S. movie data over time

Looking at the charts on the right a few

key things stand out:

○

As GDP has grown in the U.S,

more money is spent on movies by

consumers

○

But as the number of movies

released annually increases, the

average earning per movie has

gone down

○

Together, these two trends indicate

that it is more important than ever

for movie producers to understand

what movies will resonate with the

public and be economic successes



<a name="br7"></a> 

Exploratory Data Analysis

**Total U.S. Gross Box Office Compared to Annual Unemployment**

**Rates**

●

Next we wanted to better understand if there was

an obvious connection between the total amount

of money spent at the box office and the state of

the economy (as measured by the unemployment

rate in the top chart or GDP Change in the

bottom chart)

○

Note the economic recessions over the

last twenty years are clearly evident via

both the Unemployment rate and GDP

change trends: the 2000-2001 dot.com

bubble burst, the 2008 financial crisis, and

the 2020 Covid Crisis

●

The charts on the left demonstrate there is no

obvious increase or decrease in total movie

attendance during periods of economic distress



<a name="br8"></a> 

Exploratory Data Analysis

**Economic Boom Years**

**Economic Bust Years**

●

Given the lack of correlation

between movie views in theaters

and the state of the economy, we

then wanted to dive into the genre

analysis - aka are certain genres

more popular in economic booms

or busts?

●

●

We first looked to explore this idea

visually by finding the percentage

of the year that a particular genre

was the most popular in economic

boom years (1999, 2007) and

economic bust years (2000, 2008)

As can be seen in the pie charts,

certain genres like ‘Comedy’ seem

to be slightly more popular in

recessions and certain genres like

‘Fantasy’ & ‘Thriller’ seem to be

more popular in strong economies



<a name="br9"></a> 

Exploratory Data Analysis



<a name="br10"></a> 

Final Model Dataset for Model 1: Movie Success

Our Final Dataset Used in the Machine Learning Model had ~5,780 Data points and the Following Columns…..

Example of One-Hot Encoded Genres (More in Real Dataset)



<a name="br11"></a> 

Model 1 Overview: Movie Success - Regression

●

●

We utilized a few different models to try and answer the question: Can you predict a movie’s success based on the following

features?

○

○

○

Economic conditions surrounding its release (unemployment rate, S&P 500 returns, GDP change)

Release during a holiday week (binary variable)

Movie Genre & Runtime & Releases

We first faced this as a regression problem and utilized the following models from the sklearn library with a 90:10

Training/Test split of the input data and a seed of 42 for reproducibility:

○

○

**Linear Regression**: supervised learning algorithm. Default hyperparameters

**Random Forest**: supervised learning algorithm that can be used for both classification and regression problems, that

combines multiple decision trees to make a prediction. Hyperparameters in our model include: n\_estimators=100, and

max\_depth = none

○

○

**XGBoost:** Boosting algorithm used for classification and regression problems. XGBoost works by building a series of

decision trees, where each subsequent tree tries to correct the mistakes of the previous tree. Hyperparameters in our

model include: n\_estimators=100, learning\_rate=0.1, max\_depth = 6

**Neural Network:** deep learning model that uses layers of interconnected nodes to extract features from the input

data and make predictions based on those features. Hyperparameters in our model included: layers = 2, size of

hidden layers = 512, 512, Max iteration = 5000, activation functions = ReLu

●

Given our limited dataset we expected that the neural network might be less accurate than the XGBoost and Random Forest

models because tree based algorithms generally perform better with smaller datasets



<a name="br12"></a> 

Model 1 Results: Prediction of Movie Success

**Linear Regression**

**Random Forest**

Training MSE of 0.113

Test MSE of 0.118

Training MSE of 0.011

Test MSE of 0.060

**XGBoost**

**Neural Network**

Training MSE of 0.058

Test MSE of 0.078

Training MSE of 0.64

Test MSE of 0.65

**The lower MSE figures for the Random Forest and XGBoost models indicate they are better at predicting a**

**movie’s success accurately given the features provided.**



<a name="br13"></a> 

Model 1 Results: Prediction of Movie Success

**Linear Regression**

**Random Forest**

The red line’s steep

upward slope

The red line’s steep

upward slope

indicates the model’s

predictions are

indicates the model’s

predictions are

underestimating the

actual values

underestimating the

actual values

Actual Values

Actual Values

**XGBoost**

**Neural Network**

The red line’s steep

upward slope

The red line’s steep

upward slope

indicates the model’s

predictions are

indicates the model’s

predictions are

underestimating the

actual values

underestimating the

actual values

Actual Values

Actual Values



<a name="br14"></a> 

Model 1: Movie Success - Binary Classification

●

We then thought about this as a binary classification problem and utilized the following models from the sklearn

library with a 90:10 Training/Test split of the input data and a seed of 42 for reproducibility:

○

○

**Logistic Regression**: supervised learning algorithm. Default hyperparameters included

**Random Forest**: supervised learning algorithm that can be used for both classification and regression

problems, that combines multiple decision trees to make a prediction. Hyperparameters in our model

include: n\_estimators=100, and max\_depth = none

○

○

**XGBoost:** Boosting algorithm used for classification and regression problems. XGBoost works by building a

series of decision trees, where each subsequent tree tries to correct the mistakes of the previous tree.

Hyperparameters in our model include: n\_estimators=100, learning\_rate=0.1

**Neural Network (SKLearn & Pytorch):** deep learning model that uses layers of interconnected nodes to extract

features from the input data and make predictions based on those features. Hyperparameters in our model included:

layers = 2, size of hidden layers = 512, 512, Max iteration = 5000, activation functions = ReLu, (pytorch learning\_rate

= 10^(-7))

●

Given our limited dataset we expected that the neural network might be less accurate than the XGBoost and

Random Forest models



<a name="br15"></a> 

Model 1 Results: Movie Success - Binary Classification

**Logistic Regression (Binary Classification)**

**Random Forest (Binary Classification)**

Training Accuracy of 0.814

Test Accuracy of 0.804

Training Accuracy of 0.991

Test Accuracy of 0.910

**XGBoost (Binary Classification)**

**Neural Network (Binary Classification SKLearn)**

Training Accuracy of 0.923

Test Accuracy of 0.879

Training Accuracy of 0.811

Test Accuracy of 0.810

**The higher accuracy figures for the Random Forest and XGBoost models indicate they are better at**

**predicting a movie’s success accurately given the features provided.**



<a name="br16"></a> 

Model 1 Results: Movie Success - Binary Classification

**Logistic Regression**

**Random Forest**

As can be seen in the

confusion matrix, the

model was relatively

accurate at predicting

whether a movie

As can be seen in the

confusion matrix, the

model was the most

accurate of the

models tested at

predicting whether a

movie would succeed

or fail

would succeed or fail

**XGBoost**

**Neural Network**

As can be seen in the

confusion matrix, the

model was more

accurate than the

logistic regression at

predicting whether a

movie would succeed

or fail

As can be seen in the

confusion matrix, the

model was the least

accurate of the

models tested at

predicting whether a

movie would succeed

or fail



<a name="br17"></a> 

Model 1 Results: Movie Success - Binary Classification

●

When looking at the most important features in the two most accurate models, XGBoost and Random Forest, we found

economic data was less important than other features

●

●

We tried to confirm this by removing the economic data from the model and retraining and testing

When we did this we found the models were similarly accurate, which hints the economic data is not that important for

predicting movie success according to our models

●

BUT since there does seem to be a correlation between economic climate and genre popularity, the economic data in this

model could be causing multicollinearity

**XGBoost**

**Random Forest**



<a name="br18"></a> 

Model 1 Conclusion: Movie Success

**In conclusion, given the relatively high accuracy rates for our Random Forest and XGBoost**

**models, we believe there is some validity to the theory that movie popularity can be predicted**

**based on runtime, genre, and maybe economic conditions.**



<a name="br19"></a> 

Final Model Dataset for Model 2

Our Final Dataset Used in the second Machine Learning Model had ~3,530 Data points and the Following Columns…..

Example of One-Hot Encoded Genres (More in Real Dataset)

These were movies

that performed best

each week in U.S.

Theaters

Special Day

represents a

holiday fell during

the week.

There were 38

genres that were

one-hot encoded in

our data set.

Certain movies

could be parts of

multiple genres.



<a name="br20"></a> 

Model 2 Overview: Prediction of Best Movie Genre

●

●

We utilized a few different models to determine how likely it was that a particular movie genre would be popular in a

given week based on the following features:

○

○

Economic climate (as determined by the unemployment rate, the S&P 500 return, and the GDP change)

Special Occasion (Was there a holiday that week)

We utilized the following models from the sklearn library with a 90:10 Training/Test split of the input data and a seed of 42

for reproducibility:

○

○

**Linear Regression**: supervised learning algorithm. Default hyperparameters included

**Random Forest**: supervised learning algorithm that can be used for both classification and regression problems,

that combines multiple decision trees to make a prediction. Hyperparameters in our model include:

n\_estimators=100, and max\_depth = none

○

○

**XGBoost:** Boosting algorithm used for classification and regression problems. XGBoost works by building a series

of decision trees, where each subsequent tree tries to correct the mistakes of the previous tree. Hyperparameters in

our model include: n\_estimators=100, learning\_rate=0.1

**Neural Network:** deep learning model that uses layers of interconnected nodes to extract features from the input

data and make predictions based on those features. Hyperparameters in our model included: layers = 2, size of

hidden layers = 512, 512, Max iteration = 5000, activation functions = ReLu

●

Given our limited dataset we expected that the neural network might be less accurate than the XGBoost and Random

Forest models



<a name="br21"></a> 

Model 2 Results: Genre Success

**Linear Regression**

**Random Forest**

Training MSE of 0.046

Test MSE of 0.046

Training MSE of 0.011

Test MSE of 0.033

**XGBoost**

**Neural Network**

Training MSE of 0.018

Test MSE of 0.034

Training MSE of 0.089

Test MSE of 0.092

**The lower MSE figures for the Random Forest and XGBoost models indicate they are better at predicting**

**which genres will be successful in a given week given the features provided.**



<a name="br22"></a> 

Model 2 Results: Genre Success

**Linear Regression**

**Random Forest**

The red line’s steep

upward slope

The red line’s steep

upward slope

indicates the model’s

predictions are

indicates the model’s

predictions are

underestimating the

actual values

underestimating the

actual values

Actual Values

Actual Values

**XGBoost**

**Neural Network**

The red line’s steep

upward slope

The red line’s steep

upward slope

indicates the model’s

predictions are

indicates the model’s

predictions are

underestimating the

actual values

underestimating the

actual values

Actual Values

Actual Values



<a name="br23"></a> 

Model 2 Conclusion: Genre Success

**In conclusion, given the relatively low mean-squared errors for our Random Forest and XGBoost**

**models, we believe there is some validity to the theory that certain genres are more popular than**

**others during times of economic booms or busts.**

**We believe that the Neural Network model did worse than the Random Forest and XGBoost models**

**due to lack of data. Neural Networks models traditionally need more data points, so this was not**

**incredibly surprising.**



<a name="br24"></a> 

Challenges Faced

●

Many of our challenges were related to data sourcing and cleaning. The movie datasets were missing information, had incorrect information,

and were inconsistent in the information they reported

○

Example: There were different words for same genre and the genre information had different syntax (‘Comedy/Romance’ vs ‘Comedy,

Romance’)

■

Additionally, we couldn’t use tactics like imputation when genres were missing, this required pulling in additional datasets or

updating lines manually

○

Example: Because “box office weeks” are different than calendar weeks, we had to update the number of releases per calendar week

using imputation (had to choose the closest neighbor, couldn’t do mean because the number of releases exponentially increased over

time)

■

■

The difference between week timing also caused headaches around joins

Additionally, the dates in the original movie dataset required significant string analysis to be converted into datetime format

○

○

Example: Genres were too broadly categorized (Comedy, Drama, Sci-fi, Action, Adventure, Family, Romance —- what is this movie

ACTUALLY about?)

We had more data about successful movies than unsuccessful movies

●

We also struggled to properly train our machine learning algorithms

○

○

Each ML model needed hyperparameter tuning (other than regression) to find the perfect number of layers, or batch size, etc.

We ideally would have larger data sets for a Neural Network model



<a name="br25"></a> 

Next Steps & Future Directions

See if the model could be

used on global movie /

financial data. Would the

same trends hold?

Use more granular box

office financial data and

see if we could predict the

amount of money a movie

could earn

Gather more movie data

to see if we could improve

our ML model accuracy

See if a ML model could

See if the model could

similarly predict TV genre

popularity, which would

solidify the underlying

connection between genre

and economic climate

improve its prediction of

movie popularity based on

more / other features (like

number of award-winning

cast members)



<a name="br26"></a> 

T he End
