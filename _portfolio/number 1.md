---
title: "探索数据分析可视化：直方图"
collection: portfolio
type: "Data Analysis"
permalink: /portfolio/data-analysis-visualization
date: 2024-11-12
excerpt: "关键变量的分布特征<br/><img src='/images/portfolio/data-analysis-visualization/Key_Variables_Distribution_01.png'>"
header:
  teaser: /images/portfolio/data-analysis-visualization/teaser.png
tags:
  - 数据分析
  - 数据可视化
  - 直方图
tech_stack:
  - name: Python
---

### 项目背景 (Background)
在数据分析里，掌握关键变量的分布特征十分关键。直方图作为常用的可视化工具，能直观展示数据分布，助力我们快速把握数据的集中趋势、离散程度等特征。

### 核心实现 (Implementation)
#### 绘制关键变量直方图
此代码用于绘制多个关键变量的直方图，以展示其分布情况。
```python
for idx, var in enumerate(vars_to_plot):
    # 绘制单个变量的直方图，添加核密度估计曲线
    sns.histplot(x=var, data=data, alpha=0.7, kde=True, color=plt.cm.Set2(idx/len(vars_to_plot)), edgecolor='black',  linewidth=0.5, ax=axs_flat[idx])
