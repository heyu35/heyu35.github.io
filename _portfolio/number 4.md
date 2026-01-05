---
title: "综合数据分析与可视化项目"
collection: portfolio
type: "Data Analysis"
permalink: /portfolio/
date: 2026-01-05
tags:
  - 数据分析
  - 数据可视化
  - 模型评估
  - 直方图
  - 箱线图
  - 混淆矩阵
  - ROC 曲线
tech_stack:
  - name: Python
  - name: Matplotlib
  - name: Seaborn
---

综合运用数据分析和可视化手段，完成关键变量分布探索、变量特征比较以及模型评估工作

项目背景
======
在数据分析过程中，我们不仅需要对数据的关键变量分布进行探索，还需要比较基于不同结局的变量特征，同时对建立的模型进行评估。本项目通过数据可视化的方式，使用直方图、箱线图、混淆矩阵和 ROC 曲线等工具，完成了上述工作，为数据分析和决策提供了直观的依据。


分析结果
======
#### 关键变量分布特征
![1.关键变量分布直方图](/images/portfolio/data-analysis-visualization/Key_Variables_Distribution_01.png)
通过该直方图，我们可以直观地看到关键变量的分布情况，有助于把握数据的集中趋势和离散程度。

#### 基于结局不同变量的特征比较
![2.基于结局不同变量的箱线图](/images/portfolio/data-analysis-visualization/Boxplot_Variables_Distribution_01.png)
此箱线图展示了基于不同结局的变量特征差异，为进一步分析和决策提供了依据。

#### 模型评估 - 混淆矩阵
![3.混淆矩阵](/images/portfolio/data-analysis-visualization/CM_01.png)
混淆矩阵提示，模型对于 AKI 的发病预测准确性较高，说明模型在这方面有较好的表现。

#### 模型评估 - ROC 曲线
![4.ROC 曲线](/images/portfolio/data-analysis-visualization/ROC_01.png)
AUC = 0.781，这表明模型对于 CKD 患者中 AKI 发病具有较好的预测效能。

核心实现
======
以下是核心代码的实现：
```python
#数据处理部分
# 处理缺失值
data = data.dropna()
 # 提取特征并进行基线资料的比较
columns = ['age', 'sex', 'Ethnicity', 'region', "TDI","Employment","education_level","Final_Healthy_diet_score","Smoking","alcohol_intake",
           "BMI","tv","sleep_duration","grip_strength","MVPA_self","urea","urate", "LDL_C","SBP","DBP","creatinine","hba1c"]
categorical = ['sex', 'Ethnicity', 'region', "Employment","education_level","Smoking","alcohol_intake"]
groupby = "Incidental.AKI.HDC.ICD10"
table = TableOne(data,columns=columns,categorical=categorical,groupby=groupby,pval=True)
#特征分析直方图以及箱线图绘制
for idx, var in enumerate(vars_to_plot):
    sns.histplot(x=var,data=data,alpha=0.7,kde=True,color=plt.cm.Set2(idx/len(vars_to_plot)),edgecolor='black'linewidth=0.5,ax=axs_flat[idx])
for idx, var in enumerate(vars_to_plot):
    sns.boxplot(data=data,x=group_var,y=var,ax=axs_flat[idx],palette='Set2',linewidth=1,fliersize=2)
#模型构建
from sklearn.linear_model import LogisticRegression
model = LogisticRegression()
#模型评估 混淆矩阵
def confusion_matrix_plot(y_true, y_pred_prob, threshold=0.52, title='Confusion Matrix (Scaled Model)'):
    y_pred = (y_pred_prob > threshold).astype(int)
    cm = confusion_matrix(y_true, y_pred)
    fig, ax = plt.subplots(figsize=(6, 5))
    sns.heatmap(cm,annot=True,fmt='d',cmap='Blues',ax=ax,xticklabels=['Non-AKI(0)', 'AKI(1)'],yticklabels=['Non-AKI(0)', 'AKI(1)'])
#ROC曲线
def plot_roc_curve(y_true, y_pred_prob, title='ROC Curve (Kidney Disease Prediction - Scaled Model)'):
    fpr, tpr, thresholds = roc_curve(y_true, y_pred_prob)
    auc_score = roc_auc_score(y_true, y_pred_prob)
    youden_index = tpr - fpr)
#SHAP可解释性分析
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
