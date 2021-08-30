---
layout: post
title: Iterable Unpacking
date: 2021-08-31 21:40
category: SDV602
author: Mark Christison
image: assets\images\boxes.jpg
tags: [SDV602]
featured: true
hidden: false
---

In one of the lines of code that the class was shown this week, we were asked why "fig" was in it.

```python
fig, ax = plt.subplots()  # Challenge - Why "fig" here
```

The code was for drawing a plot using matplotlib. Upon a simple search I found the documentation is [here](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.subplots.html). From reading these docs, the function call plt.subplots() is used for initializing a figure and subplot axes.

The function returns 2 objects:

1. A Figure or 'fig'
2. An array of Axes or 'ax'

The function uses a feature of python called [iterable unpacking](https://www.python.org/dev/peps/pep-3132/), which uses the assignment operator but somewhat reversed such that the variables assigned are on the left of the operator rather than the right as is typical. 

```python
a, *b, c = range(5)
print(a)  # 0
print(b)  # [1, 2, 3]
print(c)  # 4
```

To me, this syntax and functionality is similar to that of a [destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment), or the [spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) of JavaScript. Upon looking at the C# documentation, it seems that similar but not quite the same functionality is also in that for [Deconstructing tuples](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/functional/deconstruct).

