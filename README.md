# Used Car Price Regression using multiple variable regression

## 1. Project Overview

This project focuses on analyzing a used-car dataset and developing a multiple
linear regression model to predict vehicle prices based on vehicle
characteristics and history.

The project emphasizes the complete machine learning workflow, including:

- data understanding
- data quality assessment
- preprocessing
- exploratory data analysis
- feature preparation
- multiple linear regression
- model evaluation
- regression diagnostics
- interpretation of results

## Problem Statement

Used-car prices depend on multiple vehicle characteristics such as mileage,
engine specifications, vehicle age, ownership history, and other attributes.

The objective of this project is to investigate the relationship between these
characteristics and used-car prices and develop a multiple linear regression
model capable of predicting vehicle price.

## Objective

The primary objective is to:

1. Understand the structure and quality of the used-car dataset.
2. Identify and address data-quality issues.
3. Prepare appropriate numerical and categorical variables for regression.
4. Investigate relationships between vehicle characteristics and price.
5. Develop a multiple linear regression model.
6. Evaluate model performance.
7. Diagnose the assumptions and limitations of the regression model.
8. Document the complete analytical workflow.

## Dataset

The dataset contains information on used cars in the Seattle area and includes
vehicle characteristics, mileage, engine specifications, ownership information,
vehicle history, and price.

According to the dataset description, there are 24 explanatory variables that
can be used to predict the final price of used cars.

The data was collected from AutoTrader and Carfax.


## Key Initial Findings

- The dataset contains 52 observations and 27 columns.
- `price` was identified as the target Variable.
- `brand`, `model`, `wheel_drive`, and `engine_type` were identified as categorical predictors.
- `num_seat`, `doors`, and `type` were found to be constant across all observations.
- `condition` contains 98.08% missing values and is unsuitable for reliable imputation.
- `speed_levels` contains one missing observation (1.92%) and will be retained for further preprocessing.
- `id` was identified as an identifier rather than a predictive feature.
- `link` was identified as metadata and was also used to investigate duplicate listings.
- Two observations were found to represent the same vehicle and will require duplicate handling.


