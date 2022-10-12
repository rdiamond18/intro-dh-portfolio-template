---
layout: page
title: Exercises Ch. 5
description: Chapter 5 from PythonCrashCourse. 
---


## Conditional Tests


```python
yankees = 'good'
mets = 'bad'
print("Are the yankees good?. I predict true.")
print(yankees == "good")

print("are the mets good? I predict false.")
print(mets == 'good')
```

    Are the yankees good?. I predict true.
    True
    are the mets good? I predict false.
    False


## More conditional tests



```python
baseballTeams = ['yankees', 'mets', 'dodgers', 'cubs', 'redSox']
teams = ['yankees', 'knicks', 'jets', 'dodgers', 'canucks']
for team in teams:
    if team in baseballTeams:
        print("The", team, "are a baseball team")
    else:
        print("The", team, "are not a baseball team")
```

    The yankees are a baseball team
    The knicks are not a baseball team
    The jets are not a baseball team
    The dodgers are a baseball team
    The canucks are not a baseball team


## Stages of Life


```python
age = 1

if age < 2:
    print("you are a baby")
elif 2 <= age < 4:
    print("you are a toddler")
elif 4 <= age < 13:
    print("you are a kid")
elif 13 <= age < 20:
    print("you are a teenager")
elif 20 <= age < 65:
    print("you are an adult")
elif age >= 65:
    print("you are an elder")
```

    you are a baby


## Favorite Fruit


```python
favoriteFruits = ['apple', 'pear', 'mango']

if 'peach' in favoriteFruits:
    print("You must really like peaches!")
else:
    print("I agree, peaches are disgusting!")
    
if 'watermelon' in favoriteFruits:
    print("You must really like watermelons!")
else:
    print("I agree, watermelons are disgusting!")
    
if 'apple' in favoriteFruits:
    print("You must really like apples!")
else:
    print("I agree, apples are disgusting!")

if 'kiwi' in favoriteFruits:
    print("You must really like kiwis!")
else:
    print("I agree, kiwis are disgusting!")
    
if 'pear' in favoriteFruits:
    print("You must really like pears!")
else:
    print("I agree, pears are disgusting!")
    
```

    I agree, peaches are disgusting!
    I agree, watermelons are disgusting!
    You must really like apples!
    I agree, kiwis are disgusting!
    You must really like pears!


## Hello Admin


```python
usernames = ['admin', 'AJudge99', 'coletrain34', 'Torres25', 'NastyNestor']
for user in usernames:
    if user == 'admin':
        print("hello admin, would you like to see a status report?")
    else:
        print("welcome back,", user)
```

    hello admin, would you like to see a status report?
    welcome back, AJudge99
    welcome back, coletrain34
    welcome back, Torres25
    welcome back, NastyNestor


## No Users


```python
usernames = []
if len(usernames) == 0:
    print("We need to find some users!")
    
```

    We need to find some users!


## Checking Usernames


```python
currUsers = ['admin', 'AJudge99', 'coletrain34', 'Torres25', 'NastyNestor']
newUsers = ['AJudge99', 'coletrain34', 'BennyBiceps', 'ClayHolmes', 'JohnnyLasagna', "TORRES25"]

usersLowers = []
usersUppers = []

for x in currUsers:
    usersLowers.append(x.lower())
    usersUppers.append(x.upper())

for z in newUsers:
    if z not in currUsers and z not in usersLowers and z not in usersUppers:
        print("that username is available")
    else:
        print("sorry, the username", z, "is taken")
```

    sorry, the username AJudge99 is taken
    sorry, the username coletrain34 is taken
    that username is available
    that username is available
    that username is available
    sorry, the username TORRES25 is taken

