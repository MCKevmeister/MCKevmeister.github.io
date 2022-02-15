---
layout: post
title: \*args and \**kwargs
date: 2021-08-30 21:40
category: SDV602
author: Mark Christison
image: assets\images\args-kwargs.jpg
tags: [SDV602]
featured: false
hidden: true
---

## *args

Python *args parameter allows the function to accept multiple arguments. The * symbol before args keyword is called an "unpacking operator". This tells the interpreter that there will be a variable number of arguments provided. These args are passed to the function as a tuple.

```python
def add(*args):
    for number in args:
        result = + number
    return result


def get_type(*args):
    print(type(args))


if __name__ == "__main__":
    total = add(1, 2, 3, 4)
    print(total)  # 10
    get_type("first argument", 1, 7)  # <class 'tuple'>
```

## **kwargs

\** kwargs is another special type of argument that can be passed to a function.\**kwargs also accepts an unknown amount of arguments as *args does. It passes the parameters to a function as a dictionary, and can also be accessed as such.

```python
def someFunction(*args, **kwargs):
    print(args)
    print(kwargs)
    print(kwargs['second_arg'])
    print(type(kwargs))


if __name__ == "__main__":
    someFunction("hello", "world", first_arg="first", second_arg="second")
    # ('hello', 'world')
    # {'first_arg': 'first', 'second_arg' = 'second'}
    # second
    # <class 'dictionary'>

```

As can be seen in the previous example, both \*args and \**args can be passed to a function together.

For the project that I am working on, I think that this will be useful in several ways.

- I will be able to pass several parameters to a function and the output will be more dynamic
- As the data will be coming from CSV's to be graphed, this data should be able to be directly passed to the functions that will do the graphing, and will be able to include headings of columns or rows.

----

Overall, I feel more comfortable now with *args and **kwargs, which at the beginning of the day seemed really confusing at first glance in comparison to parameters of functions in JavaScript or c#. I can see how the use of dynamic inputs to functions and being able to group those inputs in different ways would be useful, without having to state it explicitly in the function calls.