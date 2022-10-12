---
layout: page
title: Visualizing Data with Bokeh and Pandas
description: My First Programming Historian lesson, visualizing Bokeh and Pandas. 
---
## Source
[Charlie Harper "Visualizing Data with Bokeh and Pandas", Programming Historian (2018), https://doi.org/10.46430/phen0078.](https://programminghistorian.org/en/lessons/visualizing-with-bokeh)

## Reflection

I went through the Programming Historian lesson titled “Visualizing Data with Bokeh and Pandas”. Bokeh and Pandas are two python packages which contain several built in functions that allowed me to visualize all sorts of cool data pertaining to World War II and the various battles and bombardments that took place. In the lesson, I learned how to work with DataFrames and I also learned about the various built in ways to represent data. The lesson began with more simple representations such as bar charts and histograms, but progressed to more involved ones such as geographical mapping and smoothed line charts. 

The part of the lesson I struggled most with was syntax. Learning Bokeh syntax felt like learning a new programming language. I was able to understand what each step accomplished, as everything was thankfully thoroughly explained by the website, but it will likely take some time to commit Bokeh syntax to memory.

The part I enjoyed the most was seeing the graphs come to life. There is no better feeling than clicking into a new window and seeing a numerical representation of a story that I created. I also feel like learning how to represent data will be super important for me as I plan to major in data science and I will certainly need to know how to effectively tell stories through data visualization. I feel that I should keep chipping away at learning Bokeh as it will be super useful to me in the future.

## Code

## Creating my first plot using Bokeh - 

```python
from bokeh.plotting import figure, output_file, show
output_file('myFirstPlot.html')

#passing some data to plot
x = [1, 3, 5, 7]
y = [2, 4, 6, 8]

#creating a new figure
p = figure ()
p.circle(x,y, size = 15, color = 'blue', legend_label = 'circle')
p.line(x,y, color = 'green', legend_label = 'line')
p.triangle(x,y, size = 10, color = 'red', legend_label = 'triangle')

p.legend.click_policy='hide'
#showing the graphs in a new window
show(p)

## Importing and working with Pandas -

#importing pandas
import pandas as pd
df = pd.read_csv('/Users/richarddiamond/Desktop/thor_wwii.csv')

#printing imported data
print(df)

#get column list
df.columns.tolist()


```
## Connecting Bokeh and Pandas
```python
import pandas as pd
from bokeh.plotting import figure, output_file, show
from bokeh.models import ColumnDataSource
from bokeh.models.tools import HoverTool

output_file('columndatasource_example.html')

df = pd.read_csv('/Users/richarddiamond/Desktop/thor_wwii.csv')

#Creating sample
sample = df.sample(50)
source = ColumnDataSource(sample)

#creating the plot
plot = figure()
plot.circle(x='TOTAL_TONS', y='AC_ATTACKING',
         source=source,
         size=10, color='green')
plot.title.text = 'Attacking Aircraft and Munitions Dropped'
plot.xaxis.axis_label = 'Tons of Munitions Dropped'
plot.yaxis.axis_label = 'Number of Attacking Aircraft'

hover = HoverTool()
hover.tooltips=[
    ('Attack Date', '@MSNDATE'),
    ('Attacking Aircraft', '@AC_ATTACKING'),
    ('Tons of Munitions', '@TOTAL_TONS'),
    ('Type of Aircraft', '@AIRCRAFT_NAME')
]

plot.add_tools(hover)
#print plot
show(plot)


```
## Plotting Categorical Data
```python
import pandas as pd
from bokeh.plotting import figure, output_file, show
from bokeh.models import ColumnDataSource
from bokeh.models.tools import HoverTool

from bokeh.palettes import Spectral5
from bokeh.transform import factor_cmap
output_file('munitions_by_country.html')

df = pd.read_csv('/Users/richarddiamond/Desktop/thor_wwii.csv')

#group data by which country mission took off from
grouped = df.groupby('TAKEOFF_COUNTRY')[['TOTAL_TONS', 'TONS_HE', 'TONS_IC', 'TONS_FRAG']].sum()
#get units in kilotons
grouped = grouped / 1000

print(grouped)

#plot data
source = ColumnDataSource(grouped)
takeoffCountries = source.data['TAKEOFF_COUNTRY'].tolist()
p = figure(x_range=takeoffCountries)

color_map = factor_cmap(field_name='TAKEOFF_COUNTRY',
                    palette=Spectral5, factors=takeoffCountries)

p.vbar(x='TAKEOFF_COUNTRY', top='TOTAL_TONS', source=source, width=0.70, color=color_map)

p.title.text ='Munitions Dropped by Takeoff Country'
p.xaxis.axis_label = 'Takeoff Country'
p.yaxis.axis_label = 'Kilotons of Munitions'

hover = HoverTool()
hover.tooltips = [
    ("Totals", "@TONS_HE High Explosive / @TONS_IC Incendiary / @TONS_FRAG Fragmentation")]

hover.mode = 'vline'

p.add_tools(hover)

show(p)

```
## Using Stacked Bar Charts w/ Sub Sampling
```python
import pandas as pd
from bokeh.plotting import figure, output_file, show
from bokeh.models import ColumnDataSource
from bokeh.palettes import Spectral3
output_file('types_of_munitions.html')

df = pd.read_csv('/Users/richarddiamond/Desktop/thor_wwii.csv')

#filter out missions not US or GB affiliated
filter = df['COUNTRY_FLYING_MISSION'].isin(('USA','GREAT BRITAIN'))
df = df[filter]

grouped = df.groupby('COUNTRY_FLYING_MISSION')['TONS_IC', 'TONS_FRAG', 'TONS_HE'].sum()
grouped = grouped / 1000

source = ColumnDataSource(grouped)
countries = source.data['COUNTRY_FLYING_MISSION'].tolist()
p = figure(x_range=countries)

p.vbar_stack(stackers=['TONS_HE', 'TONS_FRAG', 'TONS_IC'],
             x='COUNTRY_FLYING_MISSION', source=source,
             legend = ['High Explosive', 'Fragmentation', 'Incendiary'],
             width=0.5, color=Spectral3)

p.title.text ='Types of Munitions Dropped by Allied Country'
p.legend.location = 'top_left'

p.xaxis.axis_label = 'Country'
p.xgrid.grid_line_color = None	

p.yaxis.axis_label = 'Kilotons of Munitions'

show(p)
```
## Time Series Graphs
```python
import pandas as pd
from bokeh.plotting import figure, output_file, show
from bokeh.models import ColumnDataSource
from bokeh.palettes import Spectral3
output_file('simple_timeseries_plot.html')

df = pd.read_csv('/Users/richarddiamond/Desktop/thor_wwii.csv')

#Convert to date/time format
df['MSNDATE'] = pd.to_datetime(df['MSNDATE'], format='%m/%d/%Y')
grouped = df.groupby('MSNDATE')['TOTAL_TONS', 'TONS_IC', 'TONS_FRAG'].sum()
grouped = grouped/1000

source = ColumnDataSource(grouped)

p = figure(x_axis_type='datetime')

p.line(x='MSNDATE', y='TOTAL_TONS', line_width=2, source=source, legend='All Munitions')
p.line(x='MSNDATE', y='TONS_FRAG', line_width=2, source=source, color=Spectral3[1], legend='Fragmentation')
p.line(x='MSNDATE', y='TONS_IC', line_width=2, source=source, color=Spectral3[2], legend='Incendiary')

p.yaxis.axis_label = 'Kilotons of Munitions Dropped'

show(p)

```
## Modifying Time Series
```python
#This process will smooth the time series
grouped = df.groupby(pd.Grouper(key='MSNDATE', freq='M'))['TOTAL_TONS', 'TONS_IC', 'TONS_FRAG'].sum()
grouped = grouped/1000

source = ColumnDataSource(grouped)

p = figure(x_axis_type='datetime')

p.line(x='MSNDATE', y='TOTAL_TONS', line_width=2, source=source, legend='All Munitions')
p.line(x='MSNDATE', y='TONS_FRAG', line_width=2, source=source, color=Spectral3[1], legend='Fragmentation')
p.line(x='MSNDATE', y='TONS_IC', line_width=2, source=source, color=Spectral3[2], legend='Incendiary')

p.yaxis.axis_label = 'Kilotons of Munitions Dropped'

show(p)

```
## Annotating Trends
```python
import pandas as pd
from bokeh.plotting import figure, output_file, show
from bokeh.models import ColumnDataSource
from datetime import datetime
from bokeh.palettes import Spectral3
output_file('eto_operations.html')

df = pd.read_csv('/Users/richarddiamond/Desktop/thor_wwii.csv')

filter = df['THEATER']=='ETO'
df = df[filter]

df['MSNDATE'] = pd.to_datetime(df['MSNDATE'], format='%m/%d/%Y')
group = df.groupby(pd.Grouper(key='MSNDATE', freq='M'))['TOTAL_TONS', 'TONS_IC', 'TONS_FRAG'].sum()
group = group / 1000

source = ColumnDataSource(group)

p = figure(x_axis_type="datetime")

p.line(x='MSNDATE', y='TOTAL_TONS', line_width=2, source=source, legend='All Munitions')
p.line(x='MSNDATE', y='TONS_FRAG', line_width=2, source=source, color=Spectral3[1], legend='Fragmentation')
p.line(x='MSNDATE', y='TONS_IC', line_width=2, source=source, color=Spectral3[2], legend='Incendiary')

p.title.text = 'European Theater of Operations'

p.yaxis.axis_label = 'Kilotons of Munitions Dropped'

show(p)

```
## Spatial Data
```python
pip install pyproj

import pandas as pd
from bokeh.plotting import figure, output_file, show
from bokeh.models import ColumnDataSource, Range1d
from bokeh.layouts import layout
from bokeh.palettes import Spectral3
from bokeh.tile_providers import get_provider
from pyproj import transformer
output_file('targets.html')


def LongLat_to_EN(long, lat):
    try:
        transformer = Transformer.from_crs('epsg:4326', 'epsg:3857')
        easting, northing = transformer.transform(long, lat)
        return easting, northing
    except:
        return None, None


df = pd.read_csv('/Users/richarddiamond/Desktop/thor_wwii.csv')

df['E'], df['N'] = zip(
    *df.apply(lambda x: LongLat_to_EN(x['TGT_LONGITUDE'], x['TGT_LATITUDE']), axis=1))

#group data frame to get desired field
grouped = df.groupby(['E', 'N'])[['TONS_IC', 'TONS_FRAG']].sum().reset_index()

filter = grouped['TONS_FRAG'] != 0
grouped = grouped[filter]

source = ColumnDataSource(grouped)

left = -2150000
right = 18000000
bottom = -5300000
top = 11000000

p = figure(x_range=Range1d(left, right), y_range=Range1d(bottom, top))

provider = get_provider('CARTODBPOSITRON')
p.add_tile(provider)

p.circle(x='E', y='N', source=source, line_color='grey', fill_color='yellow')

p.axis.visible = False

show(p)
```