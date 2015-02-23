CalMAPPER How To
=============

##What is CalMAPPER?

CalMAPPER
 
CalMAPPER is a tracking databse that CAL FIRE uses to record fuel reduction efforts within the units.  CalMAPPER records funding information (source, amount, grant IDs, etc.), treatment activity information (start/end dates, executing agency, costs, etc.), along with spatial representations of the treatments.  It is an evolving system and at SLU we incorporate various versions of CalMAPPER to produce several maps including a public facing map, print maps and PDFs for contractors and CCC crews, and a GDB for the pre-fire engineer to use to generate statistics and reports.  We use CalMAPPER v1.9 and v2.0 in order to accomplish this as v2.0 does not yet make a suitable replacement for the former ArcMap based versions.  Also by maintaining our data we are able to customize maps to suit specific needs with greater control.   

##CalMAPPER v1.9

X:\_projects\CalMapper

Copy this folder to your local drive.  Use the CalMAPPER v1.9.mxd when adding/editing records.

##CalMAPPER v1.9 User Guide

X:\_projects\CalMapper\CalMapper_v1_9\Documents\UserGuide_2014.pdf

This guide will bring you up to speed on terms and field names and how to operate CalMAPPER v1.9.  The most important aspects about it will be creating relationships between projects, treatments, funding records, and activities.  To put it simply: A project is an arbitray area (we based ours off of watersheds but this is not done in other units) that must encompass all associated treatments;  Projects hold funding records that are then linked to individual treatment areas; Treatment Area + Funding Record = Activity.


##Linking Records in CalMAPPER
---
**1.	Receive data (spatial, funding, activity)**  

Data about upcoming treatments tends to come from Alan or Greg.  The most important info for CalMAPPER besides the spatial data are the funding amount, dates the treatment was started and ended, what type of activity occurred, and who preformed the work on the ground.  

**2.	Put Data into CalMAPPER v1.9**  
Copy and paste treatments into the Treatment Polygon feature class in CalMAPPER v1.9.  Name the treatment in its attribute table and save your edits.

**3.	Relate Treatment Polygon to Project Polygon**  
Select the new treatment and the project it falls into and select All Other Relationships under the Create Relationships toolbar.  This will link your treatment to your project and give your treatment a GUID.

***If the treatment does not fall into a project polygon you will need to edit the nearest project polygon so that it includes the new treatment or if that is not optimal you will need to create a new project polygon by tracing the watershed boundary around it.  Once the new project polygon is created you need to give it a name (start each new project polygon name with 'SLU-'), select our Unit ID '3400', and then run the All Other Relationships tool.  If you add a new project polygon you will need to upload it into CalMAPPER v2.0, but if you just edit it to fit the treatment inside of it you can make these edits in v2.0 instead of uploading a newer version.***

**4.	Add Funding Record to Project**
Although treatments are the records receiving funding, CalMAPPER v1.9 requires you to add funding records to projects first and then to treatments.  Select the project polygon that is linked to your treatment needing funding and select Add Funding under the Add Table Records toolbar.  Fundind records are held in a table only as they have no spatial data.  This table can be accessed by switching your table of contents view to View by Source and then opening the Funding attribute table.  Find your new record and include the amount, the funding agency, and a grant ID if any.

**5.	Add Activity Records to Treatment+Funding Records**
The last step is to add activity records that detail the type of work preformed in the treatment  (i.e. Chipping, Rx Burn, Shaded Fuelbreak, etc.).  Treatments can be composed of multiple activities but more often than not they are a single activity type.  Select the treatment and its corresponding funding record and then select Add Activity under the Add Table records toolbar.  Fill in the appropiate info for the activity and then save your edits.  

**6.	Support Points for Chipping Events**

