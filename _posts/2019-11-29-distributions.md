---
title: "Distributions"
category: articles
tags:
 - matplotlib
 - numpy
---

## Import necessary libraries


```python
import numpy as np

%matplotlib inline
from matplotlib import pyplot as plt
```

## Generate Normal & Pareto random numbers


```python
np.random.seed(1087)

X_norm = np.random.normal(size=(500))
X_poisson = np.random.pareto(5, size=(500))
```

## Plot histogram of random variables


```python
fig, ax = plt.subplots(2,1, figsize=(15, 10))

ax[0].hist(X_norm, bins=50, density=True, label='normal', color='b', alpha=0.3)
ax[1].hist(X_poisson, bins=50, density=True, label='pareto', color='r', alpha=0.3)
ax[0].legend(loc='best');
ax[0].set_title('Normal Distribution');
ax[1].legend(loc='best');
ax[1].set_title('Pareto α=5 Distribution');
```

![png](/assets/images/Distributions_5_0.png)