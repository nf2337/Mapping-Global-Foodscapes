# Tutorial 1
-------------------------

## Tutorial 1: Visualizing and Viewing Vector Data in QGIS 

### Objectives:

This tutorial aims to introduce QGIS, a free open-source Geographic Information System tool you willl use from the computer. It will review the process of downloading, installing, setting-up QGIS, as well as short exercise to introduce working with vector data. The outcome will be a visualization of countries around the globe according to their GDP Per Capita, in a projection system of your choosing. 

### Setup:

First, you will need to download QGIS. The tutorials are written in version 3.20.2, so please make sure you are working with at least 3.2. You can download QGIS [here](https://qgis.org/en/site/forusers/download.html). 

GIS projects and files can be confusing, as you will soon learn! Please set up a GIS folder on your desktop with a subfolder for each tutorial, and keen your files well-ordered and clean!

### The QGIS Interface:

![Image 1](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/1-Tutorial-1.png)

**Here’s a quick overview of the user interface:**

**1- Map Canvas:** Where your map itself will be displayed. This will change as you rearrange or perform commands on your data. 

**2- Toolbar:** The most common tools used will be placed here, including save, open new file, pan, zoom and other commonly used tools. If you hover on any of the buttons, it will display a tooltip with brief description. 

**3- Browser Panel:** The browser panel lets you navigate your database, in other words the sources and data files that exist on your computer and that you might want to bring into QGIS.

**4- Layers Panel:** You can see a list of all layers imported into your project. You can re-arrange layers, add new groups, rename layers, expand and collapse items. Right click on the layer for all the available options. 

**5- Status Bar:** Shows you information on your current map, including the scale and mouse cursor’s coordinates. On the bottom right is also your projection system. 

To change the main interface, you can go to View>Panels 

### QGIS Project File

As soon as you open a new project, save it in a designated folder. This will create a .qgz file, where your project is located. Note this is not the final map you are producing, and you will always need to export your maps as a pdf or image. Also note that the .qgz project contains links to your data, and the datasets themselves are not embedded in the file. This means that if you change the name or location of source files, the link will break.

**Let’s add some data, but first, a bit of explanation:**

**Data Types:** There are two types of spatial data you can visualize in QGIS: vector and raster. Vector data is discrete set of features, raster data is continuous grid of pixels. If you are familiar with the abobe suite, vector is like working in Illustrator, raster is like working in Photoshop. For this tutorial, we’ll explore vector data. 

**Vector data** is used to show real world features in GIS, represented as points, lines or polygons. Features might be trees represented as points, roads represented as lines, or country boundaries represented as polygons. Every feature has a geometry (where it is in space), and a series of attributes, or data that identify it. 

**Now we’ll begin:**

![Image 2](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/2-Tutorial-1.png)

Move to the Google Drive > Tutorials > Tutorial 1 > [Data](https://drive.google.com/drive/folders/1WUO3lS13vYuyvtgiUEVwo1BOur4QrTiE), and download the `“Country-Boundaries-110”` file. Make sure to drag it into a designated folder.  
When you open the file, you will realize that there are  differen7t file extensions which all make up a shapefile. While you need them all to run your file (so keep your data organized!), the one essential file is the `.shp` extension. 

Turn to your QGIS interface, and navigate to Layer > Add Layer > Add Vector Layer. Click the […] next to the Vector Datasets and find your `“Country-Boundaries-110”` file. Click the .shp extension, and press open, then add. 

You should now see countries of the world on your **Map Canvas** and in your **Layer Panel**. Let’s learn to navigate. 

![Image 3](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/3-Tutorial-1.png)

These are some useful tools. The first is **Pan Map**, the second is **Zoom Full** (takes you to the full extent), and the third is **Identify Feature**. 

Let’s try **Identify Feature**. Click on a country, and you will get a panel on the left that will show you some information. This includes the name, and lots of other entries. Where is this information coming from? 

The **Identify Feature** tool is a quick way to view attributes associated with each feature. To understand this more fully, navigate to your **Layers Panel**, and click **Open Attributes Table**. 

![Image 4](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/4-Tutorial-1.png)

The **Attributes Table** looks a lot like an excel sheet, and that’s because it is! Every geographic feature, in our case country, has a row associated with it, and this is called a **field**. The columns are called **attributes**. 

![Image 5](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/5-Tutorial-1.png)

Scroll to the right of your attributes table, and you will find an attribute called `GDP_MD_EST`. This is shorthand for Estimated Gross Domestic Product in Million Dollars. `The GDP_YEAR` attribute indicates that the GDP estimate is for the year 2016. By clicking on the header, you can rearrange the dataset in ascending or descending order. Note that the country with the highest GDP 21,140,000 million USD, or add 6 zeros, about 21 trillion dollars. Note also, that there is an estimate for population size, under the attribute `POP_EST`.

**Can we make a map that reflects world GDP? Yes!** 

![Image 6](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/6-Tutorial-1.png)

Close your attributes table. Right click your layer again, and go to **Properties > Symbology**. There you will find settings to change the styling of your map. 

At the top, you can see that the settings are currently on Single Symbol settings. We want to change that to Graduated settings. This means you will be able to classify and represent your dataset according to an attribute, in our case: GDP. Under value, choose `GDP_MD_EST`. Then hit classify. 

![Image 7](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/7-Tutorial-1.png)

The color lamp will allow you to choose the spectrum of colors you can use. Following the small down arrow, you can choose pre-identified spectrum formats. 

The mode allows you to chose the way you want to classify your data, or how you want to create the bins that hold your data. These include Equal Count (Quantile), Equal Interval, Logarithmic Scale, Natural Breaks (Jenks), Pretty Breaks, or Standard Deviation. These modes are all a result of complex statistical theory, but I leave it up to you to chose here what you find most suitable. You can explore the distribution of your data in the historgram tab. 
 
The classes identify the number of bins you want to create for your data. If you want to classify GDP according to “High”, “Medium” and “Low”, you can chose 3 classes. If you want further gradation, like “Very High”, “High”, “Medium”, “Low”, “Very Low” you can chose 5 classes. 

Make your choice here, and I leave it up to you to experiment and find your preferred map of the world. There is no “correct” result. You can hit apply to see changes reflected on you map canvas. When you are done, click ok. 

I create 5 classes using the Natural Breaks (Jenks) mode. 

![Image 8](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/8-Tutorial-1.png)

This is my map of the world, classified according to GDP. I can use the Identify Features tool to quickly explore the results (shift+command+I shortcut). China and the USA appear in the “Very High” category. Then, India, Brazil, Russia, Indonesia and Germany appear in the “High” category, and so on. 

But something is amiss? We know, of course, that GDP really depends on the size of the country and its population. This is why economists worldwide have adopted the GDP per capita measure, which adjusts for population size. 

Can we map that instead? Yes. 

First lets keep the current layer, and rename it Countries GDP. To rename, right click the layer in the Layers Panel, and click rename layer. 

Then, duplicate your layer. Again, right click the layer > duplicate layer. Rename the duplicate Countries GDP/Capita.

Your layers panel should look like this. You can drag and drop layers to re-arrange them, untick and tick boxes to show and hide layer, etc. Drag your Countries GDP/Capita layer on top of the Countries GDP layer.

![Image 9](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/9-Tutorial-1.png)

On the new layers, go to Properties > Symbology tab. This time, we will calculate a value rather than using a pre-existing one from our attributes table. Click the calculate sign to the right of Value, and you will get the following dialogue box. Here is where we’re going to do some math to determine the GDP per capita. 

![Image 10](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/10-Tutorial-1.png)

From the right hand menu, you want to expand the “Fields and Values” tab, then chose  . This will multiple GPD by a million (remember, the attribute is GDP in Million Dollars), then will divide it by the population estimate, giving us GDP per capita. Click Ok. 

Now you will have to click classify again, and play around with the settings. When I press apply, I notice that the Natural Breaks (Jenks) mode doesn’t make a lot of sense. Antartica, because of its small population size, is the only country that appears to have Very High GDP per capita. I will classify again according to Equal Count. This makes a lot more sense! 

By turning layers on and off, I can quickly see the difference between the countries. 

![Image 11](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/11-Tutorial-1.png)

You can do a lot more with styling. Go back to Properties > Symbology. If you double click on the symbol (you need to click exactly here), this will the Symbol Selector panel. 

![Image 12](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/12-Tutorial-1.png)

From here, click the Simple Fill tab, which will allow you to play around with with Fill color and style, and Stroke color and style. I am going to change the fill style and stroke color. Feel free to experiment to find the style that best suits the scale of your map. Note that you have to make changes to every single class separately.

![Image 13](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/13-Tutorial-1.png)

Now that we’re satisfied with the style, we’ll add some labels to identify separate countries. Go back to Properties, and this time click Labels. The default is No Labels, but we’ll change that to Single Labels. 

![Image 14](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/14-Tutorial-1.png)

You can basically choose any attribute from your attributes table as a label. The default, NAME is actually what we need. Click Apply to see the results. You can change the formatting of the text with many options below. I’ll change the color of the text, and will add a small buffer (or white outline).

![Image 15](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/15-Tutorial-1.png)

The result looks pretty good, but there are way too many names on the map. What if, I want to add the names only for countries classified as Very High GDP per capita. That’s possible! 

Back to Properties > Labels. This time, you want to select Rule-based labels. Click on the rule tab, then on the calculate sign, and you’ll get Expression String Builder. You want to basically write out a formula that will say: LABEL THIS ONLY IF the country has a GDP per capita great > X amount. 

![Image 16](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/16-Tutorial-1.png)

Copy this equation into the expression builder: (("GDP_MD_EST"*1000000)/ "POP_EST") >= 35761 
You’ll get better at writing these expressions with time. Basically, this indicates the rule, that labels will appear for countries when their GDP per capita is greater than 35,761 which is the lower value in our Very High classification. I derived this number from my layer on the right. Click ok, and ok. 

![Image 17](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/17-Tutorial-1.png)

There you have it. This will allow you to see small countries, like Kuwait, that have a very small area, but now you know also have a very high GDP per capita! 

Some fun with Projections! 

So far, we’ve been seeing a “normal” map of the world in WGS84, which is the Coordinate Reference System used by the Global Positioning System. 

Coordinate Reference System (CRS): the method that QGIS uses to show the 3D surface of the globe on your 2D screen. Map projection systems are very complicated- and it can take years to master them. It is important that our data is in the same CSR so that they line up on top of each other. There are two different types of CRS: 

1) Geographic CRS: uses latitude and longitude coordinates to tell you where you are, based on differently shaped models of the globe. We’ll mostly be using WGS 84, 

2) Projected CRS: uses a mathematical algorithm to present the round earth on a flat map. Most common projected reference system is the Universal Transverse Mercator (UTM), which is fixed at the equator. 

