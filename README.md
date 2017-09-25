# **spidermaps**

# About
This AMD modules makes it easy to create a flow map using the ArcGIS API for JavaScript 4.4+ [JavaScript 4.x](https://developers.arcgis.com/javascript/).

# What does it do?
If you define a starting point. It will create straight lines dynamically to a point feature service you define. You have the option of a non-geodesic and geodesic lines.

Defining a [linesymbol](https://developers.arcgis.com/javascript/latest/api-reference/esri-symbols-LineSymbol.html) allows you to change the symbology of a line.

This module is possible to do in with Desktop solutions. But they are pre-baked/calculated. This module is live and queries the point feature layers on the fly!

# Sample
A sample app can be found [here](http://bit.ly/2hr4uSH). 

# Using
Start by cloning the repo and ensure you have a copy of the modules folder. Point to the modules folder in the head of your HTML file

```HTML
 <script>
        var dojoConfig = {
            async: true,
            isDebug: true,
            paths: {
                modules: location.href.replace(location.href.split("/").pop(), "") + "/lib/modules"
            }
        };
    </script>
```

Require the module

```JavaScript
require([
            "modules/SpiderMaps",
        

            "esri/Map",
            "esri/views/MapView"
            ...
            
        ], function(SpiderMaps, Map, MapView) {...

```

Available methods are...

```JavaScript
    
    spiderMaps.create(view, Point, FeatureLayer, LineSymbol, GeodesicBoolean, Quality); 
    
    /*
    Based on your defined start point. It will create straight lines to all points in a feature layer.
    
    view = mandatory. It's your MapView/SceneView name.
    Point = Starting point geometry
    Featurelayer =  Point FeatureService object
    lineSymbol = Symbology for the line
    GeodesicBoolean = true or false 
    quality = one of the folllowing "super-low", "low", "medium", "high", "ultra"
    Note: Quality is set to high by default.
    */
    
    spiderMaps.update(view, Point, FeatureLayer, LineSymbol, geodesic, quality); 
    //This deletes any previous layers and re-adds the new lines. This is best when either the start point changes position or when the featurelayer data is live/updates. 
```
Example of using spidermaps

```JavaScript
   
   
   var starPoints = new FeatureLayer({                       
        url:"https://services.arcgis.com/Qo2anKIAMzIEkIJB/arcgis/rest/services/whats_the_points/FeatureServer"
    });        

    //Starting coordinates (long latt)
    var startPointLongLatt = [-0.0762373,51.5054002]
            
    var lineSymbol = new SimpleLineSymbol({
        cap: "round",
        color: "gold",
        width: 1,
        style: "solid"
    });
        
            
  spiderMaps.create(view, startPointLongLatt, starPoints, lineSymbol, true, "high");              
  //Creates geodesic lines starting from startPointLongLatt and ending all points inside starPoints featurelayer. With high detail in a solid gold line.

```

This module does work for mapview and sceneview (2d & 3d).

# Issues
Find a bug or want to request a new feature? Please let us know by submitting an issue. Even better, why not fix it yourself! We're open to community updates.

# Future ideas/wish list
Save to feature layer - An option that lets you save the layer as a new feature layer once the query has been run.

# Licensing

Copyright 2017 ESRI (UK) Limited

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the Licence.
