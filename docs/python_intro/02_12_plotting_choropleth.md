---
title: Choropleth Maps
linktitle: Choropleth Maps
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ml_intro:
    parent: 02. Plotting
    weight: 12

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 12
---

## Offline Plotly Usage

Get imports and set everything up to be working offline.


```python
import chart_studio.plotly as py
import plotly.graph_objs as go 
from plotly.offline import download_plotlyjs, init_notebook_mode, plot, iplot
```

Now set up everything so that the figures show up in the notebook:


```python
init_notebook_mode(connected=True) 
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



More info on other options for Offline Plotly usage can be found [here](https://plot.ly/python/offline/).

## Choropleth US Maps

Plotly's mapping can be a bit hard to get used to at first, remember to reference the cheat sheet in the data visualization folder, or [find it online here](https://images.plot.ly/plotly-documentation/images/python_cheat_sheet.pdf).


```python
import pandas as pd
```

Now we need to begin to build our data dictionary. Easiest way to do this is to use the **dict()** function of the general form:

* type = 'choropleth',
* locations = list of states
* locationmode = 'USA-states'
* colorscale= 

Either a predefined string:

    'pairs' | 'Greys' | 'Greens' | 'Bluered' | 'Hot' | 'Picnic' | 'Portland' | 'Jet' | 'RdBu' | 'Blackbody' | 'Earth' | 'Electric' | 'YIOrRd' | 'YIGnBu'

or create a [custom colorscale](https://plot.ly/python/heatmap-and-contour-colorscales/)

* text= list or array of text to display per point
* z= array of values on z axis (color of state)
* colorbar = {'title':'Colorbar Title'})

Here is a simple example:


```python
data = dict(type = 'choropleth',
            locations = ['AZ','CA','NY'],
            locationmode = 'USA-states',
            colorscale= 'Portland',
            text= ['text1','text2','text3'],
            z=[1.0,2.0,3.0],
            colorbar = {'title':'Colorbar Title'})
