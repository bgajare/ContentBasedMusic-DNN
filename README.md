Capstone Project 



# Content Based Approach to Language Agnostic Music Recommendation - Final Report

**Author** 
Bhalchandra Gajare (bhalchandra.gajare@gmail.com)

1. Problem Statement
   Most of the famous music platforms (like Spotify, Youtube Music) that have a large Daily/Monthly Active Users follow a collaborative filtering strategy for music track recommendataions. Such filtering uses metadata of the music (ex: artist, language, user ratings, etc) to predict the likelihood of user getting satisfying recommendations. It is understandable that this is a understatement and in practical life these music platforms are performing much intensive modeling. But, as far as we know, most methods are collaborative filtering based.
   Such methods easily result into a widely known problem called "Filter Bubble" in which the recommendations provided to the user is restricted to a particular set of features (ex: ratings).

    This problem is something all of us would have faced at some point or the other. When a user subscribes to a music platform for the first time, the recommendataions seem very valid and very interesting, but over a course of months and years of using the platform, it can be easily noted that the platform feels to be repetetive and the novelty is lost.

    As a result, there exists a virtual linguistic barrier (recommendation system artifact), i.e a user that only listens to english songs, may never be suggested Spanish dance music or Italian Jazz music.

   The goal of this project is use only the audio content (hence `Content Based`) and without any other metadata from the audio/music tracks and build a model `Music Recommendation` that provides music recommendations of tracks from any other language that matches or sounds similar to the user liked music `language agnostic`
   
2. Model Outcomes or Preddictions
   
   **Type of Learning** Supervised Learning (Classification)
   In General classification algorithms, a sample is mapped to a predicted label / class (ex: apple is classified as Fruit and Brocolli is classified as Vegetable). Though this project uses classification at its core, this really does not produce a true music recommendation system since we do not just want to match the input music to a genre and suggest another language song from the predicted genre. This project treats the problem as a classification problem and uses the model to generate a mathematical fingerprint (learned features) for every song.
   
   a. Training
      Use supervised learning to teach the model to classify several music tracks into a set of 10 genres

   b. Prediction
      Once the model understands musical styles and is able to classify well, we will keep the entire model architecture, except the last stage (decision making for the label). This strategy gives rise a vector of numbers that represent what the model has learned. Note that this vector of numbers do not specifcally mean anything acoustically. They can be thought of as a `mathematical signature` of a given music track

   c. Recommendataion
      We build a index (database) of mathematical signatures of all the songs that the model learns. Now, for the actual recommendation, we use a simple nearest neighbors strategy (i.e find a song whose mathematical signature is most similar to the input song) to provide a recommendation.
   
4. Data Acquisition
5. Data Preprocessung / Preparation
6. Modeling
7. Model Evaluation


### Conclusion 
