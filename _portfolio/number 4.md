---
title: "Data Analysis and Visualization"
collection: portfolio
type: "Data Analysis"
permalink: /portfolio/
date: 2026-01-05
tags:
  - Data Analysis
  - Data Visualization
  - Model Evaluation
  - Histogram
  - Box Plot
  - Confusion Matrix
  - ROC Curve
tech_stack:
  - name: Python
  - name: Matplotlib
  - name: Seaborn
---

By comprehensively applying data analysis and visualization methods, we completed the exploration of key variable distributions, comparison of variable characteristics, and model evaluation.

Project Background
======
In the process of data analysis, we not only need to explore the distribution of key variables in the data, but also compare the variable characteristics based on different outcomes, and evaluate the established models simultaneously. This project completed the above work through data visualization methods using tools such as histograms, box plots, confusion matrices, and ROC curves, providing an intuitive basis for data analysis and decision-making.


Analysis Results
======
#### Key Variable Distribution Characteristics
![1.Key Variable Distribution Characteristics](/images/portfolio/data-analysis-visualization/Key_Variables_Distribution_01.png)
Through this histogram, we can intuitively observe the distribution of key variables, which helps to grasp the central tendency and dispersion of the data.

#### Comparison of Variable Characteristics Based on Different Outcomes
![2.Comparison of Variable Characteristics Based on Different Outcomes](/images/portfolio/data-analysis-visualization/Boxplot_Variables_Distribution_01.png)
This box plot shows the differences in variable characteristics based on different outcomes, providing a basis for further analysis and decision-making.

#### Model Evaluation - Confusion Matrix
![3.Confusion Matrix](/images/portfolio/data-analysis-visualization/CM_01.png)
The confusion matrix indicates that the model has high accuracy in predicting the incidence of AKI, demonstrating good performance in this aspect.

#### Model Evaluation - ROC Curve
![4.ROC Curve](/images/portfolio/data-analysis-visualization/ROC_01.png)
The AUC (Area Under the Curve) is 0.781, which indicates that the model has good predictive efficacy for the incidence of AKI in patients with CKD.

Core Implementation
======
The following is the implementation of the core code:
```
# Data Processing Section
# Handle missing values
data = data.dropna()
# Extract features and conduct comparison of baseline data
columns = ['age', 'sex', 'Ethnicity', 'region', "TDI","Employment","education_level","Final_Healthy_diet_score","Smoking","alcohol_intake",
           "BMI","tv","sleep_duration","grip_strength","MVPA_self","urea","urate", "LDL_C","SBP","DBP","creatinine","hba1c"]
categorical = ['sex', 'Ethnicity', 'region', "Employment","education_level","Smoking","alcohol_intake"]
groupby = "Incidental.AKI.HDC.ICD10"
table = TableOne(data,columns=columns,categorical=categorical,groupby=groupby,pval=True)
# Draw histograms and box plots for feature analysis
for idx, var in enumerate(vars_to_plot):
    sns.histplot(x=var,data=data,alpha=0.7,kde=True,color=plt.cm.Set2(idx/len(vars_to_plot)),edgecolor='black',linewidth=0.5,ax=axs_flat[idx])
for idx, var in enumerate(vars_to_plot):
    sns.boxplot(data=data,x=group_var,y=var,ax=axs_flat[idx],palette='Set2',linewidth=1,fliersize=2)
# Model Construction
from sklearn.linear_model import LogisticRegression
model = LogisticRegression()
# Model Evaluation - Confusion Matrix
def confusion_matrix_plot(y_true, y_pred_prob, threshold=0.52, title='Confusion Matrix (Scaled Model)'):
    y_pred = (y_pred_prob > threshold).astype(int)
    cm = confusion_matrix(y_true, y_pred)
    fig, ax = plt.subplots(figsize=(6, 5))
    sns.heatmap(cm,annot=True,fmt='d',cmap='Blues',ax=ax,xticklabels=['Non-AKI(0)', 'AKI(1)'],yticklabels=['Non-AKI(0)', 'AKI(1)'])
# ROC Curve
def plot_roc_curve(y_true, y_pred_prob, title='ROC Curve (Kidney Disease Prediction - Scaled Model)'):
    fpr, tpr, thresholds = roc_curve(y_true, y_pred_prob)
    auc_score = roc_auc_score(y_true, y_pred_prob)
    youden_index = tpr - fpr)
# SHAP Interpretability Analysis
scaler = pipeline.named_steps['scaler']
lr_model = pipeline.named_steps['lr']
explainer = shap.Explainer(lr_model, X_train)
shap_values = explainer(X_train)
shap.summary_plot(shap_values, X_train)
#KMeans Clustering -Elbow Method
for i in range(1, max_clusters + 1):
    kmeans = KMeans(
        n_clusters=i, 
        init='k-means++', 
        random_state=42,
        n_init=10)
    kmeans.fit(data_clustering_scaled)
    wcss.append(kmeans.inertia_)
    print(f"Number of clusters={i}, WCSS={kmeans.inertia_:.2f}")
```
