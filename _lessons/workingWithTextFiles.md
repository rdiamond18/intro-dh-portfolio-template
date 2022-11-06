---
layout: page
title: Working With Text Files
description: My third Programming Historian lesson, Working With Text Files
---
## Source
[William J. Turkel and Adam Crymble, "Working with Text Files in Python", Programming Historian (2012), https://doi.org/10.46430/phen0020.](https://programminghistorian.org/en/lessons/working-with-text-files)


## Working With Text Files
### This notebook is my work through the "Working with Text Files" Programming Historian lesson


```python
# hello world
print('hello world')
```

    hello world



```python
#this creates a file in my current directory called 'helloworld.txt' and writes into it

f = open('helloworld.txt','w')
f.write('hello world')
f.close()
```

### reading from a text file


```python
#this opens the file, saves its contents to a message, prints the message and closes it
f = open('helloworld.txt','r')
message = f.read()
print(message)
f.close()
```

    hello world


### Appending to a Pre-Existing Text File


```python
#write to a file by opening it
f = open('helloworld.txt','a')
f.write('\n' + 'I am writing straight into this text file! Isn\'t that cool. I am manipulating this file while I am not in the file! HAHAHAH! I feel like an evil genius.')
f.close()
```


```python
#opening the file to see if it wrote
f = open('helloworld.txt','r')
message = f.read()
print(message)
f.close()
```

    hello world
    I am writing straight into this text file! Isn't that cool. I am manipulating this file while I am not in the file! HAHAHAH! I feel like an evil genius.
    I am writing straight into this text file! Isn't that cool. I am manipulating this file while I am not in the file! HAHAHAH! I feel like an evil genius.



```python
#since I accidentally ran my write command twice, I had to figure out how to undo my error
```


```python
#I found this truncate method online which allows me to cut off all characters after the input parameter
with open("helloworld.txt",'r+') as file:
    file.truncate(164)

f = open('helloworld.txt','r')
message = f.read()
#now, the message should be what I want it to be
print(message)
f.close()
```

    hello world
    I am writing straight into this text file! Isn't that cool. I am manipulating this file while I am not in the file! HAHAHAH! I feel like an evil genius.

