# Project Big Data Management and Processing Course
# MySQL Schema and MongoDB Schema Benchmark

## 1. Overview 
This is a semester project for course COMP-548DL – Big Data Management and Processing


The objective as proposed was to analyze Spotify Data. To try and analyze the trends and songs' popularity in Greece/Cyprus in order to  assist in recommendation systems. But after having issues with Spark and libraries versions, as suggested by the Professor I decided to compare a MySQL schema and a MongoDB (NoSQ) schema to examine response time of different queries for Spotify Data.


In this project the Data that are being used act as a Sample from the huge volume of Spotify Data that exist in order to compare the two schemas.


Three databases are being used, a MySQL database , a MongoDB database that is being created local in my computer machine so it will use same resources as MySQL and a MongoDB atlas free cluster (a free cloud database where MongoDB offer limited resource)

MongoDB is chosen to be used locally because when response time is being calculated on the cloud database latency will also affect response time while also the free cluster will not use same recourses as the MySQL that will be using my computer's resources. 

Then queries are being designed to compare the databases for different cases.

## 2. Data Challenges
The data in this project involve in 3 Big Data Dimensions
-  **Volume**                                                                                                                                                                                                                                                                              
   Spotify contains over 100 million songs, new songs are being added every day.                                                                                                                                                                                                                                                 
   Except from data about songs, data about streamings of songs, playlists, audiobooks, audio not related to music, podcasts and other data are being stored in the Spotify Databases.
   
- **Velocity**                                                                                                                                                                                                                                                                                                                      Data are being generated/updated at a fast rate. Each time a song is being played, the streams of that song is updated and its popularity is also increasing. Data about pauses, skips are also being recorded. Millions of users use Spotify services at the same time so these data are being updated all the time.                                                                                                                                                                                                                                      
- **Variety**                                                                                                                                                                                                                                                                                                                       Each entry of a song contain a lot of different features like genre, popularity, danceability, tempo, energy, artist name, track name, album name, producer, songwriter and many other features. Also as mentioned above there are a lot of features for podcasts, stream details (skips, replays etc) along with many other     different types of data.

## 3. Data
The dataset I used is from https://www.kaggle.com/datasets/amitanshjoshi/spotify-1million-tracks/data


*Description*:

This dataset is about spotify tracks (artist,track name) and tracks' audio features.
It was extracted from the Spotify platform using the Python library "Spotipy", which allows users to access music data provided via APIs. The dataset collected includes about 1 Million tracks with 19 features between 2000 and 2023. Also, there is a total of 61,445 unique artists and 82 genres in the data.

The data are already cleaned and prepared in order to be utilized for research purposes.

**Features**:
- Artist Name
- Track Name
- Track Id
  
*Audio Features*

- Genre
- Popularity (0 to 100 with 100 most popular)
- Year (From 2000 to 2023)
- Danceability (Track suitability for dancing 0.0 to 1.0 with 1.0 most 'danceable')
- Energy (Measure of intensity 0.0 to 1.0 with 1.0 most intense)
- Key (The key the track is in -1 to -11)
- Loudness (Overall loudness of track in decibels -60 to 0 dB)
- Mode (Modality of track Major '1'/Minor '0')
- Speechiness (Presence of spoken words in the track)
- Acousticness (Confidence measure from 0 to 1 of whether the track is acoustic)
- Instrumentalness (Whether tracks contain vocals 0.0 to 1.0)
- Liveness (Presence of audience in the recording 0.0 to 1.0)
- Valence (Musical positiveness 0.0 to 1.0)
- Tempo (Tempo of the track in beats per minute-BPM)
- Time_signature (Estimates time signature 3 to 7)
- Duration_ms (Duration of track in milliseconds)

A small preview can be found here [Dataset](Dataset)
## 4. Databases Schemas
### MySQL Schema
MySQL contains 3 tables, one table with the artists, one with the tracks and one with the track features


CREATE SCHEMA 'spotify' ;


USE 'spotify';


CREATE TABLE artists (                                                                                                                                                                                                        
                      artist_id VARCHAR(50) PRIMARY KEY,                                                                                                                                                                                                        
                      artist_name VARCHAR(50)                                                                                                                                                                                                        
                      );


