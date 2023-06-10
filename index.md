{“*Anime is an important part of our culture!*” ~ Ryota Mitarai from
Danganronpa 3: The End of Hope’s Peak High School}

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
<col style="width: 26%" />
<col style="width: 73%" />
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
<col style="width: 11%" />
<col style="width: 88%" />
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

I first chose to reduce our analysis to only include anime with more
than one episodes, so no movies, one-shots, or distinctive OVAs. We
wanted to get information about anime series with continuous behavior,
even if it was just a two-episode stint. This reduced our pool to 9,181
anime.

## Research Questions

There are a few questions that we hope to answer using this dataset.

1.  What features are most important to predicting the score of an
    anime?

2.  Do the scores of these anime differ based on all users vs. users
    that have that anime marked as completed?

3.  Is there an optimal number of episodes an anime should have to be
    scored well on MyAnimeList?

4.  Can the synopsis of an anime be a good indicator of anime ranking?

### The Pinnacle of Anime: What are the most important contributors?

### Scores Galore: Do users preemptively score anime? Does the general consensus change from all users to users who have marked the anime as ‘completed’?
