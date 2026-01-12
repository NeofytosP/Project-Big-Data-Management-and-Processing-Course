# Project Big Data Management and Processing Course

## 1. Overview 
This is a semester project for course COMP-548DL – Big Data Management and Processing


The objective as proposed was to analyze Spotify Data. To try and analyze the trends and songs' popularity in Greece/Cyprus in order to  assist in recommendation systems. But after having issues with Spark and libraries versions, as suggested by the Professor I decided to compare a MySQL schema and a MongoDB (NoSQ) schema to examine response time of different queries for Spotify Data.


In this project the Data that are being used act as a Sample from the huge volume of Spotify Data that exist in order to compare the two schemas.

## 2. Data Challenges
The data in this project involve in 3 Big Data Dimensions
-  **Volume**                                                                                                                                                                                                                                                                              
   Spotify contains over 100 million songs, new songs are being added every day.                                                                                                                                                                                                                                                 
   Except from data about songs, data about streamings of songs, playlists, audiobooks, audio not related to music, podcasts and other data are being stored in the Spotify Databases.
   
- **Velocity**                                                                                                                                                                                                                                                                                                                      Data are being generated/updated at a fast rate. Each time a song is being played, the streams of that song is updated and its popularity is also increasing. Data about pauses, skips are also being recorded. Millions of users use Spotify services at the same time so these data are being updated all the time.                                                                                                                                                                                                                                      
- **Variety**                                                                                                                                                                                                                                                                                                                       Each entry of a song contain a lot of different features like genre, popularity, danceability, tempo, energy, artist name, track name, album name, producer, songwriter and many other features. Also as mentioned above there are a lot of features for podcasts, stream details (skips, replays etc) along with many other     different types of data.

  ## 3.
