## Python Crash Course - CH6

exercises - 6-1, 6-2, 6-3, 6-4, 6-5, 6-7, 6-8, 6-9, 6-11

## Person


```python
david = {'name': 'david', 'city': 'Westport', 'lastName': 'corro'}
print(david)
```

    {'name': 'david', 'city': 'Westport', 'lastName': 'corro'}


## Favorite Numbers


```python
favNumbers = {'david': 306, 'ray': 1, 'xenops': 1, 'rands': 74, 'regardo': 4}
print(favNumbers)
```

    {'david': 306, 'ray': 1, 'xenops': 1, 'rands': 74, 'regardo': 4}


## Glossary


```python
glossary = {'variable': 'an object that can change', 'compiler': 'a software service that executes code'
            , 'text editor': 'a software service in which you write code',
            'stack': 'a data structure which only allows operations from the front',
            'python': 'a programming language'}

for term in glossary:
    print(term, ":",glossary[term])
    print('\n')
```

    variable : an object that can change
    
    
    compiler : a software service that executes code
    
    
    text editor : a software service in which you write code
    
    
    stack : a data structure which only allows operations from the front
    
    
    python : a programming language
    
    


## Glossary 2: Tokyo Drift


```python
glossary['len'] =  'a function that returns the length of an object'
glossary['type'] =  'a function that returns the type of an object'
glossary['string'] = 'a variable type which represents words as arrays of characters'
glossary['char'] = 'a variable type which represents a single character'
glossary['int'] = 'a variable type which represents an integer'

for term in glossary:
    print(term, ":",glossary[term])
    print('\n')
```

    variable : an object that can change
    
    
    compiler : a software service that executes code
    
    
    text editor : a software service in which you write code
    
    
    stack : a data structure which only allows operations from the front
    
    
    python : a programming language
    
    
    len : a function that returns the length of an object
    
    
    type : a function that returns the type of an object
    
    
    string : a variable type which represents words as arrays of characters
    
    
    char : a variable type which represents a single character
    
    
    int : a variable type which represents an integer
    
    


## Rivers


```python
rivers = {'yellow': 'china', 'tigris': 'iraq', 'nile': 'egypt'}

for river in rivers:
    print("the", river, 'river runs through', rivers[river])

for eachRiver in rivers:
    print(eachRiver)

for country in rivers:
    print(rivers[country])
```

    the yellow river runs through china
    the tigris river runs through iraq
    the nile river runs through egypt
    yellow
    tigris
    nile
    china
    iraq
    egypt


## People2


```python
xenops = {'name': 'xenops', 'city': 'england', 'lastName': 'NULL'}
jobe = {'name': 'sam', 'city': 'newCaanan', 'lastName': 'jobe'}

people = []
people.append(david)
people.append(xenops)
people.append(jobe)

for person in people:
    print(person)
```

    {'name': 'david', 'city': 'Westport', 'lastName': 'corro'}
    {'name': 'xenops', 'city': 'england', 'lastName': 'NULL'}
    {'name': 'sam', 'city': 'newCaanan', 'lastName': 'jobe'}


## Pets


```python
xenopsjr = {'name': 'xenops junior', 'owner': 'xenops', 'type': 'lizard'}
sydney = {'name': 'sydney', 'owner': 'david', 'type': 'dog'}
thatDawgInMe = {'name': 'dawg', 'owner': 'Richard', 'animal': 'dog'}

pets = []
pets.append(xenopsjr)
pets.append(sydney)
pets.append(thatDawgInMe)

for pet in pets:
    print(pet)

```

    {'name': 'xenops junior', 'owner': 'xenops', 'type': 'lizard'}
    {'name': 'sydney', 'owner': 'david', 'type': 'dog'}
    {'name': 'dawg', 'owner': 'Richard', 'animal': 'dog'}


## Favorite Places


```python
david = {'name': 'david', 'place': 'Upper Saddle River'}
rands = {'name': 'Simon', 'place': 'Woodstock'}
rich = {'name': 'rich', 'place': 'DC'}

favoritePlaces = []
favoritePlaces.append(david)
favoritePlaces.append(rands)
favoritePlaces.append(rich)

for place in favoritePlaces:
    print(place)
```

    {'name': 'david', 'place': 'Upper Saddle River'}
    {'name': 'Simon', 'place': 'Woodstock'}
    {'name': 'rich', 'place': 'DC'}


## Cities


```python
newYork = {'name': 'newYork', 'country': 'USA', 'population': 8380000, 'fact': 'The First Pizzeria in the USA Opened in New York City.'}
sanFran = {'name': 'sanFrancisco', 'country': 'USA', 'population': 874784, 'fact': 'San Francisco has North Americas oldest Chinatown'}
Dallas = {'name': 'Dallas', 'country': 'USA', 'population': 1339000, 'fact': 'The frozen margarita machine was invented in Dallas.'}

cities = []
cities.append(newYork)
cities.append(sanFran)
cities.append(Dallas)

for city in cities:
    print('city is', city['name'])
    print(city['name'], 'is in', city['country'])
    print(city['name'], 'has an approximate population of', city['population']) 
    print('a fun fact about', city['name'], 'is', city['fact']) 

          
          
          
          
```

    city is newYork
    newYork is in USA
    newYork has an approximate population of 8380000
    a fun fact about newYork is The First Pizzeria in the USA Opened in New York City.
    city is sanFrancisco
    sanFrancisco is in USA
    sanFrancisco has an approximate population of 874784
    a fun fact about sanFrancisco is San Francisco has North Americas oldest Chinatown
    city is Dallas
    Dallas is in USA
    Dallas has an approximate population of 1339000
    a fun fact about Dallas is The frozen margarita machine was invented in Dallas.

