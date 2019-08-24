---
layout: single # post-no-feature
title: "Scikit Pipelines for ML"
description: "Data Preparation and Model Building"
toc: true
toc_label: "In this page"
toc_icon: "cog"
category: articles
tags:
 - ML
 - Data Science
---
## What is a Pipeline?

Transformers are usually combined with classifiers, regressors or other estimators to build a composite estimator. The most common tool is a Pipeline. *Pipeline* can be used to chain multiple estimators into one. This is useful as there is often a fixed sequence of steps in processing the data, for example feature selection, normalization and classification.

Pipeline offers these benefits:

* Convenience and encapsulation - You only have to call fit and predict once on your data to fit a whole sequence of estimators
* Joint parameter selection - Yuo can grid search over parameters of all estimators in the pipeline at once
* Safety - Pipelines help avoid leaking stats between test data into the trained model in cross-validation, by ensuring that the same samples are used to train the transformers and predictors

All estimators in a pipeline, except the last one, must be transformers (i.e must have a transform method). The last estimator may be any type (transformer, classifier, etc).

## Example

The *Pipeline* is built using a list of *(key, value)* pairs, where the *key* is a string containing the name you want to give this step and *value* is an estimator object.

```python
from sklearn.pipeline import Pipeline
from sklearn.svm import SVC
from sklearn.decomposition import PCA
estimators = [('reduce_dim', PCA()), ('clf', SVC())]
pipe = Pipeline(estimators)
pipe 
```

Parameters of the estimators in the pipeline can be accessed using the *<estimator>__<parameter>* syntax:

```python
pipe.set_params(clf__C=10)
>>> Pipeline(memory=None,
>>>         steps=[('reduce_dim', PCA(copy=True, iterated_power='auto',...)),
>>>                ('clf', SVC(C=10, cache_size=200, class_weight=None,...))],
>>>         verbose=False)
```

## Model Selection using Grid Search

Pipeline and parameter setting is particularly important for doing grid searches:

```python
from sklearn.model_selection import GridSearchCV
param_grid = dict(reduce_dim__n_components=[2, 5, 10],
                  clf__C=[0.1, 10, 100])
grid_search = GridSearchCV(pipe, param_grid=param_grid)
```

Individual steps may also be replaced as parameters, and non-final steps may be ignored by setting them to *'passthrough'*:

```python
from sklearn.linear_model import LogisticRegression
param_grid = dict(reduce_dim=['passthrough', PCA(5), PCA(10)],
                  clf=[SVC(), LogisticRegression()],
                  clf__C=[0.1, 10, 100])
grid_search = GridSearchCV(pipe, param_grid=param_grid)
```


