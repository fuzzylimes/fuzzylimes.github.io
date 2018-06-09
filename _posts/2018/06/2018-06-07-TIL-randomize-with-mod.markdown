---
layout: post
title:  "TIL: Randomizing with %"
date:   2018-06-07 21:15:00 -0000
categories: TIL
---
So I've been working on a traffic simulator project at work, and one of the things that I try to do is generate unique, sensible data for each of the posts that I send. Try to, you know, actually simulate what's going to be going through the system. In the past I'd often relied on just using the `random.random()` function to generate a base number, then multiply it by the max value I'd want, then finally round it up to where I'd want it to be. But that's a lot of overhead if I just want to, say, randomize the selection of an item from an array.

So, I came up with the following alternative:

```python
import datetime

now = datetime.datetime.now().minute
val = ["apple", "banana", "pear"][now%3]
print(val)
```
Now, if you're sending a lot of messages in a row, this probably doesn't make much since. But for me, since I'm only sending one message per minute, this allows me to cycle through the list every time that the script kicks off.

On its own, with only one item in it, there's really not much performance gain in doing things this way rather than the other. However, if you've got multiple arrays you need to select values from, this starts to pull ahead. Check out some quick numbers.

The process of loading in `datetime`, getting the minute, and getting a single value is actually pretty long:

```
python3 -m timeit -s 'import datetime' "['apple','banana','pear'][datetime.datetime.now().minute%3]"
1000000 loops, best of 3: 1.11 usec per loop
```

However, most of this time came from the actual calculation of the current minute:

```
python3 -m timeit -s 'import datetime' "datetime.datetime.now().minute"
1000000 loops, best of 3: 0.999 usec per loop
```

If the minute is already calculated, the `mod` look up is super quick:

```
python3 -m timeit "['apple','banana','pear'][56%3]"
10000000 loops, best of 3: 0.0861 usec per loop
```

Compare this process to using `random.random()` instead. Even if you pre-calculate out the random value ahead of time, like done with the time before, the `round()` method ends up dragging it out:

```
python3 -m timeit -s 'import random' "['apple','banana','pear'][round(.456*2)]"
1000000 loops, best of 3: 0.358 usec per loop
```

By that math, assuming that you have 4 or more arrays you need to pull from, the mod method seems to pull a head a little bit.

Even if it's not that practical, it's still neat to look at things a different way.

💚