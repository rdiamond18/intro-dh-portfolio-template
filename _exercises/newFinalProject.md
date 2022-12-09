## NLCS Analysis


```python
#get game ID of NLCS games
IDList = [401467584, 401467585, 401467586, 401467587, 401467588]
```


```python
#import packages
from bs4.element import NavigableString 
from bs4 import BeautifulSoup
import collections
import requests
import pandas as pd
```


```python
gameTextList = list()

#iterate through list of game IDs and scrape text
for gameID in IDList:
    response = requests.get('https://www.espn.com/mlb/recap/_/gameId/' + str(gameID))
    response_text = response.text

    soup = BeautifulSoup(response_text) 
    
    gameText = ''
    
    #add text from each game into a list
    for p in soup.find_all('p'):
        gameText += f'{p.text.strip()}'
    gameTextList.append(gameText)    
```


```python
#add list elements to df
df = pd.DataFrame(gameTextList)
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>SAN DIEGO -- — Bryce Harper hit another postse...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SAN DIEGO -- — The scrappy San Diego Padres, l...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>PHILADELPHIA -- — Jean Segura muffed a soft re...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>PHILADELPHIA -- — Bryce Harper stood on second...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>PHILADELPHIA -- — Bryce Harper broke up the Ph...</td>
    </tr>
  </tbody>
</table>
</div>



## Extracting names
I wanted to find how many times each name was mentioned, and then compare it to Championship Win Probability Added (CWPA). CWPA is a stat that estimates how much closer a single player brought his team to winning the World Series, so I felt this was an accurate stat to estimate someone's value within a singular series.


```python
from nltk import ne_chunk, pos_tag, word_tokenize
from nltk.tree import Tree

names = []
#strip all names from the list
for i in range(0,4):
    nltk_results = ne_chunk(pos_tag(word_tokenize(df.iloc[i,0])))
    for nltk_result in nltk_results:
        if type(nltk_result) == Tree:
            name = ''
            for nltk_result_leaf in nltk_result.leaves():
                name += nltk_result_leaf[0] + ' '
            if (nltk_result.label() == "PERSON"):
                names.append(name)
```


```python
#now that we have a list of names, lets make it a dict with the number of counts
from collections import Counter
nameDict = Counter(names)
nameDict = dict(nameDict)

#This is really strange. Since "Nola" could be referring to either Aaron or Austin Nola, two brothers who played for
#opposing teams, I just decided to drop "Nola" without being prefaced by Austin or Aaron.
del nameDict['Nola ']
print(nameDict)
```

    {'Bryce Harper ': 4, 'Kyle Schwarber ': 3, 'Schwarber ': 5, 'Wheeler ': 4, 'Yu Darvish ': 1, 'Aaron Nola ': 6, 'Blake Snell ': 2, 'Austin ': 2, 'Darvish ': 3, 'Harper ': 14, 'Rob Thomson ': 4, 'Statcast ': 1, 'Austin Nola ': 6, 'Padres ': 4, 'Wil Myers ': 1, 'José ': 1, 'Juan Soto ': 5, 'Alec Bohm ': 3, 'Manny Machado ': 3, 'Alvarado ': 1, 'Josh Bell ': 3, 'Gary Matthews ': 1, 'Atlanta Braves ': 1, 'Hoskins ': 5, 'Realmuto ': 5, 'Petco Park ': 1, 'Myers ': 1, 'Bob Melvin ': 4, 'Dominguez ': 1, 'Astros ': 1, 'Joe Musgrove ': 3, 'Padres LHP Blake Snell ': 1, 'San Diego Padres ': 1, 'Drury ': 7, 'San Diego ': 3, 'Atlanta ': 1, 'Snell ': 2, 'Josh Hader ': 1, 'Diego ': 1, 'Kim Ha-seong ': 1, 'Kim ': 3, 'Jurickson Profar ': 2, 'Soto ': 2, 'Machado ': 2, 'Brad ': 1, 'Bell ': 1, 'Nick Castellanos ': 3, 'Jean Segura ': 2, 'Matt Vierling ': 1, 'Sosa ': 1, 'Philly ': 3, 'Rhys Hoskins ': 2, 'Robert Suarez ': 1, 'Segura ': 6, 'Ranger Suarez ': 1, 'Zach Eflin ': 1, 'Jose Alvarado ': 1, 'Seranthony Dominguez ': 1, 'Profar ': 1, 'Todd Tichenor ': 1, 'Ted Barrett. ': 1, 'Bohm ': 1, 'Musgrove ': 3, 'Alas ': 1, 'Bryson Stott ': 1, 'Wild Card Series ': 1, 'Suarez ': 3, 'Grisham ': 2, 'Charlie Manuel ': 1, 'Ryan Howard ': 1, 'Matt Stairs ': 1, 'Tug McGraw ': 1, 'Zack Wheeler ': 1, 'Phillies ': 2, 'Bailey Falter ': 1, 'Brandon Drury ': 1, 'Falter ': 2, 'Reliever Connor Brogdon ': 1, 'Clevinger ': 2, 'Castellanos ': 1, 'Nick Martinez ': 1, 'Martinez ': 1, 'Stott ': 1, 'Padres RHP Yu Darvish ': 1}



```python
#Since this nameList included first and last names, I did some dict manipulation to make it just last names
lastNames = dict()