```

Then we create the layout nested dictionary:


```python
layout = dict(geo = {'scope':'usa'})
```

Then we use: 

    go.Figure(data = [data],layout = layout)
    
to set up the object that finally gets passed into iplot()


```python
choromap = go.Figure(data = [data],layout = layout)
```


```python
iplot(choromap)
```


<div>


            <div id="0ffd83f2-2d09-4b5b-a347-b966e925bea9" class="plotly-graph-div" style="height:525px; width:100%;"></div>
            <script type="text/javascript">
                require(["plotly"], function(Plotly) {
                    window.PLOTLYENV=window.PLOTLYENV || {};

                if (document.getElementById("0ffd83f2-2d09-4b5b-a347-b966e925bea9")) {
                    Plotly.newPlot(
                        '0ffd83f2-2d09-4b5b-a347-b966e925bea9',
                        [{"colorbar": {"title": {"text": "Colorbar Title"}}, "colorscale": [[0.0, "rgb(12,51,131)"], [0.25, "rgb(10,136,186)"], [0.5, "rgb(242,211,56)"], [0.75, "rgb(242,143,56)"], [1.0, "rgb(217,30,30)"]], "locationmode": "USA-states", "locations": ["AZ", "CA", "NY"], "text": ["text1", "text2", "text3"], "type": "choropleth", "z": [1.0, 2.0, 3.0]}],
                        {"geo": {"scope": "usa"}, "template": {"data": {"bar": [{"error_x": {"color": "#2a3f5f"}, "error_y": {"color": "#2a3f5f"}, "marker": {"line": {"color": "#E5ECF6", "width": 0.5}}, "type": "bar"}], "barpolar": [{"marker": {"line": {"color": "#E5ECF6", "width": 0.5}}, "type": "barpolar"}], "carpet": [{"aaxis": {"endlinecolor": "#2a3f5f", "gridcolor": "white", "linecolor": "white", "minorgridcolor": "white", "startlinecolor": "#2a3f5f"}, "baxis": {"endlinecolor": "#2a3f5f", "gridcolor": "white", "linecolor": "white", "minorgridcolor": "white", "startlinecolor": "#2a3f5f"}, "type": "carpet"}], "choropleth": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "type": "choropleth"}], "contour": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "contour"}], "contourcarpet": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "type": "contourcarpet"}], "heatmap": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "heatmap"}], "heatmapgl": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "heatmapgl"}], "histogram": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "histogram"}], "histogram2d": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "histogram2d"}], "histogram2dcontour": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "histogram2dcontour"}], "mesh3d": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "type": "mesh3d"}], "parcoords": [{"line": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "parcoords"}], "pie": [{"automargin": true, "type": "pie"}], "scatter": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatter"}], "scatter3d": [{"line": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatter3d"}], "scattercarpet": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scattercarpet"}], "scattergeo": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scattergeo"}], "scattergl": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scattergl"}], "scattermapbox": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scattermapbox"}], "scatterpolar": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatterpolar"}], "scatterpolargl": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatterpolargl"}], "scatterternary": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatterternary"}], "surface": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "surface"}], "table": [{"cells": {"fill": {"color": "#EBF0F8"}, "line": {"color": "white"}}, "header": {"fill": {"color": "#C8D4E3"}, "line": {"color": "white"}}, "type": "table"}]}, "layout": {"annotationdefaults": {"arrowcolor": "#2a3f5f", "arrowhead": 0, "arrowwidth": 1}, "coloraxis": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "colorscale": {"diverging": [[0, "#8e0152"], [0.1, "#c51b7d"], [0.2, "#de77ae"], [0.3, "#f1b6da"], [0.4, "#fde0ef"], [0.5, "#f7f7f7"], [0.6, "#e6f5d0"], [0.7, "#b8e186"], [0.8, "#7fbc41"], [0.9, "#4d9221"], [1, "#276419"]], "sequential": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "sequentialminus": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]]}, "colorway": ["#636efa", "#EF553B", "#00cc96", "#ab63fa", "#FFA15A", "#19d3f3", "#FF6692", "#B6E880", "#FF97FF", "#FECB52"], "font": {"color": "#2a3f5f"}, "geo": {"bgcolor": "white", "lakecolor": "white", "landcolor": "#E5ECF6", "showlakes": true, "showland": true, "subunitcolor": "white"}, "hoverlabel": {"align": "left"}, "hovermode": "closest", "mapbox": {"style": "light"}, "paper_bgcolor": "white", "plot_bgcolor": "#E5ECF6", "polar": {"angularaxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}, "bgcolor": "#E5ECF6", "radialaxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}}, "scene": {"xaxis": {"backgroundcolor": "#E5ECF6", "gridcolor": "white", "gridwidth": 2, "linecolor": "white", "showbackground": true, "ticks": "", "zerolinecolor": "white"}, "yaxis": {"backgroundcolor": "#E5ECF6", "gridcolor": "white", "gridwidth": 2, "linecolor": "white", "showbackground": true, "ticks": "", "zerolinecolor": "white"}, "zaxis": {"backgroundcolor": "#E5ECF6", "gridcolor": "white", "gridwidth": 2, "linecolor": "white", "showbackground": true, "ticks": "", "zerolinecolor": "white"}}, "shapedefaults": {"line": {"color": "#2a3f5f"}}, "ternary": {"aaxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}, "baxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}, "bgcolor": "#E5ECF6", "caxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}}, "title": {"x": 0.05}, "xaxis": {"automargin": true, "gridcolor": "white", "linecolor": "white", "ticks": "", "title": {"standoff": 15}, "zerolinecolor": "white", "zerolinewidth": 2}, "yaxis": {"automargin": true, "gridcolor": "white", "linecolor": "white", "ticks": "", "title": {"standoff": 15}, "zerolinecolor": "white", "zerolinewidth": 2}}}},
                        {"responsive": true}
                    ).then(function(){

var gd = document.getElementById('0ffd83f2-2d09-4b5b-a347-b966e925bea9');
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


### Real Data US Map Choropleth

Now let's show an example with some real data as well as some other options we can add to the dictionaries in data and layout.


```python
df = pd.read_csv('2011_US_AGRI_Exports')
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
      <th>code</th>
      <th>state</th>
      <th>category</th>
      <th>total exports</th>
      <th>beef</th>
      <th>pork</th>
      <th>poultry</th>
      <th>dairy</th>
      <th>fruits fresh</th>
      <th>fruits proc</th>
      <th>total fruits</th>
      <th>veggies fresh</th>
      <th>veggies proc</th>
      <th>total veggies</th>
      <th>corn</th>
      <th>wheat</th>
      <th>cotton</th>
      <th>text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>AL</td>
      <td>Alabama</td>
      <td>state</td>
      <td>1390.63</td>
      <td>34.4</td>
      <td>10.6</td>
      <td>481.0</td>
      <td>4.06</td>
      <td>8.0</td>
      <td>17.1</td>
      <td>25.11</td>
      <td>5.5</td>
      <td>8.9</td>
      <td>14.33</td>
      <td>34.9</td>
      <td>70.0</td>
      <td>317.61</td>
      <td>Alabama&lt;br&gt;Beef 34.4 Dairy 4.06&lt;br&gt;Fruits 25.1...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>AK</td>
      <td>Alaska</td>
      <td>state</td>
      <td>13.31</td>
      <td>0.2</td>
      <td>0.1</td>
      <td>0.0</td>
      <td>0.19</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.6</td>
      <td>1.0</td>
      <td>1.56</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>Alaska&lt;br&gt;Beef 0.2 Dairy 0.19&lt;br&gt;Fruits 0.0 Ve...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>AZ</td>
      <td>Arizona</td>
      <td>state</td>
      <td>1463.17</td>
      <td>71.3</td>
      <td>17.9</td>
      <td>0.0</td>
      <td>105.48</td>
      <td>19.3</td>
      <td>41.0</td>
      <td>60.27</td>
      <td>147.5</td>
      <td>239.4</td>
      <td>386.91</td>
      <td>7.3</td>
      <td>48.7</td>
      <td>423.95</td>
      <td>Arizona&lt;br&gt;Beef 71.3 Dairy 105.48&lt;br&gt;Fruits 60...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>AR</td>
      <td>Arkansas</td>
      <td>state</td>
      <td>3586.02</td>
      <td>53.2</td>
      <td>29.4</td>
      <td>562.9</td>
      <td>3.53</td>
      <td>2.2</td>
      <td>4.7</td>
      <td>6.88</td>
      <td>4.4</td>
      <td>7.1</td>
      <td>11.45</td>
      <td>69.5</td>
      <td>114.5</td>
      <td>665.44</td>
      <td>Arkansas&lt;br&gt;Beef 53.2 Dairy 3.53&lt;br&gt;Fruits 6.8...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CA</td>
      <td>California</td>
      <td>state</td>
      <td>16472.88</td>
      <td>228.7</td>
      <td>11.1</td>
      <td>225.4</td>
      <td>929.95</td>
      <td>2791.8</td>
      <td>5944.6</td>
      <td>8736.40</td>
      <td>803.2</td>
      <td>1303.5</td>
      <td>2106.79</td>
      <td>34.6</td>
      <td>249.3</td>
      <td>1064.95</td>
      <td>California&lt;br&gt;Beef 228.7 Dairy 929.95&lt;br&gt;Frui...</td>
    </tr>
  </tbody>
