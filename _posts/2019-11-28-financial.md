---
title: "Financial Timeseries"
category: articles
tags:
 - matplotlib
 - pandas
---

##  Get Pandas Datareader

```python
import pandas as pd
import numpy as np
from pandas_datareader import data
```

## Get Google stock prices

```python
goog = data.DataReader('GOOG', start='2004', end='2018', data_source='yahoo')
goog.head()
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
      <th>High</th>
      <th>Low</th>
      <th>Open</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Adj Close</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2004-08-19</th>
      <td>51.835709</td>
      <td>47.800831</td>
      <td>49.813286</td>
      <td>49.982655</td>
      <td>44871300.0</td>
      <td>49.982655</td>
    </tr>
    <tr>
      <th>2004-08-20</th>
      <td>54.336334</td>
      <td>50.062355</td>
      <td>50.316402</td>
      <td>53.952770</td>
      <td>22942800.0</td>
      <td>53.952770</td>
    </tr>
    <tr>
      <th>2004-08-23</th>
      <td>56.528118</td>
      <td>54.321388</td>
      <td>55.168217</td>
      <td>54.495735</td>
      <td>18342800.0</td>
      <td>54.495735</td>
    </tr>
    <tr>
      <th>2004-08-24</th>
      <td>55.591629</td>
      <td>51.591621</td>
      <td>55.412300</td>
      <td>52.239193</td>
      <td>15319700.0</td>
      <td>52.239193</td>
    </tr>
    <tr>
      <th>2004-08-25</th>
      <td>53.798351</td>
      <td>51.746044</td>
      <td>52.284027</td>
      <td>52.802086</td>
      <td>9232100.0</td>
      <td>52.802086</td>
    </tr>
  </tbody>
</table>
</div>




```python
goog_p = goog['Adj Close']
```


```python
%matplotlib inline
import matplotlib.pyplot as plt
plt.style.use('seaborn-ticks')
import seaborn; seaborn.set_style('whitegrid')
```


```python
goog_p.plot(figsize=(15,10))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x128dc0610>




![png](/assets/images/Pandas%20Time%20Series%20Plots%2020191106_4_1.png)


## Compute Yearly Return
A common context for financial timeseries data is computing difference over time. For example, we can calculate one-year returns using pandas.


```python
goog_p = goog_p.asfreq('D', method='pad')    
ROI = 100 * (goog_p.tshift(-365)/goog_p - 1)

ROI.plot(figsize=(15, 10))
plt.ylabel('% Return on Investment');
```


![png](/assets/images/Pandas%20Time%20Series%20Plots%2020191106_6_0.png)



```python
y1_return = goog['Adj Close'].pct_change().rolling(365).sum().dropna()
y1_vol = goog['Adj Close'].pct_change().rolling(365).std().dropna()
```


```python
plt.figure(figsize=(15, 10))
seaborn.distplot(y1_return*100)
plt.ylabel('% Yearly Rolling Return')
plt.title('GOOG Historical Returns');
```


![png](/assets/images/Pandas%20Time%20Series%20Plots%2020191106_8_0.png)
