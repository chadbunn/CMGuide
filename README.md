CalMAPPER How To
=============

##What is CalMAPPER?
 
CalMAPPER is a tracking database that CAL FIRE uses to record fuel reduction efforts within the units.  CalMAPPER records funding information (source, amount, grant IDs, etc.), treatment activity information (start/end dates, executing agency, costs, etc.), along with spatial representations of the treatments.  It is an evolving system and at SLU we incorporate various versions of CalMAPPER to produce several maps including a public facing map, print maps and PDFs for contractors and CCC crews, and a GDB for the pre-fire engineer to use to generate statistics and reports.  We use CalMAPPER v1.9 and v2.0 in order to accomplish this as v2.0 does not yet make a suitable replacement for the former ArcMap based versions.  Also by maintaining our data we are able to customize maps to suit specific needs with greater control.   

##CalMAPPER v1.9

X:\_projects\CalMapper

Copy this folder to your local drive.  Use the CalMAPPER v1.9.mxd when adding/editing records.

###CalMAPPER v1.9 User Guide

X:\_projects\CalMapper\CalMapper_v1_9\Documents\UserGuide_2014.pdf

This guide will bring you up to speed on terms and field names and how to operate CalMAPPER v1.9.  The most important aspects about it will be creating relationships between projects, treatments, funding records, and activities.  To put it simply: A project is an arbitray area (we based ours off of watersheds but this is not done in other units) that must encompass all associated treatments;  Projects hold funding records that are then linked to individual treatment areas; Treatment Area + Funding Record = Activity.


###Linking Records in CalMAPPER
---
**1.	Receive data (spatial, funding, activity)**  

Data about upcoming treatments tends to come from Alan or Greg.  The most important info for CalMAPPER besides the spatial data are the funding amount, dates the treatment was started and ended, what type of activity occurred, and who preformed the work on the ground.  

**2.	Put Data into CalMAPPER v1.9**  

Copy and paste treatments into the Treatment Polygon feature class in CalMAPPER v1.9.  Name the treatment in its attribute table and save your edits.

**3.	Relate Treatment Polygon to Project Polygon**  

Select the new treatment and the project it falls into and select All Other Relationships under the Create Relationships toolbar.  This will link your treatment to your project and give your treatment a GUID.

***If the treatment does not fall into a project polygon you will need to edit the nearest project polygon so that it includes the new treatment or if that is not optimal you will need to create a new project polygon by tracing the watershed boundary around it.  Once the new project polygon is created you need to give it a name (start each new project polygon name with 'SLU-'), select our Unit ID '3400', and then run the All Other Relationships tool.  If you add a new project polygon you will need to upload it into CalMAPPER v2.0, but if you just edit it to fit the treatment inside of it you can make these edits in v2.0 instead of uploading a newer version.***

**4.	Add Funding Record to Project**  

Although treatments are the records receiving funding, CalMAPPER v1.9 requires you to add funding records to projects first and then to treatments.  Select the project polygon that is linked to your treatment needing funding and select Add Funding under the Add Table Records toolbar.  Funding records are held in a table only as they have no spatial data.  This table can be accessed by switching your table of contents view to View by Source and then opening the Funding attribute table.  Find your new record and include the amount, the funding agency, and a grant ID if any.

**5.	Add Activity Records to Treatment+Funding Records**  

The last step is to add activity records that detail the type of work preformed in the treatment  (i.e. Chipping, Rx Burn, Shaded Fuelbreak, etc.).  Treatments can be composed of multiple activities but more often than not they are a single activity type.  Select the treatment and its corresponding funding record and then select Add Activity under the Add Table records toolbar.  Fill in the appropiate info for the activity and then save your edits.  

**6.	Support Points for Chipping Events**  

