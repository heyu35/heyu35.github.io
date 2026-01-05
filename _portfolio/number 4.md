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

核心实现
======
以下是核心代码的实现：
#数据处理部分
def data_preprocessing(data):
    # 处理缺失值
    data = data.dropna()
    # 提取特征
    features = data[['feature1', 'feature2']]
    labels = data['label']
    return features, labels
#模型定义部分
from sklearn.linear_model import LogisticRegression
model = LogisticRegression()
#模型训练部分
features, labels = data_preprocessing(data)
model.fit(features, labels)

分析结果
======
#### 关键变量分布特征
![关键变量分布直方图](/images/portfolio/data-analysis-visualization/Key_Variables_Distribution_01.png)
通过该直方图，我们可以直观地看到关键变量的分布情况，有助于把握数据的集中趋势和离散程度。

#### 基于结局不同变量的特征比较
![基于结局不同变量的箱线图](/images/portfolio/data-analysis-visualization/Boxplot_Variables_Distribution_01.png)
此箱线图展示了基于不同结局的变量特征差异，为进一步分析和决策提供了依据。

#### 模型评估 - 混淆矩阵
![混淆矩阵](/images/portfolio/data-analysis-visualization/CM_01.png)
混淆矩阵提示，模型对于 AKI 的发病预测准确性较高，说明模型在这方面有较好的表现。

#### 模型评估 - ROC 曲线
![ROC 曲线](/images/portfolio/data-analysis-visualization/ROC_01.png)
AUC = 0.781，这表明模型对于 CKD 患者中 AKI 发病具有较好的预测效能。
