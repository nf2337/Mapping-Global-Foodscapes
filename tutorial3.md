# Tutorial 3
-------------------------

## Tutorial 3: Mapping Flow

## Objectives: 

This tutorial aims to introduce ways of mapping flows (of people and goods) through QGIS. We’ll be following tomatoes through the people that make them and others that consume them - building on Keller Easterling’s piece, [Tomato World](https://www.jstor.org/stable/i24323420).  In the process, we’ll be downloading and processing diverse datasets on migration from the [Migration Policy Institute](https://www.migrationpolicy.org/programs/migration-data-hub?qt-data_hub_tabs=1#datahub-tabs) and on trade from the [Organization for Economic Complexity](https://oec.world/).

## Setup: 

Download the datasets for [tutorial 3](https://drive.google.com/drive/folders/1j0DYACcxkfmfbSWEjYm542Wpw1XNJnOA). 

Open QGIS, and start a new project file. Save it in your designated folder. Remember! Always keep your files well structured. Set your project Coordinate Reference System (from the bottom right corner) to **WGS 84 (ESPG:4326)**.

## Performing Table Joins: 

In [Tutorial 2](https://nf2337.github.io/Mapping-Global-Foodscapes/tutorial2), we learned that CSV sheets (tabular data) can easily become vector datasets of points, lines and polygons if they contain some spatial information. Remember: we used a csv file containing the Latitude and Longitude coordinates to visualize the size of cities. 

In this tutorial, we’ll look at another way to turn tabular data into maps through table joins. When you have a vector file and a .csv file with a common attribute field, we can join them so that the tabular data of your .csv is added to the attribute data that is defined spatially through the vector file. Confused, let’s see how this works. 

## Adding the datasets: 

Go to **Layer > Add Vector Layer** and chose your World-Map. 

Then, go to **Layer > Add Delimited Text Layer** and add your **Spain-Immigration.csv file**. Note that under **Geometry Definition**, you want to keep it at **No geometry** (attribute only table). 

![Image 1](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/1-Tutorial-3.png)

## Exploring the datasets: 

Right click each layer, and **Open Attribute Table**. 

![Image 2](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/2-Tutorial-3.png)

Let’s first explore the Spain-Immigration table. This was downloaded from [here](https://www.migrationpolicy.org/programs/data-hub/charts/immigrant-and-emigrant-populations-country-origin-and-destination/), and processed in Google Sheets (which we’ll learn about in a second). 

You’ll notice there are 10 rows of data, each representing the number and percentage of migrants going from the origin (Morocco, Romania, Colombia, etc) to one destination, Spain. Note that the percentages don’t add up to 100, this is because I’ve selected from the original dataset only the top 10 migrant flows to Spain. 

Next, consider the **World-Map**. It contains only names and ISO (International Organization for Standardization) country codes. 

The ISO is an attribute of both the World-Map (a vector file), and the **Spain-Immigration** (a .csv) file. Based on this shared attribute, we can join the datasets, and start visualizing the migration information on a map. 

## Table Joins: 

In the Layers Panel, right click the **World-Map > Properties > Joins**. Click + and choose the below settings: 

![Image 3](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/3-Tutorial-3.png)

Join layer is the layer we’re joining to our vector map. This will be **Spain-Immigration**. Join field is the shared attribute from the table. We’ll chose **Origin ISO**. Target field is the shared attribute from the vector. We’ll choose **ISO_A3**. Click Ok. 

To see the results, we’ll go back to the Layers Panel, right click the World-Map > Open Attribute Table. 

![Image 4](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/4-Tutorial-3.png)

Notice that the fields from your .csv file, Spain-Immigration, are now part of the **attribute table** of the **World-Map** vector file. This is the result of our table join. 

Now, rearrange your table by double clicking on the header of the Immigration_Destination, and all the top ten countries with migrants to Spain have appeared. Note that the NULL values are given to all other countries. That’s fine!

A small step here. Double click on the **Immigration_Migration-Percentage** field. You’ll notice that QGIS doesn’t arrange the numbers properly. This is because it’s currently registered our numbers as text. We’ll need to recalculate these fields. 

Go back to the Layers Panel, right click the **Spain-Immigration**, and **Open Attribute Table**. Click the **field calculator** at the top. For Output field name, write **Migrant-Value**. For Output field type, choose Decimal number (real). In the right hand corner, scroll to Fields and Values, then double-click **Spain-Immigration_Migrant_Value** so that it appears in the Expression window. Press Ok. 

![Image 5](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/5-Tutorial-3.png)

Now, do this again for the percentage field. In the Output field name, put Migrant-Percent, in the Output field type chose Decimal number real, and from the Fields and Values, find Spain-Immigration_Migrant_Percent and double-click it so that it appears in the Expression window. Press Ok.

Now that we’re done, we’ll just delete the fields we don’t need. Click the Delete Fields button at the top. Highlight Migrant_Value and Migrant_Percent, and click ok. 

![Image 6](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/6-Tutorial-3.png)

Go back to the Layers Panel, right click the **World-Map > Open Attributes Table,** and see the changes reflected there. Notice, that the .csv Spain-Immigration and the vector World-Map are dynamically linked. 

Visualizing Migration Data 

We’ll make a quick chloropleth map of migrants into Spain. Right click World-Map > Properties > Symbology. 

Try to do this alone, recalling the steps for graduated symbology we learned in [tutorial 1](https://nf2337.github.io/Mapping-Global-Foodscapes/tutorial1).

Need some help? Make changes reflected below: 

![Image 7](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/7-Tutorial-3.png)

Notice that you’re only displaying the top 10 countries from which migrants to Spain originate. If you want to display the rest of the world, that’s easy. 

From your Layers Panel, right click World-Map, and duplicate the layer. Rename it basemap. Now, right click **Basemap > Properties > Symbology, and revert to Single Symbol**, and change the fill. I changed mine to diagonal lines. 

Here’s what you should have so far. 

![Image 8](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/8-Tutorial-3.png)

## Mapping Flow

Please note that this part of the tutorial is from Anita Graser’s [Free and Open Source GIS Ramblings](https://anitagraser.com/2019/05/04/flow-maps-in-qgis-no-plugins-needed/)

What if, instead of a c**hloropleth map**, I want actual arrows showing the flow to Spain. Let’s look at how to do that! 

First, we’ll need to turn out polygons of countries into a series of points, from which we can map flow. For this, go to **Vector > Geometry Tool > Centroids**. For **Input Layer**, choose the Basemap, then Run it. 

![Image 9](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/9-Tutorial-3.png)

Now you have an additional layer called **Centroids**, which is dots that QGIS has placed in the middle of each country polygon. 

Go to **Layers > Add Layer > Add/Edit Virtual Layer**. Here, we’ll instruct QGIS to make a series of lines connecting the dots to reveal migration flows.

Copy and paste the below into the Query, the click Add:

```javascript 
SELECT Origin_ISO, Destination_ISO, Migrant_Percent1,
       make_line(a.geometry, b.geometry)

FROM 'Spain-Immigration'

JOIN 'Centroids' a ON 'Spain-Immigration'.Origin_ISO = a.ISO_A3

JOIN 'Centroids' b ON 'Spain-Immigration'.Destination_ISO = b.ISO_A3

WHERE a.ISO_A3 != b.ISO_A3
```

![Image 10](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/10-Tutorial-3.png)

While this query looks complicated, it’s telling QGIS to make lines between points, connecting the **Origin_ISO** to the **Destination_ISO**, and adding the **attribute Migrant_Percent**, showing the percentage of migrants from each country of origin (we’ll use this to visualize the data in a second). 

Re-arrange your layers to bring the new virtual_layer to the top, and this is what they should look like. 

![Image 11](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/11-Tutorial-3.png)

Your **virtual_Layer** is temporary, so before we go on to styling, you’ll want to save it as a geoJSON. Right click the **layer > Export > Save Features** As. Give your file a name and location, make sure the CSR is defines as WGS 84, and save it. Now remove the virtual_layer, and keep the permanent **Spain_Immigration_Flow layer**. 

![Image 12](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/12-Tutorial-3.png)

Let’s style. Right click the **layer > Properties > Symbology**. Keep it at Single Symbol, click Simple Line, and for Symbol layer type, change to Geometry Generator. 

![Image 13](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/13-Tutorial-3.png)

Copy paste the following into the equation. This will simply make your lines bend. For **Geometry type**, chose **LineString / MultiLineString**.

```javascript 
difference(
   difference(
      make_line(
         start_point($geometry),
         centroid(
            offset_curve(
               $geometry, 
               length($geometry)/-5.0
            )
         ),
     end_point($geometry)
      ),
      buffer(start_point($geometry), 0.01)
   ),
   buffer(end_point( $geometry), 0.01)
)
```

![Image 14](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/14-Tutorial-3.png)

Then, click the **Simple Line** indicated above, and in **Symbol layer type**, change to arrow. Here, we’ll use our data to make the arrow width correspond to the percentage of migrants from each country. This will take a second. 

For each of **Arrow width, Arrow width at start, Head length and Head thickness**, right click the dropdown menu on the right, and choose Assistant. 

In assistant, you’ll chose the source as **Migrant_Percent1**, click refresh. This indicates that the value is pulling from your percentage of migrants. Then add size from 0.5 to 7, and change scale method to Linear.

![Image 15](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/15-Tutorial-3.png)

You’ll have to do this for all four categories. Now, you’re almost done. Click on the **Simple Fill**. Remove the stroke (No Pen), and change the color and opacity. Using apply, check that everything is working. If yes, be sure to save your style, and call it **Spain-Flow-Style**. 

![Image 16](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/16-Tutorial-3.png)

Now your map is almost complete. We’ll just change the points so they reflect only our 10 countries of interest. 

From the Layers Panel, right click the **Centroids layer > Properties > Symbology**. Then change the symbology to Rule-based. There, Add a rule. In the filter, paste the following formula  then change the styling: 

```
"Spain-Immigration_Migrant_Percent1" >= 0
```

![Image 17](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/17-Tutorial-3.png)

Then, we’ll also add some labels. Go to Labels > Rules based Labeling. Add a rule. For the formula, we’ll add this:  
``` 
"Spain-Immigration_Migrant_Percent1" >= 0 
``` 
For the Value, we’ll do something special to display the Name and the Number of Migrants. Copy the below into the value tab, then continue styling as usual. 
```
"NAME"  || '\nNumber of Migrants: ' ||  "Spain-Immigration_Migrant_Value1" 
```
![Image 18](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/18-Tutorial-3.png)

Great. We’re done. Here’s what my map looks like! 

![Image 19](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/19-Tutorial-3.png)

## Finding data on Spain’s Tomato Export: 

Now it’s time we learn how to find, download, and edit our own data for QGIS. Go to the Observatory of Economic Complexity [Website](https://oec.world/), and explore the data. There is a TON of information on here. You might want to use the search button on the top right, to search Spain Tomato. As you can see, there are still many options that can allow you to explore Tomatoes or a range of other derivative or processed products. We’ll just click Tomatos and Spain. You can scroll through this page, which has a large amount of data. Find your way to the visualization that shows you Where Spain Exports Its Tomatos To (2019). If you get lost, just follow this [link](https://oec.world/en/visualize/tree_map/hs92/export/esp/all/20702/2019/). Click Download, then Download CSV. 

![Image 20](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/20-Tutorial-3.png)

Unzip the downloaded folder, and you’ll have a .csv file. Add it to your Google Drive, and then open it in sheets so we can edit it. 

Let’s take a look, and remove all the columns we don’t need. Right click the columns we don’t need, and click delete. I would delete Continent, Continent ID, Country ID, and Year.

![Image 21](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/21-Tutorial-3.png)

## Editting in Google Sheets

Now, we’ll do some more edits to ease processing the dataset. QGIS is case sensitive (ie. It differentiates between uppercase and lowercase text). Your ISO 3, the country codes, are in lower case, which will be an issue for the table join. So, let’s convert them to upper case. In cell D2, paste this formula:`=UPPER(B2)` 
 
Now drag to apply it to all the columns. Great. In cell D1, name this column Destination_ISO. Copy the whole column, and right click > Paste Special > Paste values only. Delete all of column B (lower case ISO_3), we don’t need it anymore. 

Note that QGIS doesn’t like to work with spacebars, so avoid them in the attribute headers. Change cell C1 to Trade_Value (replace the space with an underscore). 

Finally, we want to calculate the percentages. In G1, calculate the total of all tomato exports using the following formula, `=SUM(B2:B67)`

Then, in D1, name your attribute Trade_Percent. Then, calculate the percentage by starting from cell D2, using the formula `=(B2/1091558740)*100`
Drag down to get all the values. 

Now, go to View > Freeze > 1 row. Then, on Column D (Trade_Percent), click the arrow that pops up on the right, and Sort Sheet Z > A. 
 
Take a look at the percentages, and make a decision as to how many of these are relevant to show on your map. Perhaps, you’ll chose, like I did for the migrant origins, to keep only the top 10 countries. I’ll chose 10. Delete all rows from 12 downward. 

Lastly, for the flow diagram to work properly, we need to identify the Origin, which in this case is Spain. Add a Column called Origin_ISO, and change all the values to ESP. 

Go to **file > Download > Download Comma separated value.**

Rename you new .csv Spain_Tomato_Export and put it in the folder for tutorial 3. Now. You’ll do all the same steps from Mapping Flow to make this into another set of flows. I’ll help you with the first steps. 

## Mapping Export Flows 

Back to QGIS.

1) **Layer > Add Layer > Add Delimited Text Layer**, and navigate to your Spain_Tomato_Export file. 

2) Open the **Attribute Table**, and recalculate the Trade_Value and Trade_Percent using the Open Field Calculator. Then delete the unneeded attributes. 

3) **Layer > Add Layer > Add Virtual Layer**. In the Query, add the following. Note that I am changing some things.

```javascript 
SELECT Origin_ISO, Destination_ISO, Trade_Percent1,
       make_line(a.geometry, b.geometry)

FROM 'Spain-Immigration'

JOIN 'Centroids' a ON 'Spain-Immigration'.Origin_ISO = a.ISO_A3

JOIN 'Centroids' b ON 'Spain-Immigration'.Destination_ISO = b.ISO_A3

WHERE a.ISO_A3 != b.ISO_A3
```

4) Save your virtual layer as a **GeoJSON** called Spain_Tomato_Flow 

5) Open the Properties of **Spain_Tomato_Flow > Symbology > Load Style**. The only thing you’ll need to change is in **Arrow > Arrow width, width at start, head length and head thickness**, using the **Assistant**. There, change the source from Migrant_Percent1 to Trade_Percent1.

You may want to also duplicate the **World-Map**, **Join tables with the tomato**, reproduce the centroids, change the symbology and labels, etc. 

![Image 22](/Mapping-Global-Foodscapes/assets/img/Tutorial-3/22-Tutorial-3.png)

The central issue is that there is scalar. Migrants are coming to Spain most from Morocco, Romania, and countries in South America and the Caribbean. While Spain is producing Tomato (along with other fruits and vegetables), predominantly for the European Union. You’ll want to export your maps at different scales, and somehow arrange them to make a point about the scale and geographies of flow that make the Spanish tomato placeless. 

You can use this [Nuclear War Atlas](https://www.leventhalmap.org/digital-exhibitions/bending-lines/why-persuade/1.9.1/) for reference. 

Brainstorm what else you can add? For example, you can try to add the evolution of Almeria, Spain from [Google Earth Timeline](https://earthengine.google.com/timelapse).

You can also explore adding more datasets from [FOASTAT](http://www.fao.org/faostat/en/#data).