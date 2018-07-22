---
layout: post
title:  "TIL: Learning Python Pandas"
date:   2018-06-22 20:25:00 -0000
categories:
  - Coding
tags:
  - python
  - pandas
---
Having to learn how to process data for work, so started working with pandas tonight. I'd used it in an online course a while back, but honestly I've forgotten everything about it. So I started tonight by taking note of everything that I needed to be able to do and looking into how to do it. Here's what I learned from my searching.

# Things that I need to be able to do

## Import from csv into memory
To create a dataframe from a csv, you can use the following:
```py
df = pd.read_csv('pandas_dataframe_importing_csv/example.csv')
```
If you have a different delimiter than a comma, you can use the `sep` parameter:
```py
df = pd.read_csv('pandas_dataframe_importing_csv/example.csv', sep="\|", engine="python")
```
Notice the escape character before the delimiter character.

With no headers, you need to add the following:
```py
df = pd.read_csv('pandas_dataframe_importing_csv/example.csv', sep="\|", engine="python", header=None)
```
That will give you something like the following:
```
                          0            1    2       3
0  2018-06-22T23:59:47.965Z  123-456-789  200  12.203
1  2018-06-22T23:60:47.965Z  132-456-789  200  14.203
2  2018-06-22T23:61:47.965Z  312-456-789  400  15.203
3  2018-06-22T23:62:47.965Z  231-456-789  200  11.203
```

## Calculate the min for a column
Assuming that you know the column you want to take the min of, you'll use the column number as an index to the dataframe. For example, just using the index gives you all the column values:
```py
In [13]: df[3]
Out[13]:
0    12.203
1    14.203
2    15.203
3    11.203
Name: 3, dtype: float64
```
You can then take the `df[i]` format and tag it with the `.min()` method to give you the min value:
```py
In [11]: df[3].min()
Out[11]: 11.203
```

## Calculate the max for a column
Same as with the `.min()`, only we're switching out for the `.max()` method:
```py
In [12]: df[3].max()
Out[12]: 15.203
```

## Calculate the average for a column
Second grade fun fact: mean = average. Evidently I lost that knowladge over the years.

Same as min and max:
```py
In [19]: df[3].mean()
Out[19]: 13.203
```

## Fun side note... use `describe()`
You can use the `describe()` method a dataframe to get a whole bunch of info on all of your numeric columns super quickly. See the following:
```py
In [18]: df.describe()
Out[18]:
           2          3
count    4.0   4.000000
mean   250.0  13.203000
std    100.0   1.825742
min    200.0  11.203000
25%    200.0  11.953000
50%    200.0  13.203000
75%    250.0  14.453000
max    400.0  15.203000
```

## Calculate the 95th percentile of a column
You can calculate percentiles by using the `quantile()` method. This takes in some fractional value and returns that percentile. For example, to get the 95th, you'd use `.95`:
```py
In [28]: df[3].quantile(.95)
Out[28]: 15.052999999999999
```

## Calculate the 99th percentile of a column
Same as the previous, only using `.99`:
```py
In [26]: df[3].quantile(.99)
Out[26]: 15.173
```

## Filter by column value
Already explained above, but all you need to do is index on the dataframe with either the column header name or the index number:
```py
In [29]: df[3]
Out[29]:
0    12.203
1    14.203
2    15.203
3    11.203
Name: 3, dtype: float64
```

## Turn a column into a list
Surprise, there's another built in method to handle this too. Using the `tolist()` method, you can turn a specific column into a list:
```py
In [30]: df[3].tolist()
Out[30]: [12.203, 14.203, 15.203, 11.203]
```

## Compare csv lengths (whatever that term is in pandas)
Another method, `count()`, is your friend:
```py
In [32]: df[3].count()
Out[32]: 4
```
However, this is potentially dangerous as it will only count rows where non NaN values are present. In that case, you can use `shape[0]`:
```py
n [36]: df.shape[0]
Out[36]: 4
```

# Still ToDo
10. Merge two csv by value in column
11. Generate graphs
💚