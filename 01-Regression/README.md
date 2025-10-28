# Boston House Prices- Predicting Median House Value of Owners

## 1. Project Goal

The primary objective is to build and evaluate several regression models that can accurately predict the MEDV (Median value of owner-occupied homes) based on the 13 input features.

---

## 2. Attribute Information

### Input Features
1)  CRIM: per capita crime rate by town
2)  ZN: proportion of residential land zoned for lots over 25,000 sq.ft.
3)  INDUS: proportion of non-retail business acres per town
4)  CHAS: Charles River dummy variable (1 if tract bounds river; 0 otherwise)
5)  NOX: nitric oxides concentration (parts per 10 million) [parts/10M]
6)  RM: average number of rooms per dwelling
7)  AGE: proportion of owner-occupied units built prior to 1940
8)  DIS: weighted distances to five Boston employment centres
9.  RAD: index of accessibility to radial highways
10) TAX: full-value property-tax rate per $10,000 [$/10k]
11) PTRATIO: pupil-teacher ratio by town
12) B: The result of the equation B=1000(Bk - 0.63)^2 where Bk is the proportion of blacks by town
13) LSTAT: % lower status of the population

### Output Variable
1)  MEDV: Median value of owner-occupied homes in $100000

---

## 3. Techniques: Regression Models Used

Five different regression algorithms were applied to model the data:

* Multiple Linear Regression
* Polynomial Regression
* Support Vector Regression (SVR)
* Decision Tree Regression
* Random Forest Regression

---

## 4. How to Run
## Dependencies: Ensure you have Python installed, along with the following libraries:

pandas
numpy
scikit-learn
seaborn
matplotlib (You can install these using pip: pip install pandas numpy scikit-learn matplotlib)

Execution: Open the file in Jupyter Notebook/Lab and run the cells in order.