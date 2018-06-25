# sky_notes
## Capturing working notes for the project across multiple workstations

## Links
Google Earth Engine guidance https://geohackweek.github.io/GoogleEarthEngine/05-classify-imagery/
Google Earth Engine
https://code.earthengine.google.com/?accept_repo=geohackweek2017
Development Seed Label Maker (looks better than skyet-data)
https://developmentseed.org/blog/2018/01/11/label-maker/
https://github.com/joshwapiano/label-maker
Supervised learning methods require two things: satellite imagery and ground-truth labels. If you’re looking to train a model in Potsdam or a few other select cities, there are good datasets already available. But if you need a custom class label or want to train in areas closer to where you’ll be using the model, you’ll likely need to put together a new dataset. With Label Maker you can define your desired classes as OpenStreetMap features, specify an imagery tileset, and it will handle the rest.


## Why GEE? Planetary Scale Change: The Hansen Dataset
Google Earth Engine enables users to compute on petabytes of data on the fly without having the navigate the complexities of cloud-based parallelization. Enhancing inclusive access has spurred the growth of environmental projects conducted at scales previously unimaginable. Example uses cases that have leveraged the full power of GEE include:
•	Global Forest Watch Global Forest Watch is a forest monitoring and conservation tool based on the the Hansen dataset. The Hansen dataset was created in Earth Engine and leverages the entire Landsat archive to map forest loss and gain at a global scale. Hansen Tutorial for GEE
•	Global Surface Water Occurrence Map maps the temporal and spatial distribution of water on a global scale over the past three decades. Global Surface Water Tutorial for GEE
What are common uses of GEE?
•	operate on petabytes of imagery using Google’s cloud
•	export your analysis
•	import and export your own raster and vector data (assets)
•	share your own raster and vector data
•	embed outputs in apps
•	store, share and version control your code
#### Key Points
•	Google Earth Engine is a powerful tool for analyzing remote sensing imagery.
•	GEE’s data catalog hosts a formidable variety of earth observation data.
•	GEE is changing how we understand and study the Earth.


## Landsat 8:
Landsat 8 Collection 1 Tier 1 calibrated top-of-atmosphere (TOA) reflectance. Calibration coefficients are extracted from the image metadata. See Chander et al. (2009) for details on the TOA computation.
Landsat scenes with the highest available data quality are placed into Tier 1 and are considered suitable for time-series processing analysis. Tier 1 includes Level-1 Precision Terrain (L1TP) processed data that have well-characterized radiometry and are inter-calibrated across the different Landsat sensors. The georegistration of Tier 1 scenes will be consistent and within prescribed tolerances [<=12 m root mean square error (RMSE)]. All Tier 1 Landsat data can be considered consistent and inter-calibrated (regardless of sensor) across the full collection. See more information in the USGS docs.
4. Getting Help
There are many entry points for getting help tucked into the Code Editor. Familiarizing yourself with these tools can help soften the learning curve.
API reference (Docs tab)
Next to the Scripts tab is the Docs tab, which has the complete, searchable JavaScript API documentation for every function and call. The documentation is organized by GEE data type. Each data type has a specific set of functions that can be applied to it.
Help Button
The Help button is a gateway to many resources, including links to:
•	the Developers Guide for official GEE tutorials, reference and guides. This is the first place I go when I need to look up how to write some code.
•	the Help Forum where you can post questions and get answers. If I can’t find a guide for my specific question on the GEE Guides, I then go search for key words from my problem/question on the forum. Since people share links to their codes, you can often find great examples of solutions here.
•	Existing tutorials and the Earth Engine for Higher Education resources written by the GEE team and others (even some in Japanese!)
•	A list of keyboard shortcuts
•	links to the Suggest a Dataset page

## Nature Article
https://www.nature.com/articles/srep33194  Island building in the South China Sea: detection of turbidity plumes and artificial islands using Landsat and MODIS data
Island building detection using OLI
Using Landsat-8 OLI data, island building activities and turbidity plumes were observed for nearly all of the locations reported in the media or identified using MODIS/A (Figs 2, 3, 4), with the only exceptions being projects completed prior to the OLI time series (specifically, Southwest Cay, Namyit Island, Grierson Reef, Swallow Reef, and Thitu Island). Of the remaining island building activities studied, three of Vietnam’s projects commenced prior to the OLI dataset beginning in mid-2013 (West Reef, Sand Cay, and Central Reef), while 5 Chinese and 2 Vietnamese projects began in 2014 (for 2015, these numbers are 2 and 3, respectively). All but two of Vietnam’s projects (as well as Taiwan’s construction on Itu Aba Island) observed in the OLI time series were additions to already existing islands, while all of the Chinese projects represented entirely new islands.
https://earthexplorer.usgs.gov/ - checking sentinel 8 images do exist (THEY DO!)

## Using Google Earth Engine to detect land cover change: Singapore as a use case
https://www.tandfonline.com/doi/full/10.1080/22797254.2018.1451782 (hard copy in work laptop folder)


## The end game perhaps? A slider showing before and after of change of interest (with bounding box?) https://www.mapbox.com/help/processing-satellite-imagery/

