---
title: Logistic Regression
template: overrides/main.html
---

# Logistic Regression

For this section we will work with the <a href="https://www.kaggle.com/c/titanic" target="_blank">Titanic Data Set from Kaggle</a>. We'll be trying to predict a classification problem - survival or deceased. Let's begin our understanding of implementing Logistic Regression in Python for classification. We'll use a "semi-cleaned" version of the titanic data set, if you use the data set hosted directly on Kaggle, you may need to do some additional cleaning not shown in this notebook.

Let's import some libraries and load the dataset:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline

train = pd.read_csv('../data/titanic_train.csv')
```

Let's view the data present in the dataset:

```python
train.head()
```

<table>
    <tr>
        <td></td>
        <td>PassengerId</td>
        <td>Survived</td>
        <td>Pclass</td>
        <td>Name</td>
        <td>Sex</td>
        <td>Age</td>
        <td>SibSp</td>
        <td>Parch</td>
        <td>Ticket</td>
        <td>Fare</td>
        <td>Cabin</td>
        <td>Embarked</td>
    </tr>
    <tr>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>3</td>
        <td>Braund, Mr. Owen Harris</td>
        <td>male</td>
        <td>22.0</td>
        <td>1</td>
        <td>0</td>
        <td>A/5 21171</td>
        <td>7.2500</td>
        <td>NaN</td>
        <td>S</td>
    </tr>
    <tr>
        <td>1</td>
        <td>2</td>
        <td>1</td>
        <td>1</td>
        <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
        <td>female</td>
        <td>38.0</td>
        <td>1</td>
        <td>0</td>
        <td>PC 17599</td>
        <td>71.2833</td>
        <td>C85</td>
        <td>C</td>
    </tr>
    <tr>
        <td>2</td>
        <td>3</td>
        <td>1</td>
        <td>3</td>
        <td>Heikkinen, Miss. Laina</td>
        <td>female</td>
        <td>26.0</td>
        <td>0</td>
        <td>0</td>
        <td>STON/O2. 3101282</td>
        <td>7.9250</td>
        <td>NaN</td>
        <td>S</td>
    </tr>
    <tr>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>1</td>
        <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
        <td>female</td>
        <td>35.0</td>
        <td>1</td>
        <td>0</td>
        <td>113803</td>
        <td>53.1000</td>
        <td>C123</td>
        <td>S</td>
    </tr>
    <tr>
        <td>4</td>
        <td>5</td>
        <td>0</td>
        <td>3</td>
        <td>Allen, Mr. William Henry</td>
        <td>male</td>
        <td>35.0</td>
        <td>0</td>
        <td>0</td>
        <td>373450</td>
        <td>8.0500</td>
        <td>NaN</td>
        <td>S</td>
    </tr>
</table>


## Exploratory Data Analysis

Let's begin some exploratory data analysis! We'll start by checking out missing data!

### Missing Data

We can use seaborn to create a simple heatmap to see where we are missing data!

```python
sns.heatmap(train.isnull(),yticklabels=False,cbar=False,cmap='viridis');
```
    
<center>
    <figure>
        <img src="img/logistic_regression_01.png" alt="logistic_regression_01"/>
        <figcaption>.</figcaption>
    </figure>
</center>

Roughly 20 percent of the Age data is missing. The proportion of Age missing is likely small enough for reasonable replacement with some form of imputation. Looking at the Cabin column, it looks like we are just missing too much of that data to do something useful with at a basic level. We'll probably drop this later, or change it to another feature like "Cabin Known: 1 or 0"

Let's continue on by visualizing some more of the data such as our target variable survival:

```python
sns.set_style('whitegrid');
sns.countplot(x='Survived',data=train,palette='RdBu_r');
```

<center>
    <figure>
        <img src="img/logistic_regression_02.png" alt="logistic_regression_02"/>
        <figcaption>.</figcaption>
    </figure>
</center>

We can manipulate the data a bit and look at the difference in survival betwen men and women:

```python
sns.set_style('whitegrid');
sns.countplot(x='Survived',hue='Sex',data=train,palette='RdBu_r');
```

<center>
    <figure>
        <img src="img/logistic_regression_03.png" alt="logistic_regression_03"/>
    </figure>
</center>

We can also split the data up based on the class level of the passengers:

```python
sns.set_style('whitegrid');
sns.countplot(x='Survived',hue='Pclass',data=train,palette='rainbow');
```

<center>
    <figure>
        <img src="img/logistic_regression_04.png" alt="logistic_regression_04"/>
    </figure>
</center>


Let's now look at the distribution of age for the passengers:

```python
sns.distplot(train['Age'].dropna(),kde=False,color='darkred',bins=30);
```

<center>
    <figure>
        <img src="img/logistic_regression_05.png" alt="logistic_regression_05"/>
    </figure>
</center>


## Data Cleaning

We want to fill in missing age data instead of just dropping the missing age data rows. One way to do this is by filling in the mean age of all the passengers (imputation). However we can be smarter about this and check the average age by passenger class. For example:


```python
plt.figure(figsize=(12, 7));
sns.boxplot(x='Pclass',y='Age',data=train,palette='winter');
```

<center>
    <figure>
        <img src="img/logistic_regression_06.png" alt="logistic_regression_06"/>
    </figure>
</center>

We can see the wealthier passengers in the higher classes tend to be older, which makes sense. We'll use these average age values to impute based on Pclass for Age.

```python
def impute_age(cols):
    Age = cols[0]
    Pclass = cols[1]
    
    if pd.isnull(Age):
        if Pclass == 1:
            return 37
        elif Pclass == 2:
            return 29
        else:
            return 24
    else:
        return Age
