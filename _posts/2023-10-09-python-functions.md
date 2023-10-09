---
layout: post
title:  "Python Functions"
author: Tyler Smith
description: Create baseball functions
image:
--- 
As a data scientist in training, I have found Python to be a great training environment. Python syntax is both readable and simple, allowing me to focus more time on exploring data than attempting to understand complex syntax and struggling through the headaches of debugging my code all the time. A fundamental part of most programming languages is the ability to create functions. In this tutorial, we are going to walk through the importance of creating our own functions, and practice using them with baseball applications.

<h2>What is a function?</h2>

Simply put, Python functions take in data, process data, and returns data.

<h2>Why do we use functions?</h2>

Functions make our lives easier when we code because they help us avoid re-writing the same code over and over again. If there is a process that we are going to re-use in our code, it is wise to create a function. This helps us maintain organization in our code and also saves us time!

<h2>Creating functions</h2>

We use the keyword 'def' to notify Python that we want to create a new function. Here is a look at a basic function template:

```python
def function_name(parameters):
    # Code goes here!
    return result
```

* Parameters: In the parantheses after our function's name, we will input information. The code that follows underneath will define what our function's parameters (input values) do and what our desired outcome with those parameters are.
* * Return: When we add input values into our function, we can output information using 'return'

Let's walk through an example function together:

We are going to start by calculating one of the easiest statistics in baseball: batting average.

\[
\text{Batting Average} = \frac{\text{Hits}}{\text{At-Bats}}
\]

   




