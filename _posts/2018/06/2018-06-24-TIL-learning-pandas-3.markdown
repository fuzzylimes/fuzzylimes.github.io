---
layout: post
title:  "TIL: Learning Pythong Pandas, Part 3"
date:   2018-06-24 21:35:00 -0000
categories:
  - Coding
tags:
  - python
  - pandas
---
Another long day of work today so I didn't have any time to work on my React lessons or really do much of anything at all... That said I did get my log analyzer written using the pandas info I'd learned over the last few days, and one extra thing I had to do today was writing to a csv file.

Super simple. Once you've got your dataframe created, all you need to do is use the `to_csv()` method:

```py
df.to_csv('csv_file_name.csv', sep='|', encoding='utf-8')
```

And that's all there is to it. That will create a new csv file using the delimiter that you define (leaving out `sep` will just use commas).

💚