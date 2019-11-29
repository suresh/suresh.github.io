---
title: "Text Features"
category: articles
tags:
 - sklearn
 - ml
---

# Text Features

## Preliminaries

```python
import pandas as pd
import pandas as pd

from sklearn.decomposition import CountVectorizer, TfidfVectorizer
```

## Count Vectorizer

```python
corpus = ['Germany is the really awesome', 'France is very artistic', 'Italy has beautiful culture and history']

count_vec = CountVectorizer()
features = count_vec.fit_transform(corpus)

pd.DataFrame(features.toarray(), columns=count_vec.get_feature_names())
```


## TFIDF Vectorizer

```python
tfidf = TfidfVectorizer()
features_tfidf = tfidf.fit_transform(corpus)

pd.DataFrame(features_tfidf.toarray(), columns=tfidf.get_feature_names())
```