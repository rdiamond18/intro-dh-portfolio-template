---
layout: page
title: Exercises Ch. 3-4
description: Chapters 3 and 4 from PythonCrashCourse. 
---


## Names


```python
names = ['mond', 'barbar', 'dav', 'regardo', 'randz']
for friend in names:
    print(friend)
```

## Greetings


```python
for friend in names:
    print('Hey', friend, 'can you help me with my homework?')
```

## My own list


```python
cars = ['honda', 'toyota', 'jeep', 'ford']
for brand in cars:
    print("I have a friend that drives a", brand)
```

## Guest List


```python
people = ['Hank Aaron', 'Vin Scully', 'Jackie Robinson']

for person in people:
    print("Hello", person, "- you are formally invited to dinner in Lewis Hall tonight.")
```

## Changing Guest List


```python
people = ['Hank Aaron', 'Vin Scully', 'Jackie Robinson']
print(people[2], "can't make the dinner")
people[2] = 'Ted Williams'

for person in people:
    print("Hello", person, "- you are formally invited to dinner in Lewis Hall tonight.")
```

    Jackie Robinson can't make the dinner
    Hello Hank Aaron - you are formally invited to dinner in Lewis Hall tonight.
    Hello Vin Scully - you are formally invited to dinner in Lewis Hall tonight.
    Hello Ted Williams - you are formally invited to dinner in Lewis Hall tonight.



```python
people = ['Hank Aaron', 'Vin Scully', 'Ted Williams']
print("there is more space at the dinner table!")
people.insert(0, 'Joe Morgan')
people.insert(2, 'Lou Gehrig')
people.append('Aaron Judge')

for person in people:
    print("Hello", person, "- you are formally invited to dinner in Lewis Hall tonight.")
```

    there is more space at the dinner table!
    Hello Joe Morgan - you are formally invited to dinner in Lewis Hall tonight.
    Hello Hank Aaron - you are formally invited to dinner in Lewis Hall tonight.
    Hello Lou Gehrig - you are formally invited to dinner in Lewis Hall tonight.
    Hello Vin Scully - you are formally invited to dinner in Lewis Hall tonight.
    Hello Ted Williams - you are formally invited to dinner in Lewis Hall tonight.
    Hello Aaron Judge - you are formally invited to dinner in Lewis Hall tonight.


## Shrinking Guest List


```python
print("sorry, I just found out we only have 2 spots for dinner")
print(people)
while len(people) > 2:
    toPop = people[len(people) - 1]
    print("sorry", toPop, "we don't have space for you at dinner tonight")
    people.pop()
for stillHere in people:
    print("hey", stillHere, ", you are still invited to dinner")
del people[1]
del people[0]
print(people)
```

    sorry, I just found out we only have 2 spots for dinner
    ['Joe Morgan', 'Hank Aaron', 'Lou Gehrig', 'Vin Scully', 'Ted Williams', 'Aaron Judge']
    sorry Aaron Judge we don't have space for you at dinner tonight
    sorry Ted Williams we don't have space for you at dinner tonight
    sorry Vin Scully we don't have space for you at dinner tonight
    sorry Lou Gehrig we don't have space for you at dinner tonight
    hey Joe Morgan , you are still invited to dinner
    hey Hank Aaron , you are still invited to dinner
    []


## Seeing the world


```python
places = ['Florence', 'Milan', 'LA', 'SanDiego', 'SanFrancisco']
print(places)
print(sorted(places))
print(places)
print(sorted(places, reverse = True))
print(places)
places.reverse()
print(places)
places.reverse()
print(places)

places.sort()
print(places)

places.sort(reverse = True)
print(places)
```

    ['Florence', 'Milan', 'LA', 'SanDiego', 'SanFrancisco']
    ['Florence', 'LA', 'Milan', 'SanDiego', 'SanFrancisco']
    ['Florence', 'Milan', 'LA', 'SanDiego', 'SanFrancisco']
    ['SanFrancisco', 'SanDiego', 'Milan', 'LA', 'Florence']
    ['Florence', 'Milan', 'LA', 'SanDiego', 'SanFrancisco']
    ['SanFrancisco', 'SanDiego', 'LA', 'Milan', 'Florence']
    ['Florence', 'Milan', 'LA', 'SanDiego', 'SanFrancisco']
    ['Florence', 'LA', 'Milan', 'SanDiego', 'SanFrancisco']
    ['SanFrancisco', 'SanDiego', 'Milan', 'LA', 'Florence']


## Pizzas


```python
pizzas = ['pepperoni', 'white', 'plain']

for t in pizzas:
    print(t)

for x in pizzas:
    print(x, "is a kind of pizza I enjoy")   

print("I like pizza!")    
```

    pepperoni
    white
    plain
    pepperoni is a kind of pizza I enjoy
    white is a kind of pizza I enjoy
    plain is a kind of pizza I enjoy
    I like pizza!


## Animals


```python
animals = ['dog', 'cat', 'platypus']
for animal in animals:
    print(animal)

for x in animals:
    print('a', x, 'has 4 legs')
    
print("all these animals have 4 legs")
```

    dog
    cat
    platypus
    a dog has 4 legs
    a cat has 4 legs
    a platypus has 4 legs
    all these animals have 4 legs


## Counting to Twenty


```python
for i in range(0,21):
    print(i)
```

    0
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20


## Odd Nums


```python
for i in range(1,21,2):
    print(i)
```

    1
    3
    5
    7
    9
    11
    13
    15
    17
    19


## Slices


```python
animals = ['dog', 'cat', 'platypus', 'giraffe', 'penguin', 'frog', 'cow']

print("The first three items in this list are: ", animals[0:3])
print("The middle three items in the list are: ", animals[2:5])
print("The last three items in the list are: ", animals[4:])


    

```

    The first three items in this list are:  ['dog', 'cat', 'platypus']
    The middle three items in the list are:  ['platypus', 'giraffe', 'penguin']
    The last three items in the list are:  ['penguin', 'frog', 'cow']


## My pizzas, Your pizzas


```python
pizzas = ['pepperoni', 'white', 'plain']
friend_pizzas = []

friend_pizzas = pizzas[:]

pizzas.append('anchovy')
friend_pizzas.append('sausage')

print('my favorite pizzas are: ')
for i in pizzas:
    print(i)
    
print('my friends favorite pizzas are: ')
for z in friend_pizzas:
    print(z)
```

    my favorite pizzas are: 
    pepperoni
    white
    plain
    anchovy
    my friends favorite pizzas are: 
    pepperoni
    white
    plain
    sausage


