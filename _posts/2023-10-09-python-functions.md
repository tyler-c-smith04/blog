---
layout: post
title:  "Python Functions"
author: Tyler Smith
description: "Create batting average function"
image:
--- 
As a data scientist in training, I have found Python to be a great training environment. Python syntax is both readable and simple, allowing me to focus more time on exploring data than attempting to understand complex syntax and struggling through the headaches of debugging my code all the time. A fundamental part of most programming languages is the ability to create functions. In this tutorial, we are going to walk through the importance of creating our own functions, and practice using them with baseball applications.

<h2>What is a function?</h2>

Simply put, Python functions take in data, process data, and returns data.

<h2>Why do we use functions?</h2>

Functions make our lives easier when we code because they help us avoid re-writing the same code over and over again. If there is a process that we are going to re-use in our code, it is wise to create a function. This helps us maintain organization in our code and also saves us time!

<h2>Creating functions</h2>

We use the keyword 'def' to notify Python that we want to create a new function. After 'def', the function name, and the parameters, make sure to add a colon because the colon tells Python that we are going to add code that will process the data that we are adding in our parameters. Here is a look at a basic function template:

```python
def function_name(parameters):
    # Code goes here!
    return result
```

* Parameters: In the parantheses after our function's name, we will input information. The code that follows underneath will define what our function's parameters (input values) do and what our desired outcome with those parameters are.
* Return: When we add input values into our function, we can output information using 'return'

Let's walk through an example function together:

We are going to start by calculating one of the easiest statistics in baseball: batting average.

Batting average is calculated by dividing Hits by At-Bats. Here is how we can create this function in Python:

```python
def batting_average(hits, at_bats): # This function needs the user to add 2 parameters: hits and at_bats
    return hits / at_bats # Returns a decimal between 0 and 1

# Example
hits = 50
at_bats = 200
average = batting_average(hits, at_bats)
print(average) # Will output 0.250
```

Congratulations, you now know how to create a function to calculate batting average! However, can you think of any input values that could cause our function to not give us our desired result? Becoming data science masters requires us to keep our math skills sharp. Any value divided by zero is undefined and Python will give us an error that looks like this:
(Insert Error Screenshot)

The above error is what we will see if our at_bats parameter is equal to 0. If a player has 0 at bats in a season, we want our function to output a batting average of 0 instead of an error. Luckily, we can add to our previous function and make sure we get this desired result!

```python
def batting_avg(hits, at_bats):
  if at_bats == 0: # if statement evaluates whether or not our at_bats input value is 0
    return 0 # if at_bats is 0, our function will now return 0
  return hits / at_bats # if at_bats is not equal to 0, the function will calculate the decimal of hits / at_bats

# Example
hits = 0
at_bats = 0
average = batting_avg(hits, at_bats)
print(average) # Will output 0
```

If statements can get tricky, but hopefully the if statement in the above code is easy to follow! Just like how we need to add a colon after we define a function at the beggining, we also need to add a colon to our if statement.

Thanks for reading!



