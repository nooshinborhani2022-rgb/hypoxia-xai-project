# Hypoxia Prediction Using Explainable Machine Learning  
This repository contains the full machine learning pipeline and explainability analysis for predicting fetal hypoxia / IUGR using non-invasive prenatal Doppler indices and maternal demographic features.

The project includes:
- A complete ML workflow implemented in Python  
- Model evaluation (Logistic Regression, Random Forest, XGBoost, MLP)  
- Explainability using logistic regression coefficients + SHAP  
- Comparison with classical clinical Doppler rules  
- A research report explaining all methods and results  

---

## Project Overview  
Fetal hypoxia and intrauterine growth restriction (IUGR) are clinically high-risk conditions. Doppler ultrasound indices such as:

- **PI_UA** – Umbilical Artery Pulsatility Index  
- **PI_MCA** – Middle Cerebral Artery Pulsatility Index  
- **CPR (PI_MCA / PI_UA)** – Cerebroplacental Ratio  

are commonly used for screening.  
However, threshold-based rules may miss complex multivariate patterns.

This project builds a transparent and explainable ML model to support clinical decision-making.

---

## Dataset (Not Included in This Repository)
 
The dataset contains sensitive medical data and is not uploaded to this repository.

Dataset characteristics:
- 400 pregnancies (200 Normal, 200 IUGR)
- Gestational age  
- Maternal age  
- Doppler indices (PI_UA, PI_MCA, PI_MCA/PI_UA)

To run the notebook, place the dataset in the project folder with the filename:

```
Overall_dataset_noninvasive.xlsx
```

The code automatically loads this file.

---

## Methods  

### Data Loading & Cleaning
- Reading the Excel dataset  
- Normalization of Doppler indices  
- Label encoding (Normal / IUGR)  
- Exploratory statistics  

### Feature Engineering  
In the initial phase of the project, we performed feature engineering and explored the creation of several Doppler-derived indices and nonlinear interaction terms, including:

- **PI_Diff = PI_MCA − PI_UA**  
- **PI_Product = PI_MCA × PI_UA**  
- **GA_MCA_Interaction = Gestational Age × PI_MCA**  
- **UA_Adjusted = PI_UA / Gestational Age**

While these engineered features captured meaningful nonlinear physiological relationships, the dataset contained only 400 samples. Expanding the feature space significantly increased the risk of overfitting—particularly for high-capacity models such as XGBoost and the MLP.

For this reason, and to preserve generalizability, **the final predictive models were trained only on the five most clinically meaningful and non-invasive variables**:

- **Gestational Age**  
- **Maternal Age**  
- **PI_MCA**  
- **PI_UA**  
- **PI_MCA / PI_UA**

This approach ensured that the final models captured the essential Doppler-based pathophysiological patterns of fetal hypoxia **without introducing unnecessary noise or sparsity**.

---

### Model Training
Models used:
- Logistic Regression  
- Random Forest  
- XGBoost  
- MLP Neural Network  

Evaluation metrics:
- Accuracy  
- Precision 
- Sensitivity  
- Specificity  
- ROC-AUC  

---

### Explainability
- Logistic regression coefficients → Odds ratios  
- SHAP values for global + local interpretability  

---

## How to Run  

This project is designed to run easily on **Google Colab** without local setup.

1. Open Google Colab  
2. Upload:
   - `Hypoxi_Final.ipynb`  
   - `Overall_dataset_noninvasive.xlsx` (private dataset)  
3. Run the notebook cells from top to bottom  
4. All evaluations, plots, and SHAP explanations will be generated automatically  

---

## Full Report  
See the full research explanation in:

```
Hypoxi_Paper_Report.pdf
```

---

## About  
This project was developed as part of applied research in Explainable AI for healthcare, focusing on transparent ML pipelines and interpretable decision support tools.
