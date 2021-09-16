# Tutorial 2
-------------------------

## Tutorial 2: Working with Historical Data

## Objectives: 

This tutorial aims to further introduce QGIS tools through the lens of working with historical datasets. We’ll be looking at one historical raster dataset, [Historical Croplands Dataset, 1700-1992](https://nelson.wisc.edu/sage/data-and-models/historic-croplands/index.php), and one historical vector dataset, [Historical Urban Population Growth Data](https://urbanization.yale.edu/data). 

A lot of the politics of cartography is embedded in the datasets themselves. You might want to spend a few moments reading the documentation, or scan the summary of our data below.

**Historical Croplands Dataset:** “To reconstruct historical croplands, we first compile an extensive database of historical cropland inventory data, at the national and subnational level, from a variety of sources. Then we use our 1992 cropland data within a simple land cover change model, along with the historical inventory data, to reconstruct global 5 min resolution data on permanent cropland areas from 1992 back to 1700. The reconstructed changes in historical croplands are consistent with the history of human settlement and patterns of economic development.”

**Historical Urban Population Growth:** “The dataset was created by digitizing, transcribing, and geocoding historical, archaeological, and census-based urban population data previously published in tabular form by Tertius Chandler and George Modelski.”

## Setup:

Download the datasets for [tutorial 2](https://drive.google.com/drive/folders/15nv45-Sps_vrG1or5YcvK3t7elLuS8Ay) (Only the Croplands folder and the Urban-Populations file, ignore the sheet that says ONLY FOR PREVIEW) . I did some processing to present you with a clean and easy to navigate information. 

## QGIS Project File

Open QGIS, and start a new project file. Save it in your designated folder. Remember! Always keep your files well structured. 

## Set your CRS

Set your project **Coordinate Reference System** (from the bottom right corner) to **WGS 84 (ESPG:4326)**. 

## Adding Raster Data: 

Go to **Layer > Add Layer > Add Raster Layer**. Navigate to the **Tutorial 2 folder > Croplands >** `glcrop1750_0.5.asc` and click ok. You’ve added a raster file with data on global cropland cover for the year 1750. 

![Image 1](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/1-Tutorial-2.png)

The dataset will automatically be represented as a black and white gradient band showing values between `0` and `0.781`. `0` represented uncultivated land, and `0.781` represents the most intensively cultivated cropland. If you zoom into certain locations, you will find that the dataset is very pixilated, and this is related to the **Raster Resolution**. When you right click on the layer, you will realize that there is no **Open Attribute Table** button, like other vector datasets used in previous tutorials. 

## A bit about Raster Data:

Raster data in GIS are a continuous layer of cells that represent features on, above or below the earth’s surface. Each cell in the raster grid is the same size, and cells are usually rectangular. Typical raster datasets include remote sensing data, such as aerial photography, or satellite imagery and modelled data, such as an elevation matrix. In our case, we are using modeled data. Unlike vector data, raster data typically do not have an associated database record for each cell. They are geocoded by pixel resolution and the x/y coordinate of a corner pixel of the raster layer. This allows QGIS to position the data correctly in the map canvas. You can read more about raster datasets [here](https://docs.qgis.org/2.8/en/docs/user_manual/working_with_raster/supported_data.html). 

## Representing Raster Data: 

![Image 2](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/2-Tutorial-2.png)

In the Layers Panel, **right click the layer > Properties > Symbology**. The default Render Type is Singleband grey, we want to change that to Singleband pseudocolor. Leave the Min and Max values as is. Chose an appropriate color ramp to correspond to your spectrum of cropland cultivation. Click apply to check your results. You might also want to change the Color Rendering setting. I am going to increase the contrast of my colors. 

Once satisfied with your colors and representation, you can save the style so it can easily reproduce it in the future. **Style > Save Style,** and save the `.qml` file as Cropland Style. 

![Image 3](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/3-Tutorial-2.png)

Now, go ahead and repeat these steps, adding the global cropland data first for 1850, then for 1950, and representing it as you’ve done above. When you turn to the Properties > Symbology, you can automatically go to Style > Load Style > and choose the file you saved above. 

The only change you now have to make is with the Minimum and Maximum value. This is because for the 1750 dataset, the maximum value (ie. most intensively cultivated land) was `0.781`. For 1850, change the maximum value to `0.908`, and for 1950, change it to `1`. 

![Image 4](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/4-Tutorial-2.png)

Since your 3 datasets are represented with a unified style, you can now compare and see changes across the span of 1750-1950 by manipulating the layer visibility options by checking and unchecking boxes. 

## Adding a csv file: 

A `csv` file, or comma-separated values, is a text file that contains information superheated by commas. A common way to access and edit a csv file is in excel or google sheets. Explore the dataset using google sheets [here](https://docs.google.com/spreadsheets/d/1KwWtysKfcsJWyy6JTcQ7t114jvUQasCueFAH3H0zyH4/edit?usp=drive_web&ouid=113394421580105564513).

![Image 5](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/5-Tutorial-2.png)

In urban populations csv file, take a few minutes to explore the dataset. Each row represents a city, and the columns include population estimates for the years 1700-1975. This is shown both as the actual population size and the population rank. Look for Istanbul. In 1700, it's population was 700,000 people, while its population rank was 1. Istanbul, or Constantinople as it was known to its Ottoman rulers at the time, was the largest city in the world in 1700. 

Try to rearrange the dataset according to population rank in 1950. To do this, hover on the right corner of the cell `R1`, click the small downward pointing arrow, and chose **Sort Sheet A > Z**. 

![Image 16](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/16-Tutorial-2.png)

What was the largest city then? How many people lived there? 

(answer: Philadelphia, 17,600,000)

There might be some cities where the population is zero. This likely means that there is no recorded data for its inhabitants in that year. The rank will also be blank, or **null**. 

Notice further that you have a column showing latitude and longitude, which specify the spatial location of the data. Because of this, you can automatically turn your `.csv` file into a points vector dataset in QGIS.

![Image 6](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/6-Tutorial-2.png)

Go back to QGIS, then press **Layer > Add Delimited Text Layer**. Press the **[…]** to the right of File name, and navigate to your urban population dataset. Notice that QGIS has automatically recognized your Geometry Definition as Point coordinates, assigning the X field to Longitude, and the Y field to Latitude. This means that it will position your points in space according to the listed latitutude and logitude coordinates, creating a vector points file with all the information from your CSV file. Click add. 

![Image 7](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/7-Tutorial-2.png)

QGIS has automatically represented all the points in the dataset. However, we can choose to represent more specific subsets, according to year and population size or rank. 

Before we do that - always remember to save your CSV layers before you start editting. In the **Layers Panel, right click the layer > Export > Save Features As > click the [...]** to identify a file name and location. Make sure your format is `GeoJSON`, and click ok. 

![Image 17](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/17-Tutorial-2.png)

Now you have two identical layers, one called `Urban-Populations`, and the other called `Urban-Populations - Population1750-1975`. You want to remove the second (old one), by left clicking the **Layer > remove layer**. 

![Image 8](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/8-Tutorial-2.png)

Right click the **Layer > Properties > Symbology**, and switch to the graduated symbol method. Then, for Value, choose `Pop-1750`. Explore the histogram briefly. You will notice that most values for population in 1750 are zero, in other words, these cities simply didn’t exist in 1750. In choosing your method of classification, you should make sure that cities with value zero don’t show up on your map.

Chose your preferred color ramp. For **Mode**, chose **Natural Breaks (Jenks)**, and click **Classify**. If you click apply, you will see that there are still many dots - and many zero-value non-existing cities in 1750 appear. To change this, double click the Values tab of the first class. Change the **lower value** from 0.00 to 1.00 then click ok and apply. Notice now, there are far fewer dots on the map. 

![Image 9](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/9-Tutorial-2.png)

This is what your map currently looks like. It might be hard to read two separate sets of color gradients, the first showing global cropland, and the second showing population of cities. Furthermore, there are way too many dots on the map, and it obscures the background layer. Let's try something different with the symbology. Specifically, we'll represent the relative sizes of cities and populations by size of dots, not colors. We will also use the population rank feature. 

![Image 10](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/10-Tutorial-2.png)

## Representing Points (Vector) Data

**Right click the Layer > Properties > Symbology**. Switch your **Value** to `Pop-1750 Rank`, and your **Method** to **Size**. Note the **Size** from **11mm to 1mm**, and increase the number of **Classes** to **11**. 

We'll manually identify the values to make the largest dot symbol represet the most populated city in 1750, the second largest dot symbol to represent the second most populated city in 1750, and so forth. 

Before we do that, let's set the standards for the symbol style. Click the **Symbol tab**, and make your desired chages. I've decreased the opacity to 75%, changed the color to light blue, and removed the outline. Click Ok. 

![Image 18](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/18-Tutorial-2.png)

Now, we'll manually adjust the values to get our desired results. This will take a bit of time, so please be patient. Double click on the **Values**, and adjust the **class bounds** for each to look like this. The size of each dot symbol will manually correspond to its rank, displaying only the 10 largest cities, and the rest as very small dots.

![Image 19](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/19-Tutorial-2.png)

Now, your map looks like this! Great. Let's add some labels. 

![Image 12](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/12-Tutorial-2.png)

**Right click the layer > Properties > Labels**. Switch to **Rule-based Labeling**, double click the rule, add this expression: `10 >= "Pop-1750 Rank" >= 1`, change the **Value** to **City**, and edit the label styling. 

When you’re done, save the layer style as `Population-style` in a designated folder. This will save both your symbology and labeling settings for future use. 

This is what your map looks like! Now, let's make the same representation for urban populations in 1850 and 1950. 

![Image 13](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/13-Tutorial-2.png)

**Right click the layer > Open Attributes Table**. As you scroll through the table, remember that it’s this one vector file that contains data on the population from 1750-1950. All you need to do is make two duplicates of the layer, and change the symbology settings. 

**Right click the Urban Populations layer, and duplicate** it twice. Now rename your layers `Urban-Population-1750`, `Urban-Population-1850`, `Urban-Population-1950`. You might want to further arrange your files in groups like this. To create a group, there’s a little add group icon under layers. 

![Image 14](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/14-Tutorial-2.png)

Now, the process of symbolizing the data for years 1850 and 1950 will be seemless. From the **layers panel, right click the Urban-Populations-1850 layer > Properties > Symbology**. Change only the **Value** to **Pop Rank 1850**. Then go to **Labels > Rule >** and just change the filter to `10 >= "Pop-1850 Rank" >= 1`. 

Do the same with the 1950 layer, changing the symbology value and the label filter to 1950. 

Now you can switch layers on and off to compare between cropland and urban populations in 1750, 1850, and 1950. 

## Working with Print Layout

Go to **Project > New Print Layout** and give it a name. 

As you will soon learn, the **layout editor** is not the most robust tool in QGIS, and you’ll want to determine a good workflow for editing your maps depending on what your final product is and what software you want to use. We’ll be exporting multiple maps for the years 1750, 1850, 1950 separately as images, and we’ll bring them together in Google Slides. If you use **Adobe Illustrator** (that’s great!), you can edit all your data if you export as .svg file! You can read thorough documentation on the QGIS Layout editor [here](https://docs.qgis.org/3.4/en/docs/training_manual/map_composer/map_composer.html).

## The Print Layout Interface

![Image 20](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/20-Tutorial-2.png)

You will be using the project file and the layout interface in conjunction with each other. Practice switching between the two interfaces. 

1. **Toolbox:** this is where you'll be able to add the map, legend, scale bar, and other features to your map. 

2. **Map Canvas:** this is where your map layout itens will appear. 

3. **Dialogue Box:** this is where you'll be able to edit specific items in your layout. You might want to close everything except the item properties tab. 

## Adding your map

![Image 21](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/21-Tutorial-2.png)

Click the **Add Map** button, and drag it across the space of the canvas. You'll notice that it will automatically display the map according the settings defined in your project file. To export 1750 seperately, go to your project interace, and make sure that only your 1750 group is turned on, and that 1850 and 1950 are hidden. Aditionally, **left click the layer > Zoom to group to adjust the extent of your map**. 

Return to the layout file, and press **Refresh**. Now only your 1750 map appears in layout mode. You want to adjust the scale and the placement of the map. To do this, change the scale of the map by adjusting the numerical value in the **Main Properties** tab. The smaller the value, the more zoomed in your map is. You can do this with a bit of trial and error. Try pasting `75000000` into the scale. Once your satisfied, you can move the placement of the map using the Move Item content botton in your toolbox.

Finally, from your toolbox, add the **Scalebar** and draw it on the bottom left corner. As you see, there's a lot of information we don't need, and we'll do some work to adjust the formatting to communicate our data as swiftly as possible. 

From the toolbox, use the **Select/Move Items** to click on the **Legend**. It will appear in your **Main Properties** tab on the right. 

![Image 22](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/22-Tutorial-2.png)

Scroll down to the **Legend Items**. Unclick the **Auto Update**, and tick the **Only show items inside linked map buttom**. This will remove the lenged items for the yars 1850 and 1950, which are not currently displayed on the map. 

Using the remove selected items button, remove all the dot symbols, just keep the 4-5 one. Further remove the Band 1 item. Next, we'll change the labels that appear on the legend. Double click the 1750, which will allow you to change the **Legend Item Properties**. Type The world in 1750, and press return. Change all the legend labels, here's what I've done. 

![Image 23](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/23-Tutorial-2.png)

Finally, we'll edit the gradient of our crop coverage. Double click the gradient. Change the Height to 40mm. Under Labels, Change Minimum to Low Cultivation, and Maximim to High Cultivation. These labels make more sense than abstract numerical values. Go back. 

![Image 24](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/24-Tutorial-2.png)

Scroll down in the **Legend panel**. You'll notice you can edit the fonts, spacing, position, rotation, and much more. Under Symbol, I'm just going to untick the **Draw stroke for raster symbols** option, and untick the **Background**. 

Finally, using from the toolbox, click the **Select/Move items** feature to move your **Legend** around, and make some final adjustments. 

This is what my map looks like! 

![Image 25](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/25-Tutorial-2.png)

Now we'll export this as an image. Go to **Layout > Export as Image**. Give your file a name and location, and save it. 

That's it for the 1750 map. Now we'll want to do the same for the 1850 and 1950 map. 

![Image 26](/Mapping-Global-Foodscapes/assets/img/Tutorial-2/26-Tutorial-2.png)

Go to **Layouts > Layout Manage**r. Rename your layout 1750, and create a duplicate called 1850. 

Now make sure your on the 1850 layout. Go back to your map project file (remember, that's the one where you add data and change the properties). From there, unclick the 1750 group, and click the 1850 group. **Right click > Zoom to Group**. Return to the 1850 layout manager. Click **Select/Move Item > click the Map and in the Main Properties**, click **Refresh**.

The data will change, but so will the Legend. We'll just delete the legend for now. Click the legend, and back space to delete it. 

Now we'll export the 1850 map as an image. Go to Layout > Export as Image. Give your file a name and location, and save it. 

Back to **Layouts > Layout Manager**. Create a duplicate called 1950, and follow the same steps above to make an image of the 1950 map. 

Onto the very last step.

## Add all 3 maps together 

Open the [Google Slides Ouput deck](https://docs.google.com/presentation/d/1UjSgS-SyFlNnhPNvhzY9OqhjWUD77j7W-kwhR0G1xJs/edit#slide=id.p) and add your three map images together like I've done. Include the years and your name using the text tool.

That's it! Until next time! 


































 