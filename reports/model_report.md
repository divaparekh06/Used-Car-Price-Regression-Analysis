## 1. Objective

The objective was to investigate whether vehicle characteristics can be used to estimate used-car prices using Multiple Linear Regression.

The analysis was intentionally kept focused on a single regression technique rather than comparing multiple machine learning algorithms.

---

## 2. Baseline Model

The first model used the following predictors:

- year
- miles
- horsepower
- engine_capacity_litre
- num_owners
- wheel_drive
- speed_levels
- service_records

The model was trained using an 80/20 train-test split with `random_state=42`.

### Baseline Results

- Training MAE: 1938.21
- Testing MAE: 2307.70
- Training R²: 0.5580
- Testing R²: -0.3996
- Testing RMSE: 2910.19

The negative testing R² indicates that the baseline model performed worse than a simple baseline that predicts the mean target value on the test set.

---

## 3. Residual Analysis

Residuals were calculated as:

Residual = Actual Price - Predicted Price

For the baseline model:

- Mean residual: 942.24
- Minimum residual: -3571.72
- Maximum residual: 7127.22
- Positive residuals: 8
- Negative residuals: 3

The residual distribution was not perfectly centered around zero, and the relatively large residual range indicated substantial prediction errors for some observations.

---

## 4. Model 2 — Adding Brand and Model

To investigate whether vehicle identity provides additional predictive information, `brand` and `model` were added to the selected numerical predictors.

Categorical variables were converted into numerical dummy variables using one-hot encoding.

One observation with a missing `speed_levels` value was excluded for this comparison, resulting in 51 observations.

### Model 2 Results

- Training MAE: 894.59
- Testing MAE: 1339.78
- Training R²: 0.8778
- Testing R²: 0.0051
- Testing RMSE: 1712.27

---

## 5. Model Comparison

| Metric | Baseline | Brand + Model |
|---|---:|---:|
| Training MAE | 1938.21 | 894.59 |
| Testing MAE | 2307.70 | 1339.78 |
| Training R² | 0.5580 | 0.8778 |
| Testing R² | -0.3996 | 0.0051 |
| Testing RMSE | 2910.19 | 1712.27 |

The second model produced substantially lower test-set MAE and RMSE.

Testing MAE decreased by approximately 42%, while testing RMSE decreased by approximately 41%.

---

## 6. Overfitting Assessment

Although Model 2 achieved a training R² of 0.8778, its testing R² was only 0.0051.

This large gap indicates that the model fits the training observations substantially better than the unseen observations.

The likely contributing factors include:

- Very small dataset size
- High number of categorical dummy variables relative to observations
- Vehicle-specific characteristics
- Sensitivity to the train-test split

Therefore, the second model demonstrates improved fitted performance but poor generalization.

---

## 7. Final Interpretation

Adding brand and model improved the model's prediction error considerably.

However, the low testing R² means that the model should not be considered a reliable production prediction system.

The results are more useful for demonstrating the regression workflow and understanding the influence of vehicle characteristics than for deploying an accurate pricing model.

---

## 8. Limitations

- Small dataset
- Limited number of observations
- Single train-test split
- High dimensionality after categorical encoding
- Limited ability to generalize
- No external validation dataset

---

## 9. Final Conclusion

The analysis shows that brand and model contain meaningful information for used-car pricing.

However, the improvement in training performance was much larger than the improvement in testing performance.

Therefore, the main analytical conclusion is:

> Vehicle-specific categorical information improves the fitted regression model and reduces prediction error, but the available dataset is too small to support strong generalization.