```

Now apply that function:

```python
train['Age'] = train[['Age','Pclass']].apply(impute_age,axis=1)
```

Now let's check that heat map again!

```python
sns.heatmap(train.isnull(),yticklabels=False,cbar=False,cmap='viridis');
```

<center>
    <figure>
        <img src="img/logistic_regression_07.png" alt="logistic_regression_07"/>
    </figure>
</center>

Great! Let's go ahead and drop the Cabin column and the row in Embarked that is NaN.

```python
train.drop('Cabin',axis=1,inplace=True);
train.dropna(inplace=True);

train.head()
```

<table>
    <tr>
        <td></td>
        <td>PassengerId</td>
        <td>Survived</td>
        <td>Pclass</td>
        <td>Name</td>
        <td>Sex</td>
        <td>Age</td>
        <td>SibSp</td>
        <td>Parch</td>
        <td>Ticket</td>
        <td>Fare</td>
        <td>Embarked</td>
    </tr>
    <tr>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>3</td>
        <td>Braund, Mr. Owen Harris</td>
        <td>male</td>
        <td>22.0</td>
        <td>1</td>
        <td>0</td>
        <td>A/5 21171</td>
        <td>7.2500</td>
        <td>S</td>
    </tr>
    <tr>
        <td>1</td>
        <td>2</td>
        <td>1</td>
        <td>1</td>
        <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
        <td>female</td>
        <td>38.0</td>
        <td>1</td>
        <td>0</td>
        <td>PC 17599</td>
        <td>71.2833</td>
        <td>C</td>
    </tr>
    <tr>
        <td>2</td>
        <td>3</td>
        <td>1</td>
        <td>3</td>
        <td>Heikkinen, Miss. Laina</td>
        <td>female</td>
        <td>26.0</td>
        <td>0</td>
        <td>0</td>
        <td>STON/O2. 3101282</td>
        <td>7.9250</td>
        <td>S</td>
    </tr>
    <tr>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>1</td>
        <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
        <td>female</td>
        <td>35.0</td>
        <td>1</td>
        <td>0</td>
        <td>113803</td>
        <td>53.1000</td>
        <td>S</td>
    </tr>
    <tr>
        <td>4</td>
        <td>5</td>
        <td>0</td>
        <td>3</td>
        <td>Allen, Mr. William Henry</td>
        <td>male</td>
        <td>35.0</td>
        <td>0</td>
        <td>0</td>
        <td>373450</td>
        <td>8.0500</td>
        <td>S</td>
    </tr>
</table>

### Converting Categorical Features 

We'll need to convert categorical features to dummy variables using pandas. If we do not convert then our machine learning algorithm won't be able to directly take in those features as inputs.

```python
train.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 889 entries, 0 to 890
    Data columns (total 11 columns):
    PassengerId    889 non-null int64
    Survived       889 non-null int64
    Pclass         889 non-null int64
    Name           889 non-null object
    Sex            889 non-null object
    Age            889 non-null float64
    SibSp          889 non-null int64
    Parch          889 non-null int64
    Ticket         889 non-null object
    Fare           889 non-null float64
    Embarked       889 non-null object
    dtypes: float64(2), int64(5), object(4)
    memory usage: 83.3+ KB


