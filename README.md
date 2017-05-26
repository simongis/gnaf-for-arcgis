# G-NAF for ArcGIS

The Geocoded National Address File (referred to as G-NAF) is Australia’s authoritative, geocoded address file.  This has been made available as [Open Data on data.gov.au](https://data.gov.au/dataset/geocoded-national-address-file-g-naf) as a series of PSV files. 

Bruce Harold has provided some tools to help convert this raw data into an [Esri Address Locator](http://pro.arcgis.com/en/pro-app/help/data/geocoding/create-a-locator.htm).  I realised I had little experience building an Address Locator from scratch, so have been running through the process to better understand how they work.  As a result, I have put together this wiki to help others who might want to build their own address locator from G-NAF.

## I don't care how you did it, where is the actual Address Locator?

Here is a link to the compiled Locator, but be aware that I will not be keeping this up to date with the quarterly updates made to the G-NAF dataset and also please read the disclaimer below.

LOCATOR LINK INCLUDING DATE CREATED

## The Disclaimer

This has been a self-learning experience to better understand the G-NAF data along with building an Esri Address.  I have not spent hours checking through the quality of the output.  At the time of writing, this is just looking at G-NAF data, and does not incorporate other data sources such as placenames, business names, other PSMA admin boundaries, etc. 

Therefore, use at your own risk, especially if you are thinking about using this within an enterprise workflow.  Getting an address wrong can be huge mistake for some workflows. 

If you want an Australian geocoder that has had significantly more effort and testing put against it, along with more regular updates, I would highly encourage you to look into the following:

* [Map Data Services](http://mapdataservices.com/industries-retail-locators) - provide an Esri Address Locator
* [NAVIGATE](https://www.psma.com.au/get-data/navigate) - Provide an Esri Address Locator
* [Esri Street Map Premium for Asia Pacific](http://www.esri.com/data/streetmap) - Esri Address Locator based upon HERE data

Also worth pointing out that the [ArcGIS Online World GeoCode Service](https://developers.arcgis.com/rest/geocode/api-reference/overview-world-geocoding-service.htm) includes G-NAF data, but will only get updates around once every year or so. 

## The Goal

If others find these tools useful, I am hoping that we can make improvements to this project and build on it over time.  
* Please fork and recontribute any improvements you make!
* Please feel free to raise issues and enhancements or areas in the Wiki that needed more explanation.

Longer term some goals I want to look at accomplishing include:

* Automating the process of downloading updates from data.gov.au and updating the address locator (and a geocode service published from the locator)
* Investigating using python instead of a reliance on the Data Interop extension.
* Including other open data layers to build a more robust composite locator (e.g. PSMA boundaries, Geonames, etc.)

## Steps to build the locator

### Initial Setup

1. Download [Bruce's tools from ArcGIS Online](http://www.arcgis.com/home/item.html?id=5bdf6c128c344b3ca7aea24e68fa32e1)

2. Download the latest [PSMA GNAF PSV files](http://data.gov.au/dataset/geocoded-national-address-file-g-naf/resource/99b44dff-4e84-4cb7-9cbf-a68d3ebf964a)

3. Make sure you have the Data Interop for ArcGIS Pro installed and licensed.

This initially caught me out as it is a different installer to the ArcGIS Desktop Data Interop installer)

![Add Remove Programs](/img/ArcGIS_Pro_DI_LicenseCheck.jpg?raw=true "Add Remove Programs")

4. Create a new ArcGIS Pro Project, add a folder connection to where you downloaded the tools from #1

![Add Folder Connection](/img/AddFolderConnection.png?raw=true "Add Folder Connection")

5. Open the toolbox, and for *each tool*, right click and properties, and update the workspace path to match the FMW folder that is included in the download

![Update filepath references](/img/UpdateReferencesInToolbox.png?raw=true "Update filepath references")

6. Save Project

### Running the Data Prep Tools

7. Open the ImportPSV2 tool

WARNING: This tool took around 10hrs to run for all of Australia.  Overnight job.

#### Input Parameters
* Enter path to the GNAF ZIP file containing the PSV files
* Create an output folder and point the Destination UnZIP folder to this output folder location
* Point the tool to a destination file Geodatabase.  You can use the default geodatabase for your ArcGIS Pro project.

![ImportPSV2 tool](/img/ImportPSV2_RunTool.png?raw=true "ImportPSV2 tool")

> _Did you encounter 'A fatal error has occurred' / 'Translation Failed'?_
> 
> Do you have ArcGIS Server/Enterprise installed on your machine?
> 
> There appears to be a bug when trying to run some of the Data Interop tools on a machine that has ArcGIS Server installed.  An [issue](https://geonet.esri.com/thread/185929-etl-sketchup-to-feature-class) with multiple versions of python clashing.
> 
> One Workaround is to either unintall ArcGIS Server or run all of the tools from a machine that does not have ArcGIS Server installed
>
> Another Workaround is to open the tools from their workbench and running them from there. Steps outlined below. 

##### WORKAROUND: Running the tools from Workbench

This same process will apply for all of the Spatial ETL tools supplied in the tools provided by Bruce

* Right click the ImportPSV2 tool and hit _Edit_

![Open in workbench](/img/OpenToolFromWB.png?raw=true "Open in workbench")

* Run the tool from workbench (hit the execute button)

I found this was also a better approach to understand the progress of how the tools are running and get a better understanding of the data manipulation the tools are performning.

![Run in workbench](/img/ImportPSV2.png?raw=true "Run in workbench")

Either way, running from either the tool within ArcGIS Pro, or from the Workbench - check that the tool runs succesfuly and you should end up with the following output in your destination geodatabase:

![Success](/img/Success_ImportPSV2.png?raw=true "Success")