CREATE TABLE tracks (                                                                                                                                                                                                        
                     track_id VARCHAR(50) PRIMARY KEY,                                                                                                                                                                                                        
                     track_name VARCHAR(50) NOT NULL,                                                                                                                                                                                                        
                     release_year YEAR,                                                                                                                                                                                                        
                     genre VARCHAR(50),                                                                                                                                                                                                        
                     popularity INT,                                                                                                                                                                                                        
                     duration_ms INT,                                                                                                                                                                                                        
                     artist_id VARCHAR(50),                                                                                                                                                                                                        
                     FOREIGN KEY (artist_id) REFERENCES artists(artist_id)                                                                                                                                                                                                        
                     );
                     

CREATE TABLE track_features (                                                                                                                                                                                                                                                                                        
                            track_id VARCHAR(50) PRIMARY KEY,                                                                                                                                                                                                                                
                            danceability FLOAT,                                                                                                                                                                                                        
                            energy FLOAT,                                                                                                                                                                                                        
                            'key' INT,                                                                                                                                                                                                        
                            loudness FLOAT,                                                                                                                                                                                                        
                            'mode' INT,                                                                                                                                                                                                        
                            speechiness FLOAT,                                                                                                                                                                                                        
                            acousticness FLOAT,                                                                                                                                                                                                        
                            instrumentalness FLOAT,                                                                                                                                                                                                        
                            liveness FLOAT,                                                                                                                                                                                                        
                            valence FLOAT,                                                                                                                                                                                                        
                            tempo FLOAT,                                                                                                                                                                                                        
                            time_signature INT,                                                                                                                                                                                                        
                            FOREIGN KEY (track_id) REFERENCES tracks(track_id)                                                                                                                                                                                                        
                            );             

With indexes on track_name, release_year, genre and popularity

### Local MongoDB Schema
The id of each document will be the track id instead of the id set by MongoDB 


{                                                                                                         
       "_id": id,                                                                                                                                                                                                                  
        "track_name": string,                                                                                                         
        "artist_name": string,                                                                                                         
        "release_year": int,                                                                                                         
        "genre": string,                                                                                                         
        "popularity": int,                                                                                                         
        "duration_ms": int,                                                                                                         
        "metrics": {                                                                                                         
            "danceability": float,                                                                                                         
            "energy": float,                                                                                                         
            "key": int,                                                                                                         
            "loudness": float),                                                                                                         
            "mode": int),                                                                                                         
            "speechiness": float),                                                                                                         
            "acousticness": float,                                                                                                         
            "instrumentalness": float,                                                                                                         
            "liveness": float,                                                                                                         
            "valence": float,                                                                                                         
            "tempo": float),                                                                                                         
            "time_signature": int)                                                                                                         
            }                                                                                                         
         }     
   
With indexes being created for:


- track_name
- artist_name
- release_year
- genre
- popularity
- duration_ms
- metrics.energy


### Cloud MongoDB Schema
The cloud database will use the same schema as the local database but because of resources limitations only 1 million data are being stored and indexes are created only for:


- artist_name
- release_year
- genre
- popularity

## 5. Project
The whole code can be found here [Code](Benchmark)
This project makes 8 comparisons between the databases. Different type of queries are being designed to compare the databases in each comparison phase. More queries could be used and added in the future for more accurate results and to test bigger range of queries
### Comparison 1.
First the insertion time is being compared for each database
### Comparison 2 and 3.
MySQL contains 3 tables, 2 main tables with tracks and trackfeatures.

These two comparisons are to check the response time for querying separately each table
### Comparison 4
Here the databases are being compared for retrieving all the data
### Comparison 5
The databases are being compared for Simple Queries
### Comparison 6
The databases are being compared for Filter Queries
### Comparison 7 
The databases are being compared for Range Queries
### Comparison 8
The databases are being compared for Aggregations
## 6. Project Reproducibility
This project can easily be reproduced.
All that is needed is to download the dataset from kaggle, install MySQL and MongoDB Development and install 2 libraries for each database, pymongo and mysql.connector. Also the Pandas library is needed to handle easier the dataset and the insertion in the databases.
