# Data Analysis on Coronavirus Outbreak

## __Wuhan Coronavirus__

### What is coronavirus?

The coronavirus is a family of viruses that can cause a range of illnesses in humans including common cold and more severe forms like SARS and MERS which are life-threatening. The virus is named after its shape which takes the form of a crown with protrusions around it and hence is known as coronavirus.


```python
from IPython.display import YouTubeVideo
YouTubeVideo('mOV1aBVYKGA', width=600, height=400)
```





<iframe
    width="600"
    height="400"
    src="https://www.youtube.com/embed/mOV1aBVYKGA"
    frameborder="0"
    allowfullscreen
></iframe>




### How did the recent outbreak occur?
The recent outbreak of coronavirus is believed to have occurred in a market for illegal wildlife in the central Chinese city of Wuhan. Chinese health authorities and the WHO are investigating the outbreak of the recent coronavirus which has claimed thousands of lives.

### Data Exploration


```python
# import the necessary libraries
import numpy as np 
import pandas as pd 

# Visualisation libraries
import matplotlib.pyplot as plt
from pprint import pprint
import seaborn as sns
sns.set_style("whitegrid")
%matplotlib inline

'''Plotly visualization .'''
import plotly.offline as py
from plotly.offline import iplot, init_notebook_mode
import plotly.graph_objs as go
py.init_notebook_mode(connected = True) # Required to use plotly offline in jupyter notebook
```


<script type="text/javascript">
window.PlotlyConfig = {MathJaxConfig: 'local'};
if (window.MathJax) {MathJax.Hub.Config({SVG: {font: "STIX-Web"}});}
if (typeof require !== 'undefined') {
require.undef("plotly");
requirejs.config({
    paths: {
        'plotly': ['https://cdn.plot.ly/plotly-latest.min']
    }
});
require(['plotly'], function(Plotly) {
    window._Plotly = Plotly;
});
}
</script>




```python
df = pd.read_csv("corona_geral.csv")
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 73 entries, 0 to 72
    Data columns (total 6 columns):
    Province/State    52 non-null object
    Country/Region    73 non-null object
    Last Update       73 non-null object
    Confirmed         73 non-null int64
    Deaths            73 non-null int64
    Recovered         73 non-null int64
    dtypes: int64(3), object(3)
    memory usage: 3.5+ KB


### GLOBALY


```python
df.rename({'Country/Region': 'Country'}, axis='columns', inplace=True)
df['Country'].replace({'Mainland China':'China'},inplace=True)

countries = pd.DataFrame(df.groupby('Country')['Country','Confirmed','Deaths', 'Recovered'].sum())
countries
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
      <th>Confirmed</th>
      <th>Deaths</th>
      <th>Recovered</th>
    </tr>
    <tr>
      <th>Country</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Australia</th>
      <td>15</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Belgium</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Cambodia</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Canada</th>
      <td>7</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>China</th>
      <td>44687</td>
      <td>1115</td>
      <td>5062</td>
    </tr>
    <tr>
      <th>Finland</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>France</th>
      <td>11</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Germany</th>
      <td>16</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Hong Kong</th>
      <td>50</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>India</th>
      <td>3</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Italy</th>
      <td>3</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Japan</th>
      <td>28</td>
      <td>0</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Macau</th>
      <td>10</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Malaysia</th>
      <td>18</td>
      <td>0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Nepal</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Others</th>
      <td>175</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Philippines</th>
      <td>3</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Russia</th>
      <td>2</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Singapore</th>
      <td>47</td>
      <td>0</td>
      <td>9</td>
    </tr>
    <tr>
      <th>South Korea</th>
      <td>28</td>
      <td>0</td>
      <td>7</td>
    </tr>
    <tr>
      <th>Spain</th>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Sri Lanka</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Sweden</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Taiwan</th>
      <td>18</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Thailand</th>
      <td>33</td>
      <td>0</td>
      <td>10</td>
    </tr>
    <tr>
      <th>UK</th>
      <td>8</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>US</th>
      <td>13</td>
      <td>0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>United Arab Emirates</th>
      <td>8</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Vietnam</th>
      <td>15</td>
      <td>0</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>




```python
coordinates = pd.read_csv('coordinates.csv')

countries['Country'] = countries.index
countries.index=np.arange(1,len(countries)+1)
countries = pd.merge(coordinates,countries,on='Country')
```


```python

fig = go.Figure()
fig.add_trace(go.Scattergeo(
        lat=countries['latitude'],
        lon=countries['longitude'],
        mode="markers",
        marker=dict(
            size=17,
            color='rgb(255, 0, 0)',
            opacity=0.7
        ),
        text=countries['Country'],
        hoverinfo="text",
    ))

fig.add_trace(go.Scattergeo(
        lat=countries['latitude'],
        lon=countries['longitude'],
        mode='markers',
        marker=dict(
            size=8,
            color='rgb(242, 177, 172)',
            opacity=0.7
        ),
        hoverinfo='none'
    ))

fig.update_layout(
        autosize=True,
        hovermode='closest',
        showlegend=False,
        title_text = '<b>Countries with Confirmed, Deaths and Recovered cases of 2019-nCoV',
        font=dict(family="Courier New", color='darkred'),
    geo = go.layout.Geo(
        showframe = False,
        showcoastlines = False,
        showcountries = True,
        landcolor = "rgb(229, 229, 229)",
        countrycolor = "black",
        coastlinecolor = "black",
        projection_type="natural earth"
    ))

 
fig.show()
```


