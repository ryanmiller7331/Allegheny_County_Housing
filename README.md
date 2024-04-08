<h1> 
End-To-End Housing Market Analysis in Allegheny County, Pennsylvania 
</h1>

<h4> 
The housing market over the past few years has been interesting to say the least. The following is an encompassing analysis on housing data in the Pittsburgh area (Allegheny County) from October 2020 to October 2023. </h4>

Index: 
- Data Collection
- Aggregation & Preparation 
- Data Transformation & Cleaning 
- Web Scraper for Data Validation
- Visualization in Tableau
- Insights 
- Conclusion


<h2>
Data Collection
</h2>
 
I, like many young adults approaching 30, have spent countless hours browsing Zillow dreaming of my first home purchase. With the thousands of listings & information on the site, I thought to myself that this might make an interesting data science project. So what better place to start? Zillow is one of the largest real estate databases in the U.S., so I got to work determining how I could extract the information from the platform. 

Unfortunately, Zillow charges for their API, so I ran into a bit of an issue while trying to get access to Zillow's data on the Pittsburgh area. Luckily, there is the [Zillow Data Export Chrome Extension](https://www.zillowdataexporter.com/). This is a great extension that provides a free trial to download up to 800 listings from Zillow at a time. Naturally it took some time using this extension to collect all transactions in Allegheny County over the last 3 years, but it paid off as I was able to wrangle every transaction. 

I highly recommend the extension to anyone looking for quality Zillow data. Check them out below:

[https://www.zillowdataexporter.com/](https://www.zillowdataexporter.com/)

<h3>
Criteria
</h3> 

Transactions were collected based on the following: 
- Separated by: 
    - Single Family Homes
    - Multi (duplexes/triplexes,etc.)
    - Condos
    - Apartments
    - Manufactured Homes
    - Townhouses 
- No Lots/Land parcels
- Minimum sale price of $5000

With this criteria in mind, the extension resulted in quite a few CSVs ready to be aggregated. Check out some examples of the raw data in this repository [here](https://github.com/ryanrmiller/Allegheny_County_Housing/tree/main/Datasets/raw)

<h2>
Aggregation & Preparation
</h2>

As a newbie to the whole data science/analytics stack, I've found myself really enjoying using Python throughput my learning process. So naturally this is where the fun begins. 

For the most detailed look at my process, check out scripts/aggregation within this repository, or click [here](https://github.com/ryanrmiller/Allegheny_County_Housing/blob/main/Scripts/aggregation.ipynb). 

Some highlights of the aggregation & prep process:

- Raw files we're collected by listing type, so I combined all raw files of each listing type (I.E. single family, multi, condos, etc.) into one CSV per listing type
- Added a "Listing Type" column to each corresponding listing type CSV (all in one function, I was proud of myself after this!)
- Combined all listing type CSVs into one total, workable dataset ("full_housing_data.csv" which you can find in this repository in the "Datasets" file [here](https://github.com/ryanrmiller/Allegheny_County_Housing/blob/main/Datasets/full_housing_data.csv))

<h2>
Data Transformation & Cleaning
</h2>

Again, checkout scripts/cleaning [here](https://github.com/ryanrmiller/Allegheny_County_Housing/blob/main/Scripts/cleaning.ipynb) for the most detailed look at my process. Here's the general workflow: 
- Loading Data
- Removing duplicates
- Removing "0 non-null"
- Renaming columns 
- Converting "lot/land area" to acreage
- Filtering rows where state = "PA" (had some outliers in Maryland for reasons I'm yet to figure out)
- Converted 'Sold date (MM/DD/YYYY)' to DateTime
- Assigning columns to relevant data types
- Filled missing values
- Removed exorbitant values
- Saving the dataset. 

<h2>
Web Scraper for Data Validation
</h2>

I built a web scraper to assist cleaning and standardizing city and zip code data. The [URL](https://www.zipdatamaps.com/en/us/zip-maps/pa/county/borders/allegheny-county-zip-code-map) is a direct postal reference for zip codes in Allegheny County, Pennsylvania and their respective towns/cities associated to that zip. I noticed an issue with the "City" column where the names of cities weren't standardized. For example, East Pittsburgh and E Pittsburgh should both be under East Pittsburgh, some values show "Bradford woods" while others show "Bradfordwoods", etc. 

I was able to merge this script's resulting data frame with the data I had collected to standardize city names, pulling the zip code from each row and populating the recognized postal address, then used the resulting data frame to cross reference the proper city names.

Check out the script for the scraper and the resulting data frame below: <br>
[Web Scraper](https://github.com/ryanrmiller/Allegheny_County_Housing/blob/main/Scripts/scraper.ipynb) <br>
[Resulting Data Set](https://github.com/ryanrmiller/Allegheny_County_Housing/blob/main/Datasets/zip_city_check.csv)
<h2>
Visualization in Tableau
</h2>

From the resulting dataset after cleaning (found in this repo in [Datasets/cleaned_housing_data.csv](https://github.com/ryanrmiller/Allegheny_County_Housing/blob/main/Datasets/cleaned_housing_data.csv)) I developed a visualization dashboard in Tableau. Click the link below on Tableau Public, or checkout the embedded version on my portfolio website.

[Tableau Public Dashboard](https://public.tableau.com/app/profile/ryan.miller5041/viz/HousingData_16995619245280/AlleghenyCountyHousingTransactionPricingData102020to102023) <br>
[My Website with dashboard embedded](......................)

<h2>
Insights
</h2>

Some general insight from the dashboard include the following. Check out the dashboard for more: 

- KPI's:
    - Average Property Price: $267,682
    - Average Square Footage: 1737 sqft. 
    - Average Price per sqft.: $164
- By Zip Code:
    - Highest Avg. Sale Price: 15005
    - Lowest Avg. Sale Price: 15028
    - Highest by sqft.: 15201
    - Lowest by sqft.: 15148

<h2>
Conclusion
</h2>

If you reached this far, thanks for taking the time to read! This was my first complete, end-to-end data science project and I learned a lot throughout the way. Hopefully you've found it interesting and insightful. Be sure to checkout my other works either on my site or within my GitHub profile. 

Best, <br>
-Ryan
