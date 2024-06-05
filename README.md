# Predicting-IMDb-User-Rating

## Description
When new movies are released into the wild (theatres or internet), aside from watching the trailier, online movie ratings and recommendations have become one of the first things people check for before deciding whether they should watch the movie. That could have a serious impact on the box office revenue, especially when the box office generates $11 billion revenue annually in the US. Although a single single negative movie review can’t make or break a film, thousands or millions of them can definitely hurt. So what should you focus on if you were to produce your next film?

## Objective
The goal of this project is to use linear regression to predict IMDb user rating.

## Methodology
 - Data scope: Top 1,000 (1,136 to be exact) movies on IMDb, ranked by IMDb popularity, released in 2018. I've chosen 2018 to gather the most recent data, where still gave it at least a year to gather ratings.
 - Main libraries used:
   - Web-scraping: BeautifulSoup, Selenium, fake_useragent, requests
   - Data proccessing, cleaning, and exploring: numpy, pandas, seaborn, matplotlib.pyplot
   - Regression: scipy.stats, statsmodels, sklearn
 - Target: `imdb_user_rating` (Ex: The user rating for "Avengers: Infinity War" is 8.5)
 - Features that I started with:
    - Genres
        - `genre_list` - all genres listed for the movie
            Then, I went ahead and chose the below top genres to include in the model. The rest is groupd into `other_genre`.
        - `genre_count` - number of genres listed for the movie
        - `Drama` - movies that with "Drama" listed in the `genre_list`
        - `Comedy` - movies that with "Comedy" listed in the `genre_list`
        - `Thriller`  - movies that with "Thriller" listed in the `genre_list`
        - `Action` - movies that with "Action" listed in the `genre_list`
        - `Horror` - movies that with "Horror" listed in the `genre_list`
        - `Crime` - movies that with "Crime" listed in the `genre_list`
        - `Romance` - movies that with "Romance" listed in the `genre_list`
        - `other_genre` - genres of movies that didn't have enough movies in the genre
    - IMDb user rating count
        - `imdb_user_rating_count` - number of reviews for the movie
        - `imdb_user_rating_count_squared` - `imdb_user_rating_count` squared
        - `imdb_user_rating_count_log` - log transformation of `imdb_user_rating_count`
    - Runtime
        - `runtime_minutes` - the time between the starting of the movie upto the end of the credits scene
        - `runtime_minutes_squared` - `runtime_minutes` squared
        - `runtime_minutes_log` - log transformation of `runtime_minutes`
        - `runtime_minutes_loglog` - double log transformation of `runtime_minutes`
    - Release date
        - `Weekend` - dummy variable for movie that was released during the weekend. Note that Friday is included, as Friday is often included for "opening weekend".
        - Month - the month that the movie was released in. Note that `Apr` is dropped as these are dummy variables.
            - `Jan` - movie was released in Jan 2018.
            - `Feb` - movie was released in Feb 2018.
            - `Mar` - movie was released in Mar 2018.
            - `May` - movie was released in May 2018.
            - `Jun` - movie was released in Jun 2018.
            - `Jul` - movie was released in Jul 2018.
            - `Aug` - movie was released in Aug 2018.
            - `Sep` - movie was released in Sep 2018.
            - `Oct` - movie was released in Oct 2018.
            - `Nov` - movie was released in Nov 2018.
            - `Dec` - movie was released in Dec 2018.
        - Season - the season that the movie was released in. Note that `Fall` was dropped as these are dummy variables.
            - `Spring` - movie was released in Spring 2018.
            - `Summer` - movie was released in Summer 2018.
            - `Winter` - movie was released in Winter 2018.
- Outliers: There are 3 outliers that were removed. 
  - "Black Panther" - extremely high number of reviews.
  - "Avengers: Infinity War" - extremely high number of reviews
  - "La Flor" - 13-hour runtime
- Missing data: There are 4 movies without any runtime information, hence there were removed.          
- Regression: I used OLS as my model and used train/test (80 and 20) split to validate the accuracy of my model. 

## Results

### Final features included in the model
- `imdb_user_rating_count_log` with p-value 0.000	
- `runtime_minutes_log` with p-value 0.000	
- `Weekend` with p-value 0.000	
- `Drama` with p-value 0.000	
- `Action` with p-value 0.000	
- `Thriller` with p-value 0.001
- `Horror` with p-value 0.000	

### R^2, condition number, and coefficients

My model has condition number 282, R^2 of 0.34, with test score of 0.37. 

The results indicate that...
- For a 1% increase in number of IMDb reviews, the IMDb user rating changes by 0.09%
- For a 1% increase in movie runtime, the IMDb user rating changes by 14.12%
- If this movie includes "Drama" as one of the genres, the IMDb user rating changes by 94.75%
- If this movie includes "Action" as one of the genres, the IMDb user rating changes by -70.28%
- If this movie includes "Thriller" as one of the genres, the IMDb user rating changes by -45.6%
- If this movie includes "Horror" as one of the genres, the IMDb user rating changes by -72.17%

This suggests that try not to have your movie runtime too short, ensure that your film has the "Drama" factor, and lastly avoid focusing too much elements in "Action", "Horror", or "Thriller".

The R^2 isn't actually very high, so this leads to our next section "Future Work".

## Future Work

If I had more time, I'd love to include the following datasets in the model to see if it would improve the model accuracy:
- Demographics - As the society is now paying more attention to diversity and inclusion, it'd be interesting to see if that has any effect on the model.
- Nominations & Awards the cast has recevied until the one year from the release date: As awards and nomincations always create a lot of buzz and may lead to more reviews being submitted online, hence rating could be greatly influenced.
- Domestic Gross - I'm assuming that as revenue increases, more people are watching the movies, meaning that more reviews will be submitted. This shouhld also lead to great impact on the user rating.

## Workflow
Follow the jupyter notebooks in the order below:
- 01 IMDb Web Scraping.ipynb
- 02 Regression Analysis.ipynb