But there’s a slight problem: the earth’s surface is curved and not a perfect sphere, introducing an element of distortion. Coordinate reference systems can be used to preserve shape, distance, relative size or direction. 

Please take a few minutes to read about projection systems here. Use the interactive projections tool to check out different distortions. WGS 84 is a Mercator projection, it looks like this. 

![Image 18](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/18-Tutorial-1.png)

Click on others including: Robinson, Sinusoidal, Mollweide, Bonne. We’ll explore representing our map with these projections. 

Before we start retrojecting our data, let’s add some grid lines. 

Go to Vector > Research Tools > Create Grid

![Image 19](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/19-Tutorial-1.png)

Set the parameters of your grid. Change the Grid type to Line, Horizontal/Vertical spacing to 15 degrees, and identify the Grid extent to Calculate from Layer > Countries GDP/Capita. Then press run. This is basically creating a new vector file, with line attributes, and adding it to your Layers panel and browser panel

![Image 20](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/20-Tutorial-1.png)

Another quick step. Go to Vector > Geometry Tools > Densify By Count. Make sure the input layer is your grid. Change the number of vertices to 50, and run it. 

Great, now delete the grid layer by right clicking it > remove layer. The Densified layer is still temporary, if you close your project and open it again, it will disappear. First lets save the densified  data. Click on the temporary icon on the layer in the layers panel. Always save your files as .geoJSON which is the most efficient type, and will compress your data in 1 file (instead of 7, like the .sph shapefile format). Give your layer a location and title by clicking the […] icon and press ok. 

![Image 21](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/21-Tutorial-1.png)

Now you can also style your line by right clicking in the layers panel > Properties > Symbology. 

Once you’re done, we’ll head to change the projections. Click on the bottom right corner, as indicated below. 

![Image 22](/Mapping-Global-Foodscapes/assets/img/Tutorial-1/22-Tutorial-1.png)

There are over 7000 projections in QGIS. Each is identified by a unique Authority ID. Try some projections. To make it simple, here are a few codes you might want to type into the filter (make sure to click them once the option appears):

Robinson: ESRI:53030
Sinusoidal: ESRI:53008
Mollweide: ESRI:53009
Bonne: ESRI:53024

Once you’ve experimented and you’re satisfied with a projection, close the window. Now we’re ready to export the map. We’ll cover that next tutorial, where we’ll learn to include a title, legend and scale bar. For now, take a screenshot of your Map Canvas. From your desktop, rename the file: LASTNAME_Tutorial_1 and upload it to the Tutorial 1 > Output folder. 

See you next time!! 
