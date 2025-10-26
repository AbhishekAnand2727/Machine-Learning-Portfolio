# Breast Cancer Classification Model Performance

This file summarizes the performance of various classification models trained to predict whether a breast cancer tumor is benign (Class 2) or malignant (Class 4), based on the Wisconsin Breast Cancer (Original) dataset.

The performance metrics below are likely averaged results from K-Fold Cross-Validation, showing the mean accuracy and its standard deviation across the folds.

## Performance Metrics

| Model                     | Average Accuracy (%) | Standard Deviation (%) | Notes                      |
| :------------------------ | :------------------- | :--------------------- | :------------------------- |
| Random Forest (n=30)      | 97.00%               | 2.60%                  | Best performing model      |
| Logistic Regression       | 96.60%               | 2.58%                  | Tied for second best       |
| K-Nearest Neighbors (KNN) | 96.60%               | 3.33%                  | Tied for second best       |
| Kernel SVM                | 96.07%               | 3.37%                  | Slightly lower accuracy    |
| SVM (Linear)              | 96.06%               | 2.37%                  | Similar to Kernel SVM      |
| Naive Bayes               | 95.80%               | 3.68%                  |                            |
| Decision Tree             | 93.50%               | 3.60%                  | Lowest accuracy            |

## Conclusion

Based on the average cross-validation accuracy:

* The Random Forest model (with n_estimators=30) achieved the highest average accuracy at 97.00%, with relatively low variability (2.60% std dev).
* Logistic Regression and KNN performed almost identically well, both achieving 96.60% accuracy, though KNN showed slightly higher variability.
* SVM (both linear and kernel versions) and Naive Bayes also performed strongly, with accuracies around 96%.
* A single Decision Tree had the lowest accuracy (93.50%), which is expected as ensemble methods like Random Forest typically outperform individual trees.

Overall, several models demonstrate high predictive accuracy on this dataset, with Random Forest showing a slight edge. These results indicate that machine learning models, particularly Random Forest, Logistic Regression, and KNN, can effectively predict whether a tumor is benign or malignant based on the provided cell nuclei features with high accuracy (over 96%).