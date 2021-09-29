# Tutorial 4
-------------------------

## Tutorial 4: Downloading your own Datasets

## Objectives: 

To learn how to fetch data online, and create a chloropleth map of global calorie supplies from 1961- the present. The data we will be using is originally gathered by FAO (Food and Agriculture Organization), and is processed by [Our World in Data](https://ourworldindata.org/food-supply#data-quality-definition).

## Setup: 

Download the datasets for [Tutorial 4](https://drive.google.com/drive/u/0/folders/1VbTYjmMWf-QU5HSvEjqAw4HZ7svzv69W). 

Open QGIS, and start a new project file. Save it in your designated folder. Remember! Always keep your files well structured. Set your project Coordinate Reference System (from the bottom right corner) to WGS 84 (ESPG:4326).

## Downloading an online dataset:

Go to the Our World in Data’s [Food Supply](https://ourworldindata.org/food-supply) page. 

![Image 1](/Mapping-Global-Foodscapes/assets/img/Tutorial-4/1-Tutorial-4.png)

Scroll down to calorie supply by region. Explore the existing visualization, and then press download, and click of food-supply-kcal.csv 

Go to your Google Drive, and upload the food-supply-kcal.csv sheet. Open it with Google Sheets. 

![Image 2](/Mapping-Global-Foodscapes/assets/img/Tutorial-4/2-Tutorial-4.png)

Note the data structure of the sheet. There is a column showing Entity, Code, Year and Food Supply. For processing purposes, you want to export a sheet showing food supply in 1961, and one for 2017. To do that, you want to use the filter. 

![Image 3](/Mapping-Global-Foodscapes/assets/img/Tutorial-4/3-Tutorial-4.png)

On the top toolbar, click the filter icon, and press create new filter. 

Then, click cell C1 (Year), and in the drop down menu, first click clear all, then search for 2017, tick it, and press ok. 

Now, you only have values for 2017. You want to copy the entire dataset: Command+A to select all, then Command+C to copy. 

![Image 4](/Mapping-Global-Foodscapes/assets/img/Tutorial-4/4-Tutorial-4.png)

At the bottom left corner of the sheet, click add sheet, and name it Food-Supply-2017. Then press on cell A1, and paste it. 

Go to File > Download > Download Comma-Separated File. Rename the file Food-Supply-2017, and place it in Tutorial 4 folder. 

In the spreadsheet, repeat the filter steps to get food supply for 1961, create a new sheet, paste it there, and download the CSV. Rename it Food-Supply-1961. 

## Visualizing Food Supply in QGIS 

Head to QGIS. I’ll give brief instructions, but you can refer to [tutorial 3](https://nf2337.github.io/Mapping-Global-Foodscapes/tutorial3) if you need more help with more detailed steps. 

1) Set your CSR to WGS 84 (it should also be on default) 

2) Layer > Add Vector Layer, and add World-Map. 

3) Layer > Add Delimited Text Layer > add your datasets Food-Supply-2017 Make sure you have No geometry defined. Repeat this for the Food-Supply-1961. 

4) Open the Properties of the World-Map, and perform a table join. Remember to consider what field will create the match. In this case, ISO_A3 and Code. You’ll have to do this for both Food-Supply-2017 and Food-Supply-1961. 

5) Duplicate the World-Map layer 3 times. Rename the layers: Basemap, Food-Supply-2017, and Food-Supply-1961.

6) Open the Properties of the Food-Supply-2017 vector world map. In Symbology, change the settings to Graduated, identify the Value (Calories) and change the Color Ramp. Chose your Mode, and click Classify, then ok.

7) Open the Properties of the Food-Supply-2017 vector world map. In Labels, chose rule-based labeling. Add a new rule. Open the filter calculator, and type the following, replacing FIELD-NAME with the name of your calorie field, which can be identified from fields and values: 
```
"FIELD-NAME" <= 2500
```
This means that a name will appear for countries where food supply is less than 2500 kg/person/day. You can also change the 2500 value. 

For Value, choose NAME, and change the styling. 

8) Repeat steps 6 and 7 for the Food-Supply-1961 world map. 

9) Right click the World Map, and press Zoom To Layers. With only the Food-Supply-2017 layer and the Basemap enabled, go to Project > Export > Export map as Image, and save it. Now go back, and only enable Food-Supply-1961 layer and the Basemap, and repeat the export. 

Now you have exported two separate maps. 

10) On Google Slides [Tutorial 4 Output](https://docs.google.com/presentation/d/1wQQ1f1jhq3TsfDewPWGO3PUGnwKnoPe2EQ4e_IXtRs4/), add your two maps, and include a title and labels. You can also do this processing in Photoshop or Illustrator. 
