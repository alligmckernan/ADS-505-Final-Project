# ADS-505 Final Project — Miscarriage Risk Prediction

**Team Members:**  
Gagandeep Singh, Allison McKernan, and Celina Velazquez  
**Date:** October 2025  

---

## 📊 Project Overview
This project develops a machine learning model to predict miscarriage risk using IoT and mobile-health features such as biometrics, activity levels, and lifestyle indicators. The dataset, *Miscarriage_Prediction_dataset_New_HA.csv*, contains one million records and sixteen attributes.  

The objective is to create an interpretable model capable of providing early warnings to support clinical decision-making and improve maternal health outcomes.

---

## 🧩 Problem Statement
Pregnancy outcomes are influenced by a complex combination of physical, behavioral, and environmental factors. Detecting early signs of miscarriage risk could enable preventative interventions and monitoring. Using wearable and mobile health data, our task is to **classify pregnancies as “Miscarriage” or “No Miscarriage.”**

---

## 🧠 Methodology

### 1. Data Preparation
- Dataset size: **1,000,000 rows × 16 columns**  
- Features include *Age*, *BMI*, *bpm*, *stress*, *bp*, *Activity*, *Driving*, *Alcohol Consumption*, etc.  
- Target variable: **Miscarriage/No Miscarriage (binary)**  
- No missing values were found.  
- `BMI` was converted from text to numeric.  

### 2. Exploratory Data Analysis
- Strongest correlation with miscarriage outcome: **Age (r = 0.247)**  
- Weak correlations among most other predictors (|r| < 0.01).  
- Mann–Whitney U tests confirmed that **Age**, **Driving**, and **BMI** differed significantly between groups (p < 0.05).  
- Heatmaps, histograms, and boxplots were used to visualize these relationships.

### 3. Preprocessing
- Data split: **80% training / 20% testing (stratified)**  
- Pipeline included:
  - Median imputation for numeric features  
  - Standard scaling  
  - One-hot encoding for categorical variables (none in this dataset)

### 4. Model Training and Evaluation
Three classification models were trained and evaluated:

| Model | ROC-AUC | Accuracy | Key Notes |
|--------|----------|-----------|------------|
| **Random Forest** | **0.9255** | **0.8086** | Best model, balanced precision/recall |
| Logistic Regression | 0.6432 | 0.6050 | Linear baseline |
| K-Nearest Neighbors (k=9) | 0.6920 | 0.6444 | Moderate performance |

### 5. Feature Importance
Random Forest revealed that **Age**, **BMI**, and **Driving behavior** were the most important predictors of miscarriage risk. Feature importance visualization is provided in the notebook.

### 6. Calibration and Validation
- ROC, Precision–Recall, and Calibration curves were plotted for all models.  
- Random Forest showed strong discrimination and reasonable calibration, while Logistic Regression was underfitted.

---

## 🧾 Results Summary
- **Final Selected Model:** Random Forest Classifier  
- **ROC-AUC:** 0.9255  
- **Accuracy:** 0.8086  
- **Recall (positive class):** 0.8770  
- **Precision (positive class):** 0.7712  

The Random Forest model captures nonlinear feature interactions effectively and provides interpretable risk insights for clinical applications.

---

## 💬 Discussion
The Random Forest model demonstrates high predictive performance, indicating that IoT-derived behavioral and physiological metrics can meaningfully contribute to miscarriage risk assessment. However, model validation and data verification are necessary before clinical use. Feature semantics—particularly for *Alcohol Consumption* and *bpm*—should be reviewed for proper scaling and units.  

Future work should include:
- Cross-validation and hyperparameter tuning  
- Model calibration (Platt scaling or isotonic regression)  
- SHAP-based explainability  
- External validation with independent datasets  
- Deployment considerations for healthcare data privacy compliance (e.g., HIPAA)

---

## ⚙️ How to Reproduce
1. Clone the repository:  
   ```bash
   git clone https://github.com/alligmckernan/ADS-505-Final-Project.git
   cd ADS-505-Final-Project
