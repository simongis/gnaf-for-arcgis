## G-NAF for ArcGIS

The Geocoded National Address File (referred to as G-NAF) is Australia’s authoritative, geocoded address file.  This has been made available as [Open Data on data.gov.au](https://data.gov.au/dataset/geocoded-national-address-file-g-naf) as a series of PSV files. 

Bruce Harold has provided some tools to help convert this raw data into an [Esri Address Locator](http://pro.arcgis.com/en/pro-app/help/data/geocoding/create-a-locator.htm).  I realised I had little experience building an Address Locator from scratch, so have been running through the process to better understand how they work.  As a result, I have put together this wiki to help others who might want to build their own address locator from G-NAF.

### I don't care how you did it, where is the actual Address Locator?

Here is a link to the compiled Locator, but be aware that I will not be keeping this up to date with the quarterly updates made to the G-NAF dataset and also please read the disclaimer below.

LOCATOR LINK INCLUDING DATE CREATED

### The Disclaimer

This has been a self-learning experience to better understand the G-NAF data along with building an Esri Address.  I have not spent hours checking through the quality of the output.  At the time of writing, this is just looking at G-NAF data, and does not incorporate other data sources such as placenames, business names, other PSMA admin boundaries, etc. 

Therefore, use at your own risk, especially if you are thinking about using this within an enterprise workflow.  Getting an address wrong can be huge mistake for some workflows. 

If you want an Australian geocoder that has had significantly more effort and testing put against it, along with more regular updates, I would highly encourage you to look into the following:

* [Map Data Services](http://mapdataservices.com/industries-retail-locators) - provide an Esri Address Locator
* [NAVIGATE](https://www.psma.com.au/get-data/navigate) - Provide an Esri Address Locator
* [Esri Street Map Premium for Asia Pacific](http://www.esri.com/data/streetmap) - Esri Address Locator based upon HERE data

Also worth pointing out that the [ArcGIS Online World GeoCode Service](https://developers.arcgis.com/rest/geocode/api-reference/overview-world-geocoding-service.htm) includes G-NAF data, but will only get updates around once every year or so. 

### The Goal

If others find these tools useful, I am hoping that we can make improvements to this project and build on it over time.  
* Please fork and recontribute any improvements you make!
* Please feel free to raise issues and enhancements.

Longer term some goals I want to look at accomplishing include:

* Automating the process of downloading updates from data.gov.au and updating the address locator (and a geocode service published from the locator)
* Investigating using python instead of a reliance on the Data Interop extension.
* Including other open data layers to build a more robust composite locator (e.g. PSMA boundaries, Geonames, etc.)

### Steps to build the locator
