# Tutorial 7
-------------------------

## Mapping Census Data (Optional)

## Objectives: 

The ojectives of this tutorial is to use **Social Explorer**, a platform for easy access to demographic information about the United States to download data from the census. Bard College Libraries provides access to Social Explorer through the [library resources](https://blogs.bard.edu/library/social-explorer/). 

## Exploring Social Explorer

Head to the [Social Explorer](https://blogs.bard.edu/library/social-explorer/) through the Bard Libaries page. Please take a moment to log into your account, using the G Mail log in with your bard Username and Address. You will be forwarded to this page. Please make sure that you've accessed your account, so you can save your queries and tables, then Click Explore to begin. 

![Image 1](/Mapping-Global-Foodscapes/assets/img/Tutorial-7/1-Tutorial-7.png)

With the launch of the interface, you'll be directed to a page that by default maps Population Density. You'll be able to change several parameters of the dataset, including the actual data, the geography level of the data (visualized by state, county, census tract, amongst others), and the display styles (using shaded area, bubbles, or dot density). These will depend on the type of data that you'll be visualizing. As you will see, the interface is very robust, and will allow you to explore a vast array of demographic attributes. You can work on as many exploratory maps as you want, and when you're ready, you can chose to download the data and open it directly in QGIS for more visualization and customization capabilities. 

![Image 2](/Mapping-Global-Foodscapes/assets/img/Tutorial-7/2-Tutorial-7.png)

Go ahead and click **Change Data** and explore the options available to you. There are a lot of datasets you can chose from, and you might want to spend the time looking at ones that are relevant for your respective projects and interests. 

For now, we'll download some income data. Click on **Income** for the year 2019, the latest available data for the US Census. You are going to get several options that look like this: 

![Image 3](/Mapping-Global-Foodscapes/assets/img/Tutorial-7/3-Tutorial-7.png)

**ACS** stands for [American Community Survey](https://www.census.gov/programs-surveys/acs/about.html) collects a vast array of information including income, education, employment, transportation, housing which are vital for local and national leders to decide on programs, economic development, emergency management and other local issues. The ACS colects a sample of responses, and unlike the **Deceniial Census** conducted every 10 years (the latest in 2020), it does not count every person single person, but rather produces estimates based on sampling. 

Because the ACS doens't actually count people, but rather produces estimates based on sampling, you can chose between the **1-year estimate**, and the **5-year estimate**. 

How do you decide which estimate to use? It's really up to you, but consider the following: "the 1-year estimates for an area reflect the most current data but they have larger margins of error than the 5-year estimates because they are based on a smaller sample. The 5-year estimates for an area have larger samples and smaller margins of error than the 1-year estimates." A more technical note on the difference can be found [here](https://www.census.gov/content/dam/Census/library/publications/2018/acs/acs_general_handbook_2018_ch03.pdf). 

I will just use the **5-year estimate** for nowI'll chose the **Median Household Income (In 2019 Inflation-Adjusted Dollars)**.

![Image 4](/Mapping-Global-Foodscapes/assets/img/Tutorial-7/4-Tutorial-7.png)

Now we'll take a look at different geography levels of the data. If you click **County**, New York City will be divided into five polygons: Bronx, New York, Kings, Queens and Richmond counties (Kings county is the name for Brooklyn!, Richmond County is the name for Staten Island). However, the **Census Tract** level gives a far more granular look at income in New York City, allowing you to more closely consider geographies of inequality. 

## Downloading Census Data 

Now that we've chosen our varialbe, we want to download the data. You can export your map as an image (using the top right corner icon). However, we want to download a **report** which typically comes in the form on a .csv file. Click the **dropdown menu > Create report.**

![Image 5](/Mapping-Global-Foodscapes/assets/img/Tutorial-7/5-Tutorial-7.png)

For **Create report from**, chose **Current table selection**, and for **Geography** switch to **County**, and click on the Bronx, New York, Kings, and Queens Counties. (we'll ammend this to include all the census tracts of New York City in a second). Press Create. 

![Image 6](/Mapping-Global-Foodscapes/assets/img/Tutorial-7/6-Tutorial-7.png)

From your report page, click on **Geography**, then under **Select a Geographic Type** click **140 .... .... Census Tract**, for **State** Select New York, and then select **Bronx County, New York**, and then double click on **All census tracts in Bronx County, New York** to add it. You'll have to go back, change the **County** to Kings County, and select **All census tracts in Kings County, New York**. Do the same for New York County, Queens County, and Richmond County too. 

![Image 7](/Mapping-Global-Foodscapes/assets/img/Tutorial-7/7-Tutorial-7.png)

Once you are done, your **Current Geograhy Selection** should look like this. Then from the top toolbar, go to **Proceed to results**. 

![Image 8](/Mapping-Global-Foodscapes/assets/img/Tutorial-7/8-Tutorial-7.png)

Finally, just scroll down, and download the **Census Tract data (CSV)**. Move your downloaded file into your desktop Tutorial 7 folder, and rename it Median Income. 

![Image 9](/Mapping-Global-Foodscapes/assets/img/Tutorial-7/9-Tutorial-7.png)

## Accessing Census Data in QGIS 

To access census data CSV in QGIS, you will need to download a **Shapefile** comprised of Census Tracts polygons for QGIS. This can be found on the [NYC Open Data website](https://www1.nyc.gov/site/planning/data-maps/open-data/census-download-metadata.page). Download the first **2020 Census Tracts (Clipped to Shoreline)**. Save it in your Tutorial 7 Folder. 

Now open QGIS, and start a Tutorial 7 folder. Add the Census Tracts (Layer > Add Layer > Add Vector Layer). Click ok when your prompted with the transformation notice. 

Then, add the Median Income CSV (Layre > Add Layer > Add Delimited Text Layer). Hint: Make sure that under Geometry Definition, you click **No Geography**.

Now, to visualize the median income, you'll have to join it to the census tract shapefile. To perform a table join (remember, (tutorial 4)[https://nf2337.github.io/Mapping-Global-Foodscapes/tutorial4)?], you'll need to find a common attribute in both datasets. 

Open the attributes table of the csv and the shp files, and take a quick look. It seems that the **GEOID** from **NYC-Census-Tracts dataset** matches the **GEO-FIPS** from the **Median-Income** dataset. 

![Image 10](/Mapping-Global-Foodscapes/assets/img/Tutorial-7/10-Tutorial-7.png)

To join tables, left click **NYC-Census-Tracts** > Properties > Joins. Click the add (+ icon), and define the following parameters: 

![Image 11](/Mapping-Global-Foodscapes/assets/img/Tutorial-7/11-Tutorial-7.png). 

Go back to the attributes table of **NYC-Census-Tract**, and explore the data. You have many fields, but the last one, **INCOME_SE_SE_A14006_001** contains information on the **median income**. 

![Image 12](/Mapping-Global-Foodscapes/assets/img/Tutorial-7/12-Tutorial-7.png).

Finally, duplicate the **NYC-Census-Tracts**, and rename one basemap. Then open the **NYC-Census-Tracts > Properties > Symbology**, and visualize your data using **Graduated Symbols** with the value **Median-Income_SE_A14006_001**, using **Natural Breaks (Jenks)** for Mode. Change your map styles. Here's what I got: 

![Image 13](/Mapping-Global-Foodscapes/assets/img/Tutorial-7/13-Tutorial-7.png).

To improve the viewing experience, I want to add an outline around each borough. To do that, I need a shapefile just for each borrough of Manhattan, Brooklyn, Bronx, Queens and Staten Island. I can produce this shapefile from my census tract shapefile using the **Dissolve** tool, which allows you to merge a shapefile based on a common field. 

If you open the attributes table of the **NYC-Census-Tract**, you'll notice that the third field lists the **BoroName** - which we'll use as the common field.

Go to **Vector > Goeprocessing Tools > Dissolve**. Click the [...] selection next to **Dissolve fields(s) [Optional]**, then select **BoroName**, return, and Run it. 

![Image 14](/Mapping-Global-Foodscapes/assets/img/Tutorial-7/14-Tutorial-7.png).

Your going to get a new shapefile called **Dissolve**. Open its Properties > Symbology, make the fill transparent, and increase the outline stroke. Make sure that **Dissolved** is at the top of your Layer Panel. 

This is what my map now looks like. Export the map (Project > Import/Export > Export Map as Image). 

![Image 15](/Mapping-Global-Foodscapes/assets/img/Tutorial-7/15-Tutorial-7.png)

