---
layout: page
title: Parse TEI Assignment
description: I went through a Gibbon chapter and found all the footnotes using this Python program.
---

# Parsing a TEI Document - Assignment

## Instructions

1. Parse the tei text of Gibbon's _Decline and Fall_ as found in `gibbon.xml`.
2. Extract all the footnotes and remove extraneous white space.
3. Place footnotes in a dataframe.
4. Save the dataframe as a csv file.

## Parsing TEI


```python
# imports
from bs4 import BeautifulSoup
import re
import pandas as pd
```


```python
# load xml file
with open('/Users/richarddiamond/Desktop/tei/in-class/gibbon.xml', encoding = 'utf8', mode = 'r') as f:
    teiString = f.read()
teiString[:500]
```




    '<TEI xmlns="http://www.tei-c.org/ns/1.0">\n    <teiHeader>\n        <fileDesc>\n            <titleStmt>\n                <title>The history of the decline and fall of the Roman Empire: By Edward Gibbon, Esq; ... [pt.2]</title>\n                <author>Gibbon, Edward, 1737-1794.</author>\n            </titleStmt>\n            <extent>511 600dpi bitonal TIFF page images and SGML/XML encoded text</extent>\n            <publicationStmt>\n                <publisher>University of Michigan Library</publisher>\n '




```python
# use BeatifulSoup to instntiate tei object
teiObject = BeautifulSoup(teiString)
```


```python
# find all margin notes
footnotes = teiObject.find_all('note', attrs = {'place':'bottom'})
len(footnotes)
```




    828




```python
# clean margin notes and add to a list
cleanFootnotes = []
for note in footnotes:
    footnoteText = re.sub(r'[\ \n]{2,}', '', note.text)
    cleanFootnotes.append(footnoteText)
len(cleanFootnotes)
```




    828




```python
# convert list to dataframe
df = pd.DataFrame(cleanFootnotes)
```


```python
# check dataframe
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
      <td>\nPons Aureoli,thirteen miles from Bergamo, an...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>On the death of Gallienus, ſee Trebellius Poll...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Some ſuppoſed him, oddly enough, to be a baſta...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>\nNotoria,a periodical and official diſpatch w...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Hiſt. Auguſt. p. 208. Gallienus deſcribes the ...</td>
    </tr>
  </tbody>
</table>
</div>




```python
# save datafram as csv
df.to_csv('footnotes.csv')
```
