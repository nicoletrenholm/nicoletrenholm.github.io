



![alt text](inglefieldbanner.PNG)


### Project 2

In Project 2, I take you to the Arctic. Here we are in Greenland and the Canadian Arctic Archipelago where I have been
mapping out the seafloor and tracing warm water of Atlantic origin up into the glaciated fjords. Check out my Video Blog series film 4 or 4 below that takes you to my study site and discusses my incredibly challenging survey in mapping out the uncharted Inglefield Fjord, near the top of the world! 79° North. This data is the baseline for my graduate research work at UMBC. I the majority of my field research on sailing craft with a program Ocean Research project 501c3 based out of Annapolis, MD.

In the longterm in this project page I will develop my GIS media, graphics, animations and data analysis. I will also include locations to data respositoiries that have more relevant polar datasets. It will be part a research story map page and part a progression of various map revealing my data review, project plannning phases and data analysis. As I become more savyy with R, Python and SQL I will share and demonstrate my data processing code to provide transparency and repeatability with my analysis.
                                                                                           
![](youtube.PNG)(https://www.youtube.com/watch?time_continue=1&v=pWfDdVi2xhs)

Project Phase 1:

![](DSC_0055_1.jpg)

![](overview1.PNG)

Project Phase 2:

![](phase2.PNG)

Earlier publications, project blogs and activities [Check out Ocean Research Project Inc. 501c3](https://wwww.oceanresearchproject.org)

### Canada's Northwest Passage:
Croker Bay Glaciers
##### Changes in ocean temperature at melting glaciers at select depths from the sea surface to the seafloor.

- Elevation in Meters


![alt text](giffy.gif)
This giffy is only so meaningful. After I recover my 3D version of this similiar giffy with a heatmap legend that relates the termeprature variability at each elevation I will re make this giffy and slow it down for easier interpreation of glacial melt discharge and incoming warm ocean boundary current.


### Red Points Represent the Prevailing Route for Inbound Warm Currents.
##### Currents cutting through the natural deep channel  that brings warm water to melt the ocean terminaiting glacier

![alt text](hotspots.JPG)


### Project Parameters & Code

#### Data:

- LC08_L1TP_039007_20170814_20170825_01_T1_sr_band5 (Landsat Data)

- Ocean Profile temperature elevation data (My data)

#### Tools:

- Built tables from ocean vertical point data for 1m, 10m, 50m, 100m, 150m, 200, 250) as Add Delimited Text Layer
- Inverse Distributed Weight Interpolation from Vector
- Clip Interpolated raster surfaces of temperature at different elevations by polygon

#### Product:

Map: My map shows the temperature changes between at select sub sea level elevations in front of Canada's melting glaciers.
- The number in the right corner represents elevation in m
- The heat map indicates in red the warmer water and blue the cooler water via continuous heatmap  per elevation temperature range
- The black points are represent where the CTD cast locations temperature

#### My Coordinate Reference System Extent is:

- NAD83(CSRS) / EPSG Arctic zone 5-37

#### Goal:

- I took my ocean data and made tables of the vertical temperature info each station in front of the ocean melting glacier. I turned them into vector points by  bringing the new tables as comma Delimited text files. Then I needed to make thermal interpolation rasters at different key subsea elevations by giving it a polygon vector shape to interpolate in.

- I want to select the features in the one of my vector table file that have an ID name of C4-C10, C14-16, and C22 (these buggers show me where the ocean influence is coming in and eating away at the glacier from underneath).

- then I want to change the select Hot points to Red. I needed the original vector points of the stations to be a nice contrast color so I made the symbology change in the code.

#### Code:

```
#this is to make sure that the file path checks out
points = QgsVectorLayer('D:/Desktop/Project_2/points.shp', 'points')
points.isValid()

# Should Return "True"
QgsProject.instance().addMapLayer(points)

# this will tell it what file its going to work on
renderer = points.renderer()
renderer

# now we going to change the vector dataset to a color of I want
symbol = renderer.symbol()
symbol.setColor(QColor(Qt.black))
points.triggerRepaint()

# ya got to make sure the color matches the layer tree colors
layer_tree = iface.layerTreeView()
layer_tree.refreshLayerSymbology(points.id())

# Here we select the stations I care about by their ID attribute
selection = points.getFeatures(QgsFeatureRequest(). setFilterExpression(u'"ID" = \'C4\' or "ID" = \'C5\' or "ID" = \'C6\' or "ID" = \'C7\' or "ID" = \'C8\' or "ID" = \'C9\' or "ID" = \'C10\' or "ID" = \'C14\' or "ID" = \'C15\' or "ID" = \'C22\' or "ID" = \'C16\''))
points.selectByIds([s.id() for s in selection])
iface.mapCanvas().zoomToSelected()

# Now we got to make this selection a file
QgsVectorFileWriter.writeAsVectorFormat(points, r'D:/Desktop/Project_2/hot.gpkg', 'utf-8', points.crs(),'GPKG', True)
hot = QgsVectorLayer('D:/Desktop/Project_2/hot.gpkg', 'hot')
hot.isValid()
# Should Return "True"
QgsProject.instance().addMapLayer(hot)

# Time to make sure those puppies are red because of what they mean
renderer = hot.renderer()
symbol = renderer.symbol()
symbol.setColor(QColor(Qt.red))
hot.triggerRepaint()

# You want that layer tree to match
layer_tree = iface.layerTreeView()
layer_tree.refreshLayerSymbology(hot.id())

```