#create a new dict that contains just last names
for key in nameDict:
    splitKey = key.split()
    if splitKey[-1] in lastNames.values():
        lastNames[splitKey] += nameDict[key]
    else:
        lastNames[splitKey[-1]] = nameDict[key]

#convert dict to df
mentionsDF = pd.DataFrame.from_dict(lastNames.items())

#change column names
cols = ['name', 'mentions']
mentionsDF.columns = cols

#sort by mentions
mentionsDF = mentionsDF.sort_values(by=['mentions'], ascending = False)

#show df
mentionsDF.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>mentions</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Harper</td>
      <td>14</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nola</td>
      <td>6</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Segura</td>
      <td>6</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Realmuto</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Schwarber</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



The players that were mentioned the most, throwing out Nola because of reasons mentioned above, were Bryce Harper, Jean Segura, JT Realmuto and Kyle Schwarber. Harper Ranked 1 in CWPA and mentions, which makes sense, as he was without a doubt the star of the series. Schwarber and Realmuto were also highly ranked in CWPA, and in mentions. Perhaps Jean Segura was slighlty over-mentioned, as he had a negative CWPA, but 6 mentions in the stories. One unsung hero for the Phillies was Zack Wheeler, who added 9.3% to the Phillies championship odds, but was only mentioned once. On the Padres side, Juan Soto added the most CWPA, but was only mentioned twice, ranking 5th. This was surprising to me, as Juan Soto is one of the Padres' most popular players.

Another layer to this is that oftentimes, people mentioned in these stories are quoted, and for a variety of reasons, it is more difficult to get quotes from Latin-American born players like Juan Soto or Asian born players like Ha-Seong Kim of the Padres.

## Creating a chart to compare Series CWPA and mentions


```python
import matplotlib.pyplot as plt

cwpaDF = pd.read_csv('/Users/richarddiamond/Desktop/CLS161/cwpa.csv')
cols = ['name', 'cwpa']
cwpaDF.columns = cols

#this gives us a DF which compares cwpa and mentions
cwpaDF = pd.merge(mentionsDF, cwpaDF, on="name")

xl = 'Number of mentions'
yl = 'Series CWPA'

plt.plot(cwpaDF['mentions'], cwpaDF['cwpa'])
plt.title('Number of Mentions in ESPN Articles vs. CWPA')
plt.xlabel(xl)
plt.ylabel(yl)

plt.show()

```

    Matplotlib created a temporary config/cache directory at /var/folders/_y/tj_hz20s3174wxwq7g_yk6t80000gn/T/matplotlib-zfflf8yk because the default path (/Users/richarddiamond/.matplotlib) is not a writable directory; it is highly recommended to set the MPLCONFIGDIR environment variable to a writable directory, in particular to speed up the import of Matplotlib and to better support multiprocessing.



    
![png](output_11_1.png)
    


Certainly not the most linear trend. It seems as though there are plenty of other factors: what position a player plays, whether he is on the winning team and whether he is a popular figure in baseball that determine how much a player is mentioned.
It is interesting, however, that Bryce Harper had by far the highest CWPA and by far the highest number of mentions. It seems as though extraordinary performance will lead to extraordinary mentions.
