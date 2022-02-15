---
layout: post
title: PySimpleGUI - creating a simple game
date: 2021-08-15 12:36
category: SDV602
author: Mark Christison
image: assets\images\PySimpleGUI.png
tags: [SDV602]
featured: false
hidden: true
---

This week I have created a simple console game, that is recursive in nature but not exactly. Code is here.

With that 'game' built, we were tasked with creating a GUI for the game using PySimpleGUI, which is a GUI interface creator for python applications.

## PySimpleGUI

PySimpleGUI is a python package which supports the creation of GUIs written in Python. A GUI is specified by using a layout of elements. PySimpleGUI can the. The windows are presented in layouts which are defined in lists. Elements can be styled and positioned similar to any box model. Each element has several properties, most important of which is the key element, which allows the element to be targeted by other parts of the code.

After a window is on the screen the user can then interact with the different elements. By interacting with an element, an event can be triggered. The event can then be handled by the event loop.

For my game, the port was easy enough. However, I have a bug where when I try to reload/restart the game to keep it perpetual is in the console version, I am unable to. I don't know what exactly the bug is.

The [docs](https://github.com/PySimpleGUI/) have quite a few errors. I assume whoever wrote this does not speak English as a first language. I spent 2 hours reading through them, fixing the formatting and spelling errors (close to 1000). I opened a pull request with the formatted document [here](https://github.com/PySimpleGUI/PySimpleGUI/pull/4628).

The recipes provided in the docs put together could make an app that would be valid for the final project.
