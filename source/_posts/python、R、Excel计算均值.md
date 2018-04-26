---
title: python、R、Excel计算均值
date: 2018-03-29 14:11:42
tags: 数据分析 Python R Excel
categories: 商务与经济统计
---

平均数
### python

```python
# 平均数
def avg(lst):
    if len(lst)<1:
        return None
    else:
        return float(sum(lst))/len(lst)
```

### R
```R
height <- c(6.00, 5.92, 5.58, 5.92)
mean(height)
```

### Excel

打开一个excel，在此，计算学生的平均成绩。
![](/images/data_analysis/1.jpg)

点击想要出结果的一格，点击上方的fx，选择AVERAGE函数。
![](/images/data_analysis/2.jpg)

点击确定，选择计算的范围。
![](/images/data_analysis/3.jpg)

最终得出结果。  
![](/images/data_analysis/4.jpg)
