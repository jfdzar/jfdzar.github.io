---
bg: "tools.jpg"
layout: post
title:  Python Pandas Methods for Data Analysis
crawlertitle: Python Pandas Methods for Data Analysis
summary: Python Pandas Methods for Data Analysis
date:   2021-11-21
categories: posts
tags: ['python','data-science']
author: jfdzar
---

[Source 1](https://towardsdatascience.com/4-awesome-pandas-methods-to-quickly-analyze-any-dataset-65d2252af6e8)


```python
import pandas as pd
import numpy as np

df # Our Main DataFrame

df_country_group = df.groupby('Country')
df_country_group.mean()

df_country_group.get_group('Germany')
# Faster as df[df['Country'] == 'Germany']
# Test it in Jupyter Notebooks with %%timeit

df.nlargest(N, column_name, keep = 'first')
df.nlargest(3,'Number of Laptops')
# Same principle to nsmallest()
```

Then we have some logical comparation methods

* "<" : ".lt()"
* ">" : ".gt()"
* "<=" : ".le()"
* ">=" : ".ge()"
* "==" : ".eq()"
* "!=" : ".ne()"