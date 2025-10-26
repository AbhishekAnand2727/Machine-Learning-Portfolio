# Regression Model Performance on Boston Housing Dataset

This file summarizes the performance of various regression models trained to predict the Median House Value (MEDV). Scores are based on a standard train-test split (e.g., 80/20) after feature scaling.

## Performance Metrics

| Model                       | R2 Score (Train) | R2 Score (Test) | MSE (Test) | Notes                                      |
| :-------------------------- | :--------------- | :-------------- | :---------- | :----------------------------------------- |
| Multiple Linear Regression  | ~0.73\*          | 0.71            | 24.7        | Baseline linear model                      |
| Polynomial Regression       | 0.93             | 0.91            | 8.6         | Degree 2 (Good fit, low overfitting)       |
| Decision Tree Regression    | ---              | 0.81            | 16.4        | Performance depends heavily on `max_depth` |
| Support Vector Regression   | ---              | 0.76            | 29.6        | Default parameters? Tuning might improve.  |
| Random Forest (Tuned)       | 0.98             | 0.91            | 8.53        | Best parameters via GridSearchCV           |


## Conclusion

Based on the test set performance (R2 Score and RMSE):

* **Polynomial Regression** and the **Tuned Random Forest** achieved the highest R2 scores (0.91) on the test data, indicating they captured the underlying patterns well.
* The **Polynomial Regression** model showed the least overfitting (smallest gap between train and test R2 scores).
* The **Tuned Random Forest**, while showing slight overfitting (0.98 train vs 0.91 test), also achieved a strong test R2 and a low RMSE (2.93).
* Multiple Linear Regression provided a decent baseline, while the default SVR performed less effectively on this dataset.

Depending on the priority (highest test accuracy vs. lowest overfitting), either the **Polynomial Regression** or the **Tuned Random Forest** could be considered the best model among those tested. **Polynomial Regression** is the best fitted model compared to **Tuned Random Forest** due to overfittting on the latter