---
layout: post
title: Tuple to List
date: 2021-08-03 16:17
category: SDV602
author: Mark Christison
image: assets\images\tuple-to-list.png
tags: [SDV602]
featured: false
hidden: true
---

An assignment was set at the end of the Monday class, which was to take the files that were provided and to:

1. Add a new menu method called "run_menu_two" that is executed when the top-level menu item for Menu Two is selected. That method is to show a new menu using the same tuple format –with different menu items.
2. Change menu_example.py, replace menu_tuple with menu_list. Adjust all existing code to work with menus as lists

The code for this blog is available [here](https://github.com/MCKevmeister/SDV602_week3): https://github.com/MCKevmeister/SDV602_week3 

or available as a [zip](https://github.com/MCKevmeister/SDV602_week3/archive/refs/heads/main.zip): https://github.com/MCKevmeister/SDV602_week3/archive/refs/heads/main.zip

I noted that both python files needed to first be formatted becasue the indention wasn't correct, which was a subtle but cleaver little issue to include in the files and wouldn't have been noticed unless you fully read through the python files correctly. Also, there was a spelling error, again a cleaver little thing to leave in to make sure that everyone read through the files fully.

I have chosen to follow the [PEP 8 style guide](https://pep8.org/). It provides a constant stylising of code that also improves readability and functionality of python code.

As such, there is a necessity to remove the / added to the menus and adding spaces in between functions. The exception "Exception" is too broad as well, and instead the use of "ValueError" is preferred, as it better captures the error that is being captured by the error capturing statement.

### Exercise 1

Exercise 1 then is simply adding a function to the existing code that creates another menu, with "different", "menu" and "items" as different menu items. The code is as follows 

``` python
def run_menu_two():
    menu_two = ("Select a number.", (1, "different", test_cmd), (2, "menu", test_cmd), (3, "items", quit_cmd))
    run_menu(menu_two)
    return True
```

### Exercise 2

Exercise 2 was to replace all menu tuples with lists and to maintain the functionality of the code. 

For this is used find and replace to replace all instances of the string "menu_tuple" with "menu_list" as well as changing the surrounding brackets of the menus to [] or square brackets instead of () or parenthesis, thus converting the menus from tuples to lists. All functionality remains of the old code.

This was the end of the exercise. It was rather simple in comparison to the previous exercise, which I still do not know how to complete.
