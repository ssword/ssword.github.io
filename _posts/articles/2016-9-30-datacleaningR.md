---
layout: post
title: Some notes on data cleaning with R
---

Most of the contents here are taken fromt he R base package documents.

## Data exploring

* head()
* tail()
* str()
* class()
* dim()
* names()
* summary()
* glimpse {dplyr}
* hist
* plot
* is.na
* any(is.na())
* which(is.na())


## **gather {tidyr}**

### Description

Gather takes multiple columns and collapses into key-value pairs, duplicating all other columns as needed. You use gather() when you notice that you have columns that are not variables.

### Usage

```R
gather(data, key, value, ..., na.rm = FALSE, convert = FALSE,
  factor_key = FALSE)
```

## **spread {tidyr}**

### Description

Spread a key-value pair across multiple columns.
The opposite of gather

### Usage

```R
spread(data, key, value, fill = NA, convert = FALSE, drop = TRUE,
  sep = NULL)
```

## **separate {tidyr}**

### Description

Given either regular expression or a vector of character positions, separate() turns a single character column into multiple columns.

### Usage

```R
separate(data, col, into, sep = "[^[:alnum:]]+", remove = TRUE,
  convert = FALSE, extra = "warn", fill = "warn", ...)
```

## **unite {tidyr}**

### Usage

```R
unite(data, col, ..., sep = "_", remove = TRUE)
```

## cell processing functions

* str_trim {stringr}
* str_pad {stringr}
* str_replace {stringr}
* complete.cases()
* na.omit()




