# Tutorial 6
-------------------------

## Tutorial 6: Scraping Online Data Sources

## Objectives: 

The objectives of this tutorial will be to scrape data from online sources. There's an abundance of crowdsourced, collated, and categorized information on the internet. By scraping it, we'll be arranging it in a format that can be useful for mapmakers using GIS. We'll be making a map of falafel sandwiches in New York City based on information collated from online review networks, ordering sites, and menus. We will collectively compile a spreadsheet of data as a class, and each person will work on visualizing it in their own style. 

## Collecting online data about the Falafel Sandwich

[Tripadvisor](https://www.tripadvisor.com/) contains a wealth of information on food and culinary culture around the world. We'll be using it to compile some information on where to find a falafel sandwhich in New York City. 

In our tutorial 6 [spreadsheet](https://docs.google.com/spreadsheets/d/1H6bo_tP0rbHGjSrb5ByytfRF5RzoJUb2imZA-i3zyK8/edit#gid=0), I've compiled a list of restaruants tagged as "Middle Eastern" in tripadvisors. Every name of the restaurant also includes a link to the tripadvisor page. As a sample, I visited individual pages of restaurants to gather information about the name and address of the restaurant, the type of cuisine, the way they advertise their falafel sandwhich, and its price. 

Under the Student column, each of you has been assigned 8 restaurants to investigate. Click on the name to open the tripadvisor page. Please fill in the columns, noting wehther the restaurant is noted as Middle Easter, Israeli, Lebanese, or Fast Food, or any combination of the above designations. Fill in the address of of the restaurants. Then, visit the menu site (you might need to go the restaurant's webpage, or to UberEats or Grubhub to view this), search for their falafel sandwich (or variation, like falafel burger, pizza or taco), and note the name of the food item, its description, and the price. 

## A few notes: 

![Image 1](/Mapping-Global-Foodscapes/assets/img/Tutorial-6/1-Tutorial-6.png)

Here's the page for Mamoun's Falafel. At the top, you'll find the tags used to designate the restaurant. Mamoun's doesn't appear to be either Israeli or Lebanese, therefore fill these tags as "no". It is designated as a fast food restaurant, so in the fast food column, type "yes". 

Copy the address. Make sure that it's in the following form (this is important for **georeferencing**):
```
Number, Street, New York City, NY ZIP
```
Then, click on the webisite or menu, and explore it a little. Read about how the restaurant advertizes itself, noting how it engages with questions of gustatory identity and flavor. What demographic or class does it appear to speak to? Who is the target clientelle? What cultural elements can you identify from the design, images, and text? 

Please complete this by Monday, 25th. We'll need all the class entries to work on our map. Once all the entries all filled out, go to File > Download > Comma-seperated values. Store the .csv sheet in your Tutorial 6 folder. 

## Visualizing the Falafel Sandwich on a map of NYC 

Open QGIS, and set your project Coordinate Reference System to WGS 84 Pseudo-Mercator (EPSG:3857). This is a useful projection for making local maps at the scale of New York City. 

Next, let's add a basemap. Go to Web > OpenLayers plugin > OpenStreetMap > OpenStreetMap. Make sure the basemap is added in your **Layers Panel**. 

In previous tutorials, we worked .csv sheets in a number of ways to make point and polygon visualizations. Recall in tutorial 2, we visualized the cities based on their latitude and longitude coordinates, attributes that place location based on the Global Positioning System (GPS). Further recall in tutorial 4, we visualized a tabular dataset of average calorie intake by using the table join method. In this tutorial, we are working with tabular data that contains the address of restuarants selling falafel sandwiches in NYC. QGIS can automatically georeference addresses as points on a map, we just need to quickly install a plugin. 

## Georeferencing addressed with MMQGIS Plugin 

Go to Plugins > Manage and Install Plugins. Search for **MMQGIS** and install it. 

![Image 3](/Mapping-Global-Foodscapes/assets/img/Tutorial-6/3-Tutorial-6.png)

Next, let's add your .csv file of Falafel sandwich shops. Go to MMQGIS > Geocode > Geocode CSV with Web Service. Open the path to your .csv file. Under Address, note the address field. For Web Service, choose OpenStreetMap / Nominatom, and click apply. 

![Image 4](/Mapping-Global-Foodscapes/assets/img/Tutorial-6/4-Tutorial-6.png)

Now you have all the restaurants as points on your map. This is what it should look like. Note that your points are in a temporary file. To save it, right click temp in the Layers Panel > Export > Export features as, and save it as geoJSON in your Tutorial 6 folder. 

## Categorizing Falafel Shops in New York City 

Now, it's your chance to make a map that communicates a message. You may want to categorize your falafel shops based on what cuisine they fall under, whether they are fast food or sit down restaurants, or based on price. 

You can do all this in Properties > Symbology. You may also chose to add labels to your restaurants, from Properties > Labels. 

Hint: If you want to add a label that includes the name of the restaurant, and the price of the sandwich, you can use the following expression for the **value** of your label: 

```
"Restuarant"  || '\n$' ||  "Price" 
```

## Exporting your map 

We'll return to use the **Layout Editor** in QGIS, because we want to add a legend to our map. 

Go to Project > New Print Layout, and call it Tutorial 6. 

Add the map using the **Add Map** button on the left hand side, then change the scale of the map and the **Map Properties** panel on the right and the **Move Item Cotent** button on the left. 

![Image 5](/Mapping-Global-Foodscapes/assets/img/Tutorial-6/5-Tutorial-6.png)

Then, add the legend using the add legend tool on the left. 

You can change the legend properties from the Item properties panel. Unclick the auto update function, and then double click each item to change its name. You may also remove the basemap from the legend. 

Finally, edit the fonts, and make the background slightly opaque, and make any stylistic changes. 

![Image 6](/Mapping-Global-Foodscapes/assets/img/Tutorial-6/6-Tutorial-6.png)

Once you are done, go to Layout > Export as Image. Save your map, and upload it to the [Tutorial 6 folder](https://drive.google.com/drive/u/0/folders/1xPe0Bdca06R02FTqnUnBSivohygAKkNs).



