---
layout: page
title: String Manipulation
description: My second Programming Historian lesson, Manipulating Strings in Python
---
## Source
[William J. Turkel and Adam Crymble, "Manipulating Strings in Python", Programming Historian (2012), https://doi.org/10.46430/phen0013.](https://programminghistorian.org/en/lessons/manipulating-strings-in-python#lesson-goals)

## Reflection

For my second programming historian lesson, I chose to work through the lesson titled “Manipulating Strings in Python”. I chose this lesson for a couple reasons: First, it seems to align with what we’re doing in class, and I feel it could help me tackle some of the in-class challenges we have worked on. Second, I want to become better at working with text and strings in python. I came into this class with some background in python, but mostly on data analysis and data science topics. I wanted to use this opportunity to broaden my python horizons and learn new skills.
Most of the stuff in the lesson wasn’t new to me, as we had either covered it in class or I had known it before coming into the lesson. However, one part of the lesson that I was able to learn from was the portion about using indices to slice strings. I had known you could do that with datasets, but using it for strings is a cool application of that functionality in python. I feel this skill could be very useful for stripping unnecessary whitespace and clutter when trying to analyze strings in a topic modeling or machine learning problem. I hope to take the techniques I learned in this lesson and use them for my final project and further research down the road.


## Manipulating Strings in Python

### Declaring a string


```python
message = "Hello World"
print(message)
```

    Hello World


### Adding strings


```python
message1 = 'whats' + ' ' + 'up?'
print(message1)
```

    whats up?


### Mulitplying strings


```python
message2a = 'I came to '
message2b = 'dance ' * 4
print(message2a + message2b)
```

    I came to dance dance dance dance 


### Appending to strings


```python
message3 = 'hello'
message3 += ' '
message3 += 'world'
print(message3)
```

    hello world


### String Methods: Finding, Changing


```python
#length method
message4 = 'I attend Tufts University'
print(len(message4))
```

    25



```python
#find method finds the position of the substring
message5 = 'I attend Tufts University'
message5a = message5.find("Tufts")
print(message5a)
```

    9



```python
#find returns -1 if not found
message6 = 'I attend Tufts University'
message6b = message6.find("Northeastern")
print(message6b)
```

    -1



```python
#lowercasing
message7 = "RICHARD"
message7a = message7.lower()
print(message7a)
```

    richard



```python
#replace method
message8 = "I like Cheeseburgers"
message8a = message8.replace("Cheeseburgers", "pizza")
print(message8a)
```

    I like pizza



```python
#slice method creates a substring between the given indices
message9 = 'I attend Tufts University'
message9a = message9[9:15]
print(message9a)
```

    Tufts 



```python
#can also use variables
start = 9
end = 15
message9b = message9[start: end]
print(message9b)
```

    Tufts 



```python
#can also search in a substring
message9 = "Hello World"
#should print -1 because there is no 'd' within the indices (0,5)
print(message9[:5].find("d"))
```

    -1


### Escape Sequences


```python
#Closure sequences

#backslash tells python that the " is part of the string
print('\"')
```

    "



```python
#print a statement with quotation marks
print('The program printed \"hello world\"')
```

    The program printed "hello world"



```python
# \t indicatess tab and \n indicates newline
print('hello\thello\thello\nworld')
```

    hello	hello	hello
    world