<div>


            <div id="6148ce08-d738-408a-8b1b-ecd3fb5d809d" class="plotly-graph-div" style="height:525px; width:100%;"></div>
            <script type="text/javascript">
                require(["plotly"], function(Plotly) {
                    window.PLOTLYENV=window.PLOTLYENV || {};

                if (document.getElementById("6148ce08-d738-408a-8b1b-ecd3fb5d809d")) {
                    Plotly.newPlot(
                        '6148ce08-d738-408a-8b1b-ecd3fb5d809d',
                        [{"hoverinfo": "text", "lat": [23.424076, -25.274398, 50.503887, 56.130366, 35.86166, 51.165690999999995, 40.463667, 61.92411, 46.227638, 55.378051, 22.396428, 20.593684, 41.87194, 36.204824, 12.565679, 35.907757000000004, 7.873054, 22.198745000000002, 4.210483999999999, 28.394857000000002, 12.879721, 61.52401, 60.128161, 1.352083, 15.870032, 23.69781, 37.09024, 14.058323999999999], "lon": [53.847818000000004, 133.775136, 4.469936, -106.34677099999999, 104.195397, 10.451526, -3.7492199999999998, 25.748151, 2.213749, -3.435973, 114.10949699999999, 78.96288, 12.56738, 138.252924, 104.990963, 127.766922, 80.77179699999999, 113.543873, 101.97576600000001, 84.12400799999999, 121.77401699999999, 105.31875600000001, 18.643501, 103.819836, 100.992541, 120.96051499999999, -95.712891, 108.277199], "marker": {"color": "rgb(255, 0, 0)", "opacity": 0.7, "size": 17}, "mode": "markers", "text": ["United Arab Emirates", "Australia", "Belgium", "Canada", "China", "Germany", "Spain", "Finland", "France", "UK", "Hong Kong", "India", "Italy", "Japan", "Cambodia", "South Korea", "Sri Lanka", "Macau", "Malaysia", "Nepal", "Philippines", "Russia", "Sweden", "Singapore", "Thailand", "Taiwan", "US", "Vietnam"], "type": "scattergeo"}, {"hoverinfo": "none", "lat": [23.424076, -25.274398, 50.503887, 56.130366, 35.86166, 51.165690999999995, 40.463667, 61.92411, 46.227638, 55.378051, 22.396428, 20.593684, 41.87194, 36.204824, 12.565679, 35.907757000000004, 7.873054, 22.198745000000002, 4.210483999999999, 28.394857000000002, 12.879721, 61.52401, 60.128161, 1.352083, 15.870032, 23.69781, 37.09024, 14.058323999999999], "lon": [53.847818000000004, 133.775136, 4.469936, -106.34677099999999, 104.195397, 10.451526, -3.7492199999999998, 25.748151, 2.213749, -3.435973, 114.10949699999999, 78.96288, 12.56738, 138.252924, 104.990963, 127.766922, 80.77179699999999, 113.543873, 101.97576600000001, 84.12400799999999, 121.77401699999999, 105.31875600000001, 18.643501, 103.819836, 100.992541, 120.96051499999999, -95.712891, 108.277199], "marker": {"color": "rgb(242, 177, 172)", "opacity": 0.7, "size": 8}, "mode": "markers", "type": "scattergeo"}],
                        {"autosize": true, "font": {"color": "darkred", "family": "Courier New"}, "geo": {"coastlinecolor": "black", "countrycolor": "black", "landcolor": "rgb(229, 229, 229)", "projection": {"type": "natural earth"}, "showcoastlines": false, "showcountries": true, "showframe": false}, "hovermode": "closest", "showlegend": false, "template": {"data": {"bar": [{"error_x": {"color": "#2a3f5f"}, "error_y": {"color": "#2a3f5f"}, "marker": {"line": {"color": "#E5ECF6", "width": 0.5}}, "type": "bar"}], "barpolar": [{"marker": {"line": {"color": "#E5ECF6", "width": 0.5}}, "type": "barpolar"}], "carpet": [{"aaxis": {"endlinecolor": "#2a3f5f", "gridcolor": "white", "linecolor": "white", "minorgridcolor": "white", "startlinecolor": "#2a3f5f"}, "baxis": {"endlinecolor": "#2a3f5f", "gridcolor": "white", "linecolor": "white", "minorgridcolor": "white", "startlinecolor": "#2a3f5f"}, "type": "carpet"}], "choropleth": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "type": "choropleth"}], "contour": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "contour"}], "contourcarpet": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "type": "contourcarpet"}], "heatmap": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "heatmap"}], "heatmapgl": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "heatmapgl"}], "histogram": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "histogram"}], "histogram2d": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "histogram2d"}], "histogram2dcontour": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "histogram2dcontour"}], "mesh3d": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "type": "mesh3d"}], "parcoords": [{"line": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "parcoords"}], "pie": [{"automargin": true, "type": "pie"}], "scatter": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatter"}], "scatter3d": [{"line": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatter3d"}], "scattercarpet": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scattercarpet"}], "scattergeo": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scattergeo"}], "scattergl": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scattergl"}], "scattermapbox": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scattermapbox"}], "scatterpolar": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatterpolar"}], "scatterpolargl": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatterpolargl"}], "scatterternary": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatterternary"}], "surface": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "surface"}], "table": [{"cells": {"fill": {"color": "#EBF0F8"}, "line": {"color": "white"}}, "header": {"fill": {"color": "#C8D4E3"}, "line": {"color": "white"}}, "type": "table"}]}, "layout": {"annotationdefaults": {"arrowcolor": "#2a3f5f", "arrowhead": 0, "arrowwidth": 1}, "coloraxis": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "colorscale": {"diverging": [[0, "#8e0152"], [0.1, "#c51b7d"], [0.2, "#de77ae"], [0.3, "#f1b6da"], [0.4, "#fde0ef"], [0.5, "#f7f7f7"], [0.6, "#e6f5d0"], [0.7, "#b8e186"], [0.8, "#7fbc41"], [0.9, "#4d9221"], [1, "#276419"]], "sequential": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "sequentialminus": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]]}, "colorway": ["#636efa", "#EF553B", "#00cc96", "#ab63fa", "#FFA15A", "#19d3f3", "#FF6692", "#B6E880", "#FF97FF", "#FECB52"], "font": {"color": "#2a3f5f"}, "geo": {"bgcolor": "white", "lakecolor": "white", "landcolor": "#E5ECF6", "showlakes": true, "showland": true, "subunitcolor": "white"}, "hoverlabel": {"align": "left"}, "hovermode": "closest", "mapbox": {"style": "light"}, "paper_bgcolor": "white", "plot_bgcolor": "#E5ECF6", "polar": {"angularaxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}, "bgcolor": "#E5ECF6", "radialaxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}}, "scene": {"xaxis": {"backgroundcolor": "#E5ECF6", "gridcolor": "white", "gridwidth": 2, "linecolor": "white", "showbackground": true, "ticks": "", "zerolinecolor": "white"}, "yaxis": {"backgroundcolor": "#E5ECF6", "gridcolor": "white", "gridwidth": 2, "linecolor": "white", "showbackground": true, "ticks": "", "zerolinecolor": "white"}, "zaxis": {"backgroundcolor": "#E5ECF6", "gridcolor": "white", "gridwidth": 2, "linecolor": "white", "showbackground": true, "ticks": "", "zerolinecolor": "white"}}, "shapedefaults": {"line": {"color": "#2a3f5f"}}, "ternary": {"aaxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}, "baxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}, "bgcolor": "#E5ECF6", "caxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}}, "title": {"x": 0.05}, "xaxis": {"automargin": true, "gridcolor": "white", "linecolor": "white", "ticks": "", "title": {"standoff": 15}, "zerolinecolor": "white", "zerolinewidth": 2}, "yaxis": {"automargin": true, "gridcolor": "white", "linecolor": "white", "ticks": "", "title": {"standoff": 15}, "zerolinecolor": "white", "zerolinewidth": 2}}}, "title": {"text": "<b>Countries with Confirmed, Deaths and Recovered cases of 2019-nCoV"}},
                        {"responsive": true}
                    ).then(function(){

var gd = document.getElementById('6148ce08-d738-408a-8b1b-ecd3fb5d809d');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })
                };
                });
            </script>
        </div>



```python
others = countries[countries.Country != 'China']
others = others[countries.Country != 'Others']

f, ax = plt.subplots(figsize=(15, 10))


sns.barplot(x="Confirmed", y="Country", data=others,
            label="Infected", color="orange",alpha=0.7)


sns.barplot(x="Recovered", y="Country", data=others,
            label="Recovered", color="g",alpha=0.7)


ax.set_title('Confirmed vs Recovered comparison of Countries other than China', fontsize=20, fontweight='bold', position=(0.40, 1.05))
ax.legend(ncol=2, loc="lower right", frameon=True)
ax.set(xlim=(0, 55), ylabel="",
       xlabel="People")
sns.despine(left=True, bottom=True)
```

    /usr/lib/python3.7/site-packages/ipykernel_launcher.py:2: UserWarning:
    
    Boolean Series key will be reindexed to match DataFrame index.
    



![png](output_11_1.png)



```python
print("\nOverall, there are",df['Confirmed'].sum(),"people affected,", 
      df['Recovered'].sum(),"recovered and", 
      df['Deaths'].sum(),"deaths.")
```

    
    Overall, there are 45206 people affected, 5123 recovered and 1117 deaths.


### CHINA SCENARIO


```python

```


```python

```


```python

```


```python

```


```python

```
