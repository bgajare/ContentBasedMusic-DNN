Capstone Project 



# Content Based Approach to Language Agnostic Music Recommendation - Final Report

**Author** 
Bhalchandra Gajare (bhalchandra.gajare@gmail.com)

## 1. Problem Statement


   Most of the famous music platforms (like Spotify, Youtube Music) that have a large Daily/Monthly Active Users follow a collaborative filtering strategy for music track recommendataions. Such filtering uses metadata of the music (ex: artist, language, user ratings, etc) to predict the likelihood of user getting satisfying recommendations. It is understandable that this is a understatement and in practical life these music platforms are performing much intensive modeling. But, as far as we know, most methods are collaborative filtering based.
   
   Such methods easily result into a widely known problem called "Filter Bubble" in which the recommendations provided to the user is restricted to a particular set of features (ex: ratings).
   
   This problem is something all of us would have faced at some point or the other. When a user subscribes to a music platform for the first time, the recommendataions seem very valid and very interesting, but over a course of months and years of using the platform, it can be easily noted that the platform feels to be repetetive and the novelty is lost.

   As a result, there exists a virtual linguistic barrier (recommendation system artifact), i.e a user that only listens to english songs, may never be suggested Spanish dance music or Italian Jazz music.

   The goal of this project is use only the audio content (hence `Content Based`) and without any other metadata from the audio/music tracks and build a model `Music Recommendation` that provides music recommendations of tracks from any other language that matches or sounds similar to the user liked music `language agnostic`
   
## 2. Model Outcomes or Preddictions
   
   **Type of Learning**  -- Supervised Learning (Classification)

   
   In General classification algorithms, a sample is mapped to a predicted label / class (ex: apple is classified as Fruit and Brocolli is classified as Vegetable). Though this project uses classification at its core, this really does not produce a true music recommendation system since we do not just want to match the input music to a genre and suggest another language song from the predicted genre. This project treats the problem as a classification problem and uses the model to generate a mathematical fingerprint (learned features) for every song.
   
   a. Training
   
   Use supervised learning to teach the model to classify several music tracks into a set of 10 genres

   b. Prediction
   
   Once the model understands musical styles and is able to classify well, we will keep the entire model architecture, except the last stage (decision making for the label). This strategy gives rise a vector of numbers that represent what the model has learned. Note that this vector of numbers do not specifcally mean anything acoustically. They can be thought of as a `mathematical signature` of a given music track

   c. Recommendataion
   
   We build a index (database) of mathematical signatures of all the songs that the model learns. Now, for the actual recommendation, we use a simple nearest neighbors strategy (i.e find a song whose mathematical signature is most similar to the input song) to provide a recommendation.
   
   
## 3. Data Acquisition

**Primary Training and testing Source:**:

The GTZAN Genre Collection. This is a standard library of 1,000 songs covering 10 distinct genres (Blues, Classical, Pop, Metal, etc.). It serves as the foundation for the model to learn what different instruments and tempos sound like.

**Real Life test:** 

Prove the system works outside the set of tracks it is trained with and also outside of tracks that it is cross validated with, we acquired external tracks from YouTube (specifically non-English tracks, such as Hindi Bollywood music) to test if the model could provide recommendataions for a song that it has never seen and in a different language.

## 4. Data Preprocessung / Preparation

**Data format**

   1. convert the Audio data (waveform) to an image (spectrogram) that is like a footprint of the audio in terms of an image. As widely used in audio processing, instead of creating 1 image per song, we chunk the song into chunks of 3 seconds each and create a image for each of 3 seconds worth of audio. This uses techniques in Digital Signal Processing for the conversions.
   2. For consistency, all audio files are formatted to mono (single channel) with fixed frequency
   3. Also filter out corrupt files (GTZAN dataset has 1 corrupt file, which we remove programatically and the code can be applied to any music dataset)

**Test / Train Split**
   - 80% of audio files is used as Training set
   - 20% of audio files is used as Testing (cross Validation) set

**Special note specific to this project** 

For the model training and evaluation, we split into test and train. This is primarily for the classification problem. For the recommendataion engine, we use all the dataset to create a database of mathematical signautures to match for recommendation prediction.

## 5. Modeling

**Part 1**

The whole project is split into two parts. This readme and github is for part 2. For Part 1 please check [this github link](https://github.com/bgajare/ContentBasedMusicRecommend)
We will not go into details of Part1, but only a single line recap

In Part 1, we explored another way to convert audio files into a large set of numbers and then run a k-nearest neighbor as a baseline recommendation system. 

**Part 2 (This README)**

We experimented with a standard convolutional neural network which was not very accurate (details provided in section `Model Evaluation` below)

Next an attempt was made to understand the resons for model failure like and a new modified CNN was used.

## 6. Model Evaluation

** Basic CNN**
   The model training and test accuracy was arounc 60% and the recommendations were random. In some cases, it gave recommendation of classical song where the input was disco.
   We realized that it was just putting 0's for most of its values in the mathematical signature of the audio. i.e if it thought it was hard to learn, it just gave up and added zeros to indicate that it learned nothing. This resultes in a model that was not accurate, but more than the accuracy part, the recommendataion system was broken since a lot of songs were predicted to be similar (due to zeroes in the mathematical signature)

** Updated CNN** 
   The activation function was changed from `relu` to `elu` (Basically tell the model a different way to learn features) and Batch Normalization was added (Basically a way for the model to see all features with the same equity, removing the prejudice of preferring 0's over other numbers)

This model had a very high accurary rate consistently of > 90% which means that it could learn the data very well 

Also had a modestly high accuracy rate for Test set of > 70%, which means that it could apply what it learned to a input that it has never seen and come up with a classification. 

The results indicate that when a completely different (Hindi song) was provided, the model did not fail and actually provided very good results. A subjective listening test shows that the songs suggested by the model sound very similar to the input Hindi Song (But the beauty of it is that the recommendation is in english and the model had never seen a hindi song for its life) 


## Conclusion 

Thie project (both part 1 and part 2) combined prove the fact that a a `content based` (using only audio data) approach can be applied to achieve to break language barriers `language agnostic` for music recommendataion systems. Such a system also provides a new business opportunity to new and existing music platforms, where they provide the user with a option to look for songs similar to thier likes irrespective of language (creating a truly global and cross-culture music community) and irrespective of ratings, etc (creating an equitable marketplace for less famous or less known songs to be shown as recommendataions). Users who are really passionate about music would love that they can easily explore new cross cultural content and content creators would love to use this platform as they are guaranteed that thier songs would be recommended even if they had no ratings. 
