---
layout: post
title:  "TIL: Python Benchmarking"
date:   2018-05-18 17:20:00 -0000
categories: TIL
---
I'll be the first to admit that I've never really cared about performance when writing scripts in the past. My main goal is to accomplsh some piece of work. If it takes 5 seconds longer to do it, but it works, that's totally alright with me. But what about the cases where those extra 5 seconds aren't okay? I finally played around with benchmarking today in pythong.

There's really two ways that I played around with: timing entire portions of my code, and timing individual commands. The first gives me an idea of how long it's taking to get through my actual code. The later gives a better idea of how many cpu cycles are spent trying to do things one way vs doing them another.

## Timing Code Blocks
The way that I went about doing this was pretty simple: grab the time at the start, grab the time at the end, subtract and get your total time. So something simple like this:

```python
from datetime import datetime as DT

startTime = DT.now()

# Do your stuff
print("Function runtime: {}".format(DT.now()-startTime))
```

This would give you the run time for that specific block of code/function call. Super easy. Already knew about this but had never really used it before.

## Timing specific commands
Python has a built in timing tool called timeit that lets you check how long it takes to perform a specific action. This helped greatly in finding what was causing me the most issues with my traffic generator (spoilers: it was using `random`).

To check how long it takes to run a specific item, from the command line you can run somthing like this:

`python -m timeit 'int(1234.2345)'`

This will return output showing the performance report:

`10000000 loops, best of 3: 0.136 usec per loop`

If you need to check somthing using packages, you can use the -s command to use them. So here's an example showing how I was able to fix performance problems with random:

```python
python -m timeit -s 'import random' 'random.randint(1, 10)'
1000000 loops, best of 3: 1.2 usec per loop

python -m timeit -s 'import random' 'round(random.random()*10)'
1000000 loops, best of 3: 0.243 usec per loop
```

With just a simple tweak I'm able to shave off an entire microsecond. Not a lot on its own, but when you're doing thosands of operations per minute for a long durration, it all adds up.

💚