```python
sex = pd.get_dummies(train['Sex'],drop_first=True)
embark = pd.get_dummies(train['Embarked'],drop_first=True)
```

```python
train.drop(['Sex','Embarked','Name','Ticket'],axis=1,inplace=True)
```

```python
train = pd.concat([train,sex,embark],axis=1)
```

```python
train.head()
```
<table>
    <tr>
        <td></td>
        <td>PassengerId</td>
        <td>Survived</td>
        <td>Pclass</td>
        <td>Age</td>
        <td>SibSp</td>
        <td>Parch</td>
        <td>Fare</td>
        <td>male</td>
        <td>Q</td>
        <td>S</td>
    </tr>
    <tr>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>3</td>
        <td>22.0</td>
        <td>1</td>
        <td>0</td>
        <td>7.2500</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
    </tr>
    <tr>
        <td>1</td>
        <td>2</td>
        <td>1</td>
        <td>1</td>
        <td>38.0</td>
        <td>1</td>
        <td>0</td>
        <td>71.2833</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
    </tr>
    <tr>
        <td>2</td>
        <td>3</td>
        <td>1</td>
        <td>3</td>
        <td>26.0</td>
        <td>0</td>
        <td>0</td>
        <td>7.9250</td>
        <td>0</td>
        <td>0</td>
        <td>1</td>
    </tr>
    <tr>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>1</td>
        <td>35.0</td>
        <td>1</td>
        <td>0</td>
        <td>53.1000</td>
        <td>0</td>
        <td>0</td>
        <td>1</td>
    </tr>
    <tr>
        <td>4</td>
        <td>5</td>
        <td>0</td>
        <td>3</td>
        <td>35.0</td>
        <td>0</td>
        <td>0</td>
        <td>8.0500</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
    </tr>
</table>

Great! Our data is ready for our model!

## Building a Logistic Regression model

Let's start by splitting our data into a training set and test set (there is another test.csv file that you can play around with in case you want to use all this data for training).

### Train Test Split


```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(train.drop('Survived',axis=1), 
                                                    train['Survived'], test_size=0.30, 
                                                    random_state=101)
```

### Training and Predicting


```python
from sklearn.linear_model import LogisticRegression

logmodel = LogisticRegression()
logmodel.fit(X_train,y_train)
```


```python
predictions = logmodel.predict(X_test)
```

Let's move on to evaluate our model!

### Evaluation

We can check precision,recall,f1-score using classification report!


```python
from sklearn.metrics import classification_report

print(classification_report(y_test,predictions))
```

Not so bad! You might want to explore other feature engineering and the other titanic_text.csv file, some suggestions for feature engineering:

* Try grabbing the Title (Dr.,Mr.,Mrs,etc..) from the name as a feature
* Maybe the Cabin letter could be a feature
* Is there any info you can get from the ticket?
