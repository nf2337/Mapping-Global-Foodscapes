# Tutorial 5 
-------------------------

## Tutorial 5: Using Data Collection Apps 

## Objectives: 

The objectives of this session will be to gather our own dataset of mushrooms in Tivoli Bay using the iNaturalist application. [iNaturalist](https://www.inaturalist.org/) is a social network of naturalists, citizen scientists, and biologists built on the concept of mapping and sharing observations of biodiversity across the globe. We will be locating the GPS coordinates of the mushrooms we find, with the help of Dr. Patricia Kaishian, using her class project entiteld "Natural History of Bard College". Later, we will use this data to make a forrager's map of Bard's campus and its peripheries! 

## Setting up an iNaturalist Account: 

On your iPhone, go to the apple store, and download the iNaturalist App. 

Then, open the app and create an account with your Bard email address. 

Finally, open the project page on the app and search for `Natural History of Bard College`. Join the project, and now you are ready for collection. 

![Image 1](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/1-Tutorial-5.png)

## Collecting Data Using iNaturalist

While treading the forest, you will find mushrooms. To add a mushroom observation to our collective dataset, go to Observer > Camera and take a photo of the mushroom. You can add multiple photos to each entry. With the help of Dr. Kaishian, try to identify the name of the species, and add it to "what did you see". Note that the app automatically registers your GPS location, provided by Latitude and Logitude coordinates. This will be important for our mapping exercise. Once you are done, click share. 

On the App, under "Me", you can browse and edit your multiple observations. You need to make sure that all the observations have been successfully uploaded to the project so we can download them as a .csv and visualize them on our map! 

![Image 2](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/2-Tutorial-5.png)

## Location data as KML file

In addition to our observations, I will also be recording our [MyTracs](https://apps.apple.com/us/app/mytracks-the-gps-logger/id358697908), a GPS logger app on the iPhone. This will help us retrace our wondering path through the forest. NOTE: You don't need to download this yourself. 

## Accessing iNaturalist Data on Desktop

Go to [iNaturalist](https://www.inaturalist.org/) and log into your account. Go to Community > Your Recent Projects > Natural History of Bard College. 

![Image 3](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/3-Tutorial-5.png)

There, you will be able to see all the observations made to this project, including the ones we collected during our forraging trip. 

If you scroll down to Map of Observations, you will be able to see the observations on an interactive map. Note that most of the observations are around Bard College. If you look at the bottom, you will also find that the observations are displayed on a Basemap powerd by Google. 

![Image 4](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/4-Tutorial-5.png)

We want to download the dataset, and add it to our own map showing certain features of Bard College. Scroll back up to **Observation**, and look through the page. You will see 500+ observations made by our group trip, and by other studnets at Bard College. To donwload this as a CSV file, click **Export Observations**.

![Image 5](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/5-Tutorial-5.png)

From here, you can choose the **Query**, in other words, what observations and associated data you want to include in your **CSV file**. For now, we will keep the default settings. Note that you aready have the latitude and longitude coordinates as a column! This will help us open the dataset in QGIS! Great! 

Scroll down to **4 - Create Export**, and click the button. Once the export is complete, you can go back to the top of the page, and download the observations. 

![Image 6](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/6-Tutorial-5.png)

Rename the file **Tutorial-5-iNatralist** and store it in your folder for Tutorial 5. 

*note: if you were not able to create an iNaturalist account, you can download the data from [here](https://drive.google.com/file/d/1wuUxzzEbzuGDgrkLOI4enhpxn9XWbQn_/view).*

## Adding iNaturalist data in QGIS

Open QGIS. Before we start, lets note that the maps we made for tutorials 1-4 were all global in scale, in other words, we were mapping the whole world, and using coordinate reference system that is appropriate for such a large landmass. 

Today, we will transition to making a more localized dataset for Bard College and its surroundings. For that, we'll need a different coordinate reference system. Before you start, set the **Project CRS** to WGS 84 / UTM zone 18N (EPSG:32618). 

![Image 7](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/7-Tutorial-5.png)

Next, go to **Layers > Add Layer > Add Delimited Text Layer**. After navigating and selecting your CSV file, make sure that the **Point coordinates** are defined as Longitude for the **X field** and Latitude for the **Y Field**. Also be sure to define the **Geometry CSR** as EPSG:4326 - WGS 84. Click add. 

![Image 8](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/8-Tutorial-5.png)

Great, we have a bunch of dots appearing, but where are we? What does all of this mean? To add and edit a basemap, we'll have to briefly learn about OpenStreetMap. 

![Image 9](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/9-Tutorial-5.png)

## OpenStreetMap

[OpenStreetMap](https://www.openstreetmap.org/#map=4/38.01/-95.84) is a collaborative, free, and editible goegpraphic database of the world - or a Wikipedia of Maps. But why do we need OpenStreetMap when there's Google Maps. There are many comperable features for both sources, but OSM is free, open source, and can be easily editted, while Google Maps is proprietery and difficult to customize. 

Because it is open source, OpenStreetMaps has low coverage in some areas. I spent an immense amount of time drawing the building footprint of my city, Amman, on OSM, but the good news is that it's now available for everyone to use. Around the Bard College area, the data seems robust, with lots of detailed streets, buildings, and designated natural areas. In what follows, we'll learn how to download custom aspects of OSM and to edit it in QGIS. 

![Image 10](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/10-Tutorial-5.png)

## Using OpenStreetMap on QGIS

Return to your QGIS window for Tutorial 5. We'll have to install a few plugins to work with OSM data in QGIS. Plugins are additional features that increase the functionality of QGIS. 

Go to **Plugins > Download and Install Plugins > Settings**. Check the button for **Show also experimental plugins**. 

![Image 11](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/11-Tutorial-5.png)

Then, return to **All** and search for **OpenLayers Plugin**, and click **Install**. Again, search for **QuickOSM**, and also install it. Then close. 

![Image 12](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/12-Tutorial-5.png)

**OpenLayers** can be accessed from **Web > OpenLayers**, and it allows you to add basemap layers from numerous sources, including OSM, Google Maps, and others. Add the OSM Map, and from the **Layers Panel**, make sure that it's below the points layer. 

![Image 13](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/13-Tutorial-5.png)

In the Layers Panel, left click the OpenStreetMap layer > Properties. Notice that under **Symbology**, there are very limited features. This is because QGIS is reading the OSM layer as an image, or a raster dataset. The only thing you can edit is the rendering, in other words, the brightness, transparency, contrast, etc.

![Image 14](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/14-Tutorial-5.png)

But what if, you want to change the size of roads, the amount of text that appears on the image, and the colors of buildings, for example? 

For that, we will need to download OSM data into layers of vector data.

## Downloading OSM data in Vector Format 

Before we begin, we want to set the extent of the data we want to download, in others, what are the boundaries of the map we're making. We want a map of Bard College that also includes Tivoli Bays. We need to create a temporary layer that defines this extent.

Click the **Add Temporary Scratch Layer** icon indicated below, name the layer **Extent**, and define the **Geometry Type** as Polygon. Click Ok. 

![Image 15](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/15-Tutorial-5.png)

The layer will automatically be in **Toggle Editing Mode**. Go to **Edit > Add Rectangle > Add Rectangle from Extent**. Then, with the curser, identify a point on the top left corner, drag till the red rectangle is covering your desired extent, and click the right and left buttons together (this can take a moment to figure out). Now you have a polygon defining your extent. 

Click the **Toggle Editting** button indicated below, and save the changes to your scratch layer. Then, in the Layers Pannel, click on the **scratch layer** icon also shown below, and save the layer as a **GeoJSON**. Call it **Extent** and save it in your Tutorial 5 folder. 

![Image 16](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/16-Tutorial-5.png)

Now, rename the layer **Extent**, and left click it **> Properties > Symbology**. Make the fill transparent, and increase the stroke. Click OK. 

![Image 17](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/17-Tutorial-5.png)

Now go to **Vector > QuickOSM > QuickOSM**. 

OSM has codified ways of tagging and describing the data. For example, all the highways in the world are tagged under the "highway", with several sub-tags, including residential and service roads, primary, second and tertiary streets, and footways. 

To add a street layer, go to **Quick Query** and under the first query, type **highway**. Then, to define the area, chose **Layer Extent**, and identify the **Extent layer**. Scroll down abd press **Run Query**. 

QuickOSM is accessing the OpenStreetMap database, and its pulling all the highways defined for our designated area. 

![Image 18](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/18-Tutorial-5.png)

In your **Layers Panel** notice that you separate point, line, and polygon layers for the highway. Of course, we only want the lines, so highlight the points/polygon layers, and remove them. 

![Image 19](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/19-Tutorial-5.png)

Next, we'll add some layers to show the natural features of the landscape. Go back to **Vector > Quick OSM**.

This time, for the **Key** type in **Natural**, and define the **Layer Extent** as **Extent**. Click Run Query. 

Keep only the **Natural Polgon** and remove the line and point layers. Your map should start to look like this. Don't worry about the styling, we'll deal with this in a second. 

![Image 20](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/20-Tutorial-5.png)

Finally, let's add some buildings. This time, we'll add a few different tags to the keys to include buildings, spots, and parking lots. Follow the instructions below, and be sure to identify **Or** rather than **And**. Run the query, and remove the points layer. 

![Image 21](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/21-Tutorial-5.png)

## Styling OSM Data

Now that we've finished downloads, we'll just save our temporary layer quickly. On each of **highway**, **natural** and **building_amenity_parking**, click the scratch layer, and save each as a GeoJSON in your Tutorial 5 folder. 

Styling, as we've learned, is an art, and its difficult to create map styles wihtout a reference. For this tutorial, I'll be styling the map according to this map, by Michael the Cartographer from the 1980s. 

![Image 22](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/22-Tutorial-5.png)

Lets start with the **highway layer**. Left click the **layer > Open Attributes table**. Because this is a crowdsources dataset, there's a lot of **Null** values. However, if you click on the **highway** field, and rearrange it, you will notice that all the streets have values that include unclassified, track, tertiary, steps, service, secondary, residential, path, footway. We'll use this **highway** field in our styling. 

![Image 23](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/23-Tutorial-5.png)

On the **highway layer** > Properties > Symbology, chose Rule-based. We'll include 2 rules, one for paved roads, and the other for unpaved roads. Click **+** to add a second rule. 

![Image 24](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/24-Tutorial-5.png)

Double click on the first **(no filter)** to define the rule. 

We will label the rule **Unpaved**. For the filter, add the following: 
```
"highway" IN ('unclassified', 'track', 'steps', 'path', 'footway')
```
Change the style of the layer to make it a red dashed line. Then click Ok. 

![Image 25](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/25-Tutorial-5.png)

Click the second **(no filter)** to define the rule. We will label the rule **Paved**. For the filter, add the following: 
```
"highway" IN ('tertiary', 'service', 'secondary', 'residential')
```
Change the layer style to a slightly more prominent coloring. Make the line width 0.6 and change the color to red. Then click ok, and Apply. 

![Image 26](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/26-Tutorial-5.png)

If you unclick some layers, this is what your map should look like: 

![Image 27](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/27-Tutorial-5.png)

Next, go to the natural layer > Properties > Symbology. Chose the Categorized method, and identify the value as **natural**. Note that now you have seperate categories for beach, grasslund, scree, scrub, water, wetland, and wood. If you press apply, you'll be able to see what's what. 

![Image 28](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/28-Tutorial-5.png)

Lets change the color and styling of each. The water layer should be blue. For the grassland, wetland, wood, and scrub, you want to explore playing with dot densities to replecate the style of our above referenced map. I would recommend first searching through the available symbols, chosing the dot pattern that already exists, and changing the point patterns based on distance, displacement, and size of dot. 

![Image 29](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/29-Tutorial-5.png)

Spend some time working on this, it might take you a moment to produce styles that work with each other. This is what my map currently looks like. 

![Image 30](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/30-Tutorial-5.png)

Go to buildings layer > Properties > Symbology, and just change the fill color to black. 

Go to the extent layer > Properties > Symbology and give it a light grey fill and remove the border. This will serve as our background color. 

If you zoom in, the campus map looks quite detailed and beautiful! 

![Image 31](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/31-Tutorial-5.png)

## Styling iNaturalist data 

Finally, we'll turn to our iNaturalist data layer. Go to the layer > Open Attributes table, you will realize the dataset is quite detailed. 

Through the data collection, students have been adding the different types of species, including reptiles, funghi, plants, etc. Notice that this is all registered under the field **iconic taxon name**. If you double click this layer, you'll see that many of the entries are for Funghi, which is what we need for our Mushroom Map of Bard's Campus! 

![Image 32](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/32-Tutorial-5.png)

Go back to the **Layers Panel** and double click the iNaturlist Layer > Properties > Symbology. Chose **Rule-based symbology**. Click the first rule, call it Fungi, and add the following to the filter: 

```
"iconic_taxon_name" = 'Fungi'
```

Then sytle your points. I'm going to make mine small blue dots. Make sure your layers are carefully arranged, so that the iNaturlist layer is on the top, the Extent is on the bottom, and everything else is inbetween. 

Finally, a quick export. Project > Import/Export > Export Map as Image. Make sure the define the extent as Calculate from Layer, and to chose the Extent layer. Increase the Resolution to 300 dpi, and save it! 

![Image 33](/Mapping-Global-Foodscapes/assets/img/Tutorial-5/33-Tutorial-5.png)

Please upload your outcome to [Tutorial 5 Folder](https://drive.google.com/drive/u/0/folders/1wE5ENChPJbWfD-eIhNw_rPChwcRup7rk). 


























