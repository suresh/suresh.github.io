---
layout: single
title: "Processing Large CSV Files in Pandas"
description: "Reading and transforming large input files using Pandas"
toc: true
toc_label: "In this page"
toc_icon: "cog"
category: articles
tags:
 - ML
 - Data Science
 - Pandas
---
## Large CSV files

First step of any data science project is to analyze the dataset. Sometimes these datasets are fairly large with millions or billions of rows. It becomes a challenge to import and analyze these on laptops or AWS instances. Here is an approach to solving this problem.

For this illustration, we are going to use [citibike dataset](https://s3.amazonaws.com/tripdata/201907-citibike-tripdata.csv.zip). This dataset is from the NYC Citibike system and contains anonymized trip data for July 2019.

## Pandas read_csv *chunksize*

Pandas 'read_csv' method gives a nice way to handle large files. Parameter **'chunksize'**  supports optionally iterating or breaking of the file into chunks.

By specifying a chunksize to read_csv, the return value will be an iterable object of type TextFileReader.

## Example

Here is the sample code for reading the CSV file in chunks of 1000 and print the shape of each chunk.

```python
import pandas as pd
csv_url = 'https://s3.amazonaws.com/tripdata/201907-citibike-tripdata.csv.zip'
c_size = 1000

# load the big file in smaller chunks
for data_chunk in pd.read_csv(csv_url, chunksize=c_size):
    print(data_chunk.shape)
```

Let's now do some processing on these chunks. We want to calculate the counts of trips started for each station:

```python
results = pd.DataFrame({})
for data_chunk in pd.read_csv(csv_url, chunksize=c_size):
    results = pd.concat(results, data_chunk['start station name'].value_counts)

results = results.groupby(results.index).sum() 
```

Specifying iterator=True will also return the TextFileReader object:

```python
reader = pd.read_csv('tmp.sv', sep='|', iterator=True)

reader.get_chunk(5)
```
