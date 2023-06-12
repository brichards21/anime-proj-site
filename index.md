“*Anime is an important part of our culture!*” ~ Ryota Mitarai from
Danganronpa 3: The End of Hope’s Peak High School

![](./img/spy-family.gif)

Indeed it is, Ryota. Indeed it is.

Anime, a term derived from the Japanese abbreviation of “animation,” has
become a significant part of global popular culture in recent decades.
Its relevance in today’s culture can be attributed to several factors,
including its unique art style, diverse storytelling techniques, and the
ability to explore complex themes.

Anime’s storytelling techniques are diverse and encompass a wide range
of genres and themes. Perhaps you’ve even heard of a few! From
action-packed shonen series like “Dragon Ball” and “Naruto” to emotional
dramas like “Your Lie in April” and “Clannad,” there is an anime for
**everyone** out there! Anime also explores genres beyond traditional
boundaries, such as psychological thrillers (“Death Note”), science
fiction (“Ghost in the Shell”), and fantasy (“Attack on Titan”).

In recent years, the popularity of anime has skyrocketed, thanks to
digital platforms and streaming services making it easily accessible to
a global audience. Anime conventions and events draw massive crowds,
showcasing the passion and enthusiasm of fans. The influence of anime
has permeated various aspects of popular culture, including fashion,
music, video games, and even Hollywood adaptations.

With dozens of new series being released each season, it’s no surprised
that fans and providers alike often wonder the age-old question: What
makes an anime stick? What makes an anime go down in history like
absolute titans (no pun intended) like Attack on Titan, Naruto, Bleach,
Dragon Ball Z, and more?! And how do we know and keep track of how
audiences are receiving this media?

