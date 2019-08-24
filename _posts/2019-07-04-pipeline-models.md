---
layout: single # post-no-feature
title: "Models in Pipelines"
# description: "Pipelines for Model Building"
toc: true
toc_label: "In this page"
toc_icon: "cog"
category: articles
tags:
 - ML
 - Data Science
---
## Pipeline are useful for model building

Data transfromation is a key step in any ML problem. It can quickly become cumbersome and error prone if this is done by hand. Scikit-learn gives the *pipeline* object to solve this problem.

Let's say in a given problem, we would like to do the following:

* Impute missing values using the mean
* Transform features to quadratic
* Fit a lineear regression

## Example

```python
from sklearn.pipeline import make_pipeline

model = make_pipeline(Imputer(strategy='mean'),
                      PolynomialFeatures(degree=2),  
                      LinearRegression())

```

The pipeline object behaves like a Sklearn object and can take the *fit* and *predict* steps.

```python
model.fit(X, y)
pred = model.predict(X)
```

We could apply GridSearch for Hyperparameters selection on this pipeline object do get the best performing model.
