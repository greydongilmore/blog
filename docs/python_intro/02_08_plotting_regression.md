---
title: Regression Plots
linktitle: Regression Plots
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ml_intro:
    parent: 02. Plotting
    weight: 8

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 8
---

Seaborn has many built-in capabilities for regression plots, however we won't really discuss regression until the machine learning section of the course, so we will only cover the **lmplot()** function for now.

**lmplot** allows you to display linear models, but it also conveniently allows you to split up those plots based off of features, as well as coloring the hue based off of features.

Let's explore how this works:


```python
import seaborn as sns
%matplotlib inline
```


```python
tips = sns.load_dataset('tips')
```


```python
tips.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>total_bill</th>
      <th>tip</th>
      <th>sex</th>
      <th>smoker</th>
      <th>day</th>
      <th>time</th>
      <th>size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>16.99</td>
      <td>1.01</td>
      <td>Female</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10.34</td>
      <td>1.66</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>21.01</td>
      <td>3.50</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>23.68</td>
      <td>3.31</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>24.59</td>
      <td>3.61</td>
      <td>Female</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>



## lmplot()


```python
sns.lmplot(x='total_bill',y='tip',data=tips)
```




    <seaborn.axisgrid.FacetGrid at 0x7f62f3a8d588>




![png](../img/02/07_plotting_regression_5_1.png)



```python
sns.lmplot(x='total_bill',y='tip',data=tips,hue='sex')
```




    <seaborn.axisgrid.FacetGrid at 0x7f62f19f72b0>




![png](../img/02/07_plotting_regression_6_1.png)



```python
sns.lmplot(x='total_bill',y='tip',data=tips,hue='sex',palette='coolwarm')
```




    <seaborn.axisgrid.FacetGrid at 0x7f62f12adf60>




![png](../img/02/07_plotting_regression_7_1.png)


### Working with Markers

lmplot kwargs get passed through to **regplot** which is a more general form of lmplot(). regplot has a scatter_kws parameter that gets passed to plt.scatter. So you want to set the s parameter in that dictionary, which corresponds (a bit confusingly) to the squared markersize. In other words you end up passing a dictionary with the base matplotlib arguments, in this case, s for size of a scatter plot. In general, you probably won't remember this off the top of your head, but instead reference the documentation.


```python
# http://matplotlib.org/api/markers_api.html
sns.lmplot(x='total_bill',y='tip',data=tips,hue='sex',palette='coolwarm',
           markers=['o','v'],scatter_kws={'s':100})
```




    <seaborn.axisgrid.FacetGrid at 0x7f62f1230128>




![png](../img/02/07_plotting_regression_9_1.png)


## Using a Grid

We can add more variable separation through columns and rows with the use of a grid. Just indicate this with the col or row arguments:


```python
sns.lmplot(x='total_bill',y='tip',data=tips,col='sex')
```




    <seaborn.axisgrid.FacetGrid at 0x7f62f11b45f8>




![png](../img/02/07_plotting_regression_11_1.png)



```python
sns.lmplot(x="total_bill", y="tip", row="sex", col="time",data=tips)
```




    <seaborn.axisgrid.FacetGrid at 0x7f62f1155fd0>




![png](../img/02/07_plotting_regression_12_1.png)



```python
sns.lmplot(x='total_bill',y='tip',data=tips,col='day',hue='sex',palette='coolwarm')
```




    <seaborn.axisgrid.FacetGrid at 0x7f62f0dbe0f0>




![png](../img/02/07_plotting_regression_13_1.png)


## Aspect and Size

Seaborn figures can have their size and aspect ratio adjusted with the **size** and **aspect** parameters:


```python
sns.lmplot(x='total_bill',y='tip',data=tips,col='day',hue='sex',palette='coolwarm',
          aspect=0.6,size=8)
```

    /home/ggilmore/.local/lib/python3.6/site-packages/seaborn/regression.py:546: UserWarning: The `size` paramter has been renamed to `height`; please update your code.
      warnings.warn(msg, UserWarning)





    <seaborn.axisgrid.FacetGrid at 0x7f62f008ef98>




![png](../img/02/07_plotting_regression_15_2.png)


You're probably wondering how to change the font size or control the aesthetics even more, check out the Style and Color Lecture and Notebook for more info on that!
