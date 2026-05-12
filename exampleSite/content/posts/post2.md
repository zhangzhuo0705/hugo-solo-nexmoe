---
title: "Python数据分析入门指南"
date: 2024-05-10
cover: "/images/post2.jpg"
categories: ["技术文章"]
tags: ["Python", "数据分析"]
views: 189
---

从零开始学习Python数据分析，涵盖pandas、numpy、matplotlib等核心库的使用。

## pandas基础

pandas是Python数据分析的核心库，提供了DataFrame和Series两种数据结构。

```python
import pandas as pd

df = pd.read_csv('data.csv')
print(df.head())
```

## numpy数组操作

numpy提供了高效的数组操作功能。

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5])
print(arr.mean())
```