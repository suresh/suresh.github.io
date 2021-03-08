---
title: "Pivot Tables in Pandas, Python"
permalink: /snippets/pandas-pivot/
excerpt: "Making wide table into long table & vice versa"
last_modified_at: 2020-05-05
---
## Pivot tables

**ProTip:** __Refer to [Pandas User Guide](https://pandas.pydata.org/pandas-docs/stable/user_guide/reshaping.html#pivot-tables)__

While pivot() provides general purpose pivoting with various data types (strings, numerics, etc.), pandas also provides pivot_table() for pivoting with aggregation of numeric data.

The function pivot_table() can be used to create spreadsheet-style pivot tables. See the cookbook for some advanced strategies.

It takes a number of arguments:

* data: a DataFrame object.
* values: a column or a list of columns to aggregate.
* index: a column, Grouper, array which has the same length as data, or list of them. Keys to group by on the pivot table index. If an array is passed, it is being used as the same manner as column values.
* columns: a column, Grouper, array which has the same length as data, or list of them. Keys to group by on the pivot table column. If an array is passed, it is being used as the same manner as column values.
* aggfunc: function to use for aggregation, defaulting to numpy.mean.

## Example

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

%matplotlib inline 
```


```python
data_url = 'https://s3.amazonaws.com/tripdata/201907-citibike-tripdata.csv.zip'

data = pd.read_csv(data_url)
```


```python
data.head()
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
      <th>tripduration</th>
      <th>starttime</th>
      <th>stoptime</th>
      <th>start station id</th>
      <th>start station name</th>
      <th>start station latitude</th>
      <th>start station longitude</th>
      <th>end station id</th>
      <th>end station name</th>
      <th>end station latitude</th>
      <th>end station longitude</th>
      <th>bikeid</th>
      <th>usertype</th>
      <th>birth year</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>897</td>
      <td>2019-07-01 00:00:00.1320</td>
      <td>2019-07-01 00:14:58.0040</td>
      <td>493.0</td>
      <td>W 45 St &amp; 6 Ave</td>
      <td>40.756800</td>
      <td>-73.982912</td>
      <td>454.0</td>
      <td>E 51 St &amp; 1 Ave</td>
      <td>40.754557</td>
      <td>-73.965930</td>
      <td>18340</td>
      <td>Subscriber</td>
      <td>1966</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>267</td>
      <td>2019-07-01 00:00:05.1780</td>
      <td>2019-07-01 00:04:32.4500</td>
      <td>3143.0</td>
      <td>5 Ave &amp; E 78 St</td>
      <td>40.776321</td>
      <td>-73.964274</td>
      <td>3226.0</td>
      <td>W 82 St &amp; Central Park West</td>
      <td>40.782750</td>
      <td>-73.971370</td>
      <td>21458</td>
      <td>Customer</td>
      <td>1996</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2201</td>
      <td>2019-07-01 00:00:05.2130</td>
      <td>2019-07-01 00:36:46.7490</td>
      <td>317.0</td>
      <td>E 6 St &amp; Avenue B</td>
      <td>40.724537</td>
      <td>-73.981854</td>
      <td>3469.0</td>
      <td>India St &amp; West St</td>
      <td>40.731814</td>
      <td>-73.959950</td>
      <td>39874</td>
      <td>Subscriber</td>
      <td>1986</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1660</td>
      <td>2019-07-01 00:00:08.6010</td>
      <td>2019-07-01 00:27:48.8050</td>
      <td>249.0</td>
      <td>Harrison St &amp; Hudson St</td>
      <td>40.718710</td>
      <td>-74.009001</td>
      <td>369.0</td>
      <td>Washington Pl &amp; 6 Ave</td>
      <td>40.732241</td>
      <td>-74.000264</td>
      <td>38865</td>
      <td>Subscriber</td>
      <td>1988</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>109</td>
      <td>2019-07-01 00:00:12.1580</td>
      <td>2019-07-01 00:02:01.5670</td>
      <td>3552.0</td>
      <td>W 113 St &amp; Broadway</td>
      <td>40.805973</td>
      <td>-73.964928</td>
      <td>3538.0</td>
      <td>W 110 St &amp; Amsterdam Ave</td>
      <td>40.802692</td>
      <td>-73.962950</td>
      <td>30256</td>
      <td>Subscriber</td>
      <td>1997</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
data['starttime'] = pd.to_datetime(data['starttime'])
data.set_index('starttime', inplace=True)
```

## Create a pivoted table with count of rides for every day


```python
pivoted = data.pivot_table(values='bikeid', index=data.index.hour, columns=data.index.date, aggfunc=lambda x: len(x.unique()))
```


```python
pivoted.iloc[:5, :5]
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
      <th>2019-07-01</th>
      <th>2019-07-02</th>
      <th>2019-07-03</th>
      <th>2019-07-04</th>
      <th>2019-07-05</th>
    </tr>
    <tr>
      <th>starttime</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>605</td>
      <td>500</td>
      <td>513</td>
      <td>748</td>
      <td>865</td>
    </tr>
    <tr>
      <th>1</th>
      <td>324</td>
      <td>241</td>
      <td>301</td>
      <td>504</td>
      <td>450</td>
    </tr>
    <tr>
      <th>2</th>
      <td>176</td>
      <td>161</td>
      <td>162</td>
      <td>307</td>
      <td>291</td>
    </tr>
    <tr>
      <th>3</th>
      <td>105</td>
      <td>104</td>
      <td>98</td>
      <td>180</td>
      <td>181</td>
    </tr>
    <tr>
      <th>4</th>
      <td>156</td>
      <td>154</td>
      <td>141</td>
      <td>132</td>
      <td>122</td>
    </tr>
  </tbody>
</table>
</div>




```python
ax = pivoted.plot(legend=False, alpha=0.4, figsize=(20, 10), title='Hourly Ride counts');
ax.set_xlabel("Hour of the day")
ax.set_ylabel("Total rides");
```


![png](/assets/images/output_7_0.png)

