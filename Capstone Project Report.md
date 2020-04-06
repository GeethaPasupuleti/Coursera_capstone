# Capstone Project - The Battle of Neighborhoods


Geetha Pasupuleti

Apr 05, 2020

# 1. Introduction
## 1.1 Background
Many employees, especially in IT Industry, keep moving to different countries as part of their project assignments. Families moving to a new country face many hardships, finding a place to live, understanding the culture, learning the local language, etc. To ease the migration, they would like to find a city similar (or dissimilar) to the one they were living in their home country, with a similar or better infrastructure and quality of life. It would be helpful to have a comparison between the city that they live in their home country and the destination country, to find out which are similar.


## 1.2 Description of the problem

Being not familiar with the new place and with many alternatives it’s easy to misunderstand the data. It would be helpful if there is a comparison of the different cities in the destination country which gives a general view of each place and its advantages and disadvantages.

In this project I have taken Cities in UK as a home country to compare with Cities in India as a destination City.

The following are the requirements for choosing is an appropriate place to live:  

* Schools
* Hospitals
* Shops
* Entertainment
* Restaurant
* Parks
* Playground
* Coffee
* Nightlife

## 1.3 Interest

The findings of such an analysis would be of interest for families moving between UK and India, and also for companies expanding their businesses to new cities.
 
# 2. Data Acquisition and cleaning
## 2.1 Data sources
Wikidata provides longitude and latitude details for many cities. I will be using this [link](http://tinyurl.com/yxkqyzu2) to extract longitude and latitude for UK and India.

I obtained the venues for each place using the Foursquare API for each city in both countries.

## 2.2 Cleaning of the data
The data downloaded from Wikidata had to be cleaned by splitting the coordinates column into Longitude and Latitude, dropping _na_ values and creating a new dataset with only the cities of UK and India. 

Then I got the venues for each city using FourSquare API. I have loaded the data into dataframe, Name, City, Country, Latitude, Longitude, Category and Address. When getting the venues I added additional columns for country _(country2)_, city _(city2)_ and search query _(query)_ because I needed that information for the cluster analysis and foursquare returns empty data and differently written names. With the 2 additional columns I could get a proper dataset for the analysis.

# 3. Methodology
After creating the new dataset with cities form United Kindom and India I plotted the cities on a map using Folium to check if the coordinates were ok.

## 3.1 Venue categories for each city

After cleaning all the data and preparing the final datasets, I created a “One Hot encoding” for each category for each city base on the categories Foursquare returned.

After doing the “One Hot encoding” I had a dataset cities_onehot with shape (31589, 347), which I grouped by City with the category mean.

Then I created a new dataframe city_venues_sorted with the most common venues for each city.

## 3.2 Cluster Analysis

I used K-Means Cluster Analysis with K=5 and Hierarchical Cluster Analysis with 7 clusters and got similar results, I then plotted which on a Folium Map with Colors for each cluster.

I created a Dendogram with several linkage methods to see how the cities group. I used 7 clusters with the complete linkage method as per the following picture:

![alt text](https://github.com/pbindusagar/Coursera_Capstone/blob/master/images/image.png "picture")

## 3.3 Comparing results

For K-Means Analysis I got the following results

⋅⋅* K-means for 0 has 58 cities
⋅⋅* K-means for 1 has 12 cities
⋅⋅* K-means for 2 has 3 cities
⋅⋅* K-means for 3 has 4 cities
⋅⋅* K-means for 4 has 3 cities

With Hierarchical Clustering with complete Linkage I got, for 7 Clusters:

⋅⋅* Hierarchical for 0 has 5 cities
⋅⋅* Hierarchical for 1 has 10 cities
⋅⋅* Hierarchical for 2 has 58 cities
⋅⋅* Hierarchical for 3 has 1 cities
⋅⋅* Hierarchical for 4 has 4 cities

## 3.4 Analyzing the results

I will analyze the most frequent venues for the 7 Hierarchical Clusters:

Cluster 0

|venue|	frequency|
| ------------- |:-------------:|
|restaurant|	0.52|
|coffee|	0.15|
|shops| 	0.11|

Cluster 1

|venue|	frequency|
| ------------- |:-------------:|
|restaurant|	0.28|
|shops|	0.27|
|coffee|	0.19|

Cluster 2

|venue|	frequency|
| ------------- |:-------------:|
|shops|	0.47|
|restaurant|	0.26|
|coffee| 0.12|

Cluster 3

|venue|	frequency|
| ------------- |:-------------:|
|school|	0.74|
|university|	0.26|
|coffee|	0.00|

Cluster 4

|venue|	frequency|
| ------------- |:-------------:|
|hospital|	0.40|
|restaurant|	0.30|
|coffee|	0.14|

Cluster 5

|venue|	frequency|
| ------------- |:-------------:|
|university|	0.55|
|school|	0.45|
|coffee| 0.00|

Cluster 6

|venue|	frequency|
| ------------- |:-------------:|
|school|	1.0|
|university|	0.0|
|coffee|	0.0|

# 4. Conclusions

In this study I analysed the main cities in 2 countries based on infrastructure (venues) I got from Foursquare API.

K-Means and Hierarchical Clustering gave similar results, and because of the Dendogram for Hierarchical Cluster with complete linkage I decided for 7 clusters, even if cluster number 3 has only one city: “London” in United Kingdom.

These city groups can be very helpful for families searching for a similar city in a new country and for companies looking for similar cities to expand.

# 5. Future directions

In this study, I compared the cities using foursquare data for the venues for only 2 countries. It would be very interesting to compare all the biggest cities in the world also analysing variables such as rent cost, income and safety. It’s hard to get all that information for all the cities, as not all the countries have open data policies.

I also used 60 results in a 2000 meters radius for each city when looking for venues, and the results may change when using more data in a bigger radius.  