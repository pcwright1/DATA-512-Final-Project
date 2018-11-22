Paul Wright
University of Washington DATA512 - Human Centered Data Science
November 22, 2018

This project is being completed as part of the University of Washington's DATA512 class on Human Centered Data Science. More information about the course and the project requirements can be found [here](https://wiki.communitydata.cc/Human_Centered_Data_Science_(Fall_2018)).  

## Background and Motivation 

Using Seattle road quality data, we analyze how road quality varies across the different sections of Seattle to evaluate whether road maintanence varies across different areas of the city. Visibility into infrastructure spend and infrastructure quality is important for holding our government accountable. This drive for visibility is exactly why Seattle has chosen to expose their data for analysis on seattle.gov. While we don't expect to find anything problematic or troublesome, we hope that this analysis brings some light to the road quality across different sections of Seattle.

## Data
To do this, we use data from the city of seattle that has road name, location, quality, designation (e.g. arterial), length and surface type. The data can be found [here](http://data-seattlecitygis.opendata.arcgis.com/datasets/383027d103f042499693da22d72d10e3_0?geometry=-122.534%2C47.563%2C-122.097%2C47.644&page=2&selectedAttribute=PVMTCONDINDX1) with information about the columns [here](https://data.seattle.gov/Transportation/Seattle-Streets/jc8u-fewc). This data is updated monthly with updated road quality data. While there are many attributes in this dataset, we focus on the list above as they provide the clearest classifications to compare road quality.


The terms of use, as stated [here](http://www.seattle.gov/tech/initiatives/privacy/data-we-collect), ouline that "Seattle has long led the way in providing open data sets to the public. These are reviewed, scrubbed of personally identifiable information and made available to the public for research, entrepreneurial uses and general information to City residents.".

Seattle.gov does caveat their data [here](https://data.seattle.gov/stories/s/Data-Policy/6ukr-wvup/) that: 

"The data made available here has been modified for use from its original source, which is the City of Seattle. Neither the City of Seattle nor the Office of the Chief Technology Officer (OCTO) makes any claims as to the completeness, timeliness, accuracy or content of any data contained in this application; makes any representation of any kind, including, but not limited to, warranty of the accuracy or fitness for a particular use; nor are any such warranties to be implied or inferred with respect to the information or data furnished herein. The data is subject to change as modifications and updates are complete. It is understood that the information contained in the web feed is being used at one's own risk."

GIS data (which we will not be using other than to leverage the non-GIS components) are designated as follows (from [here](https://www.arcgis.com/sharing/rest/content/items/383027d103f042499693da22d72d10e3/info/metadata/metadata.xml?format=default&output=html)):

"Use Constraints: PDDL | This item is meant for public access and use.  The City of Seattle makes no representation or warranty as to its accuracy. Important | The City of Seattle has created this service for our GIS Open Data website. We do reserve the right to alter, suspend, re-host, or retire this service at any time and without notice. GIS staff will provide notification of changes via the Comments RSS capability in ArcGIS Online."

Here are the main columns we will be using for this analysis with 2 example rows. There are other columns as well but this will be the primary data used for the analysis.


Example data:

| Column Name   | Description                | Example 1               | Example 2                 |
|---------------|----------------------------|-------------------------|---------------------------|
| STNAME_ORD    | Name of the street         | 1ST AVE                 | 1ST AVE NE                |
| ARTDESCRIPT   | Arterial Designation       | Minor Arterial          | Not Designated            |
| SPEEDLIMIT    | Speed Limit                | 25                      | 20                        |
| SEGLENGTH     | Street Length              | 306                     | 267                       |
| SURFACETYPE_1 | Surface Type               | AC/PCC                  | PCC                       |
| STREETTYPE    | Street Type                | Downtown Neighborhood   | Neighborhood Yield Street |
| PVMTCONDINDX1 | Pavement Condition (0-100) | 19                      | 35                        |
| TRANDESCRIPT  | Transit Type Designation   | PRINCIPAL TRANSIT ROUTE | NOT DESIGNATED            |



## Project Plan

To understand how street conditions vary across different areas of the city, we will first do some data cleansing and then apply a variety of statistics using the Pandas package in a Jupyter Notebook. Before we can begin, we must create flags for the different areas of the city since we do not have a mapping to zip code or other identification. To do this, we will leverage the street names - specifically the cardinal direction associated with the street name as these are indicative of the location. We will be comparing NE, N, NW, E, S, SW, W, and downtown (or lack of a cardinal direction). We will then remove any streets that are missing data and will investigate suspicious data (e.g. roads with a condition of 0).

Once the data has been cleaned, we will perform some statistics on each region of the city. These include average condition per region, average condition by street type by region, average condition by speed limit by region and average condition by arterial designation by region. From this, we hope to see some comparable differences across the different sections of the city. In particular, we wonder if there will be a trend that aligns with historically wealthy neighborhood ([example data here](https://www.redfin.com/blog/2016/02/is-seattle-getting-richer-or-poorer.html)).

The final output will be a Jupyter notebook with visualizations comparing the road qualities across the different areas of the city. The notebook will contain the motivation, story and visualizations that summarize the key findings of this analysis.

## Expected Results

We are interested to see how road quality varies across region but also across road type. We expect that the variation in the highly trafficked roads (arterial routes) will be lower, with larger discrepancies being on the less-traveled roads. We are interested to see how road quality varies across region, with particular interest on NW (the university area), NE (around Ballard, a wealthier neighborhood) and S/SW (a historically less wealthy part of the city). 

We are also interested to see how the speed limit impacts the analysis. We expect, again, that streets with lower speed limits will have higher variations in quality (or, equivalently, that that streets with higher speed limits will be better maintained and therefore will have lower variations in quality).






