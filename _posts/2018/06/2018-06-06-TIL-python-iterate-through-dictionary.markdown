---
layout: post
title:  "TIL: Iterating Through Python Dictionary"
date:   2018-06-06 20:40:00 -0000
categories:
  - Coding
tags:
  - python
---
Somehow I've been working with python for 2 years now and never knew this was a thing. Wow.

So usually when I used to loop through dictionaries, I'd just do something simple like....

```python
a = {
  "a": 123,
  "b": 456,
  "c": 789
}

for i in a:
  print(i, a[i])
```

But it always required that extra step when trying to reference to the value in the key-value-pair. So much to my surprise (although I guess it really shouldn't have been...), there's a much cleaner way to do this same thing using the `.items()` dictionary method:

```python
a = {
  "a": 123,
  "b": 456,
  "c": 789
}

for i,j in a.items():
  print(i, j)
```

This gives full access to both the key and value by variabe name, rather than having to chain the key to the dictionary to get the value.

💚