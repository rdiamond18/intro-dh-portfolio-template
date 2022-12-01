# NER Assignment
Georeferencing automatically detected place names in Edward Gibbon's *Decline and Fall of the Roman Empire* using the Pleiades gazatteer and `spaCy`.

Your assignment this week is to output a `CSV` file of place names, frequency and coordinates, as we did in class for a chapter of Gibbon of your choice. Try to find a chapter with a lot of places as we will be turning this data into an online map next week. The steps are:

* Choose a chapter from the text
* Begin a function by parsing input text
* Create a `spaCy` dictionary of entities and frequency
* Use the Pleiaes data from class to find coordinates for each place name
* Run your function on your chosen chapter
* Save your final `CSV`
* Come to class on Monday, ready to use it


```python
# import and download any relevant data

import pandas as pd
import spacy
nlp = spacy.load('en_core_web_sm')

#download gibbon
import wget
import os
if not os.path.isfile('gibbon_text.csv'):
    wget.download('https://raw.githubusercontent.com/pnadelofficial/FallDHCourseMaterials/main/gibbon_text.csv')

gibbon_by_chapter = pd.read_csv('gibbon_text.csv').rename(columns={'Unnamed: 0':'chapter'})

#download pleiades data
if not os.path.isfile('places.csv'):
    wget.download('https://raw.githubusercontent.com/pnadelofficial/FallDHCourseMaterials/main/places.csv')
if not os.path.isfile('names.csv'):
    wget.download('https://raw.githubusercontent.com/pnadelofficial/FallDHCourseMaterials/main/names.csv')

#download tenth chapter data
chapter = gibbon_by_chapter['StringText'][10]
chapter_doc = nlp(chapter)

#Download names/places
names = pd.read_csv('names.csv')
places = pd.read_csv('places.csv')
```


```python
# any helper functions you may need

#use get pleiades id function given in class
def get_pleiades_id(term):
    """
    Iterates through all of the possible names in the names.csv file
    Returns None if no matched names
    """
    name_row = names.loc[names['attested_form'] == term]
    if len(name_row) == 1:
        return int(name_row.place_id.iloc[0])
    else:
        name_row = names.loc[names['romanized_form_1'] == term]
        if len(name_row) == 1:
            return int(name_row.place_id.iloc[0])
        else:
            name_row = names.loc[names['romanized_form_2'] == term]
            if len(name_row) == 1:
                return int(name_row.place_id.iloc[0])
            else:
                name_row = names.loc[names['romanized_form_3'] == term]
                if len(name_row) == 1:
                    return int(name_row.place_id.iloc[0])
                else:
                    return None
                
def get_lat(pl_id):
    places_row = places.loc[places['id'] == pl_id]
    if len(places_row) == 1:
        return places_row.representative_latitude.iloc[0]
    
def get_long(pl_id):
    places_row = places.loc[places['id'] == pl_id]
    if len(places_row) == 1:
        return places_row.representative_longitude.iloc[0]
    
def get_frequencies(chapter_text):
    #put into spacy parser
    chapter_text = nlp(chapter_text)
    
    import collections
    place_freq = collections.defaultdict(int)
    for entity in chapter_text.ents:
        if (entity.label_ == 'GPE') or (entity.label_ == 'LOC'):
            place_freq[entity.text] += 1 # the utility of defaultdict!
    place_freq = dict(place_freq)
    #convert place freq to df
    place_freq_df = pd.DataFrame.from_dict(place_freq, orient='index').reset_index().rename(columns={'index':'place_name',0:'frequency'})
    return place_freq_df
    
```


```python
# final functions

def get_coordinate_df(text):
    
    coordinate_df = get_frequencies(text)
    
    coordinate_df['pleiades_id'] = coordinate_df['place_name'].apply(get_pleiades_id)
    
    coordinate_df = coordinate_df.dropna().reset_index(drop=True)
    
    coordinate_df['lat'] = coordinate_df['pleiades_id'].apply(get_lat)
    coordinate_df['long'] = coordinate_df['pleiades_id'].apply(get_long)
    
    return coordinate_df

    
    #coordinate_df['lat'] = coordinate_df['pleiades_id'].apply(get_lat)
    #coordinate_df['long'] = coordinate_df['pleiades_id'].apply(get_long)
```


```python
# try your function out

get_coordinate_df(gibbon_by_chapter['StringText'][10])
```

          place_name  frequency  pleiades_id        lat       long
    0      Illyricum          3     481865.0  42.427292  17.965028
    1          Milan          5     383706.0  45.463746   9.188060
    2           Rome         20     423025.0  41.891775  12.486137
    3          Pavia          2     383798.0  45.185899   9.156562
    4         Africa          2        775.0  32.500000   7.500000
    5        Zenobia         24     894185.0  35.666634  39.810395
    6   Thessalonica          2     491741.0  40.628342  22.952885
    7      Macedonia          2     491656.0  41.250000  21.750000
    8         Umbria          1     413360.0  42.897391  12.576790
    9         Latium          1     432900.0  41.590543  13.192265
    10       Cologne          1     108751.0  50.940662   6.959907
    11      Victoria          1      89206.0  56.533420  -3.411596
    12      Hercules          1     266032.0  37.500000  -0.500000
    13         Emesa          5     668261.0  34.737656  36.719319
    14        Arabia          3     981506.0  27.500000  32.500000
    15     Euphrates          1     912849.0  35.543310  39.606018
    16        Ancyra          1     619103.0  39.943793  32.859333
    17         India          3      50004.0  22.500000  77.500000
    18          Nile          1     727172.0  19.211409  30.567330
    19        Tivoli          1     423081.0  41.963602  12.798180
    20       Lucania          1     442639.0  39.885000  17.276944
    21     Byzantium          1     520985.0  41.005902  28.973882
    22      Heraclea          1     452333.0  40.211776  16.669885



```python
# save result as CSV
coordinate_df = get_coordinate_df(gibbon_by_chapter['StringText'][10])
coordinate_df.to_csv('ch10gibbon_places.csv')
```
