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


Pandas is the go-to library in Python for data manipulation and analysis. In this guide, we’ll walk through some of the most useful methods that help you **inspect**, **filter**, **aggregate**, and **transform** DataFrames.

## 1. Quick Data Inspection

Before diving into analysis, get a feel for your DataFrame (`df`):

```python
# View first/last rows
df.head(5)
df.tail(5)

# Summary of columns, dtypes and non-null counts
df.info()

# Descriptive statistics for numeric columns
df.describe()
```

## 2. Selecting & Filtering Data

### Column & Row Selection

```python
# Single column as Series
df['Country']

# Multiple columns as DataFrame
df[['Country', 'Sales']]

# Row by integer position
df.iloc[0]

# Row by label (index)
df.loc['row_label']
```

### Boolean Indexing

Combine comparisons with logical operators:

```python
# Simple comparison
df[df['Sales'] > 1000]

# Chain conditions with bitwise operators
df[(df['Sales'] > 1000) & (df['Country'] == 'Germany')]

# Using element-wise methods
df[df['Sales'].gt(1000)]
df[df['Country'].eq('Germany')]
```

Common element-wise comparison methods:

| Operator | Method    |
|:--------:|:----------|
| `<`      | `.lt()`   |
| `>`      | `.gt()`   |
| `<=`     | `.le()`   |
| `>=`     | `.ge()`   |
| `==`     | `.eq()`   |
| `!=`     | `.ne()`   |

## 3. Grouping & Aggregation

Group data to compute summary statistics:

```python
# Group by one or more columns
df_country = df.groupby('Country')

# Compute mean of all numeric columns per country
df_country.mean()

# Get the group for a specific key
germany = df_country.get_group('Germany')
```

> **Tip:** `get_group('Germany')` is often faster than `df[df['Country'] == 'Germany']`. Benchmark in Jupyter with `%%timeit`.

Aggregate with custom functions:

```python
# Multiple aggregations
df.groupby('Country').agg({
    'Sales': ['sum', 'mean', 'max'],
    'Orders': 'count'
})
```

## 4. Finding Top / Bottom N Rows

Quickly retrieve the largest or smallest values:

```python
# Top 3 by Sales
df.nlargest(3, 'Sales', keep='first')

# Bottom 5 by Profit
df.nsmallest(5, 'Profit')
```

## 5. Value Counts & Unique Values

Understand category distributions:

```python
# Count occurrences
df['Country'].value_counts()

# Unique categories
df['Country'].unique()
```

## 6. Pivot Tables

Reshape and summarize data:

```python
pd.pivot_table(
    df,
    values='Sales',
    index='Country',
    columns='Product',
    aggfunc='sum',
    fill_value=0
)
```

## 7. Handling Missing Data

Detect and handle `NaN`s:

```python
# Count missing per column
df.isna().sum()

# Drop any rows with missing values
df.dropna()

# Fill missing with a constant or a method
df.fillna(0)
df.fillna(method='ffill')
```

## 8. Applying Functions

Element-wise or row-/column-wise transformations:

```python
# Apply a function to each element
df['Sales'].apply(lambda x: x * 1.2)

# Apply row-wise
df.apply(lambda row: row['Sales'] / row['Orders'], axis=1)
```

## 9. Combining DataFrames

Merge, join, and concatenate:

```python
# Horizontal merge on key
pd.merge(df_left, df_right, on='CustomerID', how='inner')

# Vertical concatenation
pd.concat([df1, df2], axis=0, ignore_index=True)
```

---

Inspiration came from this article
[Source 1](https://towardsdatascience.com/4-awesome-pandas-methods-to-quickly-analyze-any-dataset-65d2252af6e8)

With these methods in your toolkit, you can rapidly explore, clean, and summarize your datasets using Pandas. Happy analyzing!

