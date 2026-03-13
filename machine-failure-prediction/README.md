# Machine Failure Prediction

This project builds a machine learning model to predict machine failure using industrial sensor data.

The goal is to identify patterns in machine operating conditions that indicate potential failure, enabling predictive maintenance and reducing downtime.

---

# Dataset

AI4I 2020 Predictive Maintenance Dataset [Dataset]. (2020). UCI Machine Learning Repository. https://doi.org/10.24432/C5HS5C.

The dataset contains sensor measurements from industrial machines.

Main variables include:

- Air temperature [K]
- Process temperature [K]
- Rotational speed [rpm]
- Torque [Nm]
- Tool wear [min]
- Machine type (H, L, M)

Target variable:

Machine failure  
0 = No failure  
1 = Failure

---

# Exploratory Data Analysis

Before building machine learning models, we explore the dataset to understand variable distributions and relationships.

---

## Machine Failure Distribution

![Machine Failure Distribution](images/machine_failure_distribution.png)

Most observations correspond to normal machine operation, with relatively few failure cases.

---

## Air Temperature Distribution

![Air Temperature Distribution](images/air_temperature_distribution.png)

Air temperature values are concentrated between approximately **297K and 303K**, indicating stable environmental conditions.

---

## Process Temperature Distribution

![Process Temperature Distribution](images/process_temperature_distribution.png)

Process temperature closely follows air temperature but tends to be slightly higher.

---

## Feature Correlation Matrix

![Correlation Matrix](images/correlation_matrix.png)

Key observations:

- Air temperature and process temperature are strongly correlated
- Tool wear and torque may contribute to failure risk
- No severe multicollinearity issues detected

---

# Feature Engineering

The categorical variable **Type** was converted into dummy variables:
Type → Type_H, Type_L, Type_M

This allows machine learning models to process machine type information.

Final model features include:

- Air temperature
- Process temperature
- Rotational speed
- Torque
- Tool wear
- Machine type indicators

---

# Model

A **Random Forest Classifier** was used for failure prediction.

Reasons for choosing Random Forest:

- Handles nonlinear relationships well
- Robust for tabular industrial data
- Requires minimal preprocessing
- Provides feature importance interpretation

---

# Model Evaluation

5-fold cross validation results:
Cross Validation Scores
[0.98, 0.9756, 0.98, 0.9781, 0.9781]

Mean CV Score
0.978

The model achieves approximately **97.8% accuracy**.

### ROC Curve

The ROC curve evaluates the classification performance of the Random Forest model across different decision thresholds.

![ROC Curve](images/roc_curve.png)

The ROC curve illustrates the trade-off between the true positive rate and false positive rate across different thresholds. 

The Random Forest model achieves an AUC score of **0.968**, indicating excellent discrimination between normal machine operation and failure conditions. This suggests that the model is highly effective at identifying failure patterns based on sensor measurements.

---

# Feature Importance

![Feature Importance](images/feature_importance.png)

The most influential features for predicting machine failure are:

1. Rotational speed
2. Torque
3. Tool wear

These variables provide the strongest signal for detecting abnormal machine behavior.

---

# Error Analysis

The model misclassified **42 samples out of 2000 test observations**.

Misclassified cases typically occur when sensor values lie near the boundary between normal operation and failure conditions.

This overlap is common in predictive maintenance problems where degradation occurs gradually.

---

# Tools

Python  
Pandas  
NumPy  
Scikit-learn  
Matplotlib  
Seaborn  
Jupyter Notebook

---

## Project Structure

```
machine-failure-prediction/
│
├── images/
│   ├── air_temperature_distribution.png
│   ├── process_temperature_distribution.png
│   ├── machine_failure_distribution.png
│   ├── correlation_matrix.png
│   └── feature_importance.png
│
├── machine_failure_prediction.ipynb
└── README.md
```


---

# Author

Lewei Gao  
Statistics Student – McMaster University
