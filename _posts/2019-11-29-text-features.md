---
title: "Text Features"
category: articles
tags:
 - sklearn
 - ml
---

## Importing necessary packages

```python
import pandas as pd
import numpy as np

from sklearn.feature_extraction.text import CountVectorizer, TfidfVectorizer
```

## Count Vectorizer turns sentences into word counts


```python
corpus = ['This is first sentence', 'Here is the second sentence', 'Third sentence']
```


```python
count_vec = CountVectorizer()
features = count_vec.fit_transform(corpus)
```


```python
pd.DataFrame(features.todense(), columns=count_vec.get_feature_names())
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
      <th>first</th>
      <th>here</th>
      <th>is</th>
      <th>second</th>
      <th>sentence</th>
      <th>the</th>
      <th>third</th>
      <th>this</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



## TFIDF Vectorizer turns sentences into vectors using probabilities


```python
tfidf = TfidfVectorizer()
features_tfidf = tfidf.fit_transform(corpus)
```


```python
pd.DataFrame(features_tfidf.todense(), columns=tfidf.get_feature_names())
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
      <th>first</th>
      <th>here</th>
      <th>is</th>
      <th>second</th>
      <th>sentence</th>
      <th>the</th>
      <th>third</th>
      <th>this</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.584483</td>
      <td>0.000000</td>
      <td>0.444514</td>
      <td>0.000000</td>
      <td>0.345205</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.584483</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.000000</td>
      <td>0.504611</td>
      <td>0.383770</td>
      <td>0.504611</td>
      <td>0.298032</td>
      <td>0.504611</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.508542</td>
      <td>0.000000</td>
      <td>0.861037</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
</div>