# capstone
# Spotify Recommendation System
# Jesse Moore
# Instructor Mark Barbour

# Summary

## Business and Data Understanding: This system's goal is to recommend songs that align with users' preferences and enhance their music discovery. By leveraging Spotify's dataset, this project aims to provide personalized recommendations based on song characteristics like acousticness, tempo, and valence (mood).

## Data: The dataset, sourced from Spotify's API, consists of 105,076 unique artists and 412,679 songs. Data preparation involved extracting key features for each song, followed by normalizing and transforming the data to make it suitable for modeling.

## Libraries: The standard models were used, with scikit-learn used for KNNeighbors.

## Modeling: For modeling, I used a content-based approach, which is the most viable method without user-item interaction data. The model uses K-Nearest Neighbors (KNN), which calculates the cosine similarity between songs to find the most similar tracks based on their features.

## Evaluation: After evaluating the model, I observed that the recommendations were highly relevant to user input, with songs sharing significant features. However, limitations include the inability to account for user-specific preferences without additional data, which could be addressed in future work.

## Insights and limitations: from the project show that music recommendations are highly influenced by track features, and potential improvements include incorporating genre-based filters and user feedback for more personalized recommendations.

## Thank you for reading, and I hope you enjoy exploring the system!

# Problem Statement

Our client's own a music-streaming service and are enlisting our company toa develop a recommendation system for their users. This recommendation system will work based upon measuring the cosine similarity between tracks latent features.

## Business Objective

Our business objective is to create a recommendation system that will enhance our user's enjoyment of music by providing them with songs that they will enjoy, thus enhancing their enjoyment of our streaming service.

To achieve this we will utilize a content-based recommendation system that will recommend songs based upon the previous song the user has played.

## Stakeholder Questions

How can we analyze our song library to provide a recommendation system to our users?

What roles do features such as 'valence' and 'energy' play in a song's popularity?

# Data Source

We utilized the Spotify Track Dataset dataset available via Kaggle, which contains 125,000 songs spread across 125 musical genres. The dataset tracks such features as song popularity, a song's energy and loudness, among many others.

## Data Description

Our dataframe has 21 columns with 114000 rows, and has 3 null values.

And has the following columns:

'popularity' - How popular the track is.
'duration_ms' - How long the track is in milliseconds.
'explicit' - Whether the song is considered explicit or not, a boolean value.
'danceability' - The measure of how easy it is to dance to the song ranging from 0.0 to 1.0.
'energy' - The measure of intensity of the song, ranging from 0.0 to 1.0.
'key' - This represents the root note of the musical key the song is in, i.e. 'C', but does not reflect the major or minor aspect of the key. Given as a string object.
'loudness' - The loudness in decibels.
'mode' - The mode reflects whether the song is major (0) or minor (1).
'speechiness' - The level of spoken word on a track, ranging from 0.0 to 1.0. A higher value of speechiness, the more spoken words the track employs.
'acousticness' - The level of acoustic instrumentation versus electric, ranging from 0.0 to 1.0. A 1.0 reflects that the song is percieved to be 100% acoustic.
'instrumentalness' - The level of singing / vocalization on a track ranging from 0.0 to 1.0. A higher value of instrumentalness, the less vocalizing a song will contain. Note that, 'ooh' and 'aah' sounds are considered instrumental sounds.
'liveness' - Indicates to what degree the song was performed in front of an audience, ranging from 0.0 to 1.0. Higher values indicate that the song was most likely performed live in concert.
'valence' - This measures the tracks positivity or negativity, in terms of musical sound (not reflecting upon lyrical themes), ranging from 0.0 to 1.0, with the closer to 1.0 a track is, the 'happier' it sounds.
'tempo' - the tracks tempo in beats per minute / BPMs.
'time_signature' - a tracks time signature as experessed as a numerical value from 3 through 7, to be understood as being followed by '/4', such as '3/4', '4/4'...etc.
'track_genre' - the genre most commonly associated with the the track
From our descriptive statistics of our 'popularity' feature we see that the mean average popularity is 33.431794, with a standard deviation of 22.826615.

Next, we will feature engineer a new column called root_note, that will reflect the root note and the major or minor mode that the key is in. For example, C Major, D sharp minor.

Next, we will create another new feature based upon the key and now also the mode, 'actual_key'. This will expand upon the root_note feature and tell us the root note and whether the song is in a major or minor mode. This is usually what is refered to as the key of the song.

# Modeling

## Baseline model

We are using a K Nearest Neighbors method for our baseline model, that takes a given data point and searches for a given number (k) of data points that are similar (neighbors).

These neighbors are similar based upon their cosine similarity. Cosine similarity measures the angle between vectors or latent features in our dataset. The closer our cosine similarity is to 1, the more similar these songs are to each other, based upon the features.

Testing our recommendation system we input the artist: 'Elvis Presley' and the track: 'Blue Christmas', and the recommended track that our system gave us is: Recommended Track: '10 Feet Down' by the artists: NF, Ruelle.

Though this song shares a high cosine similarity with our Elvis song, 0.9993, and upon listening to these tracks, one can hear a similar vocal melody to Elvis' crooning on 'Blue Christmas', but overall the songs do not seem similar and doing genre research at AllMusic which reveals that this NF and Nuelle song is considered religious hip hop, I decided that refining the model would be necessary.

## Final Model

Dropping features such as 'energy', 'loudness', 'speechiness', 'valence','explicit', while leaving 'danceability', 'acousticness' and 'instrumentalness' as our features gave us a more favorable results, with our recommendation system returning the Johnny Cash song 'Give My Love to Rose', which upon listening to the two songs back to back, feels much more appropriate.

## Evaluation

'Blue Christmas' and 'Give My Love to Rose' have a cosine similarity of 0.9996. This indicates that, given the features that we have selected for, these two tracks are very similar. Picking a random (not recommended) track, we can that although Elvis and Half Crazy may be closer in popularity, other latent features, such as acousticness and root_key (E and F are closer to each other in pitch than E and B) have more importance in our model, as the Half Crazy track and Elvis only have a cosine similarity of 0.4264

# Conclusion & Future Steps

While it is impossible to know how well our listeners will like our model, we have created something that we can test, improve upon and further explore for our clients.

Some future ideas to consider: Filtering tracks by genres, recommending tracks that are only within the same genre as the original chosen song, creating playlists of that genre or of multilple genres.

Allowing the user to 'dislike' tracks, and returning ones that are dissimilar to them is also a feature that we can implement.

Collecting user data such as if our recommendations were followed, what our listener's would rate for metrics such as 'energy', etc. are all things we can add to our model in the future.

For more information please see:
or further details, please refer to the following linked project notebook and presentation:


[project_repository](https://github.com/JesseMooreDS/capstone) | [notebook](https://github.com/JesseMooreDS/capstone/blob/main/project.ipynb) | [presentation]((https://github.com/JesseMooreDS/capstone/blob/main/presentation.pdf)
