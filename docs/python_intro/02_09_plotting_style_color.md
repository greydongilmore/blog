---
title: Plots Style and Color
linktitle: Plots Style and Color
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ml_intro:
    parent: 02. Plotting
    weight: 9

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 9
---

We've shown a few times how to control figure aesthetics in seaborn, but let's now go over it formally:


```python
import seaborn as sns
import matplotlib.pyplot as plt
%matplotlib inline
tips = sns.load_dataset('tips')
```

## Styles

You can set particular styles:


```python
sns.countplot(x='sex',data=tips)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f1d2f3651d0>




![png](../img/02/08_plotting_style_color_3_1.png)



```python
sns.set_style('white')
sns.countplot(x='sex',data=tips)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f1d2f2bf3c8>




![png](../img/02/08_plotting_style_color_4_1.png)



```python
sns.set_style('ticks')
sns.countplot(x='sex',data=tips,palette='deep')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f1d2f279ef0>




![png](../img/02/08_plotting_style_color_5_1.png)


## Spine Removal


```python
sns.countplot(x='sex',data=tips)
sns.despine()
```


![png](../img/02/08_plotting_style_color_7_0.png)



```python
sns.countplot(x='sex',data=tips)
sns.despine(left=True)
```


![png](../img/02/08_plotting_style_color_8_0.png)


## Size and Aspect

You can use matplotlib's **plt.figure(figsize=(width,height) ** to change the size of most seaborn plots.

You can control the size and aspect ratio of most seaborn grid plots by passing in parameters: size, and aspect. For example:


```python
# Non Grid Plot
plt.figure(figsize=(12,3))
sns.countplot(x='sex',data=tips)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f1d2f4d8b38>




![png](../img/02/08_plotting_style_color_11_1.png)



```python
# Grid Type Plot
sns.lmplot(x='total_bill',y='tip',height=2,aspect=4,data=tips)
```

    /home/ggilmore/.local/lib/python3.6/site-packages/seaborn/axisgrid.py:375: UserWarning: Tight layout not applied. The bottom and top margins cannot be made large enough to accommodate all axes decorations. 
      fig.tight_layout()
    /home/ggilmore/.local/lib/python3.6/site-packages/seaborn/axisgrid.py:848: UserWarning: Tight layout not applied. The bottom and top margins cannot be made large enough to accommodate all axes decorations. 
      self.fig.tight_layout()





    <seaborn.axisgrid.FacetGrid at 0x7f1d2f1e7860>




![png](../img/02/08_plotting_style_color_12_2.png)


## Scale and Context

The set_context() allows you to override default parameters:


```python
sns.set_context('poster',font_scale=4)
sns.countplot(x='sex',data=tips,palette='coolwarm')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f1d2f1e7b70>




![png](../img/02/08_plotting_style_color_14_1.png)


Check out the documentation page for more info on these topics:
https://stanford.edu/~mwaskom/software/seaborn/tutorial/aesthetics.html
