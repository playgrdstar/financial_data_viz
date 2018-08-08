
## Introduction to Pandas ##

With Numpy, it may sometimes still be a pain to manipulate data. For example, matrices in Numpy can't be labelled. The library Pandas has many goodies, but one of the most important is that it allows us to represent data in a table format (not unlike how we could imagine seeing them in Excel). This makes everything a lot more intuitive.

We first import the libraries. Numpy is also imported as we will usually use Numpy functions alongside Pandas


```python
import numpy as np
import pandas as pd
```

#### Series ####

We first start with series before we go to dataframes. A dataframe is basically akin to a table, and a series akin to a column in the table.

Series will be used a lot when we do time series analysis


```python
s1 = pd.Series(np.random.rand(4), index=['a', 'b', 'c', 'd'])
s1
```




    a    0.041447
    b    0.275973
    c    0.469297
    d    0.897424
    dtype: float64




```python
s1['c']
```




    0.46929705786676734



We can also create a Series from a dict.


```python
s2 = pd.Series({'a':1, 'b':'2', 'c':3})
s2
```




    a    1
    b    2
    c    3
    dtype: object



To check if there are any entries that are null


```python
pd.isnull(s2)
```




    a    False
    b    False
    c    False
    dtype: bool




```python
s3 = pd.Series(100, index=['x', 'y', 'z'])
s3
```




    x    100
    y    100
    z    100
    dtype: int64




```python
a = np.array([2,3,4])
p = pd.Series(a, index=['a', 'b', 'c'])
p
```




    a    2
    b    3
    c    4
    dtype: int64



Extending what we do for series to a dataframe is easy.


```python
data = {'Age':[1,2,3,4,5], 
        'Income':['H', 'M', 'L', 'M', 'L'], 
        'Gender': ['M', 'F', 'M', 'F', 'M']}
profile = pd.DataFrame(data)
profile
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Income</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>M</td>
      <td>H</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>F</td>
      <td>M</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>M</td>
      <td>L</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>F</td>
      <td>M</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>M</td>
      <td>L</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Setting columns and indices
profile_2 = pd.DataFrame(data, columns=['Income', 'Age', 'Gender'], index=['A','B','C','D','E'])
profile_2
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Income</th>
      <th>Age</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>H</td>
      <td>1</td>
      <td>M</td>
    </tr>
    <tr>
      <th>B</th>
      <td>M</td>
      <td>2</td>
      <td>F</td>
    </tr>
    <tr>
      <th>C</th>
      <td>L</td>
      <td>3</td>
      <td>M</td>
    </tr>
    <tr>
      <th>D</th>
      <td>M</td>
      <td>4</td>
      <td>F</td>
    </tr>
    <tr>
      <th>E</th>
      <td>L</td>
      <td>5</td>
      <td>M</td>
    </tr>
  </tbody>
</table>
</div>




```python
cohort = pd.DataFrame([['John', 20, 'Dentist'], 
                      ['Peter', 30, 'Doctor'],
                      ['Dirk', 40, 'Teacher']], 
                     columns=['Name', 'Age', 'Job'])
cohort
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>Job</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>John</td>
      <td>20</td>
      <td>Dentist</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Peter</td>
      <td>30</td>
      <td>Doctor</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Dirk</td>
      <td>40</td>
      <td>Teacher</td>
    </tr>
  </tbody>
</table>
</div>




```python
cohort['Name']
```




    0     John
    1    Peter
    2     Dirk
    Name: Name, dtype: object



Elements can be accessed by - <br>
* loc works on labels in the index.
* iloc works on the positions in the index (so it only takes integers).
* ix usually tries to behave like loc but falls back to behaving like iloc if the label is not in the index.



```python
#iloc, ix, loc
cohort.ix[1]
```




    Name     Peter
    Age         30
    Job     Doctor
    Name: 1, dtype: object




```python
cohort.iloc[2,1]
```




    40




```python
cohort.to_csv('cohort.csv')
```


```python
cohort2 = pd.read_csv('cohort.csv')
```


