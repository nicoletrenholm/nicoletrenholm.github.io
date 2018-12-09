
![alt text](https://nicoletrenholm.github.io/P1_SLR/glacier.PNG)



# Project 1: Sea Level Rise

##  P1_SLR/2.5D Baltimore Sea Level Rise Property Impact

![hustlin_erd]( P1_SLR/2.5D Baltimore Sea Level Rise Property Impact.pdf)

## Map Background:

If the Greenland Ice Cap melts it is estimated to add 21 feet of sea level rise in which all of the city of Baltimore would be impacted. Here I focus on the 10 foot elevation contour to reveal the residential and industrial properties impacted by sea level rise. I include a streamlined 10, 15, and 20 foot elevation contour.

I have a flood zone file, want to relate population and smoothen my elevation contours on my next go at it.
Of the submerged waterfront properties what % of the structural area are impacted by sea level rise relative to residential verse industrial properties? Residential is at 15% while industrial is 58% of the submerged property. I queried structarea sums of my key usergroups ( primarily Residential and Industrial) in DB Manager with my Real_Property sqlite file. I did not know the unit for the structarea if I did I would have related the total areas not as percentages but as miles squared in relation to Baltimore City’s 81 miles squared area.

Other major observations include: At the 10 foot contour the Canton Industrial area, Fairfield Area and Locust Point Industrial area are almost entirely submerged because this terrain has a more gentle slope to sea.
The neigborhoods at greatest risk to the first 10 foot contour include: Jonestown, Inner Harbor, Little Italy, Washington hill, Perkins Homes Point. This is because the harbor appears to generate a new tributary branch extending a bay in the direction through these neighborhoods. Stacked Canton waterfront residential communities are at great risk with a new tributary branch threatening a route towards Patterson Park.

Data: DEM from Earthworks,Real Property from Dillon,Contours made from DEM than digitized and reduced, Lidar but didnt use in end
Plugin:Attempted to use qGIS2threejs with some success

Tools:
At different points fooled around with.
Polygonize,R.Contour,Fix Geometries,Clip Vector,Extract Raster,New scratch layer polygons,2.5D renderer,Zonal Statistics,Select by attribute,Save as Spatialite file,DB Manager,Filter

Product:
Map: My map shows a 2.5D view of the surrounding terrain around Baltimore Harbor.The blue coarse pixelation represents the extent of the 10 foot sea level rise as portrayed by the DEM.The contour related 10 foot red contour was produced from this DEM though I later generalized it further reducing the outlier smallcontours (I can do a better job). I did get my industrial related and residential related buildings to pop!Instead of shoot off the map to infinity by messing with the height till it looked sensible.I investigated the neighborhoods in greatest jeopardy and includ photos of the trouble spots in the map. 

My Coordinate Reference System is Extent: EPSG:3395 -180.00, -80.00, 180.00, 84.00Proj4: +proj=merc +lon_0=0 +k=1 +x_0=0 +y_0=0 +datum=WGS84 +units=m +no_defs


