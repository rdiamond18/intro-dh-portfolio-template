---
layout: page
title: Exercises Ch. 8
description: Chapter 8 from PythonCrashCourse. 
---


# Functions
### 8-1, 8-2, 8-3, 8-5, 8-6, 8-7 

## 8-1. Message


```python
def displayMessage():
    print("I am learning about functions in this chapter.")

displayMessage()
```

    I am learning about functions in this chapter.


## 8-2. Favorite Book


```python
def favoriteBook(title):
    print(f"One of my favorite books is {title}.")
    
favoriteBook("The Mazerunner")
```

    One of my favorite books is The Mazerunner.


## 8-3. T-Shirt


```python
def makeShirt(size, text):
    print(f"This shirt is of size {size} and says {text} on it.")
    
makeShirt('large', 'Go Yankees!')
```

    This shirt is of size large and says Go Yankees! on it.


## 8-5. Cities


```python
def describeCity(cityName, country = 'USA'):
    print(f"{cityName} is in {country}.")
    
describeCity('San Francisco')
describeCity('Austin')
describeCity('Rome', 'Italy')
```

    San Francisco is in USA.
    Austin is in USA.
    Rome is in Italy.


## 8-6. City Names:


```python
def cityCountry(cityName, country):
    return f"{cityName}, {country}"

print(cityCountry('Dallas', 'USA'))
print(cityCountry('Madrid', 'Spain'))
print(cityCountry('Beijing', 'China'))
```

    Dallas, USA
    Madrid, Spain
    Beijing, China


## 8-7. Album:


```python
def makeAlbum(artistName, albumTitle, numSongs = None):
    album = dict()
    album['artist'] = artistName
    album['album title'] = albumTitle
    if numSongs:
        album['number of songs'] = numSongs
    
    return album

print(makeAlbum('Kid Cudi', 'Man on the Moon'))
print(makeAlbum('J Cole', '2014 Forest Hills Drive'))
print(makeAlbum('Mac Miller', 'KIDS', 12))

```

    {'artist': 'Kid Cudi', 'album title': 'Man on the Moon'}
    {'artist': 'J Cole', 'album title': '2014 Forest Hills Drive'}
    {'artist': 'Mac Miller', 'album title': 'KIDS', 'number of songs': 12}

