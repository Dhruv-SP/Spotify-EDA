# Spotify-EDA
Performing EDA on 2 Spotify playlist, one with the like songs, other with the dislike songs, in order to gain more experience with EDA

### EDA!!


**Exploratory data analysis** has been a crucial step in any machine learning application. EDA is a process to visualize data to understand all the characteristics it has and gain insights such as hidden patterns and correlations among features. Many companies use EDA on hunk of data to optimise the operation and maximise profit, but its just not limited to companies, local private organizations also use EDA for better operation.


### Spotify API


Spotify **Application Programming interface** provides set of tools and procedures for developers to access data and functionality from Spotify music streaming platform. Using this API, we can extract details about playlists and tracks. But for that one need to have an authorization by Spotify and get a token which lasts for fixed amount of time and past that, new token needs to be generated for request and response to be approved. 


For our case, we made two playlist, one containing the tracks we (all team members) like to listen to and one playlist containing tracks that wont meet our taste. Following that, Tom took the authorization token, extracted the playlist id’s and got the file json file containing the track ID and track name, through simple text processing, we extracted all the track id’s and received meticulous file on track details containing 10+ characteristics of each track. 
