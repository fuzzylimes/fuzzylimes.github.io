---
layout: post
title:  "TIL: Learning Pythong Pandas, Part 2"
date:   2018-06-23 07:05:00 -0000
categories:
  - Coding
tags:
  - python
  - pandas
---
I really needed the rest of this information filled out before I went into work this morning, so here's some corrections to last nights blog post as well as a few more answers to questions I still had (partial repost of yesterday):

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
You can filter down columns by doing conditional evaluations, and even combine them to do more complex queries:
```py
In [40]: filtered_data = df[df[0] > '2018-06-22T23:60:47.965Z']

In [41]: filtered_data
Out[41]:
                          0            1    2       3
2  2018-06-22T23:61:47.965Z  312-456-789  400  15.203
3  2018-06-22T23:62:47.965Z  231-456-789  200  11.203

In [42]: filtered_data = df[(df[0] > '2018-06-22T23:60:47.965Z') & (df[2] != 200)]

In [43]: filtered_data
Out[43]:
                          0            1    2       3
2  2018-06-22T23:61:47.965Z  312-456-789  400  15.203
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

## Handling dates
When importing in the csv, you need to use the `parse_dates` property to set equal to the columns that have dates in them:
```py
In [37]: df = pd.read_csv('t1.csv', sep="\|", engine="python", header=None, parse_dates=[0])
```

## Merge two csv by value in column
Can be done using the merge method. The two tables will then create a new dataframe based on the key that you provided:
```py
In [46]: df = pd.merge(df1, df2, on=[1], how='left', indicator='Exist')

In [47]: df
Out[47]:
                        0_x            1  2_x     3_x                       0_y  2_y     3_y Exist
0  2018-06-22T23:59:47.965Z  123-456-789  200  12.203  2018-06-23T23:59:47.965Z  200  12.303  both
1  2018-06-22T23:60:47.965Z  132-456-789  200  14.203  2018-06-23T23:60:47.965Z  200  14.303  both
2  2018-06-22T23:61:47.965Z  312-456-789  400  15.203  2018-06-23T23:61:47.965Z  400  15.303  both
3  2018-06-22T23:62:47.965Z  231-456-789  200  11.203  2018-06-23T23:62:47.965Z  200  11.303  both
```
If the key can't be found, then a NaN value will appear in the merged version:
```py
In [49]: df = pd.merge(df1, df2, on=[1], how='left', indicator='Exist')
In [56]: df['Exist'] = np.where(df.Exist == 'both', True, False)

In [50]: df
Out[50]:
                        0_x            1  2_x     3_x                       0_y    2_y     3_y      Exist
0  2018-06-22T23:59:47.965Z  123-456-789  200  12.203  2018-06-23T23:59:47.965Z  200.0  12.303       True
1  2018-06-22T23:60:47.965Z  132-456-789  200  14.203  2018-06-23T23:60:47.965Z  200.0  14.303       True
2  2018-06-22T23:61:47.965Z  312-456-789  400  15.203  2018-06-23T23:61:47.965Z  400.0  15.303       True
3  2018-06-22T23:62:47.965Z  231-456-789  200  11.203                       NaN    NaN     NaN  False
```

## Check to see if all values are present
Can either search on the number of `NaN`s that are present in the table, or off of the created `Exists` column that we've overwritten to be `True` or `False` if the record exists:
```py
In [53]: df.isnull().sum().sum()
Out[53]: 3

In [54]: df.isnull().sum()
Out[54]:
0_x      0
1        0
2_x      0
3_x      0
0_y      1
2_y      1
3_y      1
Exist    0
dtype: int64

In [55]: df['0_y'].isnull().sum()
Out[55]: 1

In [58]: df[df['Exist'] == False]
Out[58]:
                        0_x            1  2_x     3_x  0_y  2_y  3_y  Exist
3  2018-06-22T23:62:47.965Z  231-456-789  200  11.203  NaN  NaN  NaN  False
```

11. Generate graphs

💚