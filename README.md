# Used Car Price Prediction using Multiple Linear Regression

## Overview

This repository contains a focused regression analysis for predicting used-car prices using vehicle characteristics.

The primary objective was to understand how selected vehicle attributes relate to price and evaluate whether a Multiple Linear Regression model can provide useful price predictions.

The analysis focuses on:
- Data cleaning and preprocessing
- Exploratory analysis
- Feature selection
- Multicollinearity analysis using VIF
- Multiple Linear Regression
- Model evaluation
- Residual analysis
- Comparison of two regression models

---

## Dataset

The dataset contains information about used vehicles, including:

- Brand
- Model
- Year
- Mileage
- Engine specifications
- Fuel economy
- Ownership information
- Vehicle dimensions
- Service records
- Price

The dataset used for modelling contained 52 observations initially.

After handling the missing value required for modelling, 51 observations were used in the final model comparison.

---

## Project Workflow

```text
Raw Dataset
     ↓
Data Cleaning & Validation
     ↓
Exploratory Data Analysis
     ↓
Feature Selection
     ↓
Multicollinearity Analysis (VIF)
     ↓
Multiple Linear Regression
     ↓
Model Evaluation
     ↓
Residual Analysis
     ↓
Model Comparison
     ↓
Final Findings & Limitations

```

##Data Preprocessing

The dataset was inspected for:

Missing values
Duplicate records
Invalid values
Outliers
Data types
Categorical variables
Numerical relationships

Detailed preprocessing decisions are documented in:

docs/data_quality_report.md

##Feature Selection

Correlation analysis was initially used to identify numerical variables associated with price.

The reduced numerical feature set used for the baseline regression model was:

Year
Miles
Horsepower
Engine capacity
Number of owners
Wheel drive
Speed levels
Service records

Multicollinearity was then assessed using Variance Inflation Factor (VIF).

The final reduced model showed low VIF values for the selected predictors, indicating that severe multicollinearity was not present.

##Models
###Model 1 — Reduced Numerical Model

The baseline model used the selected numerical predictors.

###Model 2 — Numerical + Vehicle Identity

The second model added:

Brand
Model

These categorical variables were one-hot encoded before regression.

The purpose was to determine whether vehicle identity provides additional predictive information beyond the numerical characteristics.

##Results
Metric	Model 1	Model 2
Training MAE	1,938.21	894.59
Testing MAE	2,307.70	1,339.78
Training R²	0.5580	0.8778
Testing R²	-0.3996	0.0051
Testing RMSE	2,910.19	1,712.27

Model 2 substantially reduced prediction error compared with the baseline model.

However, the very large difference between training and testing R² indicates that the richer model does not generalize well to unseen observations.

##Key Findings
Vehicle year had a moderate positive relationship with price.
Mileage had a moderate negative relationship with price.
Horsepower showed a positive relationship with price.
Number of owners showed a negative relationship with price.
Adding brand and model substantially improved MAE and RMSE.
The addition of categorical vehicle identity also increased the training R² substantially.
The very low testing R² of Model 2 indicates limited predictive generalization.
The small dataset size is an important limitation of the analysis.


##Model Limitations

The results should be interpreted cautiously because the dataset is very small.

Only 51 observations were available for the final modelling comparison, while the model containing brand and model generated a relatively large number of encoded predictors.

This creates a high risk of overfitting and makes the evaluation sensitive to the particular train-test split.

Therefore, the model should be viewed primarily as an analytical exercise rather than a production-ready car price prediction system.

##Conclusion

The analysis demonstrates that vehicle identity, particularly brand and model, contains useful information for explaining used-car prices.

Adding these variables reduced the testing MAE from approximately 2,308 to 1,340 and testing RMSE from approximately 2,910 to 1,712.

However, the testing R² remained close to zero, indicating that the model had limited ability to explain price variation in unseen observations.

The primary conclusion is therefore that while additional vehicle-specific information improves the fitted model, the small dataset limits reliable generalization.
