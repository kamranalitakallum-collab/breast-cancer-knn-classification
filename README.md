# Breast Cancer Classification Using K-Nearest Neighbors (KNN)

## Project Overview

This project implements a machine learning classification system for breast cancer diagnosis using the **K-Nearest Neighbors (KNN)** algorithm.

The project uses the Breast Cancer Wisconsin (Diagnostic) dataset and follows a complete machine learning workflow including data preprocessing, exploratory data analysis, feature scaling, K-value comparison, 5-fold cross-validation, model evaluation, error analysis, and ROC-AUC analysis.

The final KNN model uses **K = 7** and achieves a test accuracy of **95.61%**.

> **Note:** This project is developed for machine learning practice and educational purposes. It is not intended for medical diagnosis or clinical decision-making.

---

## Objective

The main objectives of this project are to:

- Explore and understand the breast cancer dataset.
- Clean and preprocess the data.
- Separate features and target variables.
- Split the dataset into training and testing sets.
- Apply feature scaling for KNN.
- Compare different K values.
- Select the final K value using 5-fold cross-validation.
- Train the final KNN classification model.
- Evaluate model performance using multiple classification metrics.
- Analyze incorrect predictions.
- Evaluate the model using ROC-AUC.

---

## Dataset

The project uses the **KNN Algorithm Dataset** containing breast cancer diagnostic measurements.

### Dataset Summary

- Total observations: **569**
- Original columns: **33**
- Columns after removing the unnecessary column: **32**
- Modeling features: **30**
- Target variable: `diagnosis`
- Target classes:
  - `B` = Benign
  - `M` = Malignant

### Class Distribution

| Diagnosis | Count | Percentage |
|---|---:|---:|
| B (Benign) | 357 | 62.74% |
| M (Malignant) | 212 | 37.26% |

The dataset contains numerical measurements related to cell nuclei characteristics.

---

## Data Preprocessing

The following preprocessing steps were performed:

1. Loaded the dataset using Pandas.
2. Checked the dataset shape and data types.
3. Checked for missing values.
4. Removed the `Unnamed: 32` column because it contained missing values for all observations.
5. Checked for duplicate records.
6. Verified the uniqueness of the `id` column.
7. Removed `id` from the modeling features because it is an identifier rather than a predictive feature.
8. Separated the input features (`X`) and target variable (`y`).
9. Split the dataset into training and testing sets using an 80/20 split.
10. Used stratification to maintain the class distribution.
11. Applied `StandardScaler` before KNN modeling.

### Train/Test Split

- Training samples: **455**
- Testing samples: **114**
- Number of features: **30**

---

## Exploratory Data Analysis

Exploratory analysis was performed to understand the dataset and its structure.

The project includes:

- Dataset summary statistics
- Missing-value analysis
- Duplicate-value analysis
- Diagnosis class distribution
- Feature correlation analysis
- Correlation heatmap

The correlation analysis also showed strong relationships between several measurements such as radius, perimeter, and area features.

---

## Why Feature Scaling Was Used

KNN is a distance-based machine learning algorithm.

The dataset contains features with different numerical scales. Without scaling, features with larger numerical values could have a greater influence on distance calculations.

Therefore, `StandardScaler` was used to standardize the features before applying KNN.

The final model uses a Scikit-learn `Pipeline` so that scaling and KNN are handled together.

---

## Model Development

The machine learning algorithm used in this project is:

**K-Nearest Neighbors (KNN)**

Different values of K were evaluated to understand their effect on classification performance.

The tested K values were:

- K = 1
- K = 3
- K = 5
- K = 7
- K = 9

The final value of K was selected using **5-fold cross-validation on the training data**.

---

## 5-Fold Cross-Validation

To select the final K value in a more reliable way, 5-fold cross-validation was performed using a pipeline containing `StandardScaler` and `KNeighborsClassifier`.

| K | Mean CV Accuracy | Std CV Accuracy |
|---:|---:|---:|
| 1 | 94.73% | 1.46% |
| 3 | 96.70% | 2.09% |
| 5 | 96.26% | 2.26% |
| 7 | **96.92%** | 2.35% |
| 9 | 96.70% | 1.55% |

Based on the highest mean cross-validation accuracy in this evaluation, **K = 7** was selected for the final model.

---

## Final Model

The final machine learning model consists of:

- Feature scaling: `StandardScaler`
- Classification algorithm: `KNeighborsClassifier`
- Final K value: **7**
- Cross-validation: **5-Fold**
- Training samples: **455**
- Testing samples: **114**

The scaler and KNN classifier are combined into a single Scikit-learn pipeline.

---

## Model Performance

The final KNN model was evaluated on the unseen test dataset.

| Metric | Result |
|---|---:|
| Accuracy | **95.61%** |
| Precision (Malignant) | **97.44%** |
| Recall (Malignant) | **90.48%** |
| F1-Score (Malignant) | **93.83%** |
| ROC-AUC | **98.25%** |

The model correctly classified **109 out of 114** test samples, while **5 predictions were incorrect**.

---

## Confusion Matrix

The final confusion matrix was:

```text
[[71, 1],
 [ 4,38]]