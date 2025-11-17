# Machine Learning models for predicting enthalpy of vaporization from molecular descriptors
This repository contains the code and documentation for the CHE657 course project focused on predicting the Enthalpy of Vaporization ($\Delta H_{vap}$) for Volatile Organic Compounds (VOCs) from their molecular structure using various Machine Learning (ML) regression techniques.

## Project Objective
The primary goal was to develop and evaluate ML models that can accurately and rapidly predict the enthalpy of vaporization using only a molecule's structure1.Traditional experimental measurement of Delta H_{vap} is accurate but is often slow and resource-intensive. This project sought to establish a fast, reliable, and data-driven computational method for estimating this key thermodynamic property.

## Installation

To run this project locally, you need Python 3 and the following libraries. It is highly recommended to use a virtual environment.

### Required Packages (via pip)

```bash
# Core data science, preprocessing, and model selection
pip install pandas numpy matplotlib seaborn scikit-learn

# Cheminformatics toolkit for descriptor generation
# Note: RDKit is used to generate 217 molecular descriptors. 
# RDKit installation can be complex and may be better handled via conda (conda install -c conda-forge rdkit)
pip install rdkit-pypi

# Machine Learning Models
# Includes Linear Models, SVR, Random Forest, and advanced Gradient Boosting frameworks
pip install xgboost lightgbm catboost
```
## Methodology Summary

### 1. Dataset and Feature Engineering

* **Dataset:** The project used a dataset of **Volatile Organic Compounds (VOCs)** with known Delta H_{vap} values.
* **Molecular Structure Representation:** The compounds were represented using **SMILES** (Simplified Molecular-Input Line-Entry System) strings.
* **Feature Generation Toolkit:** The **RDKit cheminformatics library** was used to convert the molecular SMILES strings into numerical features.
* **Features Generated:** Generated **217 molecular descriptors** (e.g., molecular weight, topological, and electronic properties).
* **Data Dimensions:** The final modeling dataset contained **2,410 compounds** with 217 features.

### 2. Data Preprocessing and Feature Selection

* **Target Transformation:** The raw Delta H_{vap} distribution was **heavily right-skewed** (skewness ~ 1.8). A **logarithmic transformation** (dvap\_log) was applied, which significantly reduced the skewness (~ 0.4871$), and the log-transformed values were used for modeling.
* **Feature Selection (PCA):** **Principal Component Analysis (PCA)** was performed to analyze the contribution of each original feature to the overall variance. The top 20 most **informative original features** were identified based on their loadings and explained variance to reduce redundancy and multicollinearity.

### 3. Models Evaluated

A wide range of regression models were benchmarked:

| Model Category | Models Tested |
| :--- | :--- |
| **Baseline & Linear** | Linear Regression, Ridge, Lasso, ElasticNet |
| **Traditional ML** | Support Vector Regression (SVR), Random Forest |
| **Advanced Ensemble (Boosting)** | Standard Gradient Boosting, XGBoost, LightGBM, CatBoost |
***

## Key Findings and Results

### Top Model Performance (Log Delta H_vap Target)

| Model | Test $R^2$ | Test RMSE | Test MAE |
| :--- | :--- | :--- | :--- |
| **CatBoost** | **0.9707** | **4.773** | **2.657** |
| LightGBM | 0.9696 | 4.866 | 2.829 |
| XGBoost | 0.9629 | 5.372 | 3.075 |
| Gradient Boosting | 0.9609 | 5.520 | 3.650 |

### Primary Conclusion

* **Ensemble-based methods consistently outperformed simpler linear models**.
* The **CatBoost Regressor** achieved the highest predictive accuracy with a test $R^2$ of **0.97** , indicating its strength in capturing the complex, non-linear relationships in molecular descriptor data.
* Simpler models (Linear Regression, SVR) were found insufficient for this complex task.
***

## Project Group

This project was completed by Group 3 for the CHE657 Course Project: Machine Learning in Chemical Engineering.

| Name | Roll number |
| :--- | :--- |
| Ayush Omer | 230264 |
| Harshvardhan Gaur | 230467 |
| Khushi Jain | 230560 |
| Om Jee Singh | 230718 |
| Prince Yadav | 230792 |

**Mentor:** Prof. Salman Khan 
***

## Future Work

Potential future work includes:

* Expanding the dataset.
* Applying advanced feature selection techniques.
* Exploring deep learning approaches such as **Graph Neural Networks (GNNs)** for direct molecular graph learning.
