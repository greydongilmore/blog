---
title: Categorical Data Plots
linktitle: Categorical Data Plots
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ml_intro:
    parent: 02. Plotting
    weight: 5

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 5
---

Now let's discuss using seaborn to plot categorical data! There are a few main plot types for this:

* factorplot
* boxplot
* violinplot
* stripplot
* swarmplot
* barplot
* countplot

Let's go through examples of each!


```python
import seaborn as sns
%matplotlib inline
```


```python
tips = sns.load_dataset('tips')
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



## barplot and countplot

These very similar plots allow you to get aggregate data off a categorical feature in your data. **barplot** is a general plot that allows you to aggregate the categorical data based off some function, by default the mean:


```python
sns.barplot(x='sex',y='total_bill',data=tips)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f527c50fa58>




![png](../img/02/04_plotting_categorical_4_1.png)



```python
import numpy as np
```

You can change the estimator object to your own function, that converts a vector to a scalar:


```python
sns.barplot(x='sex',y='total_bill',data=tips,estimator=np.std)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f527c506dd8>




![png](../img/02/04_plotting_categorical_7_1.png)


### countplot

This is essentially the same as barplot except the estimator is explicitly counting the number of occurrences. Which is why we only pass the x value:


```python
sns.countplot(x='sex',data=tips)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f527c460e48>




![png](../img/02/04_plotting_categorical_9_1.png)


## boxplot and violinplot

boxplots and violinplots are used to shown the distribution of categorical data. A box plot (or box-and-whisker plot) shows the distribution of quantitative data in a way that facilitates comparisons between variables or across levels of a categorical variable. The box shows the quartiles of the dataset while the whiskers extend to show the rest of the distribution, except for points that are determined to be “outliers” using a method that is a function of the inter-quartile range.


```python
sns.boxplot(x="day", y="total_bill", data=tips,palette='rainbow')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f527c4e5710>




![png](../img/02/04_plotting_categorical_11_1.png)



```python
# Can do entire dataframe with orient='h'
sns.boxplot(data=tips,palette='rainbow',orient='h')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f527c352080>




![png](../img/02/04_plotting_categorical_12_1.png)



```python
sns.boxplot(x="day", y="total_bill", hue="smoker",data=tips, palette="coolwarm")
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f527c34b6d8>




![png](../img/02/04_plotting_categorical_13_1.png)


### violinplot
A violin plot plays a similar role as a box and whisker plot. It shows the distribution of quantitative data across several levels of one (or more) categorical variables such that those distributions can be compared. Unlike a box plot, in which all of the plot components correspond to actual datapoints, the violin plot features a kernel density estimation of the underlying distribution.


```python
sns.violinplot(x="day", y="total_bill", data=tips,palette='rainbow')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f527c1cc9b0>




![png](../img/02/04_plotting_categorical_15_1.png)



```python
sns.violinplot(x="day", y="total_bill", data=tips,hue='sex',palette='Set1')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f527c14e470>




![png](../img/02/04_plotting_categorical_16_1.png)



```python
sns.violinplot(x="day", y="total_bill", data=tips,hue='sex',split=True,palette='Set1')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f527c0f6f98>




![png](../img/02/04_plotting_categorical_17_1.png)


## stripplot and swarmplot
The stripplot will draw a scatterplot where one variable is categorical. A strip plot can be drawn on its own, but it is also a good complement to a box or violin plot in cases where you want to show all observations along with some representation of the underlying distribution.

The swarmplot is similar to stripplot(), but the points are adjusted (only along the categorical axis) so that they don’t overlap. This gives a better representation of the distribution of values, although it does not scale as well to large numbers of observations (both in terms of the ability to show all the points and in terms of the computation needed to arrange them).


```python
sns.stripplot(x="day", y="total_bill", data=tips)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f527c0206d8>




![png](../img/02/04_plotting_categorical_19_1.png)



```python
sns.stripplot(x="day", y="total_bill", data=tips,jitter=True)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f527bff4a20>




![png](../img/02/04_plotting_categorical_20_1.png)



```python
sns.stripplot(x="day", y="total_bill", data=tips,jitter=True,hue='sex',palette='Set1')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f527bf5d9e8>




![png](../img/02/04_plotting_categorical_21_1.png)



```python
sns.stripplot(x="day", y="total_bill", data=tips,jitter=True,hue='sex',palette='Set1',dodge=True)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f527beceba8>




![png](../img/02/04_plotting_categorical_22_1.png)



```python
sns.swarmplot(x="day", y="total_bill", data=tips)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f527beb88d0>




![png](../img/02/04_plotting_categorical_23_1.png)



```python
sns.swarmplot(x="day", y="total_bill",hue='sex',data=tips, palette="Set1", dodge=True)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f527be82d68>




![png](../img/02/04_plotting_categorical_24_1.png)


### Combining Categorical Plots


```python
sns.violinplot(x="tip", y="day", data=tips,palette='rainbow')
sns.swarmplot(x="tip", y="day", data=tips,color='black',size=3)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f527be088d0>




![png](../img/02/04_plotting_categorical_26_1.png)


## factorplot

factorplot is the most general form of a categorical plot. It can take in a **kind** parameter to adjust the plot type:


```python
sns.catplot(x='sex',y='total_bill',data=tips,kind='bar')
```




    <seaborn.axisgrid.FacetGrid at 0x7f527bece4a8>




![png](../img/02/04_plotting_categorical_28_1.png)

