# CICIoT2023 Cybersecurity Intrusion Detection Capstone

**Master of Science in Applied Data Science — Final Project**  
**Authors:** Graham Ward, Anahit Shekikyan, Gerard Corrales Fernandez  

## Overview
This repository documents an end-to-end machine learning workflow for detecting malicious network traffic in the CIC-IoT2023 dataset. The project includes data preparation, exploratory analysis, model training across multiple algorithm families, and interpretability work using SHAP. All generated tables, metrics, and figures are stored alongside the notebooks to ensure full reproducibility.

## Repository Structure

CYBERSECURITY_CAPSTONE/
│
├── Code_Library/
│   ├── Data_Preparation.ipynb
│   │     Cleans CIC-IoT2023 flow data, standardizes column types, removes duplicates,
│   │     and derives both multi-class (Attack_Family) and binary (Binary_Label) targets.
│   │
│   ├── Data_Exploration.ipynb
│   │     Explores distributions, sparsity, skewness, zero inflation, multicollinearity,
│   │     and overall feature redundancy to guide model development.
│   │
│   ├── Modeling.ipynb
│   │     Trains and evaluates a suite of machine learning models including:
│   │     LightGBM, Random Forest, CatBoost, AdaBoost, XGBoost,
│   │     Logistic Regression, and Linear SVM.
│   │     Uses a balanced training set while leaving validation and test sets imbalanced
│   │     to reflect natural real-world attack distributions.
│   │
│   └── Feature_Importance.ipynb
│         Fits the best-performing LightGBM configuration and computes SHAP-based
│         global feature importances for interpretability.
│
├── Tables/
│   ├── EDA/
│   │     Contains summary statistics, missing-value audits, correlation matrices,
│   │     redundancy cluster outputs, and other exploratory tables.
│   │
│   └── Model_Results/
│         Classification reports, ROC-AUC summaries, confusion matrices,
│         aggregated evaluation metrics, and tuned model performance summaries.
│
├── Images/
│   ├── EDA/
│   │     Visual distributions, sparsity plots, correlation heatmaps,
│   │     and dataset structural diagrams.
│   │
│   ├── Model_Results/
│   │     ROC curves, confusion matrices, SHAP plots, and feature analysis figures.
│   │
│   ├── cic-topology-chart-2023.jpg
│   ├── cic-topology-diagram3-2023.jpg
│   └── inline-network-topology.jpg
│         Network topology visualizations used for contextualizing IoT attack flows.
│
├── requirements.txt
│     Python dependency list for environment setup.
│
└── README.md
      Project documentation file.

---


## Getting Started
1. Create a Python 3.10+ environment and install dependencies:
       pip install -r requirements.txt

2. Download the CIC-IoT2023 dataset from the official source and place raw files in your preferred directory.  
   (The dataset is not distributed with this repository.)

3. Launch Jupyter Lab or your preferred notebook environment and open the notebooks under Code_Library/.

## Workflow Summary

### Data Preparation
The Data_Preparation.ipynb notebook loads the raw CIC-IoT2023 flow exports, removes rows with missing label information, standardizes column types, resolves duplicates, and creates two supervised learning targets:
- Attack_Family (multi-class)
- Binary_Label (benign vs. malicious)

The cleaned dataset is saved in Parquet format for efficient downstream use.

### Exploratory Data Analysis
Data_Exploration.ipynb assesses:
- Dataset dimensions and missingness
- Numeric feature distributions
- Sparsity, skewness, and zero inflation
- Correlation structure and redundancy among predictors

These insights guide feature selection and inform model choice.

### Modeling
Modeling.ipynb balances the training dataset to mitigate class imbalance while keeping validation and test sets imbalanced to reflect real-world operational conditions. The notebook evaluates a diverse set of algorithms:
- LightGBM
- Random Forest
- CatBoost
- AdaBoost
- XGBoost
- Logistic Regression
- Linear SVM

Models are compared using accuracy, weighted F1, ROC-AUC, confusion matrices, and other diagnostic metrics.

### Interpretability
Feature_Importance.ipynb refits the best-performing LightGBM model and uses SHAP to quantify feature importance. Outputs include global feature rankings and SHAP distribution plots for the most influential predictors.

## Key Results
The final tuned model results are summarized in:
    Tables/Model_Results/Final_Model_Test_Results_Summary.csv

Highlights:
- LightGBM achieved an accuracy of 0.78 and a weighted F1 score of 0.80.
- Other ensemble models performed within a narrow range of LightGBM.
- Linear models (SVM, Logistic Regression) underperformed compared to nonlinear tree-based methods, reflecting the complexity of network-flow data.

## Reproducing the Analysis
1. Run Data_Preparation.ipynb to generate cleaned datasets.  
2. Run Data_Exploration.ipynb to reproduce EDA outputs.  
3. Execute Modeling.ipynb to train and evaluate models, generating all output tables and figures.  
4. Run Feature_Importance.ipynb to compute SHAP-based interpretability results.

## Project Status
The repository contains the full reproducible pipeline used for the analysis. Users may extend the notebooks, integrate new datasets, update dependencies, or adapt the workflow for production settings.