</table>
</div>



Now out data dictionary with some extra marker and colorbar arguments:


```python
data = dict(type='choropleth',
            colorscale = 'YIOrRd',
            locations = df['code'],
            z = df['total exports'],
            locationmode = 'USA-states',
            text = df['text'],
            marker = dict(line = dict(color = 'rgb(255,255,255)',width = 2)),
            colorbar = {'title':"Millions USD"}
            ) 
```

And our layout dictionary with some more arguments:


```python
layout = dict(title = '2011 US Agriculture Exports by State',
              geo = dict(scope='usa',
                         showlakes = True,
                         lakecolor = 'rgb(85,173,240)')
             )
```


```python
choromap = go.Figure(data = [data],layout = layout)
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-15-243104ae4228> in <module>
    ----> 1 choromap = go.Figure(data = [data],layout = layout)
    

    ~/.local/lib/python3.6/site-packages/plotly/graph_objs/_figure.py in __init__(self, data, layout, frames, skip_invalid, **kwargs)
        606             is invalid AND skip_invalid is False
        607         """
    --> 608         super(Figure, self).__init__(data, layout, frames, skip_invalid, **kwargs)
        609 
        610     def add_area(


    ~/.local/lib/python3.6/site-packages/plotly/basedatatypes.py in __init__(self, data, layout_plotly, frames, skip_invalid, **kwargs)
        155 
        156         # ### Import traces ###
    --> 157         data = self._data_validator.validate_coerce(data, skip_invalid=skip_invalid)
        158 
        159         # ### Save tuple of trace objects ###


    ~/.local/lib/python3.6/site-packages/_plotly_utils/basevalidators.py in validate_coerce(self, v, skip_invalid)
       2643                     else:
       2644                         trace = self.class_map[trace_type](
    -> 2645                             skip_invalid=skip_invalid, **v_copy
       2646                         )
       2647                         res.append(trace)


    ~/.local/lib/python3.6/site-packages/plotly/graph_objs/__init__.py in __init__(self, arg, autocolorscale, coloraxis, colorbar, colorscale, customdata, customdatasrc, geo, hoverinfo, hoverinfosrc, hoverlabel, hovertemplate, hovertemplatesrc, hovertext, hovertextsrc, ids, idssrc, locationmode, locations, locationssrc, marker, meta, metasrc, name, reversescale, selected, selectedpoints, showscale, stream, text, textsrc, uid, uirevision, unselected, visible, z, zauto, zmax, zmid, zmin, zsrc, **kwargs)
      81395         self["colorbar"] = colorbar if colorbar is not None else _v
      81396         _v = arg.pop("colorscale", None)
    > 81397         self["colorscale"] = colorscale if colorscale is not None else _v
      81398         _v = arg.pop("customdata", None)
      81399         self["customdata"] = customdata if customdata is not None else _v


    ~/.local/lib/python3.6/site-packages/plotly/basedatatypes.py in __setitem__(self, prop, value)
       3477             # ### Handle simple property ###
       3478             else:
    -> 3479                 self._set_prop(prop, value)
       3480 
       3481         # Handle non-scalar case


    ~/.local/lib/python3.6/site-packages/plotly/basedatatypes.py in _set_prop(self, prop, val)
       3764                 return
       3765             else:
    -> 3766                 raise err
       3767 
       3768         # val is None


    ~/.local/lib/python3.6/site-packages/plotly/basedatatypes.py in _set_prop(self, prop, val)
       3759         validator = self._validators.get(prop)
       3760         try:
    -> 3761             val = validator.validate_coerce(val)
       3762         except ValueError as err:
       3763             if self._skip_invalid:


    ~/.local/lib/python3.6/site-packages/_plotly_utils/basevalidators.py in validate_coerce(self, v)
       1619 
       1620         if not v_valid:
    -> 1621             self.raise_invalid_val(v)
       1622 
       1623         return v


    ~/.local/lib/python3.6/site-packages/_plotly_utils/basevalidators.py in raise_invalid_val(self, v, inds)
        281                 typ=type_str(v),
        282                 v=repr(v),
    --> 283                 valid_clr_desc=self.description(),
        284             )
        285         )


    ValueError: 
        Invalid value of type 'builtins.str' received for the 'colorscale' property of choropleth
            Received value: 'YIOrRd'
    
        The 'colorscale' property is a colorscale and may be
        specified as:
          - A list of colors that will be spaced evenly to create the colorscale.
            Many predefined colorscale lists are included in the sequential, diverging,
            and cyclical modules in the plotly.colors package.
          - A list of 2-element lists where the first element is the
            normalized color level value (starting at 0 and ending at 1), 
            and the second item is a valid color string.
            (e.g. [[0, 'green'], [0.5, 'red'], [1.0, 'rgb(0, 0, 255)']])
          - One of the following named colorscales:
                ['aggrnyl', 'agsunset', 'algae', 'amp', 'armyrose', 'balance',
                 'blackbody', 'bluered', 'blues', 'blugrn', 'bluyl', 'brbg',
                 'brwnyl', 'bugn', 'bupu', 'burg', 'burgyl', 'cividis', 'curl',
                 'darkmint', 'deep', 'delta', 'dense', 'earth', 'edge', 'electric',
                 'emrld', 'fall', 'geyser', 'gnbu', 'gray', 'greens', 'greys',
                 'haline', 'hot', 'hsv', 'ice', 'icefire', 'inferno', 'jet',
                 'magenta', 'magma', 'matter', 'mint', 'mrybm', 'mygbm', 'oranges',
                 'orrd', 'oryel', 'peach', 'phase', 'picnic', 'pinkyl', 'piyg',
                 'plasma', 'plotly3', 'portland', 'prgn', 'pubu', 'pubugn', 'puor',
                 'purd', 'purp', 'purples', 'purpor', 'rainbow', 'rdbu', 'rdgy',
                 'rdpu', 'rdylbu', 'rdylgn', 'redor', 'reds', 'solar', 'spectral',
                 'speed', 'sunset', 'sunsetdark', 'teal', 'tealgrn', 'tealrose',
                 'tempo', 'temps', 'thermal', 'tropic', 'turbid', 'twilight',
                 'viridis', 'ylgn', 'ylgnbu', 'ylorbr', 'ylorrd']




```python
iplot(choromap)
```

# World Choropleth Map

Now let's see an example with a World Map:


```python
df = pd.read_csv('2014_World_GDP')
df.head()
```


```python
data = dict(
        type = 'choropleth',
        locations = df['CODE'],
        z = df['GDP (BILLIONS)'],
        text = df['COUNTRY'],
        colorbar = {'title' : 'GDP Billions US'},
      ) 
```


```python
layout = dict(
    title = '2014 Global GDP',
    geo = dict(
        showframe = False,
        projection = {'type':'Mercator'}
    )
)
```


```python
choromap = go.Figure(data = [data],layout = layout)
iplot(choromap)
```
