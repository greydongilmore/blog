---
title: Distribution Plots
linktitle: Distribution Plots
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ml_intro:
    parent: 02. Plotting
    weight: 4

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 4
---

Let's discuss some plots that allow us to visualize the distribution of a data set. These plots are:

* distplot
* jointplot
* pairplot
* rugplot
* kdeplot

___
## Imports


```python
import seaborn as sns
%matplotlib inline
```

## Data
Seaborn comes with built-in data sets!


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



## distplot

The distplot shows the distribution of a univariate set of observations.


```python
sns.distplot(tips['total_bill'])
# Safe to ignore warnings
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f094c6b3a90>




![png](../img/02/03_plotting_distribution_7_1.png)


To remove the kde layer and just have the histogram use:


```python
sns.distplot(tips['total_bill'],kde=False,bins=30)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f094a543e10>




![png](../img/02/03_plotting_distribution_9_1.png)


## jointplot

jointplot() allows you to basically match up two distplots for bivariate data. With your choice of what **kind** parameter to compare with: 
* “scatter” 
* “reg” 
* “resid” 
* “kde” 
* “hex”


```python
sns.jointplot(x='total_bill',y='tip',data=tips,kind='scatter')
```




    <seaborn.axisgrid.JointGrid at 0x7f0949ed63c8>




![png](../img/02/03_plotting_distribution_11_1.png)



```python
sns.jointplot(x='total_bill',y='tip',data=tips,kind='hex')
```




    <seaborn.axisgrid.JointGrid at 0x7f094cf28cc0>




![png](../img/02/03_plotting_distribution_12_1.png)



```python
sns.jointplot(x='total_bill',y='tip',data=tips,kind='reg')
```




    <seaborn.axisgrid.JointGrid at 0x7f0949ce0eb8>




![png](../img/02/03_plotting_distribution_13_1.png)


## pairplot

pairplot will plot pairwise relationships across an entire dataframe (for the numerical columns) and supports a color hue argument (for categorical columns). 


```python
sns.pairplot(tips)
```




    <seaborn.axisgrid.PairGrid at 0x7f0949a907f0>




![png](../img/02/03_plotting_distribution_15_1.png)



```python
sns.pairplot(tips,hue='sex',palette='coolwarm')
```




    <seaborn.axisgrid.PairGrid at 0x7f094968dda0>




![png](../img/02/03_plotting_distribution_16_1.png)


## rugplot

rugplots are actually a very simple concept, they just draw a dash mark for every point on a univariate distribution. They are the building block of a KDE plot:


```python
sns.rugplot(tips['total_bill'])
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f094913c898>




![png](../img/02/03_plotting_distribution_18_1.png)


## kdeplot

kdeplots are [Kernel Density Estimation plots](http://en.wikipedia.org/wiki/Kernel_density_estimation#Practical_estimation_of_the_bandwidth). These KDE plots replace every single observation with a Gaussian (Normal) distribution centered around that value. For example:


```python
# Don't worry about understanding this code!
# It's just for the diagram below
import numpy as np
import matplotlib.pyplot as plt
from scipy import stats

#Create dataset
dataset = np.random.randn(25)

# Create another rugplot
sns.rugplot(dataset);

# Set up the x-axis for the plot
x_min = dataset.min() - 2
x_max = dataset.max() + 2

# 100 equally spaced points from x_min to x_max
x_axis = np.linspace(x_min,x_max,100)

# Set up the bandwidth, for info on this:
url = 'http://en.wikipedia.org/wiki/Kernel_density_estimation#Practical_estimation_of_the_bandwidth'

bandwidth = ((4*dataset.std()**5)/(3*len(dataset)))**.2


# Create an empty kernel list
kernel_list = []

# Plot each basis function
for data_point in dataset:
    
    # Create a kernel for each point and append to list
    kernel = stats.norm(data_point,bandwidth).pdf(x_axis)
    kernel_list.append(kernel)
    
    #Scale for plotting
    kernel = kernel / kernel.max()
    kernel = kernel * .4
    plt.plot(x_axis,kernel,color = 'grey',alpha=0.5)

plt.ylim(0,1)
```




    (0, 1)




![png](../img/02/03_plotting_distribution_20_1.png)



```python
# To get the kde plot we can sum these basis functions.

# Plot the sum of the basis function
sum_of_kde = np.sum(kernel_list,axis=0)

# Plot figure
fig = plt.plot(x_axis,sum_of_kde,color='indianred')

# Add the initial rugplot
sns.rugplot(dataset,c = 'indianred')

# Get rid of y-tick marks
plt.yticks([])

# Set title
plt.suptitle("Sum of the Basis Functions")
```




    Text(0.5, 0.98, 'Sum of the Basis Functions')




![png](../img/02/03_plotting_distribution_21_1.png)


So with our tips dataset:


```python
sns.kdeplot(tips['total_bill'])
sns.rugplot(tips['total_bill'])
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f09491856a0>




![png](../img/02/03_plotting_distribution_23_1.png)



```python
sns.kdeplot(tips['tip'])
sns.rugplot(tips['tip'])
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f0948023e80>




![png](../img/02/03_plotting_distribution_24_1.png)