Well, look no further! In comes
[MyAnimeList.net](https://myanimelist.net/).

MyAnimeList.net is an online platform dedicated to providing a
comprehensive database and community-driven hub for anime and manga
enthusiasts. Serving as a centralized resource, the website allows users
to create personal profiles and maintain detailed lists of anime series,
films, and manga they have consumed.

At its core, MyAnimeList.net offers a vast catalog of titles,
encompassing a wide range of genres and themes. Users can search and
explore the database to discover new anime and manga, while accessing
essential information such as synopses, release dates, and production
details.

The website also facilitates user engagement through its rating and
review system, enabling community members to express their opinions on
individual titles. This user-generated content fosters a vibrant
environment for critical discourse, as well as the exchange of
recommendations and insights.

## Data and Data Cleaning

We downloaded three [dataset housed on
Kaggle](https://www.kaggle.com/datasets/hernan4444/anime-recommendation-database-2020?select=anime.csv)
scraped between February 26th and March 20th containing information
about 17,562 anime and the preference from 325,772 different users.

The `anime` dataset, which is the main dataset of interest detailed the
core information of each anime listed.

We retained the following information from the `anime` dataset:

<table>
<colgroup>
<col style="width: 27%" />
<col style="width: 72%" />
</colgroup>
<thead>
<tr class="header">
<th>Column</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>MAL_ID</td>
<td>MyAnimelist ID of the anime. Unique for each anime.</td>
</tr>
<tr class="even">
<td>Name</td>
<td>full name of the anime</td>
</tr>
<tr class="odd">
<td>Score</td>
<td>average score of the anime given from all users in the MyAnimelist
database. Score out of 10 pts.</td>
</tr>
<tr class="even">
<td>Genres</td>
<td>comma separated list of genres for this anime. (e.g. Action,
Adventure, Comedy, Drama, etc.)</td>
</tr>
<tr class="odd">
<td>Type</td>
<td>TV, movie, OVA, etc</td>
</tr>
<tr class="even">
<td>Episodes</td>
<td>number of episodes</td>
</tr>
<tr class="odd">
<td>Aired</td>
<td>broadcast date (e.g. Apr 3, 1998 to Apr 24, 1999)</td>
</tr>
<tr class="even">
<td>Studios</td>
<td>comma separated list of studios</td>
</tr>
<tr class="odd">
<td>Source</td>
<td>Manga, Light novel, Book, etc.</td>
</tr>
<tr class="even">
<td>Duration</td>
<td>duration of the anime per episode (e.g. 24 min. per ep.)</td>
</tr>
<tr class="odd">
<td>Rating</td>
<td>age rate (e.g. R - 17+ (violence &amp; profanity))</td>
</tr>
<tr class="even">
<td>Ranked</td>
<td>ranking position based on the score (e.g 28))</td>
</tr>
<tr class="odd">
<td>Popularity</td>
<td>position based on the number of users who have added the anime to
their list</td>
</tr>
<tr class="even">
<td>Members</td>
<td>number of community members that are in this anime’s “group”</td>
</tr>
<tr class="odd">
<td>Favorites</td>
<td>number of users who have the anime in their “favorites” list</td>
</tr>
<tr class="even">
<td>Watching</td>
<td>number of users who have marked the anime as ‘watching’</td>
</tr>
<tr class="odd">
<td>Completed</td>
<td>number of users who have marked the anime as ‘completed’</td>
</tr>
<tr class="even">
<td>On-Hold</td>
<td>number of users who have marked the anime as ‘on-hold’</td>
</tr>
<tr class="odd">
<td>Dropped</td>
<td>number of users who have marked the anime as ‘dropped’</td>
</tr>
<tr class="even">
<td>Plan to Watch</td>
<td>number of users who have marked the anime as ‘plan to watch’</td>
</tr>
</tbody>
</table>

Additionally, we downloaded the `anime_with_synopsis` and the
`rating_complete` data. The key information retained in the
`anime_with_synopsis` data is the synopsis of each anime as recorded on
the MyAnimeList.net site.

We left-joined the `anime` data with the `anime_with_synopsis` data to
retain synopsis information on all anime that had synopsis information
in the `anime` dataset.

The `rating_complete` data only considers anime that users have marked
as ‘completed’. It gives the `user_id`, `anime_id` as it corresponds to
the MyAnimeList ID of the anime the user has rated, and the `rating`
being the rating that the user has assigned to that particular anime
that they have marked as completed. In order to synthesize this
information, we aggregated the data by anime id and derived the average
score given to each anime by users that have marked that anime as
completed. This information was also left-joined to the dataset with the
original anime data and synopsis data in order to retain the average
score of each anime as according to users that have marked the anime as
completed.

Thus, we have two more columns of interest in our dataset.

<table>
<colgroup>
<col style="width: 19%" />
<col style="width: 80%" />
</colgroup>
<thead>
<tr class="header">
<th>Column</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Synopsis</td>
<td>string with the synopsis of the anime</td>
</tr>
<tr class="even">
<td>Score_completed</td>
<td>average score of the anime given from users that have marked the
anime as ‘completed’ in the MyAnimelist database. Score out of 10
pts.</td>
</tr>
</tbody>
</table>

    ## [1] 601

I first chose to reduce our analysis to only include anime with more
than one episodes, so no movies, one-shots, or distinctive OVAs. We
wanted to get information about anime series with continuous behavior,
even if it was just a two-episode stint. This reduced our pool to 9,181
anime. Additionally, the `genres`, `aired`, and `studios` variables were
reformatted for the purpose of analysis. \*Note: For genre, we retained
information about genres that had a frequency of at least 2% of all the
genres listed in the dataset.

All data cleaning was conducted using NumPy and Pandas in Python. The
code for data cleaning can be found here.

## Research Questions

There are a few questions that we hope to answer using this dataset.

1.  What features are most important to predicting the score of an
    anime?

2.  Do the scores of these anime differ based on all users vs. users
    that have that anime marked as completed?

3.  Is there an optimal number of episodes an anime should have to be
    scored well on MyAnimeList?

4.  Can the synopsis of an anime be a good indicator of anime ranking?

### The Pinnacle of Anime: What are the most important contributors to predicting the popularity (score) of an anime?

We start by checking for multicollinearity between our predictors of
interest in order to reduce dimensionality and stabilize the variance of
our estimated coefficients. Because of their direct relationship with
the dependent variable of interest (score), we omit `ranked`,
`popularity`, and `score_completed`

![](index_files/figure-markdown_strict/unnamed-chunk-12-1.png)

Notably, number of members, favorites, watching, completed, on-hold,
dropped, and plan to watch are moderately to highly correlated. In order
to correct for this, we will retain number of community members in each
anime’s group as the representation of membership to the anime’s fanbase
in our dataset. Additionally, start year is highly correlated with end
year so we’ll just retain information on start year and instead create a
variable representing number of years running.

![](index_files/figure-markdown_strict/unnamed-chunk-14-1.png)

After removing the variables strongly correlated with number of
variables, we have a better distribution of variables without unexpected
multicollinearity. We move on to stepwise selection with these
predictors as well as our non-numeric predictors to choose the best
variables to model MyAnimeList score.

To recall, we retain the following variables as the subset of predictors
to choose from: type, number of episodes, primary studio, secondary
studio, source, rating, number of members in that anime’s community,
duration in minutes per episode, airing start year, number of animation
studios working on the anime, and binary/indication variables for the
following variables: Action, Adventure, Comedy, Drama, Fantasy,
Historical, Kids, Magic, Mecha, Romance, School, Sci-Fi, Shounen, Slice
of Life, and Supernatural.

In order to validate the generalizability, we will perform stepwise
selection on 80% of our dataset, which we’ll call the training data. The
remaining 20% will be saved to test the accuracy of our model on.

After going through stepwise selection, we yield the following model:

*E*\[*S**c**o**r**e*\]  − 14.4 + 0.0004*E**p**i**s**o**d**e**s* + 0.16*R**a**t**i**n**g*<sub>*P**G* − 13</sub> + 0.05*R**a**t**i**n**g*<sub>*P**G*</sub> + 0.22*R**a**t**i**n**g*<sub>*R*</sub> − 0.16*R**a**t**i**n**g*<sub>*R*+</sub> − 0.21*R**a**t**i**n**g*<sub>*R**x*</sub> + 0.000001*M**e**m**b**e**r**s* + 0.02*D**u**r**a**t**i**o**n* + 0.02*A**c**t**i**o**n* + 0.15*C**o**m**e**d**y* + 0.31*D**r**a**m**a* + 0.26*H**i**s**t**o**r**i**c**a**l*+

0.06*M**a**g**i**c* + 0.04*S**c**h**o**o**l* + 0.28*S**h**o**u**n**e**n* + 0.23*S**l**i**c**e* *o**f* *L**i**f**e* + 0.01*S**t**a**r**t**Y**e**a**r* + 0.03*N**u**m*. *Y**e**a**r**s* *R**u**n**n**i**n**g*

where *E*\[*S**c**o**r**e*\] is the expected value of the score of each
anime.

    ## 
    ## Call:
    ## lm(formula = score ~ episodes + rating + members + duration_mins + 
    ##     action + comedy + drama + historical + magic + school + shounen + 
    ##     slice_of_life + start_year + num_years_running, data = train)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -3.5290 -0.3887  0.0254  0.4292  1.8228 
    ## 
    ## Coefficients:
    ##                                        Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)                          -1.435e+01  1.973e+00  -7.271 4.10e-13 ***
    ## episodes                              3.973e-04  1.832e-04   2.169 0.030137 *  
    ## ratingPG-13 - Teens 13 or older       1.581e-01  3.079e-02   5.134 2.95e-07 ***
    ## ratingPG - Children                   5.012e-02  4.447e-02   1.127 0.259768    
    ## ratingR - 17+ (violence & profanity)  2.186e-01  4.212e-02   5.190 2.19e-07 ***
    ## ratingR+ - Mild Nudity               -1.615e-01  4.207e-02  -3.838 0.000126 ***
    ## ratingRx - Hentai                    -2.056e-01  4.048e-02  -5.078 3.95e-07 ***
    ## members                               1.348e-06  5.028e-08  26.804  < 2e-16 ***
    ## duration_mins                         1.640e-02  1.064e-03  15.421  < 2e-16 ***
    ## action1                               1.615e-02  2.269e-02   0.712 0.476548    
    ## comedy1                               1.481e-01  2.062e-02   7.184 7.77e-13 ***
    ## drama1                                3.114e-01  2.488e-02  12.514  < 2e-16 ***
    ## historical1                           2.626e-01  3.652e-02   7.190 7.43e-13 ***
    ## magic1                                6.428e-02  3.200e-02   2.009 0.044598 *  
    ## school1                               3.519e-02  2.608e-02   1.349 0.177276    
    ## shounen1                              2.779e-01  2.476e-02  11.224  < 2e-16 ***
    ## slice_of_life1                        2.273e-01  2.836e-02   8.015 1.36e-15 ***
    ## start_year                            1.011e-02  9.820e-04  10.298  < 2e-16 ***
    ## num_years_running                     3.291e-02  9.432e-03   3.489 0.000489 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.6343 on 5078 degrees of freedom
    ##   (2247 observations deleted due to missingness)
    ## Multiple R-squared:  0.3634, Adjusted R-squared:  0.3612 
    ## F-statistic: 161.1 on 18 and 5078 DF,  p-value: < 2.2e-16

These are the genres that are more likely to have a high score on
MyAnimeList.net in order:

1.  Drama

2.  Historical

3.  Shounen

4.  Slice of Life

5.  Comedy

6.  Magic

7.  School

8.  Action

Now, you may be wondering for example, I mean, from absolute modern day
anime titans like My Hero Academia and Jujutsu Kaisen, it’s no doubt
that action anime encompass a huge portion of the hits right now.
However… action is also the most frequently reported genre in 2020. So
while it’s a standout among the hits, in the grand scheme of things,
while there are amazing action anime that are being ranked and perceived
well, there are also action anime out there that are performing less
favorably among crowds. In fact, it seems that the action genre may even
be oversaturated with the good, the bad, and the ugly. In other words,
purely slapping the genre of action on your anime doesn’t make it an
automatic hit. Yes, it’s true. Audiences won’t just froth at the mouth
at characters going toe-to-toe in combat without it having that special
‘umph’ to it that really makes it a generational favorite.

### Scores Galore: Do users preemptively score anime? Does the general consensus change from all users to users who have marked the anime as ‘completed’?
