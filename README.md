<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/19/Spotify_logo_without_text.svg/1024px-Spotify_logo_without_text.svg.png" width="100" height="100">



# Spotify-EDA 
Performing EDA on 2 Spotify playlist, one with the like songs, other with the dislike songs, in order to gain insight on what makes a desirable track for us.


### EDA!!


**Exploratory data analysis** has been a crucial step in any machine learning application. EDA is a process to visualize data to understand all the characteristics it has and gain insights such as hidden patterns and correlations among features. Many companies use EDA on hunk of data to optimise the operation and maximise profit, but its just not limited to companies, local private organizations also use EDA for better operation.


### Spotify API

<img src="images/Spotify API.png" align="left" width="480" height="300">
Spotify **Application Programming interface** provides set of tools and procedures for developers to access data and functionality from Spotify music streaming platform. Using this API, we can extract details about playlists and tracks. But for that one need to have an authorization by Spotify and get a token which lasts for fixed amount of time and past that, new token needs to be generated for request and response to be approved. 

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br/>

### Data Collection

<img src="images/Json file.png" align="right" width="300" height="480">
For our case, we made two playlist, one containing the tracks we (all team members) like to listen to and one playlist containing tracks that wont meet our taste. Following that, Tom took the authorization token, extracted the playlist id’s and got the file json file containing the track ID and track name, through simple text processing, we extracted all the track id’s and received meticulous file on track details containing 10+ characteristics of each track. 

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br/>

### Data Preparation


At this point, all the data we received is in .Json format, our first step was to convert it to .CSV format for comfortable manipulation. The code used to perform the conversion is provided in the json_to_csv.ipynb file in this repository. During this process, we also shifted the ‘id’ from middle to the left most column as that’s the standard format followed everywhere. 


Right now, all the tracks are divided into two files, one for like tracks and the dislike track in other, in order to perform the EDA, we need all the data in one dataframe and we also don’t want any information leak, so we added new column to both the files as ‘good’ and the dataframe containing the liked songs, we placed ‘1’ for all the rows and ‘0’ in the other dataframe and then concatenated both the dataframe into one, now we can segregate each song whether its liked one or not just by referring the feature ‘good’


After manipulating the dataframe, we removed the features that don’t posses any impact on the analysis such as ‘type’, ‘uri’, ‘track_href’, and ‘analysis_url’. 


### Data Cleaning 


As the data is directly obtained from Spotify, it’s a first-party data, which means the probability of it bring noisy are minute, but still to be sure, we did performed data cleaning. Noticeable observations were obtained during outlier detection through box plots. A lot of datapoints where outside the minimum (q1 - 1.5 * IQR) and maximum(q3 + 1.5 * IQR) range. Initially the thoughts where that these datapoints are noise but after thorough consideration it revealed that these points are the songs that are highly dedicated to that particular characteristic, for example, a lot of datapoints are lying under the minimum threshold in the ‘energy’ plot, so these datapoints are the songs that are just white noise or calm/sleep songs, obviously because of the nature of the song they will be really low on energy. Same way we can see few points above the maximum threshold in ‘Speechiness’ plot, these are the hardcore rap songs, again because of their nature, there will be a lot of lyrics. 


Few more similar scenarios can be seen in different characteristic plots but the reason for all is same, so it doesn’t make sense to remove these points as they are not noise, they are just songs highly dedicated to a particular characteristic. 


### The Good Stuff


And here we begin our long-awaited task, the *** EDA ***.


We started off with the Heatmap to understand the correlation of each feature respect to ‘Liking’. Straight away we can see that characteristic such as ‘Danceability’, ‘Loudness’, ‘Speechiness’, ‘instrumentalness’, and ‘Duration’ have the highest corelation, but we can’t stop here, all these characteristics can impact liking as their values change, i.e., if the danceability is too low then its not liked, if its high then the track is liked, we need to find these thresholds for each of these characteristics.


For that, first we need to select a set od characteristics that has the high correlation to liking as analysing all the characteristics will be exhausting and its not impactful to figure out threshold for characteristics that don’t possess much importance for the listener. We selected all the features that had correlation at least one tenth to the number, either positive or negative. Those features will be 'instrumentalness', 'duration_ms', 'acousticness', 'energy', 'time_signature', 'valence', 'tempo', 'loudness', 'danceability', and 'Speechiness'. After selecting the characteristics, we plotted each characteristic against all the other characteristics and a lot of insights where explored. 


Starting with the duration of the song, it appears that the tracks with duration less than 300000 ms are liked if the acousticness is less than 0.9, energy grater than 0.3, loudness greater than -15 and danceability greater than 0.4. 


Then we have loudness, it appears that the track with the loudness greater than -15 are liked if the energy is higher than 0.3, valence is between 0.1 and 0.9, tempo is between 65 – 90 and between 120 – 160, instrumentalness is almost near 0, danceability is greater than 0.4(more preferred if between 0.6 to 0.9) and acousticness is less than 0.8.


And finally with respect to danceability, it appears that the track with danceability greater than 0.5 is liked if the instrumentalness is almost 0, acousticness is less than 0.8 and energy is more than 0.3.


One more feature/characteristic is still to be analysed is time signature, which can be explored using a pie chart. So we have created two pie charts, one for all the like songs and the other for dislike songs, one easy thing to note is that like songs have 3 different rate of ‘beats per bar’ which are 3, 5, and 4 while for the dislike songs, there are 4 different rates which are 1, 3, 4, and 5. It can be concluded that if the song is 1 beat per bar then its definitely not preferred. 


The insights can be easily explained as


>Duration less than 300000ms,


>Acousticness less than 0.9,


>Energy greater than 0.3,


>Loudness greater than -15,


>Danceability greater than 0.4,


>Valence between 0.1 and 0.9,


>Tempo between 65 – 90 and between 120 – 160,


>instrumentalness is almost near 0,


>time signature is not 1 beat per bar.


Note: the features that are not present in this list do not have clear distribution so that we can put a threshold for like and dislike. 