SLU conducts several chipping events each year as well as maintains signs throughout the county about the dangers of wildland fire.  These points were once utilized by CalMAPPER in prevous versions as Support Points, but are no longer tracked in v2.0.  However, we still show them on our public facing [MapBox.js map](http://slocountyfire.org/CalMAPPER/#10/35.4050/-120.5230/ "SLU Treatments").  When a chipping event is completed there will be a collection of sign-up forms with addresses.  These need to then be geocoded and used to select their corresponding parcels.  These parcels become a multi-polygon treatment and the points are related to their corresponding project using the All Other Relationships tool under the Create Relationships toolbar.  

##CalMAPPER v2.0
---
CalMAPPER v2.0 has a Help guide that can be accessed from within the application.  Click on the '?' icon to see it.  It will teach you how to use CalMAPPER v2.0 but there are still some special issues with the application not included in it, see below:

**1.	Accessing CalMAPPER v2.0**

Connect to the state network via VPN.  To access CalMAPPER v2.0 you must use Internet Explorer 9.  To revert to this version open Internet Explorer,  click F12 and selct '9' under the screen icon (it should read Edge by default).  Now you can login to CalMAPPER v2.0.

**2.	Uploading data into CalMAPPER**

New treatment and project polygons are uploaded into CalMAPPER by using the ShapeUp tool.  You can draw new polygons in v2.0 but it is not accurate enough and not advised.  There are two versions on the ShapeUp tool: a standalone version and an ArcMap Add-In version.  For help installing the Add-In see the Help Guide in CalMAPPER v2.0.  Unfortunately, both these versions are necessary as they each can handle different geometry types.  The tables below shows what each can handle:

###Version Comparison###

|Version|Polygon|Multi-Polygon|Point|Multi-Point|Line
|----------|-------|-------------|-----|-----------|-------
|Standalone|   x   |   x   |  x    |       |
|Add-In    |   x   |       |  x    |  x    |  x

The Add-In can also handle feature classes whereas the Standalone can only work with shapefiles.

**3.	Unsubscribing From Projects**

CalMAPPER v2.0 still has some serious bugs that can corrupt your credentials which can then only be reconciled from FRAP's end.  To avoid this terrible bug we have been advised to unsibscribe from projects before logging out.  You can find the Unsubscribe button at the top of a project's overview page.


##SLU Treatments MapBox.js Map
---
**1.	Update treatments_refined.shp**

The [SLU Treatments MapBox.js map](http://slocountyfire.org/CalMAPPER/#10/35.4050/-120.5230/ "SLU Treatments") uses a shapefile created from the CalMAPPER database called 'treatments_refined.shp'.  It is found here: 	
X:\_projects\CalMapper\CalMAPPER_Mapbox 

This file gets styled in TileMill into four layers based on status: Active, Complete, Planning, and Propsed.  This map also includes a chipping point layer that is an extract from the support points table in v1.9, and an SRA layer based off the most current SRA version.  When new treatments are added in CalMAPPER this .shp needs to be updated with all the new info (name, funding, executing agency, etc.).  There are columns for logo links that need to be updated as well.  All the logos are hosted on our Dropbox account.    

**2.	Styling & Processing in TileMill**

The layers for the SLU Treatments MapBox.js Map are created in TileMill.  The styles are already set in their indivdual project's CartoCSS.  All that needs to be done is to export each project: Active_SLU, Complete_SLU, Planning_SLU, and Proposed_SLU as MB Tiles.  ALl layers are exported at zoom layers 8-17 and then are uploaded/updated to our MapBox account under the data tab.  This automatically updates the SLU Treatments MapBox.js map.  

**3.	CalMAPPER Repo**

The HTML for the SLU Treatments MapBox.js map is housed in the [CalMAPPER repo](https://github.com/SLUGIS/CalMAPPER/ "CalMAPPER repo").  It is mostly based off of [this tutorial from MapBox](https://www.mapbox.com/mapbox.js/example/v1.0.0/layers/ "Toggling Layers Tutorial")  
