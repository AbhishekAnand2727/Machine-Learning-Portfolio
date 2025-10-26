# Breast Cancer Wisconsin (Original) - Classification Project

## 1. Goal
The objective of this project is to classify breast cancer tumors as either **benign** (non-cancerous) or **malignant** (cancerous) based on digitized image features of cell nuclei. Various classification models (e.g., Logistic Regression, SVM, KNN, Random Forest) are applied and evaluated.

---

## 2. Dataset Information

* **Source:** Dr. William H. Wolberg, University of Wisconsin Hospitals, Madison.
* **Number of Instances:** 699 (as of July 15, 1992)
* **Number of Attributes:** 9 features + 1 ID + 1 Class attribute

---

## 3. Attribute Information

The dataset contains the following attributes:

| #  | Attribute                      | Domain | Description                                      |
| :- | :----------------------------- | :----- | :----------------------------------------------- |
| 1  | Sample code number             | ID     | Unique identifier for each sample                |
| 2  | Clump Thickness                | 1 - 10 | Assessment of cell grouping                      |
| 3  | Uniformity of Cell Size        | 1 - 10 | Assessment of cell size consistency              |
| 4  | Uniformity of Cell Shape       | 1 - 10 | Assessment of cell shape consistency             |
| 5  | Marginal Adhesion              | 1 - 10 | How much cells stick together                    |
| 6  | Single Epithelial Cell Size    | 1 - 10 | Size of epithelial cells                         |
| 7  | Bare Nuclei                    | 1 - 10 | Nuclei not surrounded by cytoplasm               |
| 8  | Bland Chromatin                | 1 - 10 | Assessment of chromatin texture                  |
| 9  | Normal Nucleoli                | 1 - 10 | Assessment of nucleoli size/shape                |
| 10 | Mitoses                        | 1 - 10 | Rate of cell division                            |
| 11 | **Class** | 2 or 4 | **Target Variable:** 2 = Benign, 4 = Malignant |

---

## 4. Data Preprocessing Notes

* **Missing Values:** There are **16 instances** with a single missing attribute value, denoted by **"?"**. These need to be handled (e.g., through imputation or removal) before training the models. The missing values are primarily in the 'Bare Nuclei' column.
* **ID Column:** The 'Sample code number' is an identifier and should likely be dropped before training.
* **Class Encoding:** The target variable 'Class' uses values 2 and 4. These might be re-encoded to 0 and 1 for easier use with some algorithms.

---

## 5. Class Distribution

* **Benign (Class 2):** 458 samples (65.5%)
* **Malignant (Class 4):** 241 samples (34.5%)

## How to Run
## Dependencies: Ensure you have Python installed, along with the following libraries:

pandas
numpy
scikit-learn
seaborn
matplotlib (You can install these using pip: pip install pandas numpy scikit-learn matplotlib)
Execution: Open the file in Jupyter Notebook/Lab and run the cells in order.