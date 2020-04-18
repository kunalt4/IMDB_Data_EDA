# IMDB_Data_EDA
An EDA of Movies released between 2015 - 2019, with data collected from IMDB using the OMDB API - http://www.omdbapi.com/

## Task 1: Data Identification.

An API for movie details was chosen, provided by OMDB - http://www.omdbapi.com/.
This API takes an IMDB ID, and returns all the details of the particular movie or tv show. I have used scrapy to get IMDB IDs of all movies from the last 5 years, specifically 2015-2019.

The objective of this EDA was to answer a few basic questions:
* How many movies are made each year?
* Which languages are the most common?
* What genres are more common?
* What is the average runtime of movies across the years?
* What does the IMDB rating distribution look like for all movies?
* How does box office revenue change with genre, language of movies, and release date?

## Task 2: Data Collection.


Used scrapy to go through the list of IMDB movies, and scrape IDs from the page. These IDs are then passed one by one to the API and movie details are stored - over 70,000 API calls are made, so take heed. The API key used here has expired, but one can get it from omdbapi.com.

The data is stored into a list, and then to a pickle file and csv. It is then further read from the csv for future proofing.

The scraper by default collects IMDB movie IDs by scraping IMDB, between the years 2015 to 2019.

`get_data()` - passes the list of IDs to the API, and stores the retrieved data to a list - only movies with the year present were stored, and errors are stored in the error list but ignored ahead for this EDA.

## Task 3: Data preparation and analysis.

#### Step 1: Convert dtypes
The data was stored in a dataframe, and all columns were converted to the correct data type.

#### Step 2: Remove outliers.

We looked at the dataframe, and plotted a couple of boxplots to check for outliers. The outliers in the runtime column were removed.

#### Step 3: Check null values.

For this EDA, even nulls in certain columns were acceptable if we needed to understand data of certain other attributes. We check if there are rows almost entirely consisting of NaNs and NaTs - any row with more than 7 NaNs were dropped as they are not useful for analysis other than basic counts.

## Task 4. Performing the Analysis

##### Answering the basic questions:

* ***How many movies are made each year?***
<p align="center">
<img src="/output/op1.png" width=auto height=auto></img>
</p> 
<p>On an average, 12654 movies are made each year. 2016 was the most productive year, followed by 2015 with around 14000 movies made. Only around 9000 movies were made in 2019 in contrast.</p>

* ***Which languages are the most common?***
<p align="center">
<img src="/output/op2.png" width=auto height=auto></img>
</p>
<p>The same languages take the top 5 spots every year - English, Spanish, Japanese, German, French - with English language movies being by far the most prominent.
</p>
* ***What genres are more common?***
<p align="center">
<img src="/output/op3.png" width=auto height=auto></img>
</p>

<p align="center">
<img src="/output/op3b.png" width=auto height=auto></img>
</p>
<p align="justify">
The genres of drama and comedy have seen the most movies released overall, and across each of the last 5 years. Since we selected only the top 5 movie genres for each year, the graph looks distorted. Documentaries were common between 2015-2017, but seem to have fallen out of the top 5 for Crime and Thriller movies.</p>

* ***What is the average runtime of movies across the years?***

<p align="center">
<img src="/output/op4.png" width=auto height=auto></img>
</p>
<p>
2019 was the year of long movies, apparently. There were a lot of movies in 2016, but on average they were quite short, with an average of around 90 minutes.
</p>

* ***What does the IMDB rating distribution look like for all movies?***

<p align="center">
<img src="/output/op5a.png" width=auto height=auto></img>
</p>
<p>
The distribution here is almost normal - just slightly skewed towards a higer rating. Surprisingly, only a few movies are rated exceptionally low, as compared to very high - this might point to users only rating movies they liked.</p>

***Looking at the MetaCritic and Rotten Tomato Ratings***

<p align="center">
<img src="/output/op5b.png" width=auto height=auto></img>
</p>
<p>MetaCritic and Rotten Tomatoes both rate critics ratings, as compared to user ratings - however the distribution for both look different. This is because of the way aggregation of ratings of each website works. While MetaScore calculates weighted average ratings from each critic reviewer, Rotten Tomatoes simply takes the ratio of how many critics rated the movie positively as opposed to negatively.</p>

* ***How does box office revenue change with genre, language of movies, and release date?***
<p align="center">
<img src="/output/op6a.png" width=auto height=auto></img>
</p>
<p>Average revenue for English family movies are much higher than the second highest - Fantasy hindi movies. Action seems a common genre for big grossing movies across languages, as well as Biography.

English movies earn by far the highest revenue.</p>
<p align="center">
<img src="/output/op6b.png" width=auto height=auto></img>
</p>
<p>It seems movies released in November and December, along with May, June and July are the most successful in terms of revenue. This is understandable as those are the holidays and summer months.

</p>

## Conclusion
We used the omdb api to visualize and analyze movies released over the past 5 years.

There were some interesting results, specifically the relation between ratings from Metacritic and Rotten Tomatoes, and how the number of IMDB votes and box office revenues relate.

A lot of data was unavailable, here it was handled by either removing the rows where too many nans were present, or ignoring nan values. Another way to handle this could've been to impute mean or frequent values, but I feel there was enough data present for an EDA, and wasn't done.

Some work that could be done would be looking more into the relations between categorical and numeric data, and how if the rating (pg, adult) of a movie affect revenues. Further analysis work would be to use predictions to determine how many more movies would come out over the year, and how successful and upcoming movie can be. More data would be required to do that, of course.