SLU conducts several chipping events each year as well as maintains signs throughout the county about the dangers of wildland fire.  These points were once utilized by CalMAPPER in prevous versions as Support Points, but are no longer tracked in v2.0.  However, we still show them on our public facing [MapBox.js map](http://slocountyfire.org/CalMAPPER/#10/35.4050/-120.5230/ "SLU Treatments").  When a chipping event is completed there will be a collection of sign-up forms with address on it.  These need to then be geocoded and used to select their corresponding parcels.  These parcels become a multi-polygon treatment and the points are related to their corresponding project using the All Other Relationships tool under the Create Relationships toolbar.  

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


###SLU Treatments MapBox.js Map
---
**1.	Update treatments_refined.shp**

The SLU Treatments MapBox.js Map uses a shapefile created from the CalMAPPER database called 'treatments_refined.shp'.  It is found here:	
X:\_projects\CalMapper\CalMAPPER_Mapbox	
This file gets styled in TileMill into four layers based on status: Active, Complete, Planning, and Propsed.  This map also includes a chipping point layer that is an extract from the support points table in v1.9, and an SRA layer based off the most current SRA version.  When new treatments are added in CalMAPPER this .shp needs to be updated with all the new info (name, funding, executing agency, etc.).  There are columns for logo links that need to be updated as well.  All the logos are hosted on our Dropbox account.    

**2.	Styling & Processing in TileMill**

The layers for the SLU Treatments MapBox.js Map are created in TileMill.  The styles are already set in their indivdual project's CartoCSS.  All that needs to be done is to export each project: Active_SLU, Complete_SLU, Planning_SLU, and Proposed_SLU as MB Tiles.  ALl layers are exported at zoom layers 8-17 and then are uploaded/updated to our MapBox account under the data tab.  This automatically updates the SLU Treatments MapBox.js map.  

**3.	Missing Records:**

- Once you import your weather data> Select from the Weather Menu> ‘View Observations’> ‘Daily’> go through to look for missing SOW’s or missing records.  

- If you have missing information you need to go to: http://www.raws.dri.edu/index.html to down load the missing data.  Select CA> select your RAWS site from the list to the left or select the station on the map> Select ‘Data Lister’ from the list on the left hand side of the screen> Specify the dates in which you are missing data > If you are downloading more than 30 days worth of data you need to enter in a password (for Southern CA, try contacting the San Luis Unit)> Save this as a .txt file to the appropriate folder.   

In my case, there were so many non-consecutive missing dates that I downloaded data for the entire 10 years rather than many multiple single date files.  The directions that follow will explain how to edit and filter out only the records you need. 

- If you have only a few missing days here and there you can determine the SOW based on the days before and after it. If there is a missing SOW in the middle of July and the days that pre and proceed it are categorized as a '0' it is likely that it will also be classified as a '0' as well.  

###State of the Weather###

|Code |   State of the Weather 
|---------------|----------------
|0              | Clear, less than 1/10 cloud cover        
|1              | Scattered clouds, 1/10-5,10 cloud cover   
|2              | Broken clouds, 6/10-9/10 cloud cover      
|3              | Overcast, 10/10 cloud cover       
|4              | Fog
|5              | Drizzle 
|6              | Rain        
|7              | Snow or sleet 
|8              | Showers
|9              | Thunderstorms  


**4.	Editing Weather data**

- Open the .fw9 file you downloaded in Notepad++. 

- Remove all html code from the bottom of the file and the top of the file. 

- Remove colons from the beginning of the first two strings of line.  (This is to help format and line up the data correctly for import back into FFP).

- If there are empty lines between string of data: Find and Replace> Find: \n\r\ Replace: [nothing] >Extended Search Mode

- To isolate ‘O’ :  Find and Replace> ‘Mark’ tab> Find What: 00R> Check the bookmark option> Mark All> Search> Bookmark> Remove Bookmarked lines

- To replace first four letters with station ID: Find and Replace> Find What: _ _XXXX> Replace with:  ######

- Remove the top two strings of text that were used to format the data.

- Save as a .txt file for import. 

**5.	Importing Edited Weather data**

- From the Data Menu> Select ‘Import’> Select ‘New FW9 Files’> Select your .txt file> Import. 


**6.	Searching for Anomalies in the data**

- Once you have a complete weather database it is important to examine the data for anything that may not be accurate.  Poor quality data is due to either human error in entering in daily weather observations or mechanical errors at the RAWS stations itself.  Things to look out for:

    - Do the values make sense? For example, if the temperature was recorded being 100 degrees in December, there may be a problem. 
  
    - Repetitive values for any variable.  In my case there was an occurrence of a Relative Humidity of 4 for about three months straight.  While this may be possible, it is highly unlikely that this is accurate.

    - Are there any missing SOW (State of the Weather)?  If so, consider the time of the year and the SOW of days before and after the date you are determining to give you insight as to what the SOW for that day is likely to be. 
 
    - If you find data that is not accurate or that which yield values that seem to be outrageous you can use some of the resources below to fill in the gaps and/or verify or edit the values.  If there is no data to fix the issues you find, you will have to omit the records.  If this happens to be the case state in the FDOP that there was an omissions of records due to poor quality data.     

###Fire###
---

**1.	Download fire data from:**  

https://fam.nwcg.gov/fam-web/kcfast/mnmenu.htm

Select Fire> Standard Extract> Enter in Region/Forest and date range

**2.	Importing Fire Data**

- From the Data Menu> import>Select from drop down menu ‘USFS’> Select ‘Raw Files’> Select your .raw file
    - Region; Unit; Discovery Date; Fire Number; Acerage; Fire Name; Cause; Latitude; Longitude

**3.	Obtain LE-66 Data**

- Create an excel spread sheet for your 10 years worth of data.
- The LE-66 data is stored in on the (F:) drive so you need to be connected to the VPN in order to get access. 
	_(F:)>data>prevent>Prevention>STATS3421_

**4.	Preparing LE-66 Data**

- Create columns for date, incident number, cause, comments, latitude, longitude and copy and populate the fields. 
- Save this file as a .txt for import. 
- Make sure the date has been formatted correctly YYYYMMDD (right click>format cells)
- Change all cause codes (refer to FDOP for conversion chart)
    - _Make sure all the years are correct.  In my experience, I found incidents for 2005 in the 2004 LE-66 stat document, so correct as necessary._   
    - Cause will be represented by a letter, number, or a combination of both.  For the years 2009-2012 there is a document on the (f:) that will have a description for each letter/number value.
	_(F:)>data>prevent>Prevention>STATS3421>2009_ and after log cover causes.doc
I created another spread sheet in order to edit just the data from 2009-2012.

- Once I had this data isolated I performed a filter function on the ‘cause’ column.  Using this function I isolated each variable and replaced it with the cause description.  For the data 2002-2008 refer to 
	_(F:)>data>prevent>Prevention>STATS3421>log cover causes.doc_
when performing your filter to find and replace the cause variables. 

**5.	Additional Editing for LE-66 Data**

If you do not need your lat and long data to be in DD, then disregard the following instructions..

- The lat and long data I gathered from the LE-66 STATS were in different formats i.e. DMS, DM, and were also in different variations of each format. I created ‘working data’ columns of lat and long in order to apply excel formulas to convert these formats all into DD (the format in which my mapping platform of choice required for import).  
	
- For DMS ## ## ##:	

		=MID(B23,FIND(" ",B23)+2,2)/3600+MID(B23,FIND(" ",B23)+1,2)/60+LEFT(B23,FIND(" ",B23)-1)
- For DMS ## ##’##”:

		=MID(A1,FIND("'",A1)+2,2)/3600+MID(A1,FIND(" ",A1)+1,2)/60+LEFT(A1,FIND(" ",A1)-1)
- For MD ## ##.##:

		=MID(A1,FIND(" ",A1)+1,2)/60+Left(A1,FIND(" ",A1)-1)

Once all the data has been converted to DD I made sure that all the Longitude values were (-). I then created final columns for both lat and long and copied and pasted only the values from my lat and long ‘working data’ columns into my lat and long ‘final data’.

**6.	Using Fire Reports**

- Using Internet Explorer go to:
[WebRPTSite](http://webrpt.fire.ca.gov/InfoViewApp/logon.aspx)

- Navigate to: MyInbox> Public Folders> CAD Shared Reports> Click on the FC34 Reports> Select: FC34 Detail-All-Seg (Incident Number)
- Enter in YYYY###### to look up each individual fire report. Verify date, author, lat, and long.
- Save as a .csv for import.

**7.	Populating the ‘SubUnit’ Field**

- Export your fire data from FF+ as a shapefile. Be sure to include ‘SubUnit’ as a field during export. Import your ignition and FDRA .shps into arc. > Open the Ignition attributes table and create a text field called ‘SubUnit’ > In the ‘Select’ menu chose ‘Select by Location’.
    - I want to: ‘select features from’
    - The following layer(s): [your ignition data]
    - That: ‘are completely within’
	- The features in this layer: [your FDRA]

- In your attribute table select ‘Show: selected’ > start an editing session> right click on the SubUnit field and select ‘Field Calculator’> select ‘string’> in double quotes enter in the name of this subunit field. Complete this same process for each FDRA. If there are ignitions that fall outside of your FDRAs clear all selections> select all the data> from your Selection by Location dialog select ‘remove from current selection’ and remove all FDRAs that you just assigned. The remaining ignitions can be assigned ‘Other’ via the process described above. 
Save all edits and close editing session. 

- Open the ignition shapefile in Quantum. Select the ‘Table Manager’ tab. Arrange the fields in the appropriate order (i.e. region, unit, discovery date, fire number, acreage, fire name, cause, lat, long, subunit) and delete any fields that have been created. Save this as a .csv. 

- Open your CSV. If your date appear to be ######## right click on the DiscoveryDate column and select ‘Format Cells’. Select ‘date’ from the menu on the left. Select the default date format (##/##/####). Save the csv. 

- Import your CSV back into FF+ and be sure to include ‘SubUnit’ at the end of your field items to import and also verify that the date format matches the format you adjusted your ‘DiscoveryDate’ values in the CSV.
	

###Stats Graphs###
---
**1.	Fire Occurrence graphs**

- One including All FDRAs: Coastal, Inland, and Ob.	Coasc.
    - ‘Fires’>’Summary’>’Working Set’>Select the ‘CAL FIRE’ Tab>Region ‘3RSS’> Unit ‘SLU San Luis Obispo’>Sub Unit ‘COASTAL Coastal’> ‘Ok’
- Annual Filter should be set for the entire calendar year for these graphs. 
- Screen Shot the graph and insert into FDOP
- Complete the Steps above for each Sub Unit.
All fire occurrence graphs need to be based on the entire calendar year.


**2.	Determining Thresholds**  
For each FDRA the thresholds need to be determined.  The program will do this for you however; you need to confirm that the default percentage values for the thresholds are indeed accurate after all climatology statistics graphs have been run.  The given percentages should coincide with the data output of the fire analysis.  
  
**3.	Three indice graphs for each FDRA**

- ERC displaying: min, max, avg 
    - ‘Weather’>’Climatology’>Select the ‘Stats Graph’ box for the Variable ‘Energy Release Component’>’Run’
    - Maximize the left portion of the screen 
    - Select ‘Options’> ‘Graph Options’> Select the ‘Lines at Average’ tab> Deselect the ‘Mins’ and ‘Maxs’>’Apply’
<br>iv.	Screen Shot the Graph and insert into the FDOP
- BI displaying: min, max, avg
    - ‘Weather’>’Climatology’>Select the ‘Stats Graph’ box for the Variable ‘Burning Index’>’Run’
    - Maximize the left portion of the screen 
    - Select ‘Options’> ‘Graph Options’> Select the ‘Lines at Average’ tab> Deselect the ‘Mins’ and ‘Maxs’>’Apply’
    - Screen Shot the Graph and insert into the FDOP
- ERC displaying:  a year in which the ERC threshold before the onset of fire season (May 15th) and a year in which the ERC threshold had not been obtained until after the start of fire season.   
    - ‘Weather’>’Climatology’>Select the ‘Stats Graph’ box for the Variable ‘Energy Release Component’>Change the ‘CP #2’ value from 97 to 38 (the point at which an ERC of 200 occurs)>’Run’
    - Maximize the left portion of the screen
    - Select ‘Options’> ‘Graph Options’> Select the ‘Lines at Average’ tab> Deselect the ‘Mins’ and ‘Maxs’>’Apply’
    - The onset of fire season is illustrated here when the ‘Average’ line crosses the 38th percentile threshold.  The purpose of this graph is to show that fire season can start well before the traditional start (May 15th) of fire season and conversely, that fire season sometimes starts after the common start date.  
    - Select ‘Options’>’Overlays’>’New’>  Toggle between the years and find the year that has the earliest start date (When it crosses the 38th percentile threshold) and which has the latest start date.  Give each a unique color, a line width of 3, and make it a solid line. Select ‘Ok’.  
    - Screen Shot the Graph and insert into the FDOP

**4.	Decision Points for Dispatch Level**

- Decision points should be set using BI. 
    - Select the ‘A’ on the ribbon at the top of the screen> run the operation with default values selected> Click on the ‘Fires Probability Analysis’ Window> Select ‘View’> ‘Decision Points’> Delete 2 records so you are left with 3 classes
    - Set the first class to 0, set the second class to the value at which fires begin to take off.  Visually, this is when there appears to be a large jump from low to high.  The last class should be set at the BI value where the crest of the graph is no longer in a drastic incline and starts to plateau. The second decision class created should hold the greatest number of fires whereas the first and last should contain the least amount of fire occurrence.  
    - When these levels have been adjusted to accommodate the fire data select ‘Apply’> Adjust the screen so that all graphs fit appropriately>Screen shot and insert into the FDOP. 
    - Adjust the ‘Dispatch Level: Fire Family Plus Analysis Factors and Determinations’ Table (Specifically, the ‘Index Break Points’ section).  
NOTE: All Decision Point graphs need to be based on Fire season (May1-Oct 31), not the calendar year.

**5.	When updating numbers and percent values in FDOP**

- Follow instructions to look at fire occurrence chart> Select ‘Options’> ‘View Graph Data’
- This ‘Fire Occurrence Summary’ page will provide the exact values behind all the graphics illustrated for fire occurrence. 


###Staffing Level###
---
Staffing Level is an important component of the Adjective Fire Danger Rating and is calculated in WIMS.  It is a way for us to break up the BI continuum based on percentile to make it more useful.  Staffing level, along with Ignition Component, is a way for describe relative fire risk. 

Staffing Level will be determined using fuel model G for the San Luis Obispo Unit. This is determined by running different fuel models against fire and weather history data.  When running the different fuel models with your data you should choose the fuel model that yields the ideal statistical output. The ideal statistical output includes a BI of at least 100, all graphs should be a bell curve, the data should have a linear distribution across the spectrum, and no graphs should be inverted.  If you find a fuel model that yields these results, it means that fuel model is the best for fit for your data set and should be the fuel model you should used in the analysis of staffing level. In this analysis, fuel model G (which also happens to be the standard fuel model) was determined to be the best fit for the data set. 

- Select the appropriate ‘SIG/Station’ , ‘Data years’, ‘Annual Filter’: May 1 – Oct 31 > Select ‘Fires’ > ‘Fire Analysis’> Select: Large Fire (Acres):8, Multi Dire Dat (Fires): 3, Select ‘BI’ from the drop down, check the box for ‘Conditional Probability Analysis-FireDays Only>  ‘OK’> Select the ‘Fires Probability Analysis’ Window> Select ‘View’ > ‘Decision Points’>  close the ‘Class Lower Limits” Window  
- The default ‘Class BI Ranges’ will be the values entered into the “Staffing Level: Break Points chart”.  Round the Values for the chart.


###Preparedness Level###
---

The point at which large fires start to take off based on ERC.  

- Select appropriate ‘SIG/Station’> Data Years> Annual Filter set for fire season> Select ‘Fires’> ‘Fire Analysis’> Large Fires (Acres):8> Multi Fire Day (Fire):3> Select ERC from the drop down> Check the ‘Conditional Probability Analysis Fire Days Only’ box> 
-	Close the ‘Cumulative Fires Analysis’ Window. Looking at the ‘Fires Probability Analysis’ you can see when large fires start to take off as illustrated by the magenta line with the open square (Large Fire Day). When the data indicates an increase in occurrence of large fires, this is the point at with the threshold should be placed. Click directly on the pink square to view the value. The X-value in the bottom right hand corner of the screen in the ERC threshold value that will be recorded in FDOP.  In order to verify this threshold value:
-	Select ‘View’> ‘Decision Points’> In the ‘Class Lower Limits’ window delete all but two of the threshold classes> Make Class 1 and value of ‘0’ and Class 2 the threshold X-value> Select ‘Apply’
-	In the ERC Percentile Graph the threshold line should be drawn a the point in which the large fire data starts to rapidly increase. 
-	In the ERC Probability Graph directly below, the threshold line should be drawn through the data point that you clicked before, which is the point at which large fires start to increase. 
-	If the threshold line is not drawn at the necessary position on the graphs adjust the threshold value in the ‘Class Lower Limits’ window to determine the appropriate preparedness threshold value.
- Complete this process for both FDRAs and record the appropriate threshold value in the Preparedness Level chart. 

###Pocket Cards###
---
A pocket card must be created for each FDRA, which will display the three largest fires.  

For the Inland FDRA, instead of using the largest fires by acreage we used the top three most well known fires in San Luis County.  This is because these fires are the events that resonate with the SLU.  

- Select ‘Weather’> ‘Pocket Card’> 
- Fire Danger Area: ‘Inland FDRA’ 
- Area Locator Bitmap is located: X://projectdata>master_data>Inland.bmp 
- Years to Remember: 1950 – Present
- Area Locator Bullets: 
    - Line 1 – Interior Valley
    - Line 2 – Las Tablas RAWS 
    - Line 3 – La Panza RAWS



**Fires** 

|Fire Name |     Date    |
|----------|-------------|
|.         | 7/1/1985    |
|.         | 8/18/1994   |
|.         | 8/15/1996   |

Fire Name is left Blank or replaced with '.' because the symbology is cluttered and not legible on the graph.  Once the graph is complete, Photoshop/edit the names in.  (I did so using paint)

Past Experience Text:

- Pilitas 1 fire 7/1/1985 burned 84,271 acres
- Highway 41 fire 8/18/1995 burned 50,729 acres
- Highway 58 fire 8/15/1996 burned 33,094 acres

This bit of text can be typed into the Pocket card window.  All other descriptive text and the logo was edited using paint.  Unless a fire occurs that exceeds one of these three major fires, these are the fires that are to be displayed on the Inland Pocket Card. The Coastal FDRA pocket card displayed the top three largest fires in that FDRA. 

The bit map for each FDRA is already created:
_X://projectdata>master_data>Coastal.bmp_

Under the ‘Fire Danger Area’ enter in the region (i.e. coastal or inland), the RAWS located in the region, 

###Updating the FDOP Annually###
---

- Enter in all fire and weather records for the past year
- Run the above statistical graphics to produce new charts.  These charts shouldn’t change too drastically unless there were exceptionally large or small fires, or drastically hot or cold days.  
    - Fire Occurrence Graphs will need to be updated.  All descriptive text and percentages need to be adjusted accordingly.  
- Climatology Graphs of Temperature and Rainfall.  These can be obtained from:
    - Use http://www.ncdc.noaa.gov/cdo-web/datatools/normals, Paso Robles for inland and San Luis Obispo for coastal.

-  Tables in the FDOP that may need to be updated depending on new data include: 
    - 10 Largest Fires Recorded in the Inland FDR
    - Historic Fires for Reference Depicted on the Inland FDRA Pocket Card
    - 10 Largest Fires Recorded in the Coastal FDRA
    - Historic Fires for Reference Depicted on the Coastal FDRA Pocket Card 
- If the information in the station catalog in WIMS changes or is updated a new screenshot should be included in place of the current. If the conditions of the RAWS change, it should be noted in the ‘RAWS Site Description and Photos’ section. All pocket cards in the appendix need to be updated.  



###Cause Code	Conversion Chart###

|CDF Cause Code |   Description  |Federal Cause Code|
|---------------|----------------|------------------|
|0              | Unknown        |9                 |
|1              | Undetermined   |9                 |
|2              | Lightning      |1                 |
|3              | Campfire       |4                 |
|4              | Smoking        |3                 |
|5              | Debris Burning |5                 |
|6              | Arson          |7                 |
|7              | Equiptment Use |2                 |
|8              | Playing w/ Fire|8                 |
|9              | Miscellaneous  |9                 |
|10             | Vehicle        |2                 |
|11             | Railroad       |6                 |
|12             | Powerline      |2                 |



(Obtained from CAL FIRE intranet)

In preparation for statistical analysis, the CAL FIRE cause code must be translated to the federal cause code for use in Fire Family Plus software.  The chart above outlines the cause code conversion from CDF to Federal cause codes.

##Fuels Info

**Q: How are live and woody Fuel Moistures Calculated?**  

A: "Measured Woody Fuel Moisture: The modeled fuel moisture of live woody material does 
not always track with the measured woody fuel moistures from sampling sites. This is 
because live fuel moisture values in the NFDRS are modeled values designed for the 
broad scale of fire danger, rather than site-specific measured values. In these instances, 
fire managers have a couple of options. Physical measurements of the moisture content 
of the small branch wood and foliage of live woody plants can be collected monthly. 
Preferably the user will already be monitoring these measured live fuel moistures in 
parallel to the outputs of the NFDRS and using experience to include the measured fuel 
moisture values as another tool in their decision-making toolbox. This allows the 
NFDRS model to work for the user as it was intended.
 
Alternatively, the user can regularly enter measured live woody fuel moisture into the 
NFDRS processor to calibrate the woody fuel moisture model. The calibration based on 
measured woody fuel moisture is valid for 30 days. If no new measured value is entered 
within 30 days, the model returns to using only weather data. The woody moisture 
computed solely from weather data may be quite different from that computed from both 
weather data and the measured woody moisture. This may result in sudden or 
unacceptable changes to NFDRS outputs. This approach requires consistent care and 
feeding of the processor (i.e., a regular live fuel monitoring program) and has been 
discouraged by some agencies." 

"X-1000 Hr Fuel Moisture Value – The X-1000 value is not truly a dead fuel moisture 
value. It is the live fuel moisture recovery value. It is discussed here since it is derived 
from the 1000-hr fuel moisture value. It is an independent variable used in the 
calculation of the herbaceous fuel moisture. The X-1000 is a function of the daily change 
in the 1000-hour timelag fuel moisture, and the average temperature. Its purpose is to 
better relate the response of the live herbaceous fuel moisture model to the 1000-hour 
timelag fuel moisture value. The X-1000 value is designed to decrease at the same rate 
as the 1000-hour timelag fuel moisture, but to have a slower rate of increase than the 
1000-hour timelag fuel moisture during periods of precipitation, hence limiting excessive 
herbaceous fuel moisture recovery. "

"Live woody and herbaceous moistures fluctuate in response to drying and 
wetting cycles. Greenness factor values fluctuate up and down within the 20 and 1 range during 
this period. Annual herbaceous vegetation most likely will cure sometime during this period. In 
the NFDRS model, the live fuel moisture is initially calculated using the same formulas as are 
used after the completion of greening in the 1978 models, but is adjusted by a factor equal to the 
greenness factor divided by 20. The woody fuel moisture is calculated using the same formulas 
as are used in the 1978 models, and it too is adjusted by the greenness factor." http://fam.nwcg.gov/fam-web/pocketcards/master_gaining.pdf

**Q: What is the difference between Annuals and Perennials?**  

A: "Grass Type (live fuel type): The National Fire Danger Rating System recognizes that there are 
seasonal differences in fire danger related to the type of grass vegetation present. Annual 
vegetation produces a different dynamic situation within the fuel complex than does perennial 
vegetation. Annuals sprout from a seed each year, grow, reach maturity and die usually all in 
one season. This process is not affected significantly by seasonal weather factors such as 
temperature or precipitation. Perennial grasses on the other hand, generally start in a dormant 
condition, grow, reach maturity, then go back into dormancy. Their cycle is greatly affected by 
temperature and precipitation. Because of these differences, the mathematical formulas or 
algorithms associated with the drying of herbaceous vegetation are different for the two types of 
grasses. The loading of fine fuels associated with annual grasses shifts from live to dead and 
stays there for the duration of the season. For perennial grasses the shift from live to dead is 
much slower and may even stop or reverse if the right combinations of temperature and 
precipitation occur during the season. Where both annual and perennial grasses occur together 
select the type that predominates the site." http://fam.nwcg.gov/fam-web/pocketcards/master_gaining.pdf

**Q: When should we start seeing changes in our fuel moistures after Green Up?**

A: "The equations that predict 1000-hr and live fuel moisture contents require at least four weeks to stabilize and predict 
accurate fuel moisture content values." http://fam.nwcg.gov/fam-web/pocketcards/master_gaining.pdf
