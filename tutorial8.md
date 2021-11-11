# Tutorial 8
-------------------------

## Making Satellite Grids (Optional)

## Objectives: 

The ojectives of this tutorial is to use the **Google Static Maps API** to generate satellite grids. We'll briefly go over a how to use a python script that will automate the process of downloading satellite images of locations from a dataset of latitude and longitude coordinates. 

(Note: this tutorial, including the python code, is adapted from [Dare Brawley, CSR](https://centerforspatialresearch.github.io/methods-in-spatial-research-fa2021/tutorials/tutorial05b/)). 

## Exploring uses of Satellite Grids

Satellite grids are visually powerful ways to communicate ideas about the physical features of the world as seen by Satellites, and to comparatively play with a sense of scale. The following tool is used to make a diverse array of projects and cartographic interventions. Some projects you might want to explore for inspiration include:  

Center for Spatial Research's [In Plain Site](https://c4sr.columbia.edu/projects/plain-sight),
Josh Begley's [Best of Luck with the Wall](https://vimeo.com/189004719),
Eames Office's [Power of Ten](https://www.youtube.com/watch?v=0fKBhvDjuy0), 
and Tricontinnental's map of US Military Bases in Africa below:

![Image 1](/Mapping-Global-Foodscapes/assets/img/Tutorial-8/1-Tutorial-8.jpeg)

In this tutorial, I'll use satellite grids to make a map of supermarkets and farmers markets in Ulster and Dutchess Counties, NY. 

## Satellite Grids using the Google Static Maps API

API stands for Application Programming Interface, and its basically an intermediary interface that will allow you to automatically access information encoded in Google Maps. Although you can manually produce satellite grids through capturing screenshots from Google Maps, using the API will automate the process and allow you to swiftly grab satellite images from a set of points (latitude and longitude coordinates) at unified scale (zoom level). 

To use the Google Static Maps API, we need to run some Javascript, a popular programming language (don't worry, you'll be provided with all the code you need). Javascript needs to run in an environment, and we'll use [Google Colab](https://colab.research.google.com/), a collaborative platform for executing code. 

Before we begin, we'll need to prepare our dataset in CSV format. The CSV needs to include **ONLY three columns**, the first is an ID (unique identifyer), the second is a latitude coordinate, and the third a longitude coordinate. 

I manually scraped the location of all Hannaford Supermarkets in Ulster and Dutchess Counties from Google. I made two seperate CSV sheets. The first, to run with the satellite grids, which contains **ONLY three columns**, and a second, with more information for QGIS. Save them both on CSV files. 

![Image 2](/Mapping-Global-Foodscapes/assets/img/Tutorial-8/2-Tutorial-8.png)

Next, we'll need to open [Google Colab](https://colab.research.google.com/). Click to start a **New Notebook**. 

Each box is a block of code. Use the **+ Code** to add two more block, for a total of three. 

![Image 3](/Mapping-Global-Foodscapes/assets/img/Tutorial-8/3-Tutorial-8.png)

In the first block of code, copy and paste the following (do not change anything!). This will import the scripts needed to execute the code (io and pandas), and will allow you to upload your CSV file. 

```
from google.colab import files
import io
import pandas as pd

# upload data
uploaded = files.upload()
for fn in uploaded.keys():
  print('User uploaded file "{name}" with length {length} bytes'.format(
      name=fn, length=len(uploaded[fn])))
``` 

Click **play** to run the code, and when prompted, upload choose your Hannafords CSV (with only 3 columns) to upload. Your notebook should look like this: 

![Image 4](/Mapping-Global-Foodscapes/assets/img/Tutorial-8/4-Tutorial-8.png)

Next, copy and paste the below in the second block, and click **play**

```
# required modules
import requests
import csv
from io import open as iopen

# functions needed
def locationreader(uploaded_filename):
  df = pd.read_csv(io.BytesIO(uploaded[uploaded_filename]), names=['id','lat','lng'])
  list_df = df.values.tolist()
  return(list_df)

# defining a function, it takes four parameters:
# the path to a csv file containing lat/lon coordinates
# your API key
# the zoom level you would your images to be downloaded as
# the size, in pixels of your images, the maximum is 640 
# unless you have signed up for a premium account

def satellite_squares_colab(uploaded_filename,APIkey,zoom,size):
    API_KEY = APIkey
    base = "https://maps.googleapis.com/maps/api/staticmap?scale=2&size="
    # this section reads the csv file
    locations = locationreader(uploaded_filename)
    
    # here we format a url to pass to the API for each row in the csv file
    for location in locations:
        ind, lat, lng = location
        latlng = "center={},{}".format(lat, lng)
        view = "zoom={}&maptype=satellite".format(zoom)
        keys = "key={}".format(API_KEY)
        url = "{}{}x{}&{}&{}&{}".format(base,size,size, latlng, view, keys)
        # defining the name for the image files that will be downloaded
        filename = "{}_{}.png".format(ind,zoom)
        print(url)
        print(filename)
        res = requests.get(url)
        if res.status_code == requests.codes.ok:  
            with iopen(filename, 'wb') as file:
                file.write(res.content)
            files.download(filename)
            print(filename)
        #here we tell the function to show us an error message if it is unable to download an image
        else:
            print(res.status_code)
            print(url)
            return False 
```

Lastly, copy and paste the below in the third block. 

Before you click **play**, you'll need to change "uploaded_filename" to the name of the CSV file you uploaded in the first block. The string of numbers is my Google Maps API Access Key, which you don't need to worry about. The third number, 18, is the zoom scale. This is a standardized number that shows the extent of your satellite square's coverage. You can explore more about zoom scales [here](https://wiki.openstreetmap.org/wiki/Zoom_levels). A zoom scale of 1 will show you the whole world, a zoom scale of 13 will capture roughly a village, and scale of 18 will cover some buildings or trees. You want to change this number depending on what you are trying to capture. The fourth number, 640, is the pixel resolution of your square grid. 640 is the maximum. After making your edits, run the third block, and your images will start to download. Note: you might need to enable your browser to download multiple images in one hit. 

```
satellite_squares_colab("uploaded_filename","AIzaSyC2fldKcC0kOiFyoC6yHZnOO6gt9PjOru8",18,640)
```

## Formatting Satellite Grids 

The images will download seperately, and they'll be given the name on the ID field (the first column). You can choose to arrange the images in a grid (I arranged them on Illustrtor, but you can use any software):

![Image 5](/Mapping-Global-Foodscapes/assets/img/Tutorial-8/5-Tutorial-8.png)

Another option is to include the Satellite Grids on a map. In my case, I made a QGIS map showing the Hannafords Supermarkets and Farmer's Markets in the area (using the geolocating CSV using lat and long coordinates method). Then I added a basemap using OpenLayers. I exported a pdf of the map from QGIS, and continued to edit the labels and satellite grids in Illustrator: 

![Image 6](/Mapping-Global-Foodscapes/assets/img/Tutorial-8/6-Tutorial-8.png)







