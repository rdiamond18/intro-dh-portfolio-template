---
layout: page
title: PythonCrashCourse - Chapter2
description: Chapter 2 of Pyhton Crash Course
---


# Python Crash Course - Chapter 2
## Richard Diamond 
### Sep 22, 2022

## Q1 - Simple Message


```python
message = "Hi, my name is Richard"
print(message)
```

    Hi, my name is Richard


## Q2 - Simple Messages


```python
message = "Hi, my name is Richard"
print(message)
message = "Whats up?"
print(message)
```

    Hi, my name is Richard
    Whats up?


## Q3 - Personal Message


```python
name = "Sophie"
print("Hello", name, " - how is your homework going?")
```

    Hello Sophie  - how is your homework going?


## Q4 - Name Cases


```python
name = "Adam Levine"
print(name.lower())
print(name.upper())
print(name.title())
```

    adam levine
    ADAM LEVINE
    Adam Levine


## Q5 - Famous Quote


```python
quote = "Forrest Gump once said, 'Life is like a box of chocolates, you never know what you're gonna get.''"
print(quote)
```

    Forrest Gump once said, 'Life is like a box of chocolates, you never know what you're gonna get.''


## Q6 - Famous Quote 2


```python
famous_person = "Forrest Gump"
print(famous_person, "once said 'Life is like a box of chocolates, you never know what you're gonna get.'")
```

    Forrest Gump once said 'Life is like a box of chocolates, you never know what you're gonna get.'


## Q7 - Stripping Names


```python
name = "\tAaron Judge"
print(name)
print(name.lstrip())
print(name.rstrip())
print(name.strip())

name = "\nGleyber Torres"
print(name)
print(name.lstrip())
print(name.rstrip())
print(name.strip())
```

    	Aaron Judge
    Aaron Judge
    	Aaron Judge
    Aaron Judge
    
    Gleyber Torres
    Gleyber Torres
    
    Gleyber Torres
    Gleyber Torres


## Q10 - Adding Comments


```python
famous_person = "Forrest Gump" #Declaring name as Forrest Gump
print(famous_person, "once said 'Life is like a box of chocolates, you never know what you're gonna get.'")

message = "Hi, my name is Richard" #declaring initial message
print(message)
message = "Whats up?" #Changing message to "whats up"
print(message)

```

    Forrest Gump once said 'Life is like a box of chocolates, you never know what you're gonna get.'
    Hi, my name is Richard
    Whats up?

