### Concepts
1. What are geometries?
  - Points
  - Polygons
  - Lines
2. data vs attributes

### The type of geometry and the amount of geometires determine the tool stack

- What kind of data do you have?
  - Points
    - How much data?
      - **Just enough**: Convert the data to GeoJSON & make a simple Leaflet map
      - **Too much, but each point's data is important**: Cluster your points with [Leaflet.markercluster](https://github.com/Leaflet/Leaflet.markercluster)

        ![](http://f.cl.ly/items/1X312Y3q3t2W1v0T0c13/Screen%20Shot%202014-06-26%20at%205.03.10%20PM.png)

        example: http://open.undp.org/#2014/filter/operating_unit-AFG
      
      - **Too much, the points have some value that can be aggregated**: Create hexbins of your points with the [QGIS hexbin](https://www.mapbox.com/blog/binning-alternative-point-maps/) plugin
        
        ![](http://f.cl.ly/items/3A1R2m3T380Q113o1029/Screen%20Shot%202014-06-26%20at%205.02.46%20PM.png)

      - **Too much, the points just represent presence - like tweets**: Create a heatmap with [Leaflet.heat](https://github.com/Leaflet/Leaflet.heat) or QGIS heatmap plugin.
        
        ![](http://f.cl.ly/items/0H2O031Y0L290n2S313U/Screen%20Shot%202014-06-26%20at%205.06.14%20PM.png)

  - Polygons
    - How much data?
      - **Just enough**:Convert the data to [GeoJSON](http://geojson.org/) & make a simple Leaflet map

        ![](http://f.cl.ly/items/3Z2z1U022u020w1n0C1v/Screen%20Shot%202014-06-26%20at%205.07.02%20PM.png)

        example: http://leafletjs.com/examples/choropleth.html
      
      - **Too much, the polygons have necessary detail**: Use TileMill to render an interactive map with [UTFGrid](https://www.mapbox.com/developers/utfgrid/). If you've ever made a map with tilemill, the interactivities are using UTFGrid. See [tutorial](https://www.mapbox.com/tilemill/docs/crashcourse/tooltips/).

      - **Too much, the polygons have unnecessary details**: Simplify them with [TopoJSON](https://github.com/mbostock/topojson) or QGIS
    
    - What kind of attributes do they have?
      - **Absolute numbers**:Convert the points to centroids with [QGIS](http://www.qgis.org/)
      - **Normalized the absolute*: Make a choropleth map with Leaflet for small data, [TileMill](https://www.mapbox.com/tilemill/)for big data

- Visualization defaults
  - Projection:
    - If it's a web map with tiles, it's using [Spherical Mercator](http://epsg.io/3857)
    - If using [d3](http://d3js.org/) and not using tiles anywhere, use whatever fits best. Bonus projections are in [d3-geo-projection](https://github.com/d3/d3-geo-projection).

  - Colors:
    - When in doubt, use [ColorBrewer](http://colorbrewer2.org/)
    - Want to know more? Read [Subtleties of Color](http://earthobservatory.nasa.gov/blogs/elegantfigures/2013/08/05/subtleties-of-color-part-1-of-6/)

  - Scales:
    - For any data
      - Try linear first
      - Then quantile
    - For data of rates or compounding values
      - Try log and power scales: "A logarithmic scale is a scale of measurement that displays the value of a physical quantity using intervals corresponding to orders of magnitude, rather than a standard linear scale."

  - Points:
    - Start with normal circles with no strokes
    - Scale points by area, not diameter (proportional)

  - Flair:
    - Only add a north arrow if north isn't up
    - Always attribute your data, especially [OpenStreetMap](http://www.openstreetmap.org/), to avoid the nerd wrath
    - If it zooms, add visible zoom controls. Pan isn't necessary, but not everyone has a scroll wheel / multitouch