```python
cohort2
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>Name</th>
      <th>Age</th>
      <th>Job</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>John</td>
      <td>20</td>
      <td>Dentist</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Peter</td>
      <td>30</td>
      <td>Doctor</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Dirk</td>
      <td>40</td>
      <td>Teacher</td>
    </tr>
  </tbody>
</table>
</div>




```python
s2
```




    a    1
    b    2
    c    3
    dtype: object




```python
s2.reindex(['a', 'e', 'b'], fill_value='MISSING')
```




    a          1
    e    MISSING
    b          2
    dtype: object




```python
cohort.tail(2)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>Job</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Peter</td>
      <td>30</td>
      <td>Doctor</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Dirk</td>
      <td>40</td>
      <td>Teacher</td>
    </tr>
  </tbody>
</table>
</div>




```python
cohort.head(2)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>Job</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>John</td>
      <td>20</td>
      <td>Dentist</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Peter</td>
      <td>30</td>
      <td>Doctor</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1 = pd.DataFrame(np.arange(12).reshape(3,4))
df2 = pd.DataFrame(np.arange(20).reshape(4,5))
```


```python
df1
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>13</td>
      <td>14</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15</td>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Broadcast when they are not the same size
df1 + df2
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.0</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>6.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9.0</td>
      <td>11.0</td>
      <td>13.0</td>
      <td>15.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>18.0</td>
      <td>20.0</td>
      <td>22.0</td>
      <td>24.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
df3 =df1.add(df2, fill_value=0)
```


```python
df3
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.0</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>6.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9.0</td>
      <td>11.0</td>
      <td>13.0</td>
      <td>15.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>18.0</td>
      <td>20.0</td>
      <td>22.0</td>
      <td>24.0</td>
      <td>14.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15.0</td>
      <td>16.0</td>
      <td>17.0</td>
      <td>18.0</td>
      <td>19.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df3.eq(df2)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
cohort
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>Job</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>John</td>
      <td>20</td>
      <td>Dentist</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Peter</td>
      <td>30</td>
      <td>Doctor</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Dirk</td>
      <td>40</td>
      <td>Teacher</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Python 2 only
# cohort.irow(1)
```


```python
# Python 2 only
# cohort.icol(1)
```

Something like **covariance** is trivial in Pandas


```python
s_one = pd.Series(np.random.rand(3))
```


```python
s_two = pd.Series(np.random.rand(3))
```


```python
s_one.cov(s_two)
```




    0.03388788576785875




```python
df_three = pd.DataFrame(np.random.rand(12).reshape(4,3),  
                       columns=['a','b','c'])
```


```python
df_three
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.040781</td>
      <td>0.136619</td>
      <td>0.454001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.983112</td>
      <td>0.032677</td>
      <td>0.705141</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.672182</td>
      <td>0.706941</td>
      <td>0.348606</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.716236</td>
      <td>0.885049</td>
      <td>0.043661</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_three.cov()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>0.159395</td>
      <td>0.028200</td>
      <td>0.013909</td>
    </tr>
    <tr>
      <th>b</th>
      <td>0.028200</td>
      <td>0.175759</td>
      <td>-0.104322</td>
    </tr>
    <tr>
      <th>c</th>
      <td>0.013909</td>
      <td>-0.104322</td>
      <td>0.075019</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_three.corr(method='spearman') # pearson, kendall, spearman
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>1.0</td>
      <td>-0.2</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>b</th>
      <td>-0.2</td>
      <td>1.0</td>
      <td>-1.0</td>
    </tr>
    <tr>
      <th>c</th>
      <td>0.2</td>
      <td>-1.0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Correlation between Series with the same label in different Series
df_four = pd.DataFrame(np.arange(8).reshape(4,2), 
                       columns=['a', 'b'])
```


```python
df_five=df_four.corrwith(df_three)
```


```python
df_five
```




    a    0.554705
    b    0.899046
    c         NaN
    dtype: float64




```python
df_five.isnull()
```




    a    False
    b    False
    c     True
    dtype: bool




```python
df_five.notnull()
```




    a     True
    b     True
    c    False
    dtype: bool




```python
df_five.dropna()
```




    a    0.554705
    b    0.899046
    dtype: float64




```python
df_five.fillna(-1)
```




    a    0.554705
    b    0.899046
    c   -1.000000
    dtype: float